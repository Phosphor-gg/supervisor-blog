---
title: "Moderation API vs Sightengine vs Supervisor"
date: 2026-10-26
description: "Moderation API, Sightengine and Supervisor compared from their own sites and docs: models and labels, media, languages, review tooling, pricing and free tiers."
---

# Moderation API vs Sightengine vs Supervisor

**Bottom line:** Moderation API is a platform: detection plus a review queue, author moderation and a rules engine. Sightengine is a detection API strongest on images and video, with many visual classes. **Supervisor** is a detection API for communities that returns decisions and labels, with context handling, text, image and video in one API and a Discord bot, but it has no review queue or rules engine of its own in what we compare here. Choose the platform if you want to build a moderation workflow, Sightengine if visuals dominate, Supervisor if community behaviour does.

Read from vendor sites and docs on 26 October 2026. We have not benchmarked accuracy or speed.

## The short answer

- **Moderation API** if you want review queues, author-level views, webhooks and rules, with a broad language claim.
- **Sightengine** if images and video are the main problem and you want published plans.
- **Supervisor** if you need scams, spam and context handled on text, plus images and video, with a decision-oriented response.

## At a glance

| | Moderation API | Sightengine | Supervisor |
| --- | --- | --- | --- |
| Media | Text, images, video, audio | Image, video, text, audio | Text, images, video |
| Models and labels | 20+ ready-made models (homepage lists toxicity, NSFW, profanity, PII, spam, self-harm, scams, phishing, hate speech, harassment) | 136 image and video classes in 26 models; text ML classes plus rule-based | 16 labels |
| Review tooling | Review queue, author moderation, rules engine, webhooks | Callbacks | None in this comparison |
| Languages | "120+" claimed | ML text 7, rule-based 18 | Translated to English first |
| Free tier | 100 messages a month | 2,000 operations a month | 7 day trial and signup credits |
| Entry price | $79 a month (USD) | $29 a month ("$") | £13.99 a month (GBP) |
| SDKs | TypeScript, Python, PHP, Ruby, CLI (in the OpenAPI spec) | Raw HTTP examples in the docs we read | Python, JavaScript, Go, Rust, Java |
| Auth | Bearer API key | `api_user` and `api_secret` | Bearer API key |

## Moderation API

The homepage describes an "AI content moderation API and review platform" with "Detection, Review, User Management, and Compliance". Quota is counted in units: text costs 1, audio 2 and images 3, and video starts at 3 and rises with length and the number of models. Plans: free Hobby (100 messages a month, no card); Basic at $79 a month for 10,000 messages then $2.50 per 1,000; Growth with 100,000 messages and $1.00 per 1,000 beyond (we could not verify its monthly price); Enterprise custom. With pay-as-you-go off, the API returns an error until the next billing cycle. Documented submit-content rate limits depend on plan tier and the numbers are not published on the rate-limits page.

## Sightengine

Detection only, but wide: nudity (31 classes), violence, weapons, gore, hate, self-harm, drugs, alcohol, gambling and more for images and video; text classes for sexual, discriminatory, insulting, violent, toxic and self-harm, plus rule-based classes such as profanity, spam, links and personal information. Plans: Free (2,000 operations a month), Starter $29 (10,000), Pro $99 (40,000), each overage at $0.002; Enterprise on request. It documents a misleading-usernames check and AI-generated media detection. Currency is shown only as "$".

## Supervisor

Returns `flagged` and labels from 16: profanity, toxicity, harassment, hate, insult, sexual (three variants), sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. `include_context` flags messages needing conversation history, `implicit_labels` covers implied harm, and a username endpoint checks names. Three model tiers, half-price batches, video with timestamps (60 seconds, 10 MB), SDKs in five languages and a Discord bot. £13.99 a month, 90,000,000 credits, billed by the byte, which makes long messages and large images use the allowance faster. If you need a review queue or rules engine, you would build that around the API or choose Moderation API.

Scams and spam are not unique to us: Moderation API lists scams, phishing and spam models, and Sightengine has rule-based spam. The difference is how they are packaged and what else sits beside them.

## Which to choose

| Your situation | Choose |
| --- | --- |
| Need a human review queue and rules out of the box | Moderation API |
| Image-heavy product | Sightengine |
| Discord community or platform chat | Supervisor |
| Many languages, broad claim | Moderation API (test it) |
| Smallest entry price | Sightengine |

Sources: [Moderation API homepage](https://moderationapi.com/), [Moderation API pricing](https://moderationapi.com/pricing), [rate limits](https://docs.moderationapi.com/api-reference/rate-limits.md), [OpenAPI spec](https://api.moderationapi.com/v1/openapi.json), [Sightengine pricing](https://sightengine.com/pricing), [classes and concepts](https://sightengine.com/docs/image-video-moderation-classes-and-concepts), [text moderation](https://sightengine.com/docs/text-moderation-introduction). Also see our [Sightengine comparison](/blog/supervisor-vs-sightengine).

Test Supervisor in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
