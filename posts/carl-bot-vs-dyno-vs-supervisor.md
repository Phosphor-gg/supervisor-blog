---
title: "Carl-bot vs Dyno vs Supervisor: two rule engines and one that reads meaning"
date: 2026-08-29
description: "Carl-bot and Dyno are the two most moderation-first general purpose bots on Discord. Here is the honest answer on which to pick, from their own docs, plus what neither can do."
---

# Carl-bot vs Dyno vs Supervisor: two rule engines and one that reads meaning

Carl-bot and Dyno are the two most moderation-first general purpose bots on Discord, and they are
similar enough that choosing between them is genuinely difficult. This post resolves that first,
from both bots' own documentation, then covers a third option that does a different job.

We make Supervisor, so treat that section accordingly. Everything about Carl-bot and Dyno comes
from their documentation, checked on 29 August 2026.

## The short answer

- **Pick Carl-bot** if you want the best response system on Discord: composable punishments and a
  way to route ambiguous cases to human moderators instead of guessing.
- **Pick Dyno** if you want the most detection surface: nineteen automod filters against
  Carl-bot's eight, all free.
- **Add Supervisor** if the messages hurting your community trip neither bot's filters, which is
  what happens when harm is contextual rather than countable.

## At a glance

| | Carl-bot | Dyno | Supervisor |
| --- | --- | --- | --- |
| Automod modules | 8 | 19 | 16 AI labels |
| Punishments | 11, combinable | 6 | 3 |
| Moderator voting queue | Yes, `defer` | No | No |
| Reads meaning | No | No | Yes |
| Conversation context | No | No | Yes |
| Images and video | Rate limits only | Image spam counts | Yes, reads content |
| Can ban or kick | Yes | Yes | No |
| Free tier includes automod | Yes | Yes | No, 7 day trial |
| Billing unit | Per server slot | Per server | Per account |
| Entry price | £6.50 / month via Patreon | $5.99 / month | £13.99 / month |

## Carl-bot vs Dyno: the differences that actually matter

### Detection surface

**Dyno wins on breadth.** Nineteen filters: All Caps, Bad Words, Chat Clearing Newlines,
Duplicate Text, Character Count, Emoji Spam, Fast Message Spam, Image Spam, Invite Links, Known
Phishing Links, Links, Links Cooldown, Mass Mentions, Mentions Cooldown, Spoilers, Masked Links,
Stickers, Sticker Cooldown and Zalgo Text.

**Carl-bot has eight modules**: message spam, attachment spam, bad words, caps limit, honeypot,
invites, links and mentions.

The gap is real but narrower than nineteen against eight suggests, because several of Dyno's
filters are variations on a theme, and Carl-bot has one Dyno lacks: a **honeypot** channel, which
is a trap for spam bots rather than a filter on human messages. Dyno's genuinely distinct
additions are Known Phishing Links, Zalgo Text, Sticker Cooldown and Character Count.

### Response model

**Carl-bot wins here, decisively.** Its punishments are delete, warn, tempmute, mute, timeout,
kick, tempban, ban, message, DM and defer. Durations are written naturally as `3h42m`, and
crucially **multiple punishments combine with commas**, so `delete, tempmute 20m` is a single
valid response to a rule. Dyno gives you one action per rule from a set of six: Warn, Delete, Auto
Mute, Auto Ban, Instant Mute, Instant Ban.

And Carl-bot has **`defer`**, which has no equivalent in any bot in this series. Instead of acting
automatically, it sends the offending context to a drama channel where moderators decide with
reactions. That is the only mechanism here that treats an ambiguous case as something to route to
a human rather than something to guess at. It requires premium, and it is the single most
thoughtful feature in this category.

### Warnings and history

**Carl-bot's warns do not automatically expire**, and the threshold punishment re-triggers on each
new warning while a member is above the limit. That is a deliberate choice that keeps history
meaningful.

**Dyno's automod warnings are deliberately separate** from its manual warning system. Its docs are
explicit that the Automod Warn action "is not a `?warn` and will not dm the user, be logged in the
Modlog channel, appear on `?warnings` or `?modlogs`, or go toward any Autopunish settings", and
that automod violations expire after 5 minutes.

If you want automod incidents to build a lasting record, Carl-bot's model does that and Dyno's
does not without extra work.

### Pricing model

Both are effectively per server, in different shapes.

