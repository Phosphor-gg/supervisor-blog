---
title: "Build vs buy: content moderation for your product"
date: 2026-10-26
description: "Should you build your own moderation system or use an API? A decision framework covering what building involves, when it makes sense, and what Supervisor costs, without invented numbers."
---

# Build vs buy: content moderation for your product

**Bottom line:** most teams should start with an API, because moderation is a distinct product with its own data, models and upkeep. Building makes sense in a few specific situations. This post gives you the questions that decide it, and the one set of costs we can state precisely: Supervisor's.

We make Supervisor, so weigh this accordingly. We have tried to keep the framework fair, and we do not give figures for building because we do not have verified ones.

## What "build" actually includes

"We'll just train a classifier" hides several jobs:

- **Data.** You need labelled examples of the content you want to catch, in the languages and formats your users produce. Labelling needs policy decisions, and often a human team.
- **Models.** Text, then images, then video if users upload them. Each is a separate problem.
- **Evaluation.** You need a test set that reflects reality, and a way to measure false positives and misses per category before and after every change.
- **Serving.** Running the models reliably, including capacity, failures and the case where they are unreachable.
- **Evasion.** Users adapt, so the system needs retraining as they find gaps. See [why word lists fail](/blog/stop-word-filter-bypasses).
- **Everything around it.** Review tools, appeals, logging, abuse of the moderation system itself.

None of that is impossible. All of it is ongoing, and the cost of it depends on your team, your volume and your tolerance for mistakes, so we will not put a number on it.

## What "buy" gets you, and what it does not

With an API you get a classifier that already exists, behind a function call, with the upkeep done by someone else. You do not get your rules, your enforcement or your review process; those remain yours either way.

Limits to know before you commit, for Supervisor specifically:

- It is a hosted API. You send content to it.
- The 16 labels are fixed. You scope them with `enabled_labels` but cannot add your own.
- It classifies. It does not ban, delete or warn for you in your product (the Discord bot does act on Discord, but that is a different surface).
- It is paid. There is no ongoing free tier for new accounts.

## When building makes sense

- **Your policy is unusual.** If what you need to catch is specific to your domain and not covered by general categories, general labels will not fit.
- **Content cannot leave your infrastructure.** Legal or contractual limits on sending data to a third party may rule out any hosted API.
- **You already have the pieces.** A trust and safety team, labelled data and ML infrastructure change the maths.
- **Moderation is your product.** Then it is your core, not a dependency.

## When buying makes sense

- **You need coverage across text, images and video** without three separate projects.
- **You have no labelled data yet.**
- **You want to ship moderation this month.**
- **Your team is better spent on your product.**

## A middle path

Many teams combine both: an API for general categories, plus a small rule layer of their own for the specifics, such as your brand names, a handful of terms, or account-age rules. The API handles meaning; your code handles policy.

## What Supervisor costs

These figures come from the API reference and the pricing page:

| | |
| --- | --- |
| Premium | £13.99 a month |
| Included credits | 90,000,000 a month |
| Text, per KB | roughly £0.0014 (Observer), £0.0027 (Sentinel), £0.0055 (Arbiter) |
| Images | roughly £0.0014 per KB of image data, plus OCR text at the model rate |
| Video frames | a quarter of the image rate |
| Batches of two or more | 50% off |
| Repeated identical requests | free within the cache window |

Premium includes all three models, context-aware moderation, image and video moderation and implicit moderation. As an example worked from those rates: text is billed at 1, 2 or 4 credits per byte on Observer, Sentinel and Arbiter, so a 100 byte message on Sentinel is 200 credits, and the monthly allowance covers about 450,000 messages of that size (about 900,000 on Observer). Batching halves the cost again.

New accounts get free credits to test with (Observer model, text only), and there is a 7 day Premium trial.

## How to decide

Answer these honestly:

1. Do general categories (toxicity, harassment, scam, spam and so on) cover most of what you need to catch?
2. Can content be sent to a hosted service?
3. Do you have, or want to have, a team to own a moderation system long term?
4. How soon do you need it?

If the first two are yes, and the third is no, buy. If the first is no, or the second is no, you are in build territory, or at least a hybrid. For comparisons with other tools, see the comparison posts on [the blog](/blog/).

The cheapest way to test the "buy" side of the question is to run a few hundred of your own messages through it. The [what is a content moderation API](/blog/what-is-a-content-moderation-api) post covers the mechanics.

## Summary

- Building means data, models, evaluation, serving and ongoing retraining, not one project.
- Build when your policy is unusual, data cannot leave, or moderation is your product.
- Otherwise, start with an API and keep a small rule layer of your own.
- Supervisor's costs are the ones above; we have not invented any for building.

Read the [API reference](/docs/integrations/api), test your own content in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
