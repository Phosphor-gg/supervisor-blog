---
title: "Supervisor vs OpenAI's moderation endpoint: which should you use?"
date: 2026-07-13
description: "OpenAI's moderation API is free and excellent at safety classification. Supervisor is a paid product built for community and platform moderation. Here is an honest, accurate comparison so you can pick the right one."
---

# Supervisor vs OpenAI's moderation endpoint

People often ask how Supervisor compares to OpenAI's free moderation endpoint. It is a fair question, and we are not going to pretend the honest answer is "always us." OpenAI's moderation API is genuinely good, and it is free. But it was built to solve a different problem than Supervisor, and for a lot of real communities and platforms the difference matters. Here is a straight comparison, with the facts checked.

## What OpenAI's moderation endpoint is

OpenAI's `omni-moderation-latest` model classifies text and images against **13 harm categories** and returns a confidence score and a pass/fail flag for each. The categories are safety-focused: sexual content (including a minors category), self-harm (intent and instructions), violence (including graphic), harassment (including threatening), hate (including threatening), and illicit activity (including violent). A subset of those categories also accept image input. It runs at the `/v1/moderations` endpoint, handles images up to 20 MB, and does not process audio.

Two things make it genuinely attractive: it is **free** for OpenAI API users, and it is fast, with low latency when run inline on user input. If your need is "flag clearly unsafe content before it reaches a model or a user," it does that job well and costs nothing.

## What Supervisor is

Supervisor is a paid, purpose-built moderation product for communities and platforms. It moderates text and images against **16 labels**, runs three model tiers you can choose between, and adds two capabilities that a pure safety classifier does not have: it reads implied intent, and it can consider recent conversation history. It also ships as a Discord bot and a Platform API, not just a raw endpoint.

The two products overlap on the safety basics. They diverge everywhere community moderation actually gets hard.

## The differences that matter

### Labels: safety vs community

OpenAI's 13 categories are the classic trust-and-safety set. They do not include several things that break real communities every day: **spam, promotional content, scams, profanity, insults, or sensitive-but-not-unsafe topics**. Supervisor has dedicated labels for all of those, alongside the safety categories. If your problem is a Discord server full of crypto scams and self-promo, or a marketplace drowning in spam, a safety classifier will wave most of it straight through because none of it is "harm" in the safety sense.

Supervisor also lets you **choose which labels to enable per request**, so you only get flagged on what your community actually cares about. OpenAI returns the full set every time.

### Reading intent, not just categories

This is the biggest gap. OpenAI's model classifies each input in isolation against fixed categories. Supervisor adds **implicit moderation**, which catches harm that is implied rather than stated: the message that contains no flaggable word but is clearly a threat, an insult, or a scam in context. It can also **look at recent conversation history** when a message is ambiguous on its own, so a coordinated harassment campaign made of individually-innocent messages does not slip through one message at a time. Scoring messages one at a time, with no memory, is exactly where isolated classifiers miss the subtle cases.

### Evasion

Determined users bypass filters with l33t-speak, Unicode look-alike characters, zero-width characters, and creative spelling. Any model that reads meaning rather than exact strings handles this well, and both products are strong here. It is worth naming because it is a common reason keyword filters fail, and it is a baseline expectation for either of these tools rather than a differentiator between them.

### Where it runs

OpenAI gives you an endpoint. That is the whole product, and for developers building their own stack that is often exactly what you want. Supervisor gives you the endpoint **plus** a Discord bot you can add to a server in a couple of minutes with no code, and a **Platform API** with client credentials, a user consent flow, and optional revenue-share billing so you can resell moderation to your own users. If you run a Discord community or a platform with end users, that is a lot less to build.

### Model choice

OpenAI serves one moderation model. Supervisor lets you pick a tier: **Observer** for fast, high-volume filtering, **Sentinel** for sharper judgement, and **Arbiter** for the hardest calls, or Auto to route each request to the right one. You trade cost against accuracy deliberately instead of taking a single fixed point.

### Rate limits, and the key-pooling problem

This one is a quiet dealbreaker for Discord bots specifically, and it is worth spelling out because a lot of people learn it the hard way.

OpenAI's free moderation tier allows **250 requests per minute but only 5,000 requests per day**. A Discord bot moderates every message, and a single moderately active server can produce more than 5,000 messages in a day on its own. Multiply that across a few servers and you hit the daily wall before lunch.

You can raise those limits, but only by moving up OpenAI's **usage tiers**, which are based on how much you have spent on the API. Here is the catch: the moderation endpoint is free and **does not count toward that spend**. So a bot that only calls the moderation endpoint never advances a tier and stays pinned to the free daily cap forever. The only way to raise your moderation limits is to go spend money on OpenAI's other, paid endpoints, whether or not your product uses them.

Faced with that, a lot of bot developers do something OpenAI's usage policies do not allow: they **pool API keys** across multiple accounts, each holding a little credit, and rotate through them to spread the load and dodge the per-key limits. It works until it doesn't. Circumventing rate limits and sharing accounts this way is against OpenAI's terms, and the accounts get banned. You have built your community's safety on an arrangement that can be switched off without warning.

Supervisor's limits scale directly with your plan, and they are sized for the reality of moderating every message in a server. There is no tier you have to buy your way into with unrelated spend, no daily cliff that ignores your plan, and nothing that pushes you toward pooling keys or breaking anyone's terms of service. With Supervisor it is simple: you want a higher limit, you pay for it. And unlike OpenAI's endpoint, that same plan also gets you context-aware and implicit moderation, not just a bigger request quota.

## Price: the honest part

OpenAI's moderation endpoint is free. Supervisor is not. That is a real advantage for OpenAI and we are not going to talk around it.

What you pay Supervisor for is the things above: the community-specific labels, implicit and context-aware detection, per-label control, the Discord and platform integrations, and model tiers. Supervisor bills per byte, with images billed at a flat rate and repeat requests served free from cache. If none of the extra capabilities matter to your use case, OpenAI's free endpoint is the sensible choice and we will happily tell you so.

## So which should you use?

**Use OpenAI's moderation endpoint if** you need free, fast safety classification of standalone text and images against the standard harm categories, you are comfortable integrating a raw API, and you do not need spam/scam/promotional detection, implied-intent or conversation-aware moderation, per-label control, or a ready-made Discord or platform integration.

**Use Supervisor if** you are moderating a community or a platform: if scams, spam, and self-promo are as much of a problem as overt harm, if the abuse in your space is subtle and contextual, if you want to enable only the labels you care about, or if you want a Discord bot or a resell-ready Platform API instead of wiring everything yourself.

They are not really competing for the same job. One is a free safety classifier. The other is a moderation product for people running communities. Pick the one that matches the problem you actually have.

Want to see the difference on your own content? Paste a message into the [live demo](https://supervisor.gg/demo), or read the [API docs](https://supervisor.gg/docs) to compare the surfaces directly.
