---
title: "Carl-bot pricing: what it costs and what is paywalled"
date: 2026-08-29
description: "Carl-bot premium is sold through Patreon from £6.50 a month and works on a server slot system. Automod itself is free. Here is what premium changes, and how Supervisor prices moderation."
---

# Carl-bot pricing: what it costs and what is paywalled

Carl-bot premium is sold through **Patreon**, starting at **£6.50 a month**, and it works on a
**server slot** system rather than a flat account upgrade. Automod itself is free, so if
moderation is what you are here for, you may not need to pay at all.

## What Carl-bot costs

Carl-bot's premium page offers two routes, "Buy on Patreon" and "Buy on Discord". The Patreon page
says premium gives "access to exclusive benefits starting at £6.50/month".

Prices checked on 29 August 2026. Two honest caveats:

- **That £6.50 was displayed to us in pounds**, and Patreon localises currency, so you may see a
  different figure and a different currency.
- **We only read the entry price.** The full tier list sits behind Patreon's "Membership options"
  button, which we could not read, so we are not going to describe the higher tiers or what they
  cost. The docs do confirm tiers exist and that they differ in how many premium slots you get,
  since the FAQ has an entry for "I am missing premium slots. A different tier is shown than the
  one I subscribed to on Patreon."

Vendors change pricing, so check before you buy.

## How the server slot system works

This is the part that makes Carl-bot's pricing different from most bots, and it is worth
understanding before you subscribe.

You do not upgrade an account or a server directly. You subscribe on Patreon, link Patreon to
Discord, and then **mark servers as premium yourself** using `/premium addpremium`. The related
commands make the model obvious: `/premium removepremium` frees a slot, and `/premium listpremium`
"shows a list of all premium activated servers by you", plural.

That means premium is **transferable**. Carl-bot's FAQ spells out the process: remove premium from
the current server, then add it to the new one, and if you have lost access to the old server you
can list your server IDs and remove it remotely. For anyone running or helping run several
communities, being able to move a slot without contacting support is genuinely useful.

What we cannot tell you is how many slots each tier includes, because we could not read the tier
list.

## What you get for free

Carl-bot's automod is free, and it is substantial. The modules cover message spam, attachment
spam, bad words, caps limit, invites, links, mentions and a honeypot, each with its own rate
limits and its own punishments.

The punishment set is free too, and it is the richest in this category: delete, warn, tempmute,
mute, timeout, kick, tempban, ban, message and DM, with durations written as `3h42m` and multiple
punishments combinable with commas, so `delete, tempmute 20m` is one valid response. Warn
thresholds, role and channel whitelisting, media-only channels and the `deletefiles` toggle for
unsafe file types are all included.

The free tier also gives you 250 reaction roles per server, 5 YouTube channel alerts, 2 Twitch
stream alerts and 100 weblog entries.

## What sits behind the paywall

From Carl-bot's own free versus premium table:

| Feature | Free | Premium |
| --- | --- | --- |
| Reaction roles per server | 250 | 1,000 |
| YouTube channel alerts | 5 | 20 |
| Twitch stream alerts | 2 | 5 |
| Weblog entries | 100 | 500 |
| Levels and XP system | No | Yes |
| Sticky messages | No | Yes |
| Auto Purge | No | Yes |
| Voice-role links | No | Yes |
| Timed reaction roles | No | Yes |
| Separate farewell channel | No | Yes |
| Drama Watcher | No | Yes |
| Custom bot avatar and banner | No | Yes |

Note what is **not** on that list: the automod modules themselves. Premium raises limits and adds
features around the edges rather than unlocking detection.

The one moderation feature that is premium is **Drama Watcher**, and it is the most interesting
thing Carl-bot sells. The `defer` punishment sends an offending message to a drama channel where
moderators decide with reactions instead of digging through logs. If you want humans in the loop
on ambiguous cases rather than fully automatic enforcement, that is the feature you are paying
for.

## How Supervisor prices moderation

Supervisor is an AI moderation bot rather than a general purpose one, and it prices differently:
one plan with everything in it, billed per account rather than per server slot.

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and one subscription covers any number of
servers, all drawing on that same allowance. There is no slot to move around, and no per-server
multiplication.

There is a seven day free trial on the monthly and annual cycles, and every new account gets £0.25
of moderation free on signup with no card. There is no free tier for new accounts.

Moderation is billed by the size of what it reads and the model you pick. Stating the assumption
out loud: at an average message of 100 bytes, £120 a month covers roughly 900,000 messages on
Observer, 450,000 on Sentinel, or 225,000 on Arbiter. Batched requests get 50% off, repeated
identical requests inside the cache window are free, and the link and word filters run before the
AI models so anything they block costs nothing.

## Comparing the two honestly

Both figures above happened to display in pounds for us, but Patreon localises and we only read
Carl-bot's entry tier, so treat any direct comparison carefully and check your own currency.

What is comparable is the shape:

- **Carl-bot's moderation is free.** If its modules catch what your server struggles with, you
  should not pay anyone, including us. That is the honest answer for a lot of servers.
- **Carl-bot's premium is mostly not about moderation.** Levels, sticky messages, higher reaction
  role limits and social alert slots. The exception is Drama Watcher, which is a real moderation
  feature and has no Supervisor equivalent.
- **Slots versus account.** Carl-bot premium attaches to a number of servers you choose and can
  move. Supervisor covers all your servers at once from one subscription, sharing one allowance.
- **They are not buying the same thing.** Carl-bot's premium refines a rule engine you already
  have for free. Supervisor's plan buys a different detection mechanism: models that read what a
  message means rather than matching strings and counting events.

Which is why the honest answer for many servers is both. There is a
[full comparison of the two approaches](/blog/supervisor-vs-carl-bot-moderation) covering the
mechanism, and our [Carl-bot review](/blog/carl-bot-review) covers what it is like to use.

## For developers and platforms

Carl-bot is a Discord bot, so its pricing has no bearing on moderating your own product.
Supervisor bills the same way outside Discord as inside it, per byte at the model rate, through a
REST API with SDKs for Python, JavaScript, Go, Rust and Java. The
[API reference](https://supervisor.gg/docs/integrations/api) has the current rates and the
[pricing page](https://supervisor.gg/pricing) has the plan.

Before paying anyone, see what each approach catches on your own content. Paste a message that
gets past a keyword filter into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
