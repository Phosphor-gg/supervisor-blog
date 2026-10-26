---
title: "Azure AI Content Safety review: strengths, limits and who it suits"
date: 2026-10-26
description: "An honest review of Azure AI Content Safety from a company that sells a competing product: severity levels, blocklists, Prompt Shields, language coverage, limits, and where its four categories run out."
---

# Azure AI Content Safety review: strengths, limits and who it suits

**Bottom line:** Azure AI Content Safety is a well documented, enterprise-shaped service with four harm categories, graded severity, blocklists and a free tier. It runs out if you need categories beyond hate, sexual, violence and self-harm, or if you are not already working inside Azure. We make Supervisor, a paid competitor, so weigh this as an interested party's view. We did not test Azure's accuracy or speed and make no claim about either.

Everything about Azure below comes from Microsoft's own pages, linked at the end.

## What it is

Microsoft describes it as "an AI service that detects harmful user-generated and AI-generated content in applications and services." It includes text and image APIs, plus Prompt Shields (which scan text for the risk of a user input attack on a large language model), groundedness detection (preview), protected material text detection and a task adherence API.

## What it does well

**Graded severity, not just a flag.** The text model "supports the full 0-7 severity scale", and you can ask for four or eight levels via `outputType`. If you want to set different thresholds for different surfaces (strict in a children's product, looser in a mature forum), a number per category is genuinely useful. Image results come back trimmed to 0, 2, 4 and 6.

**Four clear categories.** Microsoft classifies harmful content "into four categories, hate, sexual, violence, and self-harm, for both text and image content". They are well defined and documented in detail.

**Blocklists.** Microsoft says Content Safety Studio includes built-in terms blocklists to flag profanities, and that you can upload your own. In the text API you pass `blocklistNames` and can set `haltOnBlocklistHit`. This is a practical feature for brand-specific terms.

**More than moderation.** Prompt Shields, protected material detection and groundedness detection matter if you are shipping an LLM application.

**A free tier and commitment tiers.** 5,000 text records and 5,000 images a month free, then pay as you go or a monthly commitment. See [our pricing breakdown](/blog/azure-content-safety-pricing).

**Enterprise plumbing.** Key authentication, Microsoft Entra ID support and managed identity, SDKs for Python, .NET, Java and JavaScript, a documented rate-limit table, and regional availability. Microsoft also documents a 90 day deprecation period for old API versions.

**Custom categories (rapid).** An LLM-based option where you create an incident from a text description and upload text or image samples, with no training step.

## Where it runs out

**Four categories.** There is no built-in spam, scam, promotional, insult or profanity category among the four. Blocklists and custom categories can fill some of that gap, but you build and maintain them.

**Languages.** Microsoft says the text classifiers are "trained and tested on Chinese, English, French, German, Italian, Japanese, Portuguese, and Spanish", and that the features "can work in many other languages, but the quality might vary." Some features (protected material, groundedness, task adherence, custom categories standard) were trained and evaluated on English.

**Input types.** Text, images and a multimodal API in preview (text limit 1,000 characters). We did not find video on the overview, harm categories, region availability or quickstart pages. Check Microsoft's API reference if video matters.

**Size limits.** Text up to 10,000 characters per call by default, images up to 4 MB.

**Setup.** You create a Content Safety resource in a supported region and pick a pricing tier. That is normal for Azure and a step up in effort from a bare API key.

**Pricing page.** When we read it, Microsoft's public pricing page showed placeholders instead of amounts. We used the Retail Prices API instead.

**A moving custom categories story.** Microsoft's custom categories page says "Custom categories (standard) is retiring on September 1, 2026" and points to Custom text classification in Foundry. We could not confirm whether the API is still live today, so check before depending on it. Separately, Azure Content Moderator, the older service, is retiring on 15 March 2027. See our [migration guide](/blog/azure-content-moderator-migration-guide).

## Who it suits

- Teams already on Azure that want a managed, documented service with severity levels.
- LLM applications that benefit from Prompt Shields or groundedness checks.
- Projects whose harm model matches the four categories.

## Where Supervisor differs

Supervisor is paid, and its per-message cost can be higher than Azure's, especially for longer text and for images. In return it has 16 labels including spam, promotional, scam and illegal, a `flagged` decision with `labels`, `include_context` (`needs_context` and `context_labels`), `implicit_labels`, video, translation of non-English messages before classification, three model tiers, a username endpoint, five SDKs and a Discord bot. It does not return a severity number per category in its documented response, so if graded severity is your requirement, Azure has the advantage. Full comparison: [Supervisor vs Azure AI Content Safety](/blog/supervisor-vs-azure-content-safety). Also see [alternatives](/blog/azure-content-safety-alternatives).

Test messages from your own community in the [live demo](https://supervisor.gg/demo), read the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg).

## Sources

- Microsoft, [Content Safety overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview)
- Microsoft, [Harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories)
- Microsoft, [Region availability and limits](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability)
- Microsoft, [Text quickstart](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/quickstart-text)
- Microsoft, [Custom categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/custom-categories)
- Microsoft, [Content Moderator overview](https://learn.microsoft.com/en-us/azure/ai-services/content-moderator/overview)
- Supervisor, [API reference](/docs/integrations/api)
