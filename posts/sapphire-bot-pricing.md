---
title: "Sapphire bot pricing: free, with two paid add-ons"
date: 2026-08-29
description: "Sapphire gives away its whole feature set including AI moderation, and sells only Custom Branding from 5 euros a month and a Limit Increase plan. Here is what free actually covers and where the limits bite."
---

# Sapphire bot pricing: free, with two paid add-ons

Sapphire, the multi-purpose Discord bot at sapph.xyz (not to be confused with sapphirejs.dev, an
unrelated bot-building framework), describes itself in three words on its own home page:
"Completely free."

That is broadly true, and it is worth being precise about the exceptions, because there are two
paid add-ons and one of them affects moderation directly.

## What free gets you

The entire feature set. Moderation with case management, reason aliases and customisable DM
notifications. Auto moderation across five categories. Social notifications for Twitch, YouTube
and TikTok. Logging with over 80 log types. Reaction roles, join roles, welcome messages, role
connections and a built-in editor for every message the bot sends.

The auto moderation deserves spelling out, because it is more than most paid bots offer:

- **AI Moderation**, detecting insults, threats, identity attacks and other offensive language,
  with sensitivity set per category to low, medium or high.
- **Discord's built-in Auto Moderation**, where Sapphire attaches additional actions to the
  AutoMod rules you already have in Server Settings. This is genuinely clever and nobody else
  does it.
- **Advanced Auto Moderation**, 12 modules built on conditions like "at least 5 mentions in 15
  seconds", with word groups, regular expressions, and word list import and export.
- **Join Guard**, seven filters combined with AND logic: account age, account creation date,
  default avatars, generated names, name content, guild tags and unverified bots.
- Auto-deletion of thread creation system messages.

Actions include reporting to moderators, deleting, sending messages, DMing the user, opening a
moderation case that warns, mutes, kicks or bans, adding reactions, and adding, removing or
setting roles.

For zero cost, that is a remarkable amount of product.

## What you pay for

Two add-ons, neither of which unlocks a feature you otherwise cannot use.

**Custom Branding, starting at €5 per month.** It gives your bot a custom name, avatar, status and
about me, plus access to logs without webhooks, global user update logs, and what Sapphire calls
"highest uptime". Its FAQ confirms the price varies with server size, with entries for "Why are
there different price tiers?" and "My server is growing quite fast, what happens if I reach
another price tier?". We did not read the tier table, so we are not going to describe what a
larger server pays.

**Limit Increase**, which raises Sapphire's usage limits. We could not read its pricing, so we are
not quoting a figure.

Checked on 29 August 2026, in euros as displayed to us. Vendors change pricing, so check before
you buy.

## The limit that actually matters

If you are evaluating Sapphire for moderation specifically, this is the number to know, and it
comes from Sapphire's own documentation:

> Sapphire currently only scans 10 messages per server per minute. This limit can be increased
> with Sapphire's Limit Increase plan.

That cap applies to the AI moderation. Ten messages a minute is fine for a quiet server. In a
channel running at sixty messages a minute, roughly one message in six reaches the model, and the
rest are covered only by the rule modules and your own word groups.

So the honest summary of Sapphire's pricing is not "free versus paid features". It is that the
features are free and the *throughput* is what is metered. For a small community that is a
generous deal. For a busy one, the Limit Increase plan is not optional if you want the AI side to
actually see your traffic.

The rule-based modules, Join Guard and Discord AutoMod integration are not documented as being
subject to that cap.

## How Supervisor prices moderation

Supervisor sells one plan with everything in it, billed per account rather than per server.

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and one subscription covers any number of
servers drawing on that allowance. There is a seven day free trial on monthly and annual, and
every new account gets £0.25 of moderation free on signup with no card. There is no free tier for
new accounts.

The pricing model is the mirror image of Sapphire's. Supervisor has **no per-minute scan cap**:
every message in a moderated channel goes through a model. What is metered is the monthly
allowance, spent by the size of what is read and the model chosen. At an average message of 100
bytes, £120 a month covers roughly 900,000 messages on Observer, 450,000 on Sentinel, or 225,000
on Arbiter. Batched requests get 50% off, repeated identical requests inside the cache window are
free, and the link and word filters run before the AI models so anything they block costs nothing.

Nine hundred thousand messages a month is around 30,000 a day, or roughly 20 a minute sustained
around the clock.

## Comparing the two honestly

The currencies differ, Sapphire in euros and Supervisor in pounds, and we are not going to convert
them for you, because a comparison that quietly converts is one you cannot check.

What is comparable is the shape:

- **Sapphire is free and Supervisor is not.** If Sapphire covers your server, use Sapphire. We
  would rather say that than pretend otherwise.
- **Sapphire meters throughput, Supervisor meters volume over a month.** Ten messages a minute is
  a hard ceiling regardless of how quiet the rest of your day was. A monthly allowance lets a busy
  hour borrow from a quiet one.
- **Sapphire gives you far more surface**: reaction roles, logging, joins, social notifications,
  bans and kicks. Supervisor has three slash commands and no utility features.
- **Supervisor gives you more coverage on the moderation itself**: 16 labels against four
  categories, over 100 languages against two fully supported, images and video as well as text,
  and conversation context for ambiguous messages.

Which is why running both is reasonable, and running Sapphire alone is also reasonable. There is a
[full comparison of the two moderation systems](/blog/supervisor-vs-sapphire-moderation) if you
want the detail.

## For developers and platforms

Sapphire is a Discord bot, so its pricing has no bearing on moderating your own product.
Supervisor bills the same way outside Discord as inside it, per byte at the model rate, through a
REST API with SDKs for Python, JavaScript, Go, Rust and Java. The
[API reference](https://supervisor.gg/docs/integrations/api) has the current rates and the
[pricing page](https://supervisor.gg/pricing) has the plan.

Before paying anyone, and Sapphire may well mean paying nobody, see what each approach catches on
your own content. Paste a message that gets past a keyword filter into the
[live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
