---
title: "Discord bot pricing compared in 2026"
date: 2026-09-06
description: "What Wick, Dyno, Carl-bot, MEE6, Sapphire, Discord AutoMod and Supervisor actually cost, read from each vendor's own pricing page, with the billing unit that decides your real bill."
---

# Discord bot pricing compared in 2026

**Bottom line:** moderation is free on almost all of them, so if cost is your deciding factor you
probably do not need to spend anything. The number that actually decides your bill is not the
headline rate, it is the billing unit: MEE6, Dyno, Carl-bot and Wick all charge **per server**, so
three communities means three subscriptions. **Supervisor** is the only one billed **per account**,
at £13.99 a month covering every server you run, so its price is the only one here that does not
multiply. Against MEE6, both quoted in pounds, that crossover lands at two servers.

Every figure below was read from the vendor's own pricing page on the date given. Currencies are
mixed and we do not convert them, because a comparison that quietly converts is one you cannot
check.

## The table

| Bot | Free tier | Entry paid price | Billing unit | Currency shown |
| --- | --- | --- | --- | --- |
| Discord AutoMod | **Everything, it is free** | No paid tier | Not applicable | Free |
| Sapphire | **Everything, including AI moderation** | Custom Branding from €5 / month | Per server | EUR |
| Carl-bot | Automod and 250 reaction roles | From £6.50 / month via Patreon | Per server slot, transferable | GBP |
| Dyno | Automod and full ban ladder | $5.99 / month, or $49.99 / year | Per server | USD |
| MEE6 | Automod and moderator commands | £11.99 / month, £49.99 / year, £89.99 lifetime | Per server | GBP |
| Wick | Base protection | $5 / month, VIP $20 / month | Per server | USD |
| Supervisor | None, 7 day trial | £13.99 / month, £83.85 / year | **Per account** | GBP |

Prices checked on 29 August 2026, except Supervisor's, which come from our own billing system.
Vendors change pricing, so check before you buy. MEE6, Carl-bot and Sapphire localise their
currency, so you may see different figures and a different symbol.

## The billing unit is the real number

Headline rates make products look closer than they are. The multiplier is what separates them.

At standard rates, running the same setup across several communities:

| Servers | MEE6 yearly | Dyno yearly | Supervisor yearly |
| --- | --- | --- | --- |
| 1 | £49.99 | $49.99 | £83.85 |
| 2 | £99.98 | $99.98 | £83.85 |
| 3 | £149.97 | $149.97 | £83.85 |
| 5 | £249.95 | $249.95 | £83.85 |

MEE6 states it plainly: "A subscription is valid for a single Discord server. If you wish to get
premium for multiple servers, you need a subscription for each server." Dyno's plans are described
as "for one server of your choice".

Carl-bot is a middle case worth knowing about. Premium is a **server slot** system: you subscribe
on Patreon, then mark servers yourself with `/premium addpremium`, free a slot with
`/premium removepremium`, and list them with `/premium listpremium`. Slots move between servers
without contacting support, and higher tiers carry more of them.

Wick's VIP tier is the other interesting shape: $20 a month advertises **12 premium servers**,
which works out at about **$1.67 per server per month** if you use them all, cheaper per server
than its own $5 Premium tier for anyone running a network.

Supervisor is the only one here billed per account, so one subscription covers any number of
servers. They share one monthly allowance rather than multiplying, which is the trade.

## What is actually behind each paywall

Worth separating, because "paid tier" rarely means "paid moderation".

- **Dyno**: all nineteen automod filters and the full Warn, Delete, Auto Mute, Auto Ban, Instant
  Mute and Instant Ban ladder are free. **Advanced Automod** buys per-rule log channels and custom
  responses. Free servers cap at 3 autopunishments, 14 day mutes and 3 month bans.
- **MEE6**: the eight automod checks, the warning-escalation ladder, `/ban`, `/tempban`, `/kick`
  and the audit log are free. Premium buys enhanced limits and engagement features, plus the Bot
  Personalizer addon on yearly and lifetime.
