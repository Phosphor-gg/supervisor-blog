---
title: "Hive vs Sightengine vs Supervisor"
date: 2026-10-26
description: "Two media-first moderation APIs and a paid API for communities. Hive, Sightengine and Supervisor compared from their own docs and pricing pages, including limits and what is sales-gated."
---

# Hive vs Sightengine vs Supervisor

**Bottom line:** Hive and Sightengine both started from visual moderation and both cover text, video and audio. Hive is the more sales-led and handles live streams; Sightengine publishes self-serve plans from $29 a month. **Supervisor** is narrower on media (text, images and short video, no audio or live streams) but adds scams, spam, context and a Discord bot. Choose Hive or Sightengine when images and video are your core problem, Supervisor when community behaviour is.

Read from vendor docs on 26 October 2026. We have not tested accuracy or speed.

## The short answer

- **Hive** if you need live-stream moderation, a large visual taxonomy and a vendor who will negotiate.
- **Sightengine** if you want to sign up and see your price, with many image classes and a free tier.
- **Supervisor** if you moderate people talking to each other and want context, scams and spam as labels.

## At a glance

| | Hive | Sightengine | Supervisor |
| --- | --- | --- | --- |
| Media | Text, images, video, audio, live streams | Image, video, text, audio | Text, images, video |
| Text labels | Sexual, hate, violence, bullying, promotions, spam, external links; severity 0 to 3 | ML: sexual, discriminatory, insulting, violent, toxic, self-harm; rule-based incl. profanity, spam, links | 16 labels |
| Text languages | About 30 | 7 ML, 18 rule-based | Translated to English first |
| Batch endpoint | Docs say not supported | Not found | Yes, half price for 2+ |
| Public pricing | Partly; annual contract mentioned in docs | Yes: free, $29, $99 | Yes: £13.99 a month |
| Free option | "$50+" credits with a card | 2,000 operations a month, no time limit | 7 day trial and signup credits |
| SDK | No Hive SDK in the pages we read | Raw HTTP examples | 5 SDKs |

## Hive

Hive's visual moderation classifies images and video into classes with confidence scores across five groups: sexual content, violent imagery, drugs, hate imagery and image attributes. Video is sampled at one frame per second by default, and live streams over RTMP or HLS are supported. Text moderation is capped at 1,024 characters. It also has a prompt-driven vision-language model.

Friction to know about: video moderation must be enabled through a contact form; higher limits and CSAM detection are "Contact Sales"; and the docs say text and visual moderation require an annual contract, which does not match its pricing page, so confirm pricing directly with Hive. Hive's docs say its APIs do not support batch processing.

## Sightengine

Image and video moderation with 136 classes across 26 models per its docs (the pricing page says 150+), plus text, audio and AI-generated media detection. Starter is $29 a month for 10,000 operations and Pro is $99 for 40,000, each with $0.002 per extra operation; there is a free tier with 2,000 operations a month and a limit of 500 a day. Starter videos are limited to 50 MB with no live streams; Pro allows 500 MB and live moderation. Rate limits are 1 request per second on Free and Starter, 10 on Pro. Currency is shown only as "$". It also documents a misleading-usernames check.

Where it runs out for community work: its machine-learning text classes are six (sexual, discriminatory, insulting, violent, toxic, self-harm); scams and spam come from rule-based pattern matching rather than a model. We did not find a context flag in the text docs we read.

## Supervisor

Where it is narrower: no audio, no live streams, video limited to 60 seconds and 10 MB. Where it is different: 16 labels in one API for text, images and video, including spam, promotional, scam and illegal; `include_context` returning `needs_context`; `implicit_labels`; three model tiers; batches at half price; a username endpoint; five SDKs; and a ready-made Discord bot.

Price is a flat £13.99 a month for £120 of credits, with images billed at about £0.0014 per KB. A large image costs a lot more than a message, so image-heavy workloads should be priced before committing. See [the pricing comparison](/blog/content-moderation-api-pricing-compared).

## Which to choose

| Your situation | Choose |
| --- | --- |
| Live streams | Hive, or Sightengine Pro |
| Images and video, self-serve, published prices | Sightengine |
| Enterprise visual moderation with sales support | Hive |
| Community chat where context, scams and spam matter | Supervisor |
| Audio | Hive or Sightengine |

Sources: [Hive pricing](https://thehive.ai/pricing), [Hive FAQ](https://docs.thehive.ai/docs/frequently-asked-questions-faq), [Hive visual moderation](https://docs.thehive.ai/docs/visual-content-moderation), [Hive text classification](https://docs.thehive.ai/docs/classification-text), [Sightengine pricing](https://sightengine.com/pricing), [Sightengine classes](https://sightengine.com/docs/image-video-moderation-classes-and-concepts), [Sightengine text moderation](https://sightengine.com/docs/text-moderation-introduction).

See how Supervisor handles your content in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg). Also see our [Sightengine comparison](/blog/supervisor-vs-sightengine).
