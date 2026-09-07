---
title: "MEE6 pricing: what it costs and what is paywalled"
date: 2026-08-29
description: "MEE6 Premium is £11.99 a month, £49.99 a year, or £89.99 once for lifetime, and every plan covers one server. Here is what each tier includes, where the headline rates mislead, and how Supervisor prices moderation."
---

# MEE6 pricing: what it costs and what is paywalled

**Bottom line:** MEE6 Premium is £11.99 a month, £49.99 a year or £89.99 for lifetime, and every
one of those covers **a single server**. Its moderation is free, so you only pay for engagement
features and higher limits. At one server MEE6 is cheaper than Supervisor; at two or more,
Supervisor's £83.85 a year covering every server you run costs less than stacking subscriptions.

In MEE6's own words: "MEE6 Premium applies to a single server. To use Premium on multiple servers,
you'll need a separate subscription for each."

Those are the standard rates. When we checked, a "Limited Time Offer, 50% off all MEE6 Products"
banner was running with a countdown, which is where the lower promotional figures below come
from.

## What MEE6 costs

| Plan | Promotional rate | Standard rate |
| --- | --- | --- |
| Monthly | £5.99 first month | £11.99 a month |
| Yearly | £24.99 first year | £49.99 a year |
| Lifetime | £44.99 once | £89.99 once |

Prices checked on 29 August 2026 from MEE6's own premium page. Vendors change pricing, so check
before you buy.

**A currency note that matters.** Those figures are in pounds because that is what MEE6 showed
us. MEE6's FAQ says "The only currency available is the one displayed", so if you are outside
the UK you will see different numbers. It does mean the comparison later in this post is
unusually clean, since both products are quoted here in the same currency.

### Where the headline rates mislead

Three things on the pricing cards are worth reading carefully, because the number in large type
is not the number you will pay ongoing.

- The yearly card leads with **"£2.08 /mo"**. That is the £24.99 first-year promotional price
  divided by twelve. After the first year the rate is £49.99, which is £4.17 a month.
- That card's **"Save 83%"** compares £24.99 against £143.88. The £143.88 is twelve months at
  the full £11.99 monthly rate, not the standard yearly price of £49.99.
- The monthly card's **£5.99 is a first-month rate**. The ongoing rate is £11.99.

None of that is unusual for subscription pricing, and MEE6 does print the standard rate next to
the promotional one. It is just worth knowing which number renews.

## What you get for free

MEE6's moderation works without paying. The Moderator plugin's automod ruleset covers Bad Words,
Repeated Text, Server Invites, External Links, Excessive Caps (default 70%), a combined Excessive
Emojis, Spoilers and Mentions check, Zalgo, and a separate Anti-Spam feature watching message
frequency.

You also get the enforcement side: `/ban`, `/tempban`, `/kick`, `/clear`, an infractions system,
warning-based automated actions that escalate to temporary or permanent bans, immunity roles, and
an extensive audit log covering around two dozen event types.

The docs do carry the caveat that "certain parts or the entirety of the plugin/feature may
require a Premium Subscription", so individual settings within those features may sit behind the
paywall even where the feature itself does not.

## What sits behind the paywall

Premium is described by MEE6 as "enhanced versions of existing features with extended limits and
additional customization options", plus exclusive tools. The Lifetime and Yearly plans also
include the Bot Personalizer addon, which the Monthly plan does not.

Two terms in your favour worth knowing: every plan is **fully refundable for 7 days**, and a
subscription is **transferable to another server**. Given the per-server licensing, that
transferability is more useful than it first sounds.

One thing we did not read, so we are not going to describe it: **MEE6 AI is marketed as a
separate product**, and the discount banner refers to "all MEE6 Products" in the plural. We did
not read MEE6 AI's pricing, so do not assume Premium includes it.

## What per server billing means if you run several

This is the arithmetic that actually decides things for anyone running more than one community.
At the standard rates:

| Servers | Monthly | Yearly | Lifetime |
| --- | --- | --- | --- |
| 1 | £11.99 | £49.99 | £89.99 |
| 2 | £23.98 | £99.98 | £179.98 |
| 3 | £35.97 | £149.97 | £269.97 |
| 5 | £59.95 | £249.95 | £449.95 |

Per server pricing is a perfectly reasonable model and it keeps the entry price low for a single
community. It simply multiplies if you run a network.

## How Supervisor prices moderation

Supervisor is an AI moderation bot rather than an all-in-one, and it prices differently in two
ways: one plan containing every feature, and billing per account rather than per server.

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and **one subscription covers any number of
servers**, all drawing on that same monthly allowance.

There is a seven day free trial on the monthly and annual cycles, and every new account gets
£0.25 of moderation free on signup with no card. There is no lifetime option and no free tier
for new accounts.

Moderation is billed by the size of what it reads and the model you pick. Stating the assumption
out loud: at an average message of 100 bytes, £120 a month covers roughly 900,000 messages on
Observer, 450,000 on Sentinel, or 225,000 on Arbiter. Batched requests get 50% off, repeated
identical requests inside the cache window are free, and the link and word filters run before the
AI models, so anything they block costs nothing.

## Comparing the two honestly

Both are quoted in pounds here, so the comparison is unusually direct. It still needs two
caveats: MEE6's currency depends on where you are, and the two products are not buying you the
same thing.

On price alone, at standard rates:

- **One server: MEE6 is cheaper.** £49.99 a year against Supervisor's £83.85, or £89.99 once
  against a subscription that never ends. If you run one community and cost is the deciding
  factor, MEE6 wins and you should not pay us.
- **Two servers or more: Supervisor is cheaper.** Two MEE6 subscriptions are £99.98 a year
  against £83.85 for a Supervisor account covering all of them, and the gap widens with every
  server you add.
- **Lifetime has no equivalent.** If you want to pay once and never think about it again for one
  server, MEE6 offers that and Supervisor does not.

On what you are buying:

- **MEE6 gives you far more surface.** Levels, economy, giveaways, social alerts, bot
  personalisation, an audit log suite, and bans and kicks. Supervisor has three slash commands
  and no utility features at all.
- **Supervisor gives you a different detection mechanism.** MEE6's eight automod checks are
  string matches and counters. Supervisor's models read what a message means, classify across 16
  labels including harassment, threats, scams and self-harm, weigh conversation context, and
  moderate images and video in over 100 languages.

Which is why the honest answer for most servers is both, with MEE6 doing the breadth and the
enforcement, and an AI layer reading the messages a counter cannot see. The
[full comparison of the two approaches](/blog/supervisor-vs-mee6-moderation) covers the
mechanism, and our [MEE6 review](/blog/mee6-review) covers what it is like to use.

## For developers and platforms

MEE6 is a Discord bot, so its pricing has no bearing on moderating your own product. Supervisor
bills the same way outside Discord as inside it, per byte at the model rate, through a REST API
with SDKs for Python, JavaScript, Go, Rust and Java. The
[API reference](https://supervisor.gg/docs/integrations/api) has the current rates and the
[pricing page](https://supervisor.gg/pricing) has the plan.

Before paying anyone, see what each approach catches on your own content. Paste a message that
gets past a keyword filter into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
