---
title: "Architecture First: Why Every IT Decision Should Start with a Diagram, Not a Vendor"
description: "A case for putting architecture, strategy, and business requirements at the front of every IT solutioning conversation — backed by the voices of Schneier, Shostack, SABSA, and NIST."
date: 2026-02-17
---

![Architecture First — Start with the diagram, not the vendor.](/assets/images/architecture-first-header.png)

Over the course of my career, I've walked into more meetings than I can count where the problem and solution are being discussed — and I'm arriving at the tail end of the process. A new platform, a new piece of software, a new appliance. The vendor is already decided. In some cases, the solution has been built and is nearing production. My chair is barely warm before someone asks me to "take a look."

The questions I always lead with are the same: *"What is the strategy?"* and *"What are the requirements?"* — from the client or end users, whether internal or external.

More often than not across the industry, those questions haven't been fully contemplated until later in the process. But it's these questions that lay the foundation for everything that follows.

I believe that most solutioning discussions should start with the architecture. A picture is worth a thousand words, and for IT engineers, drawing out a network diagram forces you to think about the overall strategy and the business requirements. The security architect's job is to overlay the enterprise architecture — aligned to standards, compliance requirements, and company strategy — on top of any proposed solution. From there, you can see in stark contrast where risks are introduced.

And I'm far from alone in this belief.

## The Anti-Pattern: Vendor First, Architecture Last

There's a pattern that plays out across industries, company sizes, and maturity levels. It goes something like this:

1. A business unit identifies a pain point.
2. Someone finds a vendor that solves the pain point.
3. A proof of concept is run in isolation.
4. Procurement gets involved. Contracts are drafted.
5. Somewhere around step four or five, someone asks: *"Did we loop in security? What about compliance? Does this fit our architecture?"*

By then, the momentum is difficult to redirect. Political capital has been spent. The vendor has been promised a signature. And the security architect — the one person whose job it is to see the whole board — is asked to rubber-stamp a decision that was made without them.

This is the anti-pattern: **vendor-first, architecture-last.** It's how organizations end up with sprawling tool portfolios, overlapping capabilities, security gaps between platforms, and compliance findings that cost more to remediate than the original solution cost to implement.

To be fair, this isn't always the case. Mature organizations with strong governance processes involve architecture early. But it's remarkable how often — even in well-run shops — the gravitational pull of a compelling vendor demo can accelerate a process past the architectural review that should have happened first.

## The Cost of Skipping Architecture

When architecture is treated as an afterthought, the consequences are predictable:

**Rework.** Solutions that don't align with the enterprise architecture get re-engineered, re-integrated, or replaced entirely. What was supposed to save time ends up doubling the timeline.

**Shadow risk.** Systems deployed without architectural review introduce risks that nobody is tracking. They sit outside the risk register, outside the vulnerability management program, and outside the incident response playbook — until something goes wrong.

**Compliance gaps.** Regulatory frameworks don't care about your vendor's sales cycle. If a system processes regulated data and wasn't designed with the appropriate controls, the finding lands on your desk regardless of how the buying decision was made.

**Integration debt.** Every platform that bypasses architectural review becomes another silo. Over time, the environment becomes a patchwork of point solutions that don't talk to each other, each with its own identity model, its own logging format, and its own attack surface.

## The Voices Behind "Architecture First"

The "architecture first" position isn't contrarian — it's the consensus view of the most respected voices in security engineering. The challenge is that organizations hear the message and still struggle to change the process.

