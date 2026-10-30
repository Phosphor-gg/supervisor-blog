---
title: "Moderation API pricing: plans, units and overage"
date: 2026-10-26
description: "What Moderation API (moderationapi.com) costs: the free Hobby plan, Basic at $79 a month, how units are counted for text, images, audio and video, overage rates, and a worked comparison with Supervisor."
---

# Moderation API pricing: plans, units and overage

**Bottom line:** Moderation API has a free Hobby plan (100 messages a month), then Basic at $79 a month for 10,000 messages with extra messages at $2.50 per 1,000. Growth includes 100,000 messages with extra at $1.00 per 1,000. Enterprise starts at 1,000,000 messages and is custom. Text costs one unit, images three, so a media-heavy workload uses quota faster than a text-only one.

We make a competing product, Supervisor, so we have kept to what Moderation API states on its [pricing page](https://moderationapi.com/pricing) and [homepage](https://moderationapi.com/), read on 26 October 2026. The pricing page quotes USD.

## The plans

| | Hobby | Basic | Growth | Enterprise |
| --- | --- | --- | --- | --- |
| Price | $0, no card | $79 a month, billed monthly | See note below | Talk to their team |
| Messages a month | 100 | 10,000 | 100,000 | 1,000,000+ |
| Pay-as-you-go beyond quota | Not stated | $2.50 per 1,000 | $1.00 per 1,000 | Custom rate |

Growth's monthly price: we could not confirm it from the page source, so we do not print it. Check the live pricing page. On rate limits, the docs say submit-content limits follow "your plan's rate limit tier" and publish no per-plan request numbers, so ask before you depend on a throughput figure.

The homepage also says: "Paid plans start at $79 a month for Basic, which includes a larger monthly quota and pay-as-you-go beyond it." The pricing page lists "20+ ready-made models" and support for "120+ languages" across the plans, and the comparison table covers text, image, video and audio moderation and URL risk analysis.

## How units are counted

The homepage defines it: "Quota is counted in units, where one unit is one message: text costs 1 unit, audio 2 and images 3. Video starts at 3 and rises with length and the number of models you enable."

| Content | Units |
| --- | --- |
| Text | 1 |
| Audio | 2 |
| Image | 3 |
| Video | From 3, rising with length and the number of models enabled |

So 10,000 units on Basic is 10,000 text messages, or about 3,333 images.

## Overage: pay-as-you-go on or off

This is the setting to decide on before launch. From the pricing page: "If pay-as-you-go is on, extra units get billed at the overage rate. If it's off, the API returns an error until your next billing cycle."

With it off, a traffic spike means your moderation calls fail. With it on, a spike is a bill.

## Worked example: 450,000 short text messages a month

This is a derived example. It uses Moderation API's published rates and assumes one unit per text message.

- **Basic:** 10,000 included, 440,000 extra at $2.50 per 1,000, which is $1,100, plus $79, so $1,179 a month.
- **Growth:** 100,000 included, 350,000 extra at $1.00 per 1,000, which is $350, plus the Growth plan fee we have not confirmed.

## How Supervisor compares

Supervisor has one plan, Premium, at £13.99 a month with £120 of credits. Text is billed by size, so the same 450,000 messages is a worked example for Supervisor too: a 100 byte message on Sentinel costs about £0.00027, so Premium covers about 450,000 such messages. Observer covers about 900,000, Arbiter about 225,000, and batches of two or more halve the cost.

The currencies differ (pounds against dollars) and we have not converted them, but at this volume the gap between £13.99 and Basic's $1,179 is wide enough that no plausible exchange rate closes it. The shape of the two plans:

| | Moderation API | Supervisor |
| --- | --- | --- |
| Unit | One message | Price per KB, by model |
| Text | 1 unit | 100 bytes on Sentinel is about £0.00027 |
| Images | 3 units | About £0.0014 per KB of the file |
| Plans | Hobby, Basic, Growth, Enterprise | One paid plan, Premium |
| Free | 100 messages a month, no card | £0.10 of credits for 7 days from your first moderated message (Observer, text only), plus a 7 day Premium trial (card needed, £1 check hold released) |

**Where Moderation API's model is simpler or cheaper:** long messages and images. Its quota unit is one message (we did not find a per-length charge, though message length limits are not covered here), whereas Supervisor charges by size, so a 2 KB message on Sentinel costs about £0.0053 and Premium covers about 22,500 of them. Images are billed at three units flat at Moderation API, whereas Supervisor bills the file size: a 200 KB image (an assumed size) costs about £0.27, so Premium covers about 450 of them. For image-heavy workloads Supervisor is the more expensive of the two.

**Where Supervisor's is cheaper:** large volumes of short text. The plan also includes all three models, context-aware moderation, and image and video moderation, with no separate tiers to climb.

Moderation API includes more than detection: a review queue, author moderation and a rules engine. If you use those, price them into the comparison, because they are not in Supervisor's plan.

## Sources

- [Moderation API pricing](https://moderationapi.com/pricing)
- [Moderation API homepage](https://moderationapi.com/)
- Supervisor rates: [API reference](/docs/integrations/api)

Try your own messages in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
