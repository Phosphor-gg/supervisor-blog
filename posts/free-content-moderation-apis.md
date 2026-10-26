---
title: "Free content moderation APIs in 2026"
date: 2026-10-26
description: "Which content moderation APIs are actually free? OpenAI's endpoint is, and several others have free tiers or credits. Each one read from the vendor's own page, with the limits."
---

# Free content moderation APIs in 2026

**Bottom line:** only one of these is free without a cap on its own page: OpenAI's moderation endpoint. The others offer free tiers or starter credits that are fine for testing and small projects but have monthly or daily limits. Llama Guard is free to download but costs whatever your hardware costs. **Supervisor** has no permanent free tier for new accounts. We say so up front, then explain what you can try for free and why you might still pay.

Read from vendor pages on 26 October 2026. Free tiers change often, so check before you build on one.

## Summary

| Option | What is free | Limits we found |
| --- | --- | --- |
| OpenAI moderation | The endpoint | No limits on the guide page; rate limits not published for moderation |
| Azure AI Content Safety | F0 tier | 5,000 text records and 5,000 images a month, 5 requests per second, usage stops at the limit |
| AWS Rekognition | Free tier for images | 1,000 images a month during the free tier period (duration not stated on the page we read) |
| AWS Comprehend toxicity | Not confirmed | We could not confirm toxicity is covered by the free tier |
| Hive | Credits | "$50+ in Free Credits after adding a payment method"; 100 requests a day on self-serve models |
| Sightengine | Free tier, no time limit | 2,000 operations a month, 500 a day, 1 request per second |
| Moderation API | Hobby plan | 100 messages a month, no card |
| Llama Guard | Open weights | Licence gate; you pay for hardware |
| Supervisor | Signup credits and trial | 187,500 credits usable for 7 days; 7 day Premium trial with a card |

## OpenAI moderation endpoint

The one genuinely free option. OpenAI's guide says: "The moderation endpoint is free to use, and image files can be up to 20 MB." It takes text and images and returns scores across categories such as harassment, hate, violence, sexual and self-harm. The pricing page we read does not list a separate moderation price. What the guide does not give you is a published rate limit for moderation, a language list, or categories for spam, scams or promotion. It is aimed at screening content around an LLM, and it asks you not to send suspected CSAM. For many projects, that is all you need. See [how it compares with Supervisor](/blog/supervisor-vs-openai-moderation).

## Azure AI Content Safety F0

Azure's free tier allows 5,000 text records and 5,000 images a month, and "Usage is stopped if the transaction limit is reached on the Free tier." A text record is 1,000 characters, so a 7,500 character input counts as 8 records. The free tier runs at 5 requests per second. Good for a prototype.

## AWS

Rekognition's pricing page says that "during the free tier period you can analyze 1,000 images per month for free". We did not extract how long that period lasts. For Comprehend, the pricing page mentions a free tier of 50K units per API per month, but we could not confirm that toxicity detection is among the eligible APIs, so do not assume it is.

## Hive

Hive's pricing page says "$50+ in Free Credits after adding a payment method". The self-serve models list a limit of 100 requests a day, and the currency is shown only as "$". Credit expiry terms were not stated.

## Sightengine

The most generous clearly time-unlimited tier of the paid vendors: 2,000 operations a month (max 500 a day), basic content moderation and AI detection, no time limit ("Yes, you can. There is no time limit."). It runs at 1 request per second. Intended, in its own words, for "testing the API and building proof-of-concepts".

## Moderation API

A free Hobby plan with 100 messages a month and no credit card. Quota units count text as 1, audio as 2 and images as 3, so 100 messages goes quickly if you send images.

## Llama Guard

Free as in no licence fee: Meta publishes weights on Hugging Face under its community licence behind an access gate. The real cost is a GPU to run a 12 billion parameter model (Llama Guard 4), plus the work of serving and scaling it. We could not find an official cost figure.

## Supervisor

Supervisor no longer includes a permanent free tier for new accounts (see [why](/blog/retiring-the-free-tier)). What you can try free: new accounts get 187,500 credits, usable for 7 days from your first moderated message, and there is a 7 day Premium trial that needs a card (a £1 card check is held and released). By our arithmetic, 187,500 credits covers roughly 1,875 messages of 100 bytes on the Observer model, which is the only model free credits can use (context, images, video, Sentinel and Arbiter need Premium or the trial). That is enough to test your own content but not to run a service. After that, Premium is £13.99 a month. If a free endpoint covers your needs, use it. We are for the cases where scams, spam, context and media matter enough to pay.

## How to choose a free option

- **Prototype or LLM guardrail:** OpenAI.
- **Image or video testing with a bigger quota:** Sightengine's free tier.
- **Already on Azure or AWS:** their free tiers, within the limits above.
- **Need to test a review queue or rules engine:** Moderation API's Hobby plan.
- **Production community moderation with context:** budget for a paid plan and use the free credits to test.

## Sources

[OpenAI](https://developers.openai.com/api/docs/guides/moderation), [Azure pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/), [Rekognition pricing](https://aws.amazon.com/rekognition/pricing/), [Comprehend pricing](https://aws.amazon.com/comprehend/pricing/), [Hive pricing](https://thehive.ai/pricing), [Sightengine pricing](https://sightengine.com/pricing), [Moderation API pricing](https://moderationapi.com/pricing), [Llama Guard 4](https://huggingface.co/meta-llama/Llama-Guard-4-12B).

Use your free credits in the [live demo](https://supervisor.gg/demo) or [create a free account](https://supervisor.gg), and see the [API reference](/docs/integrations/api).
