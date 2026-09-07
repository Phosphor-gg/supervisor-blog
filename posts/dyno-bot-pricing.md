---
title: "Dyno bot pricing: what it costs and what is paywalled"
date: 2026-08-29
description: "Dyno Premium runs from $5.99 a month or $49.99 a year for one server, with automod itself on the free tier. What each plan covers, what per server billing costs if you run several, and how Supervisor prices moderation."
---

# Dyno bot pricing: what it costs and what is paywalled

**Bottom line:** Dyno Premium is $5.99 a month or $49.99 a year **per server**, and all nineteen
automod filters plus the full ban ladder are free, so you rarely need to pay Dyno for moderation
at all. Pay Supervisor instead when the messages hurting your server trip none of those filters,
which is what happens when harm is contextual rather than countable.

Dyno Premium starts at **$5.99 a month, or $49.99 a year, for one server**, rising to $7.99 and
$12.99 a month on the higher plans. The automod engine itself is free. The detail that matters
most if you run more than one community is that every plan is priced **per server**, in Dyno's
own words "for one server of your choice".

## What Dyno costs

| Plan | Monthly | Annual | Annual works out at | What Dyno calls it |
| --- | --- | --- | --- | --- |
| Standard | $5.99 | $49.99 | $4.17 / month | "Standard Premium for one server of your choice" |
| Premium | $7.99 | $59.99 | $5.00 / month | "Dyno Premium for one server of your choice" |
| Custom | $12.99 | $99.99 | $8.33 / month | "A fully hosted custom Dyno Premium" |

Prices checked on 29 August 2026 from Dyno's own pricing page, in US dollars. Vendors change
pricing, so check before you buy.

Paying annually is a real discount rather than a rounding difference. Twelve months of Standard
at the monthly rate is $71.88 against $49.99 for the year, a saving of $21.89. On Premium it is
$95.88 against $59.99, and on Custom $155.88 against $99.99, saving $35.89 and $55.89.

What each plan adds:

- **Standard** brings Levels, Advanced Automod, Advanced Starboard, Autopurge, Slowmode,
  Voice-Text Linking, and unlimited commands and modules.
- **Premium** adds the social integrations: Twitch, YouTube, TikTok, Reddit and Kick.
- **Custom** adds a fully hosted custom bot with an uploadable avatar, custom username, custom
  status, and what Dyno describes as "Increased Performance and Uptime".

## What you get for free

Dyno's free tier is genuinely substantial, and the pricing page lists it plainly: Starboard,
Tickets, Automod, 3 customisable embeds, 25 custom commands, 10 autoresponders, 3 active
giveaways, 3 forms, 3 reaction role menus, 3 autoroles, 1 autodelete, 1 automessage, and 1
autoban per rule.

**Automod is on that list.** All nineteen filters, from Bad Words and Fast Message Spam through
to Known Phishing Links and Zalgo Text, work without paying anything. So does the full action
ladder: Warn, Delete, Auto Mute, Auto Ban, Instant Mute and Instant Ban.

If your question was "do I have to pay Dyno to moderate my server", the answer is no.

## What sits behind the paywall

The paid tier is called **Advanced Automod**, and per Dyno's documentation the moderation
pieces it unlocks are per-rule refinements rather than detection itself:

- A per-rule automod log channel, rather than only the default one.
- A per-rule custom response, so Dyno can reply differently to different rules.
- Custom moderation responses on moderator commands.

The documented free-tier limits are worth knowing before you build a policy around them: a
non-Premium server can have a maximum of **3 autopunishments**, mutes cap at **14 days**, bans
at **3 months**, and role additions at **30 days**.

One naming point, because it is easy to get wrong: Dyno documents a **Dyno Premium**
subscription, whose plans are the three above, and separately a **Dyno Membership**
subscription. They are different products, so a feature marked as needing one is not unlocked
by the other.

## What per server billing means if you run several

This is the part worth doing the arithmetic on, because the headline rate is per server and
most people comparing bots are thinking about one.

At the Standard plan's rates:

| Servers | Monthly | Annual |
| --- | --- | --- |
| 1 | $5.99 | $49.99 |
| 3 | $17.97 | $149.97 |
| 5 | $29.95 | $249.95 |

That is not a criticism. Per server pricing is a completely reasonable model, and it means a
single small community pays a small amount. It just scales linearly with the number of
communities you run, which matters if you run a network rather than a server.

## How Supervisor prices moderation

Supervisor is an AI moderation bot rather than a general purpose one, and it prices differently
in two ways: one plan with everything in it, and billing per account rather than per server.

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and **one subscription covers any number
of servers**, which all draw on that same monthly allowance. So five communities is one
subscription shared between them rather than five subscriptions multiplied.

There is a seven day free trial on the monthly and annual cycles, and every new account gets
£0.25 of moderation free on signup with no card.

Moderation is billed by the size of what it reads and the model you choose. Stating the
assumption out loud: at an average message of 100 bytes, the included £120 a month covers about
900,000 messages on the Observer model, 450,000 on Sentinel, or 225,000 on Arbiter. Batched
requests get 50% off, repeated identical requests inside the cache window are free, and the
link and word filters run before the AI models so anything they block costs nothing.

## Comparing the two honestly

**The currencies are different and we are not going to convert them for you.** Dyno prices in US
dollars, Supervisor in pounds. Exchange rates move, and a comparison that quietly converts one
into the other is a comparison you cannot check. Compare them in whatever currency you actually
pay in.

What is comparable is the shape:

- **Dyno's free tier covers moderation.** Supervisor has no free tier for new accounts, just a
  seven day trial and £0.25 of moderation to try it. If cost is the deciding factor and Dyno's
  filters catch what your server struggles with, Dyno wins outright and you should not pay us.
- **Dyno charges per server, Supervisor per account.** One community favours Dyno's model, a
  network of communities favours Supervisor's.
- **They are not buying you the same thing.** Dyno's paid tier refines a rule engine you already
  have for free. Supervisor's plan buys a different detection mechanism: models that read what a
  message means rather than matching strings and counting events.

That last point is why the honest answer for many servers is both, with Dyno doing the countable
work and the banning, and an AI layer reading the messages no counter can see. The
[full comparison of the two approaches](/blog/supervisor-vs-dyno-moderation) covers the
mechanism, and our [Dyno review](/blog/dyno-bot-review) covers what it is like to use.

## For developers and platforms

Dyno is a Discord bot, so its pricing has no bearing on moderating your own product. Supervisor
bills the same way outside Discord as inside it, per byte at the model rate, through a REST API
with SDKs for Python, JavaScript, Go, Rust and Java. The
[API reference](https://supervisor.gg/docs/integrations/api) has the current rates and the
[pricing page](https://supervisor.gg/pricing) has the plan.

Before paying anyone, see what each approach actually catches on your own content. Paste a
message that gets past a keyword filter into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
