---
title: "Supervisor vs Llama Guard: hosted moderation API versus self-hosted classifier"
date: 2026-10-26
description: "Llama Guard is Meta's open-weight safety classifier for LLM prompts and responses; Supervisor is a hosted moderation API for community content. An honest comparison of labels, control, cost and who should use which."
---

# Supervisor vs Llama Guard: hosted moderation API versus self-hosted classifier

**Bottom line:** they are built for different jobs. Llama Guard 4, the version covered here, is a free-to-download classifier for **LLM prompts and responses** that you host yourself, with total control over the infrastructure. **Supervisor** is a hosted moderation API and Discord bot for **user-generated community content**, with 16 labels including scam, spam, promotional, self-harm and illegal, context-aware moderation, and translation for non-English text. Llama Guard costs you GPUs and engineering time, and Supervisor costs £13.99 a month. If you are guarding an LLM, start with Llama Guard. If you are moderating people, start with Supervisor.

We make Supervisor, so weigh this accordingly. Llama Guard facts come from its Hugging Face model card, which is gated, so we read it as extracted text and recommend checking it against the live page. Read on 26 October 2026.

## What each one is

**Llama Guard 4** is described on its card as "a natively multimodal safety classifier with 12 billion parameters", "designed to be used in an integrated system with a generative language model". It is a dense model pruned from Llama 4 Scout, classifies against 14 categories based on the MLCommons safety taxonomy, and takes text and multiple images. It is distributed under the Llama 4 Community License behind an access gate on Hugging Face. You run it with the `transformers` library.

**Supervisor** is a moderation API (`POST /api/moderate`) and a ready-made Discord bot for communities, games and platforms. You send text, an image or a short video and get back a decision: `flagged`, plus the `labels` that triggered it.

## Side by side

| | Llama Guard 4 | Supervisor |
| --- | --- | --- |
| Designed for | LLM prompt and response safety | Community and platform content moderation |
| Delivery | Open weights you host | Hosted API and Discord bot |
| Categories | 14 MLCommons-based: violent crimes, non-violent crimes, sex-related crimes, child sexual exploitation, defamation, specialized advice, privacy, intellectual property, indiscriminate weapons, hate, suicide and self-harm, sexual content, elections, code interpreter abuse | 16 labels: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam, illegal |
| Spam, scam, promotional | No category with those names | Yes |
| Conversation context | Not covered here | `include_context`: `needs_context` and `context_labels` |
| Implicit harm | Not covered here | `implicit_labels` |
| Inputs | Text and multiple images | Text, image, video |
| Languages | English plus French, German, Hindi, Italian, Portuguese, Spanish and Thai tested | Non-English translated before classification, including slang and mixed-language messages |
| Model choice | One 12B model | Observer, Sentinel, Arbiter |
| Integration | Your own serving stack | REST API, SDKs for Python, JavaScript, Go, Rust and Java |
| Price | No licence fee, your own GPU and hosting | £13.99 a month, 90,000,000 credits |
| Where content goes | Stays on your infrastructure | Sent to Supervisor |

## Where Llama Guard is better

- **Control.** You own the deployment, the data path and the upgrade schedule. Content never leaves your infrastructure unless you send it elsewhere. A hosted API cannot match that.
- **No licence fee.** Weights are free to download once you accept the licence. Whether that is cheaper than a plan depends on your volume and hardware, and we do not have a number.
- **Fit for LLM guardrails.** It is built to classify prompts and responses around a generative model, and its taxonomy includes categories like code interpreter abuse and elections that a community moderation API does not name.
- **Multi-image input.** The card says it supports safety classification when multiple images are given, though its testing mostly used prompts with a few images (three most frequently).
- **Taxonomy breadth on legal topics.** Defamation, intellectual property and specialised advice are not among Supervisor's labels.

## Where Supervisor is better

- **No infrastructure.** No GPU to provision, no serving stack to build. You make an HTTP call:

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "stop it",
    "model": "sentinel",
    "include_context": true
  }'
```

- **Labels communities actually deal with.** Scams, spam, promotional content, insults and profanity are first-class labels. Llama Guard's categories have none of those names.
- **Context.** With `include_context`, the response says when a message needs conversation history and which labels it might fall under.
- **Implicit harm.** `implicit_labels` for content that is harmful without saying so.
- **Language handling.** Translation before classification means slang and mixed-language text take the same path as English. We do not quote a language count.
- **Video, a username endpoint, batches at half price, five SDKs and a Discord bot** are part of the product.

## Pricing, honestly

Llama Guard has no per-message price, which is a real advantage at very high volume if you already have GPU capacity. Supervisor has one: £13.99 a month for 90,000,000 credits, billed by size.

A derived worked example for Supervisor: a 100 byte message on Sentinel is 200 credits, so Premium covers about 450,000 such messages a month (900,000 on Observer, 225,000 on Arbiter), and batches of two or more cost half. A 2 KB message is 4,000 credits, about 22,500 a month. A 200 KB image (assumed size) is 200,000 credits, about 450 a month.

Supervisor may be more expensive per message than a GPU you already own. Self-hosting is not free, though: you pay for hardware, power, operations and the time to keep it running, and we have no figure for that cost.

## Which should you use?

- **Guarding an LLM or agent**: Llama Guard.
- **Moderating chat, comments, uploads or a Discord server**: Supervisor.
- **Data must never leave your infrastructure**: Llama Guard.
- **You do not want to run GPUs**: Supervisor.
- **Both**: a self-hosted guard on model traffic and Supervisor on user content is a sensible split.

## Sources

- Llama Guard 4: [model card](https://huggingface.co/meta-llama/Llama-Guard-4-12B)
- Llama Guard 3 8B: [model card](https://huggingface.co/meta-llama/Llama-Guard-3-8B)

See the [alternatives to Llama Guard](/blog/llama-guard-alternatives), try the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
