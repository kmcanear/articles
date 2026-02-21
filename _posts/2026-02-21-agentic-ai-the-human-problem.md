---
title: "Agentic AI: The Human Problem"
description: "We spent decades teaching that the weakest link in security is the human. Now we're building AI systems designed to think and act like one — and handing them the keys to our most sensitive data."
date: 2026-02-21
---

Hollywood loves to show hacking as some genius typing furiously into a terminal, plugging a mysterious device into a server rack, or watching green text cascade down a screen before triumphantly declaring, "We're in." But most security professionals know the truth: the majority of successful breaches don't come from cracking encryption or zero-day exploits. They come from social engineering — a well-crafted email, a convincing phone call, a manipulated human.

We've spent decades teaching that the weakest link in security is the human.

Now we're building AI systems designed to think, reason, and act like one — and handing them the keys to our most sensitive data.

I'm currently working through an AI security certification program, and every lab exercise deepens a concern I can't shake. In one recent exercise, I tested a fine-tuned model built for a medical facility. With a handful of prompts — ones I crafted myself, no exploit toolkit required — I extracted Protected Health Information. 

Let that sink in: PHI. Exfiltrated through conversation.

This isn't a theoretical risk. It's the logical outcome of what we're building.

Here's the uncomfortable truth: For years, attackers have exploited humans through social engineering — trust manipulation, authority spoofing, urgency tactics. These techniques work because humans are context-driven, persuadable, and eager to be helpful. We've now engineered AI systems that share those exact characteristics, and we're deploying them autonomously inside regulated environments with access to our most sensitive assets.

And the research confirms what many of us feared.

- **Gray Swan AI, the UK AI Security Institute, and the U.S. AI Safety Institute** published results from the largest public AI agent red-teaming competition ever conducted. Nearly 2,000 participants launched 1.8 million adversarial attacks against 22 frontier AI agents across 44 realistic deployment scenarios — including healthcare, finance, and legal. The result? A 100% policy violation rate. Every single model — from OpenAI, Google, Anthropic, Meta, xAI, Amazon, Cohere, and Mistral — was successfully compromised. The only variable was the number of queries it took. Within just 10 to 100 attempts, nearly all agents violated their own deployment policies. Attacks transferred across models, meaning an exploit built for one system often worked on others. And critically, **neither model size, capability, nor additional inference compute correlated with improved robustness.** Bigger, smarter models weren't harder to break. ([arxiv.org/pdf/2507.20526](https://arxiv.org/pdf/2507.20526))

Now, to be fair — the models tested are not the latest versions, this was 2025. It's reasonable to assume newer models have improved their defenses. But that's exactly the point: we've been "improving" human security awareness for decades, too, and social engineering still works. When you engineer a system to be helpful, contextual, and persuadable — whether it's carbon-based or silicon-based — there are no guarantees. The attack surface isn't a bug to be patched. It's a feature of the design.

- **The folks at McKinsey** call AI agents "digital insiders" — entities that operate with privilege and authority within systems, capable of causing harm through poor alignment or compromise, just like their human counterparts. ([mckinsey.com](https://www.mckinsey.com/capabilities/risk-and-resilience/our-insights/deploying-agentic-ai-with-safety-and-security-a-playbook-for-technology-leaders))

This is a social engineer's dream. Technology that is designed to be helpful, that maintains context, that trusts its inputs, that can be gradually manipulated through conversation — and that operates with privileged access to financial records, health data, intellectual property, and critical infrastructure.

We didn't eliminate the weakest link.
We automated it.

The path forward isn't to stop building. It's to stop deploying without the same rigor we'd apply to any privileged insider: zero trust principles, least-privilege access, continuous behavioral monitoring, human-in-the-loop controls for high-risk actions, and security testing that treats these systems as what they are — persuadable entities with access to sensitive data. Some of us are actively researching architectural approaches that borrow from the isolation and containment models we've relied on for decades in traditional infrastructure — applying concepts like ring-based privilege separation and continuous verification to the way AI agents are governed. It's early-stage work, but the principles aren't new. We just need to apply them to this new class of insider.

If you're in a regulated industry and deploying agentic AI without red-teaming these systems the way you'd pen-test your network, you're not innovating. You're gambling.

*Note: The views expressed here are my own.*

**Further Reading:**

- [OWASP Top 10 for Agentic Applications (2025)](https://genai.owasp.org/2025/12/09/owasp-genai-security-project-releases-top-10-risks-and-mitigations-for-agentic-ai-security/)
- [Shadow AI in Healthcare (IBM / TechTarget)](https://www.techtarget.com/healthtechsecurity/feature/Shadow-AI-in-healthcare-The-hidden-risk-to-data-security)
- [Cisco State of AI Security 2026](https://blogs.cisco.com/ai/cisco-state-of-ai-security-2026-report)
- [NIST RFI on AI Agent Security (Jan 2026)](https://www.federalregister.gov/documents/2026/01/08/2026-00206/request-for-information-regarding-security-considerations-for-artificial-intelligence-agents)
- [LLM Patient Privacy in Healthcare (JMIR, 2025)](https://www.jmir.org/2025/1/e76571)

#AISecurity #AgenticAI #Cybersecurity #CAISP #HealthcareSecurity #HIPAA #ZeroTrust #OWASP #InfoSec #AI #LLM #GenAI #RedTeaming
