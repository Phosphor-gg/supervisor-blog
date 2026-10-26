---
title: "Sightengine pricing: plans, operations and what each tier unlocks"
date: 2026-10-26
description: "What Sightengine costs in 2026: the Free, Starter, Pro and Enterprise plans, how operations work, overage rates, and a worked comparison with Supervisor's single plan."
---

# Sightengine pricing: plans, operations and what each tier unlocks

**Bottom line:** Sightengine has a permanent free tier (2,000 operations a month), then Starter at $29 a month for 10,000 operations and Pro at $99 a month for 40,000, with extra operations at $0.002 each. Enterprise is custom. It is cheap per image, but the text pricing rule is not readable on its public pages, so confirm it before you plan a text workload.

We make a competing product, Supervisor, so we have kept to what Sightengine publishes on its own [pricing page](https://sightengine.com/pricing) and documentation, read on 26 October 2026. The page shows a "$" and never states a currency code, so we write "$" and do not convert anything.

## The plans

| | Free | Starter | Pro | Enterprise |
| --- | --- | --- | --- | --- |
| Price | $0 | $29 a month | $99 a month | Custom |
| Operations a month | 2,000 (max 500 a day) | 10,000 | 40,000 | Custom |
| Extra operations | Not stated | $0.002 each | $0.002 each | Custom |
| Max requests per second | 1 | 1 | 10 | Custom |
| Max video size | Not listed | 50 MB, no live streams | 500 MB, live moderation | Custom |
| Concurrent video jobs | Not listed | 1 | 5 | Custom |

Sightengine describes the free tier as "ideal for testing the API and building proof-of-concepts", and the FAQ confirms there is no time limit.

## What each tier unlocks

- **Free:** basic content moderation and AI detection.
- **Starter:** visual moderation, text moderation, AI image and AI video detection, and deepfake detection.
- **Pro:** everything in Starter plus audio moderation, image and video custom search, liveness detection, recapture detection, age estimation, and AI speech and music detection.
- **Enterprise:** custom models and classes, geo-fencing, enterprise SLAs and a dedicated support engineer. The pricing page does not publish SLA figures.

Custom video frame rate is also tiered: 0.5 to 2 fps on Starter and Pro, 0.1 to 10 fps on Enterprise.

## How operations work

Sightengine's definition: "Operations are used to track usage across our services. The number of operations consumed will depend on the type of request made. As an example, running Nudity Detection on an image counts as 1 operation."

Two billing rules worth knowing, both quoted from the FAQ:

- Failed requests are free: "we only count requests that result in a successful response."
- Overage is automatic: "If you exceed your quota we will simply apply the per operation rate and charge you for this additional usage a few days later."

Downgrades and terminations take effect at the end of the current period, which is a 30 day period on monthly plans.

## What the public pages do not tell you

We could not read these from Sightengine's public pages, so we do not state them:

- **How many operations a text request uses.** One example response in the docs, a request using the `general` and `self-harm` models, reports 2 operations, which suggests it counts per model, but that is an example and not a pricing rule.
- **Text length limits.**
- **Annual billing.** The FAQ lists the question, but the answer was not readable.
- **Per-operation pricing for video and live streams.**

Check these with Sightengine before you size a bill.

## Comparing with Supervisor's pricing honestly

Supervisor has one plan: Premium at £13.99 a month, with £120 of credits, all three models, context-aware moderation, and image and video moderation. Credits are billed by size, not per request.

The two plans measure different things, so here are worked examples. They are derived from published rates, not benchmarks, and the currencies are different.

| Workload | Supervisor Premium | Sightengine Starter |
| --- | --- | --- |
| 100 byte text messages on Sentinel (about £0.00027 each) | About 450,000 a month | Text rule not published |
| 200 KB images (about £0.27 each), assumed size | About 450 a month | 10,000 if one operation per image |
| Longer text, 2 KB on Sentinel (about £0.0053 each) | About 22,500 a month | Text rule not published |

**Be clear about the image row.** Supervisor bills images by file size, so images are where we are expensive. If your workload is mostly images, Sightengine is far cheaper per image than Supervisor, and it also offers a far larger set of visual classes. We would not pretend otherwise.

Text is where the arithmetic flips. At about £0.0027 per KB, a short message is cheap, and batching two or more messages in a request halves the cost again. Observer halves the per-byte price, to about £0.0014 per KB against £0.0027 on Sentinel and £0.0055 on Arbiter.

A fair summary: pick Sightengine on price if you moderate lots of images, and Supervisor if you moderate lots of text and want scams, spam, self-harm and context handling in the same call.

Free credits differ too. Sightengine's free tier renews monthly forever. Supervisor gives £0.25 of credits on signup, usable for 7 days from your first moderated message (roughly 1,875 Observer messages of 100 bytes; free credits are Observer and text only), plus a 7 day Premium trial that needs a card, with a £1 check hold that is released.

## Sources

- Sightengine pricing and FAQ: [sightengine.com/pricing](https://sightengine.com/pricing)
- Operation example in text docs: [text moderation ML models](https://sightengine.com/docs/text-moderation-ml-models)
- Supervisor rates: [API reference](/docs/integrations/api) and the [pricing page](https://supervisor.gg/pricing)

Test it on your own content in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
