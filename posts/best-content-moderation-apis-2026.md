---
title: "Best content moderation APIs in 2026"
date: 2026-10-26
description: "Eight content moderation APIs compared from their own docs and pricing pages: OpenAI, Azure, AWS, Hive, Sightengine, Moderation API, Llama Guard and Supervisor, each with an honest best-for."
---

# Best content moderation APIs in 2026

**Bottom line:** there is no single best moderation API, because the tools solve different jobs. OpenAI's endpoint is free and strong for screening an LLM app. Azure and AWS suit teams already on those clouds. Hive and Sightengine are built around images and video. Moderation API adds a review queue and rules engine. Llama Guard is the one you host yourself. **Supervisor** is our own product, a paid API for communities and platforms that need scams, spam and context handled alongside harm, with text, images and video behind one API. We put it first because we wrote this, so read the best-for line on each entry rather than the order.

Everything below was read from each vendor's own documentation or pricing page on 26 October 2026. Where a page contradicted itself, or we could not read a detail, we say so or leave it out. We have not run accuracy or latency tests across these tools, so you will not find a speed or accuracy ranking here.

Google's Perspective API is not on the list because it is [shutting down after 31 December 2026](/blog/perspective-api-migration-guide).

## Quick picks

| If you need | Look at |
| --- | --- |
| Free text and image safety screening for an LLM app | OpenAI moderation endpoint |
| Moderation inside an existing Azure estate | Azure AI Content Safety |
| Image and stored-video moderation inside AWS | Amazon Rekognition (plus Comprehend for text) |
| Visual moderation with live streams, sales-led | Hive |
| Image and video moderation with public monthly plans | Sightengine |
| A review queue, rules engine and many languages | Moderation API |
| A model you host yourself | Llama Guard |
| Scams, spam and context for a community or platform, plus a Discord bot | Supervisor |

## At a glance

| | Text | Images | Video | Pricing shape | Free option |
| --- | --- | --- | --- | --- | --- |
| Supervisor | Yes | Yes | Yes | £13.99 a month, one plan | 7 day trial and signup credits |
| OpenAI | Yes | Yes | Not listed | Free | The endpoint itself |
| Azure AI Content Safety | Yes | Yes | Not in the pages we read | Per 1,000 records (USD) | F0 tier |
| AWS | Comprehend (text) | Rekognition | Rekognition (stored video) | Per unit, per image, per minute (USD) | Partial |
| Hive | Yes | Yes | Yes | Per request list rates, plus contact sales | Credits after adding a card |
| Sightengine | Yes | Yes | Yes | Monthly plans from $29 | Free tier, no time limit |
| Moderation API | Yes | Yes | Yes | Monthly plans from $79 | 100 messages a month |
| Llama Guard 4 | Yes | Yes | No (multi-image prompts) | Your own hardware | Open weights, gated licence |

## Supervisor

**Best for:** communities and platforms that need more than a harm filter: scams, spam and self-promotion caught alongside abuse, a way to flag messages that cannot be judged alone, and one API for text, images and video. Also the only entry here with a ready-made Discord bot.

Supervisor returns 16 labels: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. A few things are worth knowing:

- **Context.** Set `include_context` and the response carries `needs_context`, so you know when a message such as "stop it" needs the conversation around it before you act.
- **Implicit harm.** `implicit_labels` covers content that is harmful without saying so outright.
- **Media.** Text, images and video go through the same API. Video accepts clips up to 60 seconds and 10 MB, analyses up to 20 frames and returns a timestamp for each flagged frame.
- **Languages.** Non-English messages are translated to English before classification, including slang and mixed-language text. We do not publish a language count.
- **Three model tiers.** Observer, Sentinel (the default) and Arbiter, billed at about £0.0014, £0.0027 and £0.0055 per KB of text.
- **Batching.** The batch endpoint bills batches of two or more at half price.
- **Extras.** A username check endpoint and SDKs for Python, JavaScript, Go, Rust and Java.

**The honest part on price.** Supervisor has no permanent free tier and is not the cheapest option. Premium is £13.99 a month (£83.85 a year) with £120 of credits. New accounts get £0.25 of free credits, usable for 7 days from the first moderated message, and there is a 7 day Premium trial with a card. Against OpenAI's free endpoint, Supervisor always costs more. Against per-request APIs the answer depends on your message size and volume, which is why we wrote a [pricing comparison](/blog/content-moderation-api-pricing-compared) that shows the arithmetic.

