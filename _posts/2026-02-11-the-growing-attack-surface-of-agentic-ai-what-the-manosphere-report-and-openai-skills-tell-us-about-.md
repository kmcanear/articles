---
title: "The Growing Attack Surface of Agentic AI: What the Manosphere Report and OpenAI Skills Tell Us About Production LLM Security"
description: "Two recent developments highlight how AI systems are rapidly moving from experimentation to production—and exposing critical security gaps in PII handling, prompt injection defense, and sandboxing that enterprise security teams aren't prepared for."
date: 2026-02-11
---

Two articles crossed my desk this week that perfectly illustrate where we are with production AI security—and it's not a comfortable place. Simon Willison highlighted both [the New York Times' Manosphere Report](https://simonwillison.net/2026/Feb/11/manosphere-report/#atom-everything), an internal LLM tool that transcribes and summarizes dozens of podcasts for journalists, and OpenAI's new [Skills API](https://simonwillison.net/2026/Feb/11/skills-in-openai-api/#atom-everything) that allows shell execution through API calls with inline base64-encoded packages. These aren't proof-of-concepts or research demos. These are production systems handling sensitive information and executing arbitrary code. And they represent exactly the kind of deployment pattern that should terrify anyone responsible for enterprise security architecture.

## The Times' Manosphere Report: When Production AI Meets PII at Scale

What strikes me about the Manosphere Report isn't that it exists—automated transcription and summarization are obvious use cases for LLMs. What's interesting is that it's described as being delivered "directly to the email inboxes of journalists" and was "essential" to their coverage. This tells me it's a core operational tool, not an experiment. And that raises immediate questions about the security architecture around it.

The article doesn't provide technical details, but let's think through what this system likely involves:

1. **Ingestion layer**: Automated download or streaming of podcast audio from dozens of sources
2. **Transcription**: Likely using Whisper or a similar model
3. **Summarization**: LLM-based analysis to extract key themes and quotes
4. **Distribution**: Automated email delivery to internal users

Each of these stages represents a distinct attack surface. What I find most concerning is the PII exposure risk. Political podcasts frequently mention specific individuals—not just public figures, but callers, participants, sources. A well-designed system needs to identify and handle this information appropriately before it hits journalists' inboxes.

From an enterprise security perspective, the practical implication here is that you need **layered PII detection and redaction** in any LLM pipeline processing uncontrolled external content. This isn't a single checkpoint—it's defense in depth:

**Detection layer**: Named entity recognition (NER) models running in parallel with your primary LLM workflow. You want these to flag potential PII before summarization happens. Microsoft's Presidio and AWS Comprehend both offer reasonable detection, but you'll need to tune them for your specific use case. Political podcasts will have different PII patterns than customer service calls.

**Redaction decision layer**: Not every name needs redacting. Public figures are fair game; random callers aren't. This is where you need business logic, not just ML. I've seen teams implement allowlists of public figures combined with heuristic rules (mentioned more than N times across sources = likely public figure).

**Output validation**: Even with upstream detection, you need final-stage validation before distribution. This is your last chance to catch leakage. Regex patterns, keyword matching, and a secondary PII scan on the generated summaries themselves.

What the Times likely learned—and what every team building similar tools discovers—is that PII detection at the summary output stage is too late. You need it throughout the pipeline. The LLM might hallucinate PII connections ("John mentioned his neighbor Sarah who...") or restructure information in ways that create new disclosure risks.

## OpenAI Skills: The Shell Execution Problem

The Skills API announcement is where things get really interesting from a security architecture standpoint. The ability to send base64-encoded zip files containing arbitrary code that gets executed in response to an API call is... exactly what adversarial researchers have been warning about.

Here's what OpenAI is offering:

```python
r = OpenAI().responses.create(
    model="gpt-5.2",
    tools=[{
        "type": "shell",
        "environment": {"type": "container_auto"}
    }]
)
```

That `container_auto` parameter is doing a lot of heavy lifting. It's essentially saying "we'll spin up a container, execute whatever code you sent us, and return the results." The obvious question: what are the sandbox boundaries?

What this article highlights—and what I've been watching unfold across the industry—is the rapid convergence of LLMs with traditional code execution. We spent decades building security models around the principle that data and code are separate. SQL injection, XSS, command injection—these entire vulnerability classes exist because we failed to maintain that separation. Now we're deliberately blurring it again, and calling it "agentic AI."

The practical implication here is that **prompt injection defense patterns need to account for code execution contexts**. Traditional prompt injection focuses on jailbreaking content filters or extracting training data. But when the LLM can execute shell commands, prompt injection becomes remote code execution with extra steps.

## Ring-Based Defense for Agentic AI Systems

Both of these examples point to the same architectural conclusion: production AI systems need ring-based security models, similar to what we use for operating systems and network segmentation.

**Ring 0 (Core LLM)**: The base model, running in the most restricted environment. No external network access, no file system access, no ability to execute arbitrary code. This handles the pure language understanding and generation tasks.

**Ring 1 (Controlled Extensions)**: Pre-approved tools and functions with defined interfaces. This is where you implement database queries, API calls, and other necessary integrations—but through strictly controlled channels with input validation and output sanitization at every boundary.

**Ring 2 (Sandboxed Execution)**: Code execution environments (like OpenAI's Skills) that run in isolated containers with resource limits, network restrictions, and comprehensive logging. This is your "anything goes" layer, but it's treated as untrusted from the start.

**Ring 3 (External Interface)**: The boundary between your AI system and the outside world. This needs rate limiting, authentication, input sanitization, and DDoS protection. Every prompt is potentially adversarial.

What I find interesting about the Skills API is that OpenAI is essentially offering Ring 2 as a managed service. That's valuable, but it doesn't eliminate your responsibility for Rings 0, 1, and 3. You still need to control what prompts reach the Skills-enabled model, validate the outputs, and ensure the executed code can't pivot to attack other systems.

## The Missing Piece: Output Validation and Sanitization

Neither article discusses output validation in detail, but it's the critical control that makes these systems safe for production use. The Manosphere Report is generating content that gets sent directly to journalists. The Skills API is returning the results of arbitrary code execution. In both cases, you need robust output validation:

**Structure validation**: Does the output match expected schemas? If you asked for a summary with specific sections, did you get them? Unexpected structure often indicates prompt injection or model confusion.

**Content sanitization**: Strip or encode anything that could be interpreted as active content. HTML, JavaScript, shell metacharacters—treat LLM output like user input, because that's effectively what it is.

**Semantic validation**: Does the output make sense in context? If you asked for a podcast summary and got Python code, something went wrong. This requires business logic, not just pattern matching.

**PII leakage checks**: As discussed earlier, this needs to happen even on generated content. The LLM might expose information from its training data or recombine input data in revealing ways.

The challenge with output validation is that LLMs are probabilistic by nature. You can't whitelist expected outputs the way you can with traditional APIs. Instead, you need heuristic validation that flags anomalies without being so strict that it breaks legitimate use cases. This is where security teams need to work closely with ML engineers to understand the model's behavior patterns.

## Threat Intelligence for AI-Specific Attacks

What both of these deployments need—and what most organizations lack—is a threat intelligence pipeline specifically focused on AI system attacks. Traditional threat intel focuses on CVEs, IOCs, and malware signatures. AI security needs different indicators:

**Prompt injection patterns**: Adversaries are constantly developing new jailbreak techniques. You need to track these, test your systems against them, and update defenses accordingly. This isn't a one-time exercise—it's continuous monitoring.

**Model behavior anomalies**: Unusual output patterns, excessive tool use, unexpected confidence scores. These can indicate ongoing attacks or successful prompt injection.

**Resource abuse patterns**: LLM calls are expensive. Adversaries targeting your API might focus on resource exhaustion rather than data exfiltration. Monitor for calls that maximize compute cost relative to legitimate value.

**Data exfiltration attempts**: Watch for outputs that suspiciously match training data patterns or that attempt to encode information in unexpected ways (steganography, unusual formatting).

The Skills API makes this even more critical. When your AI system can execute code, you need the same kind of behavioral monitoring you'd apply to EDR solutions. What processes are spawning? What network connections are being established? What files are being accessed?

## The Red Teaming Gap

What I find most concerning about both of these examples is that neither article mentions red teaming. The Manosphere Report is described as having been "essential" to the Times' coverage, suggesting it went from development to critical operational use quickly. The Skills API is being released to general availability. But where's the discussion of adversarial testing?

Red teaming LLM deployments requires different skills than traditional pentesting. You need people who understand both prompt engineering and traditional exploitation techniques. They need to think about:

- **Prompt injection for privilege escalation**: Can they manipulate the system into executing unintended commands?
- **Data exfiltration through generation**: Can they extract training data, system prompts, or other users' information?
- **Sandbox escape**: For systems like Skills, can they break out of the container?
- **Supply chain attacks**: Can they poison the training data, tool definitions, or skill packages?

The Skills API's ability to accept inline base64-encoded packages is particularly interesting from a red team perspective. What happens if I send a skill that pretends to do something innocuous but actually attempts to fingerprint the container environment, probe for network access, or establish persistence?

## Practical Recommendations

For teams building production AI systems—whether internal tools like the Manosphere Report or external-facing APIs—here are the architectural patterns that need to be non-negotiable:

1. **Implement ring-based separation** between the core LLM, controlled extensions, and any code execution environments
2. **Deploy layered PII detection** at ingestion, processing, and output stages
3. **Validate all outputs** structurally, semantically, and for content safety before they reach end users
4. **Establish AI-specific threat intelligence** collection and monitoring
5. **Red team aggressively** with people who understand both AI and traditional security
6. **Log everything** with sufficient detail to reconstruct attacks, but sanitized to avoid PII exposure in logs themselves
7. **Rate limit and monitor** for both abuse and operational anomalies

The Manosphere Report and OpenAI Skills represent exactly where production AI is heading: powerful, operationally critical systems that handle sensitive data and execute arbitrary code based on natural language instructions. That's an enormous attack surface, and traditional security controls aren't sufficient. We need new architectures, new monitoring approaches, and a much more adversarial mindset about what these systems can be tricked into doing.

What concerns me most is the speed at which these systems are moving from experiment to production. The Times built an internal tool that became essential to their coverage. OpenAI released an API that allows arbitrary code execution. Neither seems to have been accompanied by public discussion of the security implications. That's the gap we need to close—not by slowing down AI adoption, but by ensuring security architecture keeps pace with deployment velocity.

## Sources

- [Quoting Andrew Deck for Niemen Lab](https://simonwillison.net/2026/Feb/11/manosphere-report/#atom-everything) - Simon Willison, February 11, 2026
- [Skills in OpenAI API](https://simonwillison.net/2026/Feb/11/skills-in-openai-api/#atom-everything) - Simon Willison, February 11, 2026