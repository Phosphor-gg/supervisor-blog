---
title: "OpenAI moderation vs Llama Guard vs Supervisor"
date: 2026-10-26
description: "A free hosted endpoint, a self-hosted open-weights classifier and a paid community moderation API. OpenAI, Llama Guard and Supervisor compared from their own model cards and docs."
---

# OpenAI moderation vs Llama Guard vs Supervisor

**Bottom line:** these are three different kinds of thing. OpenAI's endpoint is a free hosted API. Llama Guard is an open-weights model you run yourself, so you control the data and the infrastructure and pay for the GPU. **Supervisor** is a paid hosted API for community and platform moderation. If you are guarding an LLM, OpenAI or Llama Guard are the natural pair. If you are moderating people talking to each other, Supervisor's extra labels and context handling are the reason to pay.

Read from vendor pages on 26 October 2026. The Llama Guard model cards are gated on Hugging Face, so quotes from them come from a rendered copy and should be checked against the live card. We have not benchmarked any of these.

## The short answer

- **OpenAI** for free, hosted, no infrastructure.
- **Llama Guard** if you must keep content on your own hardware, or want a safety model you can run beside your own LLM.
- **Supervisor** for communities and platforms that need scams, spam, context and media in one hosted API.

## At a glance

| | OpenAI | Llama Guard 4 | Supervisor |
| --- | --- | --- | --- |
| Type | Hosted API | Open-weights model (12B), self-hosted | Hosted API and Discord bot |
| Input | Text, images | Text and multiple images | Text, images, video |
| Taxonomy | 13 category keys in the guide | 14 categories (MLCommons-based) | 16 labels |
| Spam, scam, promotional | Not in the categories shown | Not in the taxonomy | Yes |
| Languages | No list | English plus 7 tested | Translated to English first |
| Price | Free | No API price; your hardware | £13.99 a month |
| Access | API key | Hugging Face account and accepted licence | API key |

## OpenAI

Free to use, accepts text and images, returns categories and scores for sexual, harassment, hate, illicit, self-harm and violence (with subcategories). It can also return moderation alongside a generated response. The guide advises treating scores as signals, not automatic blocking decisions, and says not to send suspected CSAM.

## Llama Guard

Llama Guard 4 is described as a natively multimodal safety classifier with 12 billion parameters, "designed to be used in an integrated system with a generative language model". It classifies LLM inputs (prompt classification) and responses. Its labels follow the MLCommons taxonomy: violent crimes, non-violent crimes, sex-related crimes, child sexual exploitation, defamation, specialised advice, privacy, intellectual property, indiscriminate weapons, hate, suicide and self-harm, sexual content, elections, and code interpreter abuse (text only). It supports English and multilingual text, tested on French, German, Hindi, Italian, Portuguese, Spanish and Thai, and the card says it can run on a single GPU. Weights sit behind a licence gate under the Llama 4 Community Licence.

What you take on: hosting, scaling, updates, and the work of turning a safety classification into the decisions your community needs. There is no spam or scam category, and we found no published cost or rate limit, because it depends on your setup. Its design centre is LLM prompts and responses rather than community chat, per its own description.

## Supervisor

Hosted, so nothing to run. 16 labels, three tiers, `include_context`, `implicit_labels`, video with timestamps, batches at half price, a username endpoint, five SDKs, a Discord bot. Premium is £13.99 a month for 90,000,000 credits, with no permanent free tier. You do not get weights or an on-premises option from us in this comparison, so if data must never leave your hardware, Llama Guard is the right answer.

## Which to choose

| Your situation | Choose |
| --- | --- |
| Free, quick, hosted | OpenAI |
| Data must stay on your hardware | Llama Guard |
| You already run GPUs for an LLM | Llama Guard, perhaps beside OpenAI |
| Community with scams, spam and subtle abuse | Supervisor |
| Video | Supervisor (60 seconds, 10 MB per clip) |

Sources: [OpenAI moderation guide](https://developers.openai.com/api/docs/guides/moderation), [Llama Guard 4 model card](https://huggingface.co/meta-llama/Llama-Guard-4-12B), [Llama Guard 3 8B model card](https://huggingface.co/meta-llama/Llama-Guard-3-8B). See also our [OpenAI comparison](/blog/supervisor-vs-openai-moderation).

Try your own messages in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
