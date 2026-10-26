---
title: "Moderation API review: what it is good at and where it runs out"
date: 2026-10-26
description: "An honest review of Moderation API (moderationapi.com) from a company that makes a competing tool: its review queue, 20+ models, language claims, pricing and where a per-message platform stops."
---

# Moderation API review: what it is good at and where it runs out

**Bottom line:** Moderation API is more than a classifier. It combines detection with a review queue, author management and a rules engine, supports text, images, video and audio, and claims 120+ languages. That workflow layer is its strength. Its weak spots are cost at volume (Basic is $79 a month for 10,000 messages) and a first paid step that is not small. Supervisor is a lighter, cheaper-per-text-message option when you want a decision API and a Discord bot rather than a platform.

We make Supervisor, so treat this as an interested party's assessment. Every Moderation API claim comes from its own homepage, pricing page, docs and OpenAPI spec, linked at the end and read on 26 October 2026. Where we could not confirm something, we say so.

## What Moderation API is

Its homepage: "Moderation API is an AI content moderation API and review platform for text, images, video and audio, with custom rules and support for 120+ languages." It groups its product into "Detection, Review, User Management, and Compliance, in one platform."

The API base is `https://api.moderationapi.com/v1`, with endpoints for moderating text, images and combined content, plus authors, review queue items, actions, webhooks, wordlists, projects and channels. Authentication is an API key as a Bearer token over HTTPS.

## What Moderation API does well

**It is a platform, not just a score.** The homepage lists a review queue, author moderation and a rules engine, with an example rule: "If Content contains links And Account age < 7 days Then Reject". Webhooks cover queue and author events such as new queue items, completed items, author blocked and author trust level changed.

**The model list is broad.** Ready-made models named on the homepage: toxicity, NSFW, profanity, PII, spam, self-harm, sentiment, sensitive topics, scams, phishing, URL risks, hate speech, harassment, SHAFT and language ID. The pricing page says "20+ ready-made models".

**Custom guidelines.** You can write policies in plain language and add custom models.

**Many input types.** Text, images, video and audio, all through one account.

**A free plan with no card.** Hobby covers 100 messages a month.

**Language reach.** "Global 120+ languages, one API." The homepage shows examples including Spanish, Portuguese, Danish, Italian, Arabic, Chinese, Hindi, Swahili and Indonesian.

**SDKs.** The OpenAPI spec includes code samples for TypeScript (`@moderation-api/sdk`), Python (`moderation_api`), PHP, Ruby and a CLI.

**Published rate-limit behaviour.** The rate-limit docs list `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset` and `Retry-After` headers, and a 429 response when you exceed a limit.

## Where Moderation API runs out

**Cost grows quickly with volume.** Basic is $79 a month for 10,000 messages and extra messages are $2.50 per 1,000. A worked example: 450,000 text messages a month on Basic comes to $1,179 (10,000 included plus 440,000 at $2.50 per 1,000, plus $79). See the [pricing breakdown](/blog/moderation-api-pricing).

**Images and video use more quota.** Images are 3 units each, audio 2, and video starts at 3.

**Overage can stop the API.** With pay-as-you-go off, "the API returns an error until your next billing cycle."

**Throughput is plan-dependent and unpublished.** Submit-content limits follow your plan's tier, with no numbers on the rate-limits page.

**What we could not confirm.** The monthly price of Growth, the exact label names returned by the moderate endpoint, and per-plan rate-limit numbers. We did not read those from a primary page, so we do not state them.

## Where Supervisor fills the gaps, and where it does not

| | Moderation API | Supervisor |
| --- | --- | --- |
| Review queue, author management, rules engine | Yes | Not claimed here |
| Models and labels | 20+ models, per its pricing page | 16 labels: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam, illegal |
| Conversation context | Not confirmed | `include_context`: `needs_context` and `context_labels` |
| Implicit harm | Not confirmed | `implicit_labels` |
| Languages | 120+ claimed | Non-English translated before classification, including slang and mixed-language messages. No count claimed |
| Inputs | Text, image, video, audio | Text, image, video |
| SDKs | TypeScript, Python, PHP, Ruby, CLI confirmed | Python, JavaScript, Go, Rust, Java |
| Discord bot | Not covered | Ready-made bot |
| Pricing | From $79 a month for 10,000 messages | £13.99 a month for £120 of credits |

Two honest cost notes. Supervisor bills by size, so a 2 KB message on Sentinel costs about £0.0053 (about 22,500 a month) and a 200 KB image about £0.27 (about 450 a month, an assumed size). Moderation API charges three units per image. For short text Supervisor goes much further: about 450,000 messages of 100 bytes a month on Sentinel, a derived worked example.

## Who Moderation API is right for

- **Trust and safety teams** that want a hosted review queue and author-level controls.
- **Products that need audio moderation** or very broad language claims.
- **Small projects** that fit inside the 100 message free plan or the 10,000 message Basic plan.

It is a weaker fit if you mostly need a cheap, fast decision API for large volumes of short text, or a ready-made Discord bot.

## Sources

- [Moderation API homepage](https://moderationapi.com/) and [pricing](https://moderationapi.com/pricing)
- [Authentication docs](https://docs.moderationapi.com/api-reference/authentication.md) and [rate limits](https://docs.moderationapi.com/api-reference/rate-limits.md)
- [OpenAPI spec](https://api.moderationapi.com/v1/openapi.json)

Read the [alternatives](/blog/moderation-api-alternatives) and the [direct comparison](/blog/supervisor-vs-moderation-api), try the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
