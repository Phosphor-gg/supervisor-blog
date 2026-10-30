---
title: "Supervisor vs Sightengine: text-first moderation versus visual-first"
date: 2026-10-26
description: "Sightengine is the broader visual moderation API; Supervisor is built around community text, context and scams. An honest comparison of labels, languages, media, pricing and who should use which."
---

# Supervisor vs Sightengine: text-first moderation versus visual-first

**Bottom line:** Sightengine is the stronger choice for images and video, with 136 classes across 26 models, AI-generated media detection and live-stream moderation, and it is much cheaper per image. **Supervisor** is the stronger choice for text, with 16 labels that include scam, spam, promotional, self-harm and illegal, context-aware moderation, implicit labels, and translation for non-English messages. Supervisor may cost more per message in some workloads, and we show the arithmetic below. Many teams could reasonably run both.

We make Supervisor, so weigh this accordingly. Sightengine facts come from its own pricing and documentation pages, linked at the end and read on 26 October 2026.

## What each one is

**Sightengine** is a moderation API for images, video, text and audio, scoring each item per class and billing in operations. Plans run from a free tier to Starter ($29 a month), Pro ($99 a month) and a custom Enterprise.

**Supervisor** is a moderation API and a ready-made Discord bot, built for communities, games and platforms. It returns a decision (`flagged`, plus the `labels` that triggered it) and has one paid plan, Premium, at £13.99 a month.

## Side by side

| | Sightengine | Supervisor |
| --- | --- | --- |
| Inputs | Image, video, text, audio | Text, image, video |
| Image and video classes | 136 classes across 26 models | Returns `flagged` and `labels`, as for text |
| Text classes | 6 ML classes plus rule-based classes | 16 labels |
| Scam, promotional labels | Not found as named text classes | Yes, `scam` and `promotional` |
| Conversation context | Not found in docs | `include_context`: `needs_context` and `context_labels` |
| Implicit harm | Not found in docs | `implicit_labels` |
| Non-English text | ML: 7 languages. Rule-based: 18. Others on request | Translated before classification, including slang and mixed-language messages |
| Video | Up to 50 MB (Starter) or 500 MB with live moderation (Pro) | Up to 10 MB and 60 seconds, 20 frames analysed |
| AI-generated media detection, liveness, age estimation | Yes (paid plans) | Not in Supervisor's docs |
| Model tiers | Choose models per request | Observer, Sentinel, Arbiter |
| Batch | Not covered here | Batches of 2 or more at half price |
| Username check | Misleading usernames guide | Dedicated `/username` endpoint |
| SDKs | HTTP examples: curl, Python, PHP, Node | Python, JavaScript, Go, Rust, Java |
| Discord bot | Not found in docs | Ready-made bot |
| Free option | 2,000 operations a month, no time limit | £0.10 of credits for 7 days, plus 7 day Premium trial |

## Where Sightengine is better

- **Visual breadth.** Nudity alone has 31 classes. It also covers violence, weapons, gore, hate imagery, self-harm, drugs, alcohol, tobacco, gambling and more.
- **Media forensics.** AI image and video detection (with generator classes updated through October 2026), deepfake detection, recapture detection, face liveness and AI speech and music detection.
- **Video at scale.** Larger files, live-stream moderation on Pro, and a configurable frame rate.
- **Image cost.** An image with nudity detection counts as one operation. At Starter's $29 for 10,000 operations, that is up to 10,000 images if you run one model each.
- **A free tier that never expires.**

## Where Supervisor is better

- **The labels communities actually fight.** Scam, spam and promotional content are first-class labels, alongside harassment, hate, insult, self-harm and illegal. Sightengine does have spam and self-harm classes, so this is about scam and promotional, plus having them all in one scheme.
- **Context.** A message like "stop it" cannot be judged alone. With `include_context` set, Supervisor tells you when it needs history and which labels it might fall under:

```json
{
    "flagged": false,
    "labels": [],
    "needs_context": true,
    "context_labels": ["harassment"]
}
```

- **Implicit harm.** `implicit_labels` flags content that is harmful without saying so.
- **Language handling.** Non-English text is translated before it is classified, so slang and mixed-language messages go through the same path as English. We do not quote a language count because we have not measured one.
- **Three tiers.** Pick Observer for volume, Sentinel as the default, or Arbiter for the most accurate results.
- **Ecosystem.** Five SDKs, a username endpoint, a batch endpoint, and a Discord bot you can invite without writing code.

## Pricing, honestly

Supervisor may be more expensive per message than a per-operation plan. It bills by size: roughly £0.0014 per KB on Observer, £0.0027 on Sentinel and £0.0055 on Arbiter, from one pool of £120 of credits for £13.99 a month.

Worked examples (derived from published rates, with assumed sizes, in different currencies):

| Workload | Supervisor Premium | Sightengine Starter |
| --- | --- | --- |
| 100 byte text on Sentinel | About 450,000 a month | Text rule not published |
| 2 KB text on Sentinel | About 22,500 a month | Text rule not published |
| 200 KB images (assumed) | About 450 a month | Up to 10,000 with one operation each |

For images, Sightengine is far cheaper. For short text, the plan covers a lot of messages, and batching halves the cost. Read the [Sightengine pricing breakdown](/blog/sightengine-pricing) for the rest.

## Which should you use?

- **Image or video platform** (marketplace, dating, user uploads): Sightengine.
- **Chat, forums, comments, games, Discord**: Supervisor.
- **Both text and media at volume**: use Sightengine for visuals and Supervisor for text, and compare results on your own data.

Detection of AI-generated media, liveness and age estimation are not in Supervisor's docs, so if you need those, Sightengine is the answer.

## Sources

- [Sightengine pricing and FAQ](https://sightengine.com/pricing)
- [Image and video classes](https://sightengine.com/docs/image-video-moderation-classes-and-concepts)
- [Text ML models](https://sightengine.com/docs/text-moderation-ml-models), [text introduction](https://sightengine.com/docs/text-moderation-introduction), [rule-based](https://sightengine.com/docs/text-moderation-rule-based)
- [Sightengine changelog](https://sightengine.com/docs/changelog)

Paste a message your current filter misses into the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
