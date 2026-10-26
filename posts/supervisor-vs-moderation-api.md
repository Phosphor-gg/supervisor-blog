---
title: "Supervisor vs Moderation API: decision API versus review platform"
date: 2026-10-26
description: "Moderation API (moderationapi.com) is a detection plus review platform; Supervisor is a labelled decision API with a Discord bot. An honest comparison of labels, context, languages, media, pricing and who should use which."
---

# Supervisor vs Moderation API: decision API versus review platform

**Bottom line:** Moderation API is the better choice if you want a hosted review queue, author management and a rules engine around detection, and it claims 120+ languages and audio support. **Supervisor** is the better choice if you want a labelled decision API with 16 labels, context-aware moderation, implicit labels and translation for non-English text, plus a ready-made Discord bot, at one flat plan. Supervisor may cost more per message for images and long text, and much less for large volumes of short text. We show the arithmetic.

We make Supervisor, so weigh this accordingly. Moderation API facts come from its own homepage, pricing page, docs and OpenAPI spec, linked at the end and read on 26 October 2026.

## What each one is

**Moderation API** describes itself as "an AI content moderation API and review platform for text, images, video and audio, with custom rules and support for 120+ languages". Detection, review, user management and compliance sit in one platform.

**Supervisor** is a moderation API and Discord bot for communities, games and platforms. It returns `flagged` plus the `labels` that triggered it. It does not describe a hosted review queue, and this post does not claim it has one.

## Side by side

| | Moderation API | Supervisor |
| --- | --- | --- |
| Inputs | Text, image, video, audio | Text, image, video |
| Labels and models | 20+ ready-made models, including toxicity, NSFW, profanity, PII, spam, self-harm, scams, phishing, hate speech, harassment | 16 labels, including scam, spam, promotional, self-harm, illegal |
| Conversation context | Not confirmed | `include_context` returns `needs_context` and `context_labels` |
| Implicit harm | Not confirmed | `implicit_labels` |
| Languages | 120+ claimed | Non-English text translated before classification, including slang and mixed-language messages |
| Review queue, author moderation, rules engine | Yes | Not claimed here |
| Model tiers | Not covered | Observer, Sentinel, Arbiter |
| Batch | Not covered | Batches of 2 or more at half price |
| Username check | Not confirmed | Dedicated `/username` endpoint |
| SDKs | TypeScript, Python, PHP, Ruby, CLI confirmed | Python, JavaScript, Go, Rust, Java |
| Discord bot | Not covered | Ready-made bot |
| Plans | Hobby, Basic, Growth, Enterprise | One plan, Premium |

"Not confirmed" means we did not find it in the sources we read, not that it is absent. Check before you decide.

## Where Moderation API is better

- **The workflow.** A review queue, author moderation, wordlists, a rules engine and webhooks for queue and author events. The example rule on the homepage is "If Content contains links And Account age < 7 days Then Reject". If your moderators work in a queue, this is the reason to choose it.
- **Audio.** Audio moderation is part of the product (2 units each).
- **Stated language reach.** "Global 120+ languages, one API." We do not quote a Supervisor language count because we have not measured one.
- **Simple units for images.** Three units per image, which is easy to predict.
- **Custom guidelines.** Policies written in plain language, plus custom models.

## Where Supervisor is better

- **Context.** "Stop it" means nothing alone. With `include_context` set, the response tells you when it needs the conversation:

```json
{
    "flagged": false,
    "labels": [],
    "needs_context": true,
    "context_labels": ["harassment"]
}
```

- **Implicit harm.** `implicit_labels` flags content that is harmful without saying so.
- **Three model tiers.** Observer for volume, Sentinel by default, Arbiter for the most accurate results. Pick per request.
- **Volume pricing.** One pool of 90,000,000 credits for £13.99 a month, with batches halved.
- **A username endpoint and a Discord bot** that you can invite without writing code.
- **Five SDKs**, including Go, Rust and Java.

Moderation API also covers scams, spam and self-harm, so these are not gaps on its side. The difference is the shape of the product and the extras around labels.

## Pricing, honestly

Supervisor may be more expensive per message in some cases. It bills by size, from one pool of credits.

Derived worked examples, with different currencies and assumed sizes:

| Workload | Supervisor Premium (£13.99) | Moderation API Basic ($79) |
| --- | --- | --- |
| 100 byte text on Sentinel | About 450,000 a month | 10,000 included, then $2.50 per 1,000 |
| 2 KB text on Sentinel | About 22,500 a month | 10,000 included, then $2.50 per 1,000 |
| 200 KB images | About 450 a month | About 3,333 (3 units each) |

At 450,000 short text messages, Basic would cost $79 plus 440,000 extra at $2.50 per 1,000, which is $1,179. For long messages and images Moderation API's unit model is simpler and, for images, cheaper. For short text at volume, Supervisor is much cheaper. Growth includes 100,000 messages with $1.00 per 1,000 beyond, but we have not confirmed its monthly price, so we leave it out.

The [Moderation API pricing breakdown](/blog/moderation-api-pricing) has the detail.

## Which should you use?

- **You run a moderation team with a queue**: Moderation API.
- **You need audio moderation**: Moderation API.
- **Chat, comments, games or a Discord server with high text volume**: Supervisor.
- **You need context handling and implicit labels**: Supervisor.
- **Unsure**: run both on a week of real traffic and compare where they disagree.

## Sources

- [Moderation API homepage](https://moderationapi.com/) and [pricing](https://moderationapi.com/pricing)
- [Authentication](https://docs.moderationapi.com/api-reference/authentication.md) and [rate limits](https://docs.moderationapi.com/api-reference/rate-limits.md)
- [OpenAPI spec](https://api.moderationapi.com/v1/openapi.json)

Paste a message your current setup misses into the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
