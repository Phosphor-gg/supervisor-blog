---
title: "collony.ai pricing: what $29 and $99 a month actually buy"
date: 2026-11-16
description: "collony.ai has a free plan, Protect at $29 a month and Grow at $99 a month, billed in daily message credits. Here is what each plan includes, how far the credits go, and how that compares with Supervisor."
---

# collony.ai pricing: what $29 and $99 a month actually buy

**Bottom line:** collony.ai's free plan has no AI. AI moderation starts at **$29 a month** on
Protect, which checks **500 messages a day** on one platform, about 15,000 a month. Grow at **$99
a month** adds Telegram and Discord together, AI answers and insights, with 2,000 messages a day
checked. If you need moderation on a busy Discord server, Supervisor Premium is £13.99 a month and
covers roughly 900,000 messages a month across all your servers.

All collony.ai figures below come from its pricing page and billing documentation, read on 16
November 2026.

## The plans

| Plan | Monthly | Billed yearly | Platforms | Daily usage |
| --- | --- | --- | --- | --- |
| Free | $0 | $0 | Telegram or Discord | Up to 1,000 messages, no AI |
| Protect | $29 a month | $24.17 a month | Telegram or Discord | 500 security credits |
| Grow | $99 a month | $82.50 a month | Telegram and Discord | 2,000 security and 2,000 chat credits |
| Scale | Custom | Custom | Telegram and Discord | Sized to your community |

Yearly billing gives two months free. Protect and Grow come with a seven day free trial with no
card, and if you do not subscribe the project drops back to Free with your settings kept.

**Free** gives you blocklists, link and scam source checks, Surge Guard and flood limits, a review
queue and an audit log. It is useful, but it is a rules bot: the AI is not included.

**Protect** adds AI moderation with your own plain-language rules, and image, GIF and sticker
checks.

**Grow** adds AI answers and chat replies from your knowledge base, insights, scheduled posts and
the MCP server, and is the first plan that runs Telegram and Discord together.

**Scale** is priced around your volume, with several projects on one bill and setup and tuning
from the collony.ai team, arranged on a call.

## How the credits work

collony.ai's billing docs define a security credit as **one message checked**, and a chat credit
as one AI reply the bot sends. Credits reset daily at 00:00 UTC, and each project has its own
subscription.

So the real numbers are:

| Plan | Messages checked a day | Roughly a month |
| --- | --- | --- |
| Protect | 500 | 15,000 |
| Grow | 2,000 | 60,000 |

Those are generous for a quiet Telegram group and tight for an active Discord server, where 500
messages can go by in an hour on a busy evening. The docs say that when credits run out
"protection never stops" and AI chat replies pause first. They do not say how messages past the
daily allowance are checked, so if your server is busy, ask before you buy.

## What you are paying for

Part of what you pay for is AI you do not run. collony.ai's privacy policy names "AI service
providers (e.g. OpenAI)" as sub-processors for moderation and replies. Per-message credits are a
sensible way to price a product built on someone else's per-request API, and it explains why the
allowances are counted in hundreds rather than hundreds of thousands.

## How Supervisor prices the same job

Supervisor runs its own models on its own hardware, so it can price differently.

**The security suite is free** for every server and uses no credits: anti-nuke, a join gate,
Heat spam filtering, auto lockdown, quarantine, verification and numbered moderation cases.

**AI moderation is in Premium:**

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and one subscription covers any number of
servers. Moderation is billed by the size of what it reads and the model you pick. At an average
message of 100 bytes, £120 covers roughly 900,000 messages a month on Observer, 450,000 on
Sentinel or 225,000 on Arbiter. Batched requests are 50% off, repeats inside the cache window are
free, and the link and word filters run first so anything they block costs nothing.

There is a seven day free trial on monthly and annual, and every new account gets £0.10 of
moderation free with no card.

## Side by side

We are not going to convert currencies for you, because exchange rates move. Taking each product's
own entry plan for AI moderation:

| | collony.ai Protect | Supervisor Premium |
| --- | --- | --- |
| Price | $29 a month | £13.99 a month |
| Messages moderated | 500 a day, about 15,000 a month | About 900,000 a month at 100 bytes on Observer |
| Platforms or servers | One platform | Any number of Discord servers |
| Languages moderated | Not stated | Over 100 |
| Images and video | Images, GIFs, stickers | Images and video |
| Security suite | Surge Guard, flood limits, impersonation | Anti-nuke, join gate, Heat, lockdown, verification, free |
| Answers member questions | Grow only | No |

## Which is better value?

For Discord moderation, Supervisor gives you far more messages for less money, plus server
security that collony.ai does not offer.

collony.ai is better value if you are paying for the things Supervisor does not do: Telegram,
answering member questions, and sentiment insights. If that is what you need, Grow is the plan
that includes it.

See what Supervisor catches on your own content in the [live demo](https://supervisor.gg/demo),
or [add it to your server](https://invite.supervisor.gg).

## Frequently asked questions

### How much does collony.ai cost?

collony.ai has a free plan without AI, Protect at $29 a month ($24.17 a month billed yearly), Grow at $99 a month ($82.50 billed yearly), and custom Scale pricing.

### What is a collony.ai credit?

Its billing documentation says one security credit is one message checked, and one chat credit is one AI reply the bot sends. Credits reset daily at 00:00 UTC.

### Does collony.ai have a free trial?

Yes. Protect and Grow come with a seven day free trial with no card required.

### Is Supervisor cheaper than collony.ai?

For Discord moderation volume, yes. Supervisor Premium is £13.99 a month and includes £120 of moderation, about 900,000 messages at 100 bytes on the Observer model, compared with 500 messages a day on collony.ai Protect at $29.
