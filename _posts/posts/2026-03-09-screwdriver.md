---
categories: posts
layout: post
title: "The screwdriver test"
description: If I cannot open it, I do not really own it. A short note on understanding by disassembly.
date: 2026-03-09
en: "/robots_txt/posts/the-screwdriver-test/"
comments: true
excerpt: I carry a screwdriver. Not as a bit, as a habit. Here is what it is actually for.
keywords: "hacking, curiosity, repair, right to repair, learning"
tags: [thoughts]
authors:
  - Het Joshi
---

I carry a screwdriver. I wrote that once before and people thought it was a bit. It is not a bit. It is the most honest description of how I learn anything.

Here is the test. Pick up a thing you use every day. A router, a smart plug, the badge reader at your office, a charging brick. Now ask whether you could open it, follow what is inside, and put it back together with a rough idea of why it does what it does. If the answer is no, you do not understand that thing. You are renting an explanation from whoever sold it to you.

That bothers me more than it probably should. I once opened the motion sensor switch in a college bathroom just to see how it decided someone was there. I learned how the sensor worked. The college learned it was down one switch. Worth it.

The screwdriver test is not really about hardware. It is a stance. When I read about a protocol, I want to send the packets myself and watch them, not take the spec's word for it. When I use a library, I want to read the one function that actually matters. When a system tells me it is secure, I want to know which assumption it is leaning on, because there is always exactly one load-bearing assumption and it is usually written down nowhere.

The reason this matters for security specifically: attackers run the screwdriver test on your systems whether or not you do. They are not impressed by your documentation. They open the thing. The only way to meet them on level ground is to have opened it first, found the load-bearing assumption, and decided for yourself whether it holds.

So open things. Break a few. Put most of them back. The point was never the screwdriver. The point is refusing to treat any system as a sealed box you are not allowed to question.
