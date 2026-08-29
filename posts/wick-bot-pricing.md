---
title: "Wick bot pricing: what it costs and what is paywalled"
date: 2026-08-29
description: "Wick Premium is $5 a month and VIP is $20 a month for 12 servers. The security features themselves are free in their base form, and the paid tiers buy the advanced versions. Here is the breakdown."
---

# Wick bot pricing: what it costs and what is paywalled

Wick has two paid plans: **Premium at $5 a month** and **VIP at $20 a month**. There is no free
tier section on the pricing page, because the bot itself is free to use. What the paid plans buy
is the advanced version of protections that already exist in a base form.

If you are weighing Wick specifically, that distinction is the whole story, so it is worth being
precise about it.

## What Wick costs

| Plan | Price | What it adds |
| --- | --- | --- |
| Premium | $5 per month | Advanced Anti Raid, Advanced Anti Nuke, Advanced Automod, Advanced Quarantine, Smart Backups, Advanced Lockdown System, Customizable Verification, Increased Ratelimits |
| VIP | $20 per month | Everything from Premium, plus Dedicated Resources, Custom Branding, Super Low Latency, and 12 Premium Servers |

Prices checked on 29 August 2026 from Wick's own premium page, displayed in dollars. Two things we
could not read and are not going to guess at: whether an annual billing option exists, and how
many servers the Premium plan covers. VIP names 12 premium servers explicitly, which implies
Premium covers fewer, but the page does not say how many.

Vendors change pricing, so check before you buy.

## What the paid tier actually buys

Look at the naming and the model becomes obvious. Every Premium line is an **Advanced**,
**Customizable** or **Increased** version of something: Advanced Anti Raid, Advanced Anti Nuke,
Advanced Automod, Advanced Quarantine, Advanced Lockdown System, Customizable Verification,
Increased Ratelimits.

That naming strongly implies base versions of anti raid, anti nuke, automod, quarantine, lockdown,
verification and ratelimits exist without paying, and Wick's documentation supports that reading:
it describes the Anti-Nuke system, Panic Mode, the Restore System, the Heat system and Auto
Timeouts in full detail without marking any of them as premium-only.

So the honest summary is that **Wick's protection is free and its depth is paid**. You are not
buying anti-nuke. You are buying a more capable anti-nuke. We could not read a feature-by-feature
free versus premium table, so we are not going to tell you exactly where each line is drawn.

Smart Backups is the one Premium item that does not follow the pattern, and backups matter more
than most of the list. Wick's own docs are blunt about the alternative: with Imaging disabled,
restoring a nuked server "is a finicky process and lacks a lot of information and the server may
not be restored properly". If restore is why you are running Wick, that line is the argument for
paying.

## What VIP adds, and when it makes sense

VIP at $20 a month adds Dedicated Resources, Custom Branding, Super Low Latency and **12 Premium
Servers**.

That last item is the one worth arithmetic. If you actually use all twelve slots, VIP works out at
about **$1.67 per server per month**, against $5 a month for Premium on a smaller number of
servers. For anyone running a network of communities, VIP is the cheaper shape by a wide margin.
For a single server it is four times the price for infrastructure benefits you may not need.

The rest of VIP is quality of service rather than capability: dedicated resources and lower
latency matter if you are large enough for either to be a real constraint.

## What you get without paying

The bot, and the architecture behind it. Wick's documentation describes the following without
gating any of it behind a plan:

- **Anti-Nuke**, monitoring channel and role creation and deletion, bans and kicks, and webhook
  creation and deletion, with bypass attempts, dangerous permission grants and vanity URL changes
  all triggering quarantine.
- **Panic Mode**, locking the server down on a detected nuke and deploying an isolated "miniWick"
  to gather pre-attack state.
- **The Heat system**, Wick's automod, where actions accumulate heat that decays over time rather
  than tripping fixed thresholds, drawing on message repetition, emojis, characters, new lines,
  mentions, attachments, blacklisted words and links, advertisement, and NSFW and malicious
  websites.
- **Auto Timeouts** with an escalating Multiplier so raiders cannot wait out a fixed cap.
- **Moderation commands**: Ban, Kick, Lockdown, Notes, Purge, Quarantine, Sanitize, Slowmode,
  Timeout, Verify and Warn, plus case tracking.

For a server that wants protection against raids and rogue admins and has not yet been attacked,
that free baseline is a lot.

## How Supervisor prices moderation

Supervisor solves a different problem, so this is a comparison of pricing models rather than of
products. It is an AI moderation layer that reads what messages mean, and it has none of Wick's
security features.

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and one subscription covers any number of
servers drawing on that allowance. There is a seven day free trial on monthly and annual, and
every new account gets £0.25 of moderation free on signup with no card. There is no free tier for
new accounts.

Moderation is billed by the size of what it reads and the model you pick. Stating the assumption
out loud: at an average message of 100 bytes, £120 a month covers roughly 900,000 messages on
Observer, 450,000 on Sentinel, or 225,000 on Arbiter. Batched requests get 50% off, repeated
identical requests inside the cache window are free, and the link and word filters run before the
AI models so anything they block costs nothing.

## Comparing the two honestly

The currencies differ, Wick in dollars and Supervisor in pounds, and we are not going to convert
them, because a comparison that quietly converts is one you cannot check.

More importantly, **these two are not substitutes and the pricing comparison is close to
meaningless on its own**. Wick protects the structure of your server: anti-nuke, raid defence,
verification, quarantine, backups and restore. Supervisor reads what legitimate members are
saying. Neither does the other's job at any price, and a server with both problems needs both
tools.

What is comparable is the shape:

- **Wick's core protection is free**, and paying buys depth plus, at VIP, server count. Supervisor
  has no free tier for new accounts.
- **Wick's server model is slot-based** at the VIP tier, twelve of them for $20. Supervisor is one
  account subscription covering any number of servers.
- **Both get cheaper per server as you add servers**, which is unusual in this category. Most
  Discord bots multiply.

If you are choosing between them because budget only allows one, the question is not which is
better value. It is which risk is real in your server: being attacked, or being harmed by what
members post. Answer that first.

There is a [full comparison of the two approaches](/blog/supervisor-vs-wick-moderation) and a
[Wick review](/blog/wick-bot-review) covering what it is like to run.

## For developers and platforms

Wick is a Discord security bot, so its pricing has no bearing on moderating your own product, and
server structure is a Discord concept that does not transfer. Supervisor bills the same way outside
Discord as inside it, per byte at the model rate, through a REST API with SDKs for Python,
JavaScript, Go, Rust and Java. The [API reference](https://supervisor.gg/docs/integrations/api) has
the current rates and the [pricing page](https://supervisor.gg/pricing) has the plan.

Before paying anyone, work out which layer you are missing. Paste a message that gets past your
current filters into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