We have not published accuracy or latency numbers in this post and you should not take our word for either. Paste your own worst messages into the [live demo](https://supervisor.gg/demo).

## OpenAI moderation endpoint

**Best for:** free text and image safety screening in front of or behind an LLM.

OpenAI's guide says the endpoint accepts text and images with `omni-moderation-latest`, and that it "doesn't classify audio". It is free: "The moderation endpoint is free to use, and image files can be up to 20 MB." Its categories are the safety set: sexual (including minors), harassment, hate, illicit, self-harm, and violence, each with subcategories. It also supports inline moderation, where you pass a `moderation` object in a generation request and get scores for input and output together.

Limits to know: the guide tells you to treat scores "as signals for your application's policy, not as an automatic blocking decision", it asks you not to send suspected CSAM to it, and it does not publish a language list or moderation-specific rate limits. The categories shown in the guide have no spam, scam or promotional label. If your problem is harm in an app you control, this is hard to beat on price. See our [direct comparison with OpenAI](/blog/supervisor-vs-openai-moderation).

## Azure AI Content Safety

**Best for:** teams already on Azure who want text and image moderation with severity levels, blocklists and Microsoft's identity and SDK tooling.

Azure classifies text and images into four harm categories: hate, sexual, violence and self-harm. Text supports a 0 to 7 severity scale (trimmable to four levels); the image model returns 0, 2, 4 or 6. Blocklists are supported. Microsoft says its classifiers are trained and tested on eight languages (Chinese, English, French, German, Italian, Japanese, Portuguese and Spanish) and "can work in many other languages, but the quality might vary". SDKs exist for Python, .NET, Java and JavaScript. The F0 free tier allows 5,000 text records and 5,000 images a month.

The four categories mean no spam or scam label. We did not find a video API on the Content Safety pages we read, though the retired Content Moderator product did list video.

## AWS: Amazon Rekognition and Amazon Comprehend

**Best for:** AWS shops that want image and stored-video moderation, or a text toxicity call, billed as part of their AWS account.

AWS splits the job in two. **Rekognition** moderates images and stored video with a three-level label taxonomy and a confidence score per label, and supports custom moderation adapters you train on your own images. **Comprehend** has a `DetectToxicContent` API for text, returning scores for seven labels: graphic, harassment or abuse, hate speech, insult, profanity, sexual, and violence or threat. Rekognition's docs say plainly that it "isn't an authority on, and doesn't in any way claim to be an exhaustive filter of, inappropriate or offensive content" and that the moderation APIs don't detect illegal content such as CSAM. Moderation of streaming video is not among the Rekognition streaming features we found.

## Hive

**Best for:** organisations that want visual moderation across images, video and live streams and are happy to go through sales.

Hive classifies whole images or videos into classes with a confidence score, samples video at one frame per second by default, and accepts live streams over RTMP or HLS. Its text moderation covers classes such as sexual, hate, violence, bullying, promotions and spam, with severity from 0 to 3, across roughly 30 languages. It also offers a prompt-driven vision-language model. Video must be enabled through its contact form, and its docs say Hive APIs do not support batch processing. Pricing is split between public list rates and contact-sales items, and the docs and pricing page disagree on whether an annual contract is needed (details in our [pricing comparison](/blog/content-moderation-api-pricing-compared)).

## Sightengine

**Best for:** image and video moderation with a wide set of visual classes and public monthly plans.

Sightengine's docs list 136 classes across 26 image and video models (its pricing page says 150+), covering nudity, violence, weapons, gore, hate, self-harm, drugs, alcohol and more. Text moderation combines machine-learning classes (sexual, discriminatory, insulting, violent, toxic, self-harm) with rule-based classes such as profanity, spam, personal information and links. It also offers audio moderation, AI-generated media detection and a documented misleading-usernames check. Plans are public: a free tier, $29 and $99 a month, and a custom enterprise tier.

## Moderation API

**Best for:** teams that want a review queue, an author-level view and a rules engine on top of the detection API.

Moderation API describes itself as a platform for text, images, video and audio with "120+ languages". Its homepage lists ready-made models including toxicity, NSFW, profanity, PII, spam, self-harm, scams, phishing, hate speech and harassment. Beyond detection it has a review queue, author moderation and a rules engine, plus webhooks. Plans start with a free Hobby tier of 100 messages a month, then $79 a month for 10,000.

## Llama Guard

**Best for:** teams that need the classifier on their own hardware, or want to adapt a safety model around an LLM.

Llama Guard 4 is a 12 billion parameter multimodal safety classifier from Meta, designed "to be used in an integrated system with a generative language model". It predicts labels from a 14-category taxonomy based on the MLCommons hazard taxonomy, from violent crimes through hate, suicide and self-harm, to code interpreter abuse. It supports English and multilingual text, tested on French, German, Hindi, Italian, Portuguese, Spanish and Thai. There is no API price: the weights are on Hugging Face behind a licence gate, and you pay for the hardware. That also means you own the latency, scaling and updates.

## How to choose

1. **Is it a harm filter or community moderation?** If scams, spam and self-promotion matter as much as abuse, check that the label set includes them. Supervisor, Hive, Moderation API and Sightengine's rule-based text classes do; Azure's four categories and OpenAI's published categories do not.
2. **What media do you take in?** Text only, text and images, or video too. Video support varies a lot: clip limits, frame sampling and live-stream support all differ.
3. **Which languages?** Only some vendors publish a list. See our [multilingual comparison](/blog/best-multilingual-moderation-apis).
4. **How do you want to pay?** Free, per request, monthly plan, or your own GPU. Do the arithmetic for your own message size.
5. **Test it.** Run a few hundred of your own messages through two or three candidates and read the disagreements.

## Sources

- OpenAI: [moderation guide](https://developers.openai.com/api/docs/guides/moderation)
- Azure: [overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview), [harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/)
- AWS: [Rekognition moderation](https://docs.aws.amazon.com/rekognition/latest/dg/moderation.html), [Comprehend DetectToxicContent](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html)
- Hive: [pricing](https://thehive.ai/pricing), [visual moderation](https://docs.thehive.ai/docs/visual-content-moderation), [text classification](https://docs.thehive.ai/docs/classification-text)
- Sightengine: [pricing](https://sightengine.com/pricing), [classes and concepts](https://sightengine.com/docs/image-video-moderation-classes-and-concepts)
- Moderation API: [homepage](https://moderationapi.com/), [pricing](https://moderationapi.com/pricing)
- Llama Guard: [Llama Guard 4 model card](https://huggingface.co/meta-llama/Llama-Guard-4-12B)
- Perspective: [perspectiveapi.com](https://www.perspectiveapi.com/)

Vendors change their products and prices, so check the source before you buy.

Try Supervisor on your own messages in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg) and get an API key.