**John Sherwood, Andy Clark, and David Lynas** built the [SABSA framework](https://sabsa.org/) around a single premise: *everything must be derived from an analysis of the business requirements for security.* SABSA creates a chain of traceability from business requirements through strategy, concept, design, implementation, and ongoing operations. Their foundational work, [*Enterprise Security Architecture: A Business-Driven Approach*](https://www.amazon.com/Enterprise-Security-Architecture-Business-Driven-Approach/dp/157820318X), makes the case that security architecture is not a technical exercise — it's a business exercise. When someone asks *"What is the strategy?"* in a solutioning meeting, they're asking the SABSA contextual question. It's the question most organizations skip entirely.

**Bruce Schneier** put it plainly two decades ago: *"Security is a process, not a product."* In [*Secrets and Lies*](https://www.amazon.com/Secrets-Lies-Digital-Security-Networked/dp/0471253111), he argued that anyone who thinks technology alone solves security problems understands neither the problems nor the technology. That was written in 2000. Twenty-six years later, organizations are still selecting vendors before defining requirements — buying products when they should be designing processes.

**Adam Shostack**, in [*Threat Modeling: Designing for Security*](https://shostack.org/books/threat-modeling-book), argues that security must be addressed in the design phase — before code is written, before infrastructure is provisioned, before products are purchased. His approach to threat modeling is fundamentally an architectural exercise: draw the system, identify the trust boundaries, trace the data flows, and find the threats. The diagram comes first. Everything else follows from it.

**Ross Anderson**, in [*Security Engineering*](https://www.amazon.com/Security-Engineering-Building-Dependable-Distributed/dp/1119642787), demonstrates that security failures are rarely about missing technology. They're about flawed system design and misaligned incentives. Architecture-level decisions — access control models, trust boundaries, fault tolerance — determine security outcomes far more than any individual product selection.

**Gene Kim** captured the organizational dysfunction in [*The Phoenix Project*](https://www.amazon.com/Phoenix-Project-DevOps-Helping-Business/dp/1942788290) and later in [*The DevOps Handbook*](https://www.amazon.com/DevOps-Handbook-World-Class-Reliability-Organizations/dp/1942788002). His prescription: product management, development, IT operations, and information security should all work together from the beginning. In high-performing organizations, he writes, *"quality, availability, and security aren't the responsibility of individual departments, but are a part of everyone's job, every day."* Security can't be everyone's job if security wasn't in the room when the architecture was defined.

Even **NIST**, in [Special Publication 800-37](https://nist-sp-800-37-r2.bsafes.com/docs/chapter-three/enterprise-architecture/) (the Risk Management Framework), explicitly ties security architecture to enterprise architecture. The guidance states that integrating security and privacy requirements into the enterprise architecture ensures they are *"addressed throughout the system development life cycle"* and are *"explicitly related to the organization's mission and business processes."* This isn't a suggestion — it's a federal standard.

## What "Architecture First" Looks Like in Practice

So what does it actually look like to lead with architecture? It comes down to a few disciplines:

**Start with the business requirement, not the technology.** Before any vendor conversation, the team should be able to articulate — in plain language — what business problem they're solving, who the stakeholders are, and what success looks like. If you can't write it on a whiteboard in two sentences, you're not ready to talk to a vendor.

**Draw the diagram before you build the solution.** A network diagram, a data flow diagram, a system context diagram — whatever is appropriate for the scope. The act of drawing forces clarity. It exposes assumptions. It reveals dependencies. And it gives the security architect something concrete to evaluate rather than a slide deck full of marketing language.

**Overlay the enterprise architecture.** Every organization has — or should have — an enterprise architecture that reflects its standards, compliance obligations, and strategic direction. The proposed solution should be mapped against it. Where does it align? Where does it diverge? Where does it introduce risk? A diagram answers these questions immediately. A vendor presentation never will.

**Involve security at the requirements phase, not the review phase.** There is a meaningful difference between being asked *"Can you review this before we go live?"* and being asked *"We're defining requirements for a new capability — what should we be thinking about?"* The first is damage control. The second is architecture.

## The Diagram Is the Strategy

When you can get a team to draw the architecture before they've committed to a solution, the conversation changes entirely. The questions shift from *"Which vendor should we buy?"* to *"What are we actually trying to accomplish, and what's the smartest way to get there?"*

That shift — from vendor-first to architecture-first — is where the real work of security architecture begins. It's where risks become visible before they become incidents. It's where compliance is designed in rather than bolted on. And it's where enterprise strategy and technical implementation finally speak the same language.

The diagram is not a deliverable. It's the starting point. Everything else is commentary.