**Dyno** is straightforwardly per server: $5.99 a month or $49.99 a year for Standard, "for one
server of your choice". Advanced Automod, meaning per-rule log channels and custom responses, is
the paid moderation feature. All nineteen filters and the full ban ladder are free.

**Carl-bot** sells premium through Patreon from £6.50 a month on a **transferable server slot**
system: you mark servers with `/premium addpremium`, free slots with `/premium removepremium`, and
list them with `/premium listpremium`. Tiers grant different numbers of slots. Automod is free;
the paid moderation feature is Drama Watcher, which is what powers `defer`.

Carl-bot's slots being movable without contacting support is a genuine advantage if you spin
servers up and down. Dyno's model is simpler to reason about.

### Verdict on Carl-bot versus Dyno

**Pick Carl-bot if you have active human moderators.** The composable punishments and the defer
queue are built for a team that wants to make the calls, and the reaction roles are the best on
Discord if you need those too.

**Pick Dyno if you want the bot to handle it.** More filters, finer thresholds, and an automatic
ban ladder that works without anyone watching.

Full breakdowns: [what Carl-bot costs](/blog/carl-bot-pricing) and
[what Dyno costs](/blog/dyno-bot-pricing), plus our [Carl-bot review](/blog/carl-bot-review) and
[Dyno review](/blog/dyno-bot-review).

## Where both hit the same ceiling

Both are rule engines, so both share a blind spot that no amount of configuration closes.

**Word lists only catch what you wrote down.** Carl-bot's censor lists and Dyno's Banned Words
fail on the same input: `fr33 n1tr0`, `h8`, `5c4m`, `h a t e`, `s.c.a.m`, homoglyphs, zero-width
characters. Dyno's documentation shows the trade-off explicitly, since wildcard mode matching "hi"
inside "high" is the cost of catching variations.

**Rate limits measure volume, never meaning.** Message spam, attachment spam, caps and mentions
all ask how many and how fast. A targeted threat or a well-written scam is one calm message that
satisfies no condition.

**Neither classifies harm by category.** No harassment module, no threat module, no scam module,
no self-harm module in either. Those are word lists you maintain, per language.

**Neither weighs conversation context**, and neither reads what is inside an image.

Carl-bot's honeypot catches bots, and Dyno's phishing detection catches known bad links. Neither
catches a person being deliberately cruel in correctly spelled English.

## What Supervisor adds, and what it does not

Supervisor reads what a message means rather than matching strings and counting events: 16 labels
including harassment, hate, threats, scams, self-harm and illegal activity, conversation context
and implicit moderation for ambiguous messages, image and video moderation that reads content, and
over 100 languages. Billed per account at £13.99 a month, or about £4.99 on the three year cycle,
so one subscription covers every server.

What it does not do:

- **No bans, kicks or mutes.** Delete, Timeout and Warn only, which is a much weaker response set
  than either bot here. Carl-bot's eleven combinable punishments are in a different league.
- **Nothing like `defer`.** No moderator voting queue.
- **No counters, no honeypot, no rate limits.**
- **No reaction roles, embeds, tags, triggers or starboard.** Three slash commands.
- **No free tier for new accounts**, just a seven day trial and £0.25 of moderation on signup.

The pairings in depth: [Supervisor vs Carl-bot](/blog/supervisor-vs-carl-bot-moderation) and
[Supervisor vs Dyno](/blog/supervisor-vs-dyno-moderation).

## So which should you use?

**One bot, moderators active:** Carl-bot. The defer queue alone justifies it.

**One bot, mostly automated:** Dyno. More filters, automatic escalation, all free.

**Either bot, and harmful messages still getting through:** the other bot will not fix it. Both
read strings and count events. Add a layer that reads meaning and keep the rule engine for the
countable work, which it does better than any AI would.

**Running several servers:** Dyno multiplies per server, Carl-bot consumes a slot per server, and
Supervisor is one subscription for the account.

The setup we would actually recommend for a busy server is all three layers: Discord AutoMod free
and blocking before messages post, Carl-bot or Dyno for countable rules and enforcement, and an AI
layer for the messages that read as harmless to a counter.

## For developers and platforms

Carl-bot and Dyno are Discord bots, so neither helps you moderate your own product. Supervisor has
a REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for
provisioning moderation to your own users. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and rates.

Whichever you pick, test it on your own content. Paste a message that gets past a keyword filter
into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
