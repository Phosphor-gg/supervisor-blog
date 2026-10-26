---
title: "Best multilingual moderation APIs in 2026"
date: 2026-10-26
description: "Which moderation APIs publish a language list, and which do not? Hive, Sightengine, Azure, Llama Guard, Moderation API, OpenAI, AWS and Supervisor compared on what each vendor actually states."
---

# Best multilingual moderation APIs in 2026

**Bottom line:** "supports many languages" means very different things. Hive and Sightengine publish per-language tables. Azure and Llama Guard publish the languages they trained and tested on. Moderation API claims 120+ languages. OpenAI and AWS's toxicity API are unclear. **Supervisor**, our own product, takes a different approach: it translates non-English text to English before classifying it, including slang and mixed-language messages. We do not publish a language count, and we have not published per-language accuracy, so we cannot tell you it is better on any particular language. It is best for communities where members mix languages and slang in the same message and you want one label set regardless.

This post only repeats what each vendor states, as read on 26 October 2026. A vendor that publishes a list is not necessarily more accurate than one that does not, and we have not tested any of them across languages. Test on your own languages.

## What each vendor states

| | What the vendor says | Where |
| --- | --- | --- |
| Supervisor | Non-English text is translated to English before classification | Our implementation, no count published |
| OpenAI | No language list in the moderation guide | Moderation guide |
| Azure AI Content Safety | Trained and tested on 8 languages; others may work, quality varies | Overview and region pages |
| AWS Comprehend toxicity | Conflicting: 12 codes listed, but "English is the only supported language" | API reference |
| AWS Rekognition | Not applicable, visual | n/a |
| Hive | About 30 languages, 31 listed, with per-class coverage | Text classification docs |
| Sightengine | ML text: 7 languages. Rule-based: 18 listed | Text moderation docs |
| Moderation API | "120+ languages" | Homepage and pricing page |
| Llama Guard 4 | English and multilingual text; 7 non-English languages tested | Model card |

## Supervisor

**Best for:** mixed-language and slang-heavy communities that want one pipeline and one set of labels.

Non-English messages are translated to English first and then classified, including slang and mixed-language messages. The upside: the same 16 labels, context handling and `implicit_labels` apply whatever language the user wrote in, and you do not manage per-language configuration. The trade-off is inherent to the approach: the classification can only be as good as the translation step, and we do not claim a number of supported languages or per-language accuracy. If your community writes in a language with limited translation support, test it first in the [live demo](https://supervisor.gg/demo). There is more in our [multilingual Discord moderation post](/blog/multilingual-discord-moderation).

## Hive

**Best for:** teams that want to see exactly which languages and classes are covered.

Hive says: "We support ~30 languages, and our models also understand emojis." Its table lists 31 languages, including English, Spanish, Hindi, French, Portuguese, Arabic, German, Italian, Turkish, Chinese, Russian, Dutch, Korean, Japanese, Vietnamese, Thai, Ukrainian and Haitian Creole. Coverage varies by class: for example, some Dutch classes are marked beta, and Vietnamese and Romanian have no hate class. When a class is not supported for a detected language, its score is -1. Hive also says it will add languages on request.

## Sightengine

**Best for:** teams who need explicit language selection and are fine with two tiers of coverage.

The machine-learning text classes support English, French, Italian, Portuguese, Spanish, Russian and Turkish, with others available on request. The rule-based classes list eighteen: English, Chinese, Danish, Dutch, Finnish, French, German, Italian, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, Spanish, Swedish, Tagalog and Turkish. You can pass several language codes as a comma-separated list if you are unsure what language a user writes in.

## Azure AI Content Safety

**Best for:** Azure teams working mainly in major European and East Asian languages.

Microsoft says its text classifiers for hate, sexual, violence and self-harm are trained and tested on Chinese, English, French, German, Italian, Japanese, Portuguese and Spanish, and that the features "can work in many other languages, but the quality might vary". Some features (protected material, groundedness, custom categories) are English only or trained on English.

## Moderation API

**Best for:** teams that want a broad language claim and a review queue.

The homepage says "Global 120+ languages, one API", and the pricing page repeats "Support for 120+ languages". Its example languages include English, Spanish, Portuguese, Danish, Italian, Arabic, Chinese, Hindi, Swahili and Indonesian. We did not find per-language quality statements, so the claim is breadth, not a quality guarantee.

## Llama Guard 4

**Best for:** self-hosted setups in the languages Meta tested.

The model card says it supports "English and multilingual text prompts", with non-English languages tested being French, German, Hindi, Italian, Portuguese, Spanish and Thai. Coverage beyond those is not stated. (Quotes are from the gated Hugging Face model card.)

## OpenAI and AWS

OpenAI's moderation guide does not state supported languages. AWS Comprehend's toxicity reference lists twelve language codes (en, es, fr, de, it, pt, ar, hi, ja, ko, zh, zh-TW) but also says English is currently the only supported language; those statements conflict on the same page, so confirm with AWS before sending non-English text. Rekognition is visual, so language does not apply to it.

## How to test

1. Collect 100 to 200 real messages in each language you care about, including slang and mixed-language ones.
2. Run them through two or three candidates.
3. Read the disagreements, not the average.
4. Check how each handles a language it does not list: Hive returns -1 for an unsupported class, Azure says quality varies, and Supervisor translates.

## Sources

[Hive text classification](https://docs.thehive.ai/docs/classification-text), [Sightengine ML text](https://sightengine.com/docs/text-moderation-ml-models), [Sightengine rule-based text](https://sightengine.com/docs/text-moderation-rule-based), [Azure overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview), [Azure region availability](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability), [Moderation API](https://moderationapi.com/), [Llama Guard 4](https://huggingface.co/meta-llama/Llama-Guard-4-12B), [OpenAI](https://developers.openai.com/api/docs/guides/moderation), [Comprehend DetectToxicContent](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html).

Paste a non-English message into the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
