---
categories: posts
layout: post
title: "Shadow AI is a measurement problem"
description: Everyone at Black Hat agreed shadow AI is the problem. Nobody could tell me how to see it. A field report on where the landscape actually stands.
date: 2026-09-09
en: "/robots_txt/posts/shadow-ai-is-a-measurement-problem/"
comments: true
excerpt: You cannot govern a data flow you cannot observe. Right now most enterprises cannot observe this one, and the vendor slides are ahead of the science.
keywords: "shadow AI, genAI security, eBPF, TLS inspection, BYOD, DLP, enterprise security"
tags: [thoughts]
authors:
  - Het Joshi
---

<img width="1536" height="680" alt="image" src="https://github.com/user-attachments/assets/85f8b4f9-c6b6-4919-b8b7-2c2d64c9ad3b" />


Last time I wrote that if you cannot open a thing, you do not own it. Shadow AI is the version of that problem where the sealed box was installed by your own employees, on purpose, because it made their Tuesday easier.

I spent Black Hat asking people the same question. How do you actually know which AI tools are running in your org, who is using them, and what is going into them? Everyone agreed it was the problem. Nobody had a definitive answer. That gap is the whole post.

## Why this one is hard

Shadow IT was findable. A new SaaS app meant a new domain, a new OAuth grant, a new invoice. Shadow AI has none of those tells.

It is all port 443 to a handful of endpoints that also serve traffic you approved. Your sanctioned ChatGPT tenant and an engineer's personal account resolve the same name, negotiate the same TLS, and look identical to a resolver. Netskope's 2026 telemetry puts roughly 47% of workplace genAI use on personal, unmanaged accounts, which is precisely the traffic a network-layer control cannot separate from the sanctioned kind.

Worse, most of it is not a standalone app at all. It is a copilot inside software you already bought, a browser extension with read-and-change-all-site-data, an IDE plugin, an MCP server somebody wired up on a Thursday. Verizon's 2026 DBIR found the average company had more than 15% of users running unauthorized AI browser extensions. The perimeter is not being crossed. The perimeter is being asked politely to summarize a document.

## The landscape, honestly

There are four families of products and each one sees exactly one layer.

**Network and proxy.** Sees destination. Without TLS inspection it cannot see identity or content. It is a reasonable first control and a terrible last one.

**Browser and extension.** Sees the paste, sees the account, sees the prompt. Blind to a desktop app, a CLI tool, or anything outside the managed browser.

**Identity and SaaS posture.** Sees OAuth grants, service accounts, non-human identities, agent registrations. Excellent for agents. Completely blind to a personal account on a phone hotspot.

**DLP and data lineage.** Sees content on the way out, usually after the fact, usually keyword-shaped. Source code, which is the most commonly leaked category, barely trips classic rules at all.

Of the people I talked to, Zscaler had the most implementable plan, and I want to be specific about why. It is inline. Traffic already goes through their enforcement nodes, so app cataloguing, prompt and response extraction, and policy at the point of submission all sit on infrastructure the customer already deployed. That is a real engineering answer, not a dashboard. Marc Lopez ([linkedin.com/in/cyber-marc](https://www.linkedin.com/in/cyber-marc/)) was the one who walked me through it properly.

It also inherits the limits of a proxy. It needs TLS interception, so certificate-pinned and native applications fall outside it. It needs a maintained catalog of thousands of AI apps, which is a treadmill. And on an unmanaged device it has nothing to stand on. That is not a criticism of them specifically. It is where the entire field currently ends.

## What I would build

Four instruments, layered, because no single one is sufficient.

**1. Headers and endpoints, passively.** Before you decrypt anything, you can fingerprint. SNI, JA4 and JA4S, HTTP/2 header ordering, path shape, and the very distinctive timing signature of token streaming: a small request followed by a long-lived server-sent-event response that trickles. This is cheap, needs no agent, and gets you an inventory. It does not get you the account or the content.

**2. Webhooks and outbound integrations.** This is where agents actually live. OAuth grants, MCP server registrations, callback URLs pointed into Slack, Jira, GitHub. A chatbot leaks a prompt; an agent leaks a permission. The second one compounds. This layer is the most neglected and the cheapest to instrument, because most of it is already in audit logs nobody reads.

**3. eBPF at the kernel level.** Uprobes on `SSL_write` and `SSL_read` in libssl, with equivalents for GnuTLS, NSS, and BoringSSL for Go binaries. You get plaintext before encryption and after decryption, and, more importantly, you get the PID. Which binary, which user, which session. Published benchmarks put the overhead around 0.2 microseconds per hook, so cost is not the objection. Static Go binaries are the real work, since you cannot rely on dynamic symbols and end up doing offset-based attachment that breaks on every app update.

**4. MITM where you can, kernel where you cannot.** Interception proxies are fine for browser traffic and break immediately on pinned clients and native desktop apps that ship their own TLS stack. Do not try to defeat pinning. Treat pinning as a routing decision: the proxy handles what it can, and everything it cannot becomes a kernel-monitoring case. The network layer tells you something is happening, the kernel layer tells you what and who, the integration layer tells you what it can reach.

## Scaling this

On a managed fleet, it is buildable today. Agent in the golden image, probe attachment at library load, classification at the endpoint. Do not ship raw prompts to a central collector. Average organizations are already generating roughly 18,000 prompts a month and the top percentile far more. Ship verdicts and metadata, keep content local, sample deliberately.

Two things will bite you. First, offset maps rot; every Chrome or Slack update can move your attachment point, so the maintenance surface is continuous, not one-time. Second, and this is the one I care about more: a kernel probe on plaintext reads everything. Including the employee's banking session on their lunch break. If this ships without hard process scoping, a documented allowlist, and an audit trail on the probe itself, it is not a security tool, it is a wiretap with a compliance sticker on it.

BYOD is where the whole architecture collapses, and I would rather say that than pretend otherwise. You cannot put a kernel agent on someone's personal phone, and you should not want to. What is left is thinner: an enterprise browser for work context, per-app MDM containers, and pushing enforcement up to the identity plane so the personal tenant cannot reach corporate data in the first place. Plus the unglamorous one that consistently outperforms controls in the survey data, which is providing a sanctioned tool good enough that nobody bothers with the shadow one. On BYOD you are not doing detection. You are doing displacement, and you should measure it as such.

## Where this leaves us

The industry has four partial views and a lot of slides that say complete visibility. The open questions are still open. Can you fingerprint AI traffic reliably enough without decryption to skip the agent entirely? How do you attribute across NAT and unmanaged devices? How do you scope a kernel probe so it is defensible to an employee, not just to an auditor? What is the false-positive cost of blocking, given that every published attempt at a blanket ban has pushed the behavior further underground?

None of those have answers I would call settled, and that is the actual state of the field in 2026. More research here is not a nice-to-have.

I want to work on this one properly. If you are building in this space, or you have measurement data and a problem you cannot see the bottom of, come find me.

Attackers run the screwdriver test on your systems whether or not you do. With shadow AI, so do your own employees. The security team is currently the only party that has not opened the box.