- **Carl-bot**: automod is free. Premium raises reaction roles from 250 to 1,000, YouTube alerts
  from 5 to 20, Twitch from 2 to 5, weblog entries from 100 to 500, and adds levels, sticky
  messages, auto purge, voice-role links, timed reaction roles and **Drama Watcher**, the one
  genuine moderation feature behind the paywall.
- **Sapphire**: the whole feature set is free, including AI moderation. The paid products are
  Custom Branding, tiered by server size, and a **Limit Increase** plan. That second one matters:
  Sapphire's docs state its AI "only scans 10 messages per server per minute" without it.
- **Wick**: every Premium line is an **Advanced**, **Customizable** or **Increased** version of
  something, which implies base versions are free, and Wick's documentation describes anti-nuke,
  panic mode, the restore system and Heat without marking them premium-only. Smart Backups is the
  exception worth paying for if restore matters to you.
- **Discord AutoMod**: free, with no paid tier of any kind.
- **Supervisor**: one plan with everything in it. There is no free tier for new accounts, just a
  seven day trial and £0.25 of moderation on signup with no card.

## Trial and refund terms

| Bot | What you get before committing |
| --- | --- |
| MEE6 | Fully refundable for 7 days, and transferable to another server |
| Supervisor | 7 day free trial on monthly and annual, plus £0.25 of moderation on signup |
| Sapphire | Not applicable, the features are free |
| Discord AutoMod | Not applicable, it is free |
| Dyno, Carl-bot, Wick | Free tiers cover moderation, so you can evaluate without paying |

## How usage pricing compares to a flat fee

Supervisor is the only one here that bills by usage rather than a flat fee, so the comparison needs
its own arithmetic rather than a row in a table.

Its plan includes **£120 of moderation a month**. Stating the assumption out loud: at an average
message of 100 bytes, that covers roughly **900,000 messages a month** on the Observer model,
450,000 on Sentinel, or 225,000 on Arbiter. Batched requests get 50% off, repeated identical
requests inside the cache window are free, and the link and word filters run before the models so
anything they block costs nothing.

Nine hundred thousand messages a month is about 30,000 a day. For most servers the allowance is not
the constraint, and the flat fee is what you actually pay.

The honest trade against a flat per-server fee: a flat fee is predictable and does not care how
busy you get, while usage pricing tracks your actual traffic and gets better the more servers you
spread it across.

## Why trust these figures

Every competitor price came from that vendor's own pricing page or documentation on 29 August 2026,
not from a comparison site. MEE6's premium page was rendered in a browser because it serves no
prices to a plain fetch; Dyno's monthly and annual views were both read, because reading only one
produces a wrong figure; Carl-bot's entry price came from its Patreon, where it is actually sold;
Wick's and Sapphire's came from their own premium pages.

Two things we could not read, and are not guessing at: the full Carl-bot Patreon tier list with its
slot counts, and Sapphire's Limit Increase pricing. Both are marked as unread above rather than
estimated.

We make Supervisor, so this is not a neutral comparison. What we have done instead is lead with the
fact that almost everything here moderates for free, put our own lack of a free tier in the table,
and show the arithmetic where our billing model looks worse as well as where it looks better.

We have no customer reviews or ratings to show you, because we have not collected any.

## So what should you actually pay?

- **One server, countable problems:** nothing. Discord AutoMod plus Dyno or Carl-bot covers it, and
  both moderate free.
- **One server, want AI moderation:** still nothing. Sapphire's AI is free, within its documented
  scan limit and its two fully supported languages.
- **Several servers:** the billing unit decides it. Per-server plans multiply, Carl-bot's slots
  move, and a per-account plan does not multiply at all.
- **Busy, multilingual, or harm arriving as images:** that is where the free options run out and
  paying for coverage starts to make sense.

Deeper breakdowns per bot: [MEE6](/blog/mee6-pricing), [Dyno](/blog/dyno-bot-pricing),
[Carl-bot](/blog/carl-bot-pricing), [Wick](/blog/wick-bot-pricing),
[Sapphire](/blog/sapphire-bot-pricing) and [Discord AutoMod](/blog/discord-automod-pricing).

Before paying anyone, and you may well not need to, see what each approach catches on your own
content in the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
