---
title: "Supervisor vs Sapphire: two AI moderation systems compared"
date: 2026-08-29
description: "Sapphire is the only major free Discord bot with real AI moderation, and it is genuinely good. An honest comparison with Supervisor covering categories, language support, and the scan rate limit that decides it."
---

# Supervisor vs Sapphire: two AI moderation systems compared

Sapphire, the free multi-purpose Discord bot at sapph.xyz, is not to be confused with
sapphirejs.dev, which is an unrelated framework for building Discord bots. This post is about the
bot.

Of every comparison in this series, this is the one where the other tool is closest to what we do.
Sapphire has real AI moderation, not a keyword list with a marketing label on it, and it gives it
away for free. So this comparison is not "rules versus AI". It is two AI moderation systems with
different scopes, and there are specific, checkable differences that decide which fits your
server. This is an honest comparison, and unlike the rest of this series, these two really are the
same kind of tool.

## What Sapphire's moderation actually is

Sapphire's Auto Moderation module is split into five categories, and it is a genuinely impressive
amount of engineering to give away.

**AI Moderation** uses a model to flag messages, with per-category sensitivity set to low, medium
or high. It detects insults, threats, identity attacks, and other offensive language.

**Discord's built-in Auto Moderation**, which is the cleverest idea in the product. Rather than
replacing Discord's native AutoMod, Sapphire reads the rules you have already set up under Server
Settings and lets you attach *additional* actions and conditions to them. Nobody else in this
comparison does that.

**Advanced Auto Moderation**, Sapphire's own rule engine, made of 12 modules built on conditions.
A condition is an operator (exactly, or at least), a message count, a time frame and a time unit,
so "at least 5 mentions in 15 seconds" is expressed directly. Words live in groups that bind to
conditions, with toggles for ignoring capitalisation and requiring whole words, custom regular
expressions, nested sub-groups, and import and export of word lists as text or JSON. Sapphire's
docs note the one regex limitation up front: no negative lookahead or lookbehind.

**Join Guard**, seven filters combined with AND logic covering account age, account creation date,
default avatars, generated names, name content, guild tags and unverified bots.

**Auto-delete of thread creation system messages**, which is a small quality-of-life thing.

The action set is broad: report to moderators, delete message, send message, DM user, open a
moderation case that warns, mutes, kicks or bans, add reactions, and add, remove or set roles.

This is genuinely good tooling, and the free tier includes all of it.

## Where Sapphire's AI moderation runs out

Three limits, all documented by Sapphire itself, and the first is the one that decides most
servers.

**It scans 10 messages per server per minute.** Sapphire's own documentation says: "Sapphire
currently only scans 10 messages per server per minute. This limit can be increased with
Sapphire's Limit Increase plan." That is a hard ceiling on the AI moderation specifically, and in
a busy channel it means most messages are never seen by the model. A server posting 60 messages a
minute is getting roughly one in six checked. Sapphire is upfront about it and sells a plan to
raise it, which is fair, but you should know it before assuming your server is covered.

**Its categories are insults, threats, identity attacks, and other offensive language.** Four,
and they are well chosen, but they do not cover scams, self-harm, sexual content, spam or illegal
activity as classified categories. Those fall back to the rule modules and your own word groups.

**Full language support is English and German.** From the docs: "AI Moderation currently fully
supports English and German. Other languages are supported as well, but do not support
categorization of inappropriate language." Insults, threats and identity attacks are flagged in
English and German. The broader "other offensive language" category extends to Italian, French,
Russian, Portuguese, Spanish and Turkish. If your community speaks something else, the AI side is
thinner.

Beyond the AI, the 12 advanced modules are condition-based, meaning they count messages within
time frames. Those are volume rules, so the same ceiling applies as with any counter: a single
calmly written harmful message satisfies no condition.

## What Supervisor does differently

Supervisor is AI moderation as the whole product rather than one module among many, and the
differences are specific:

- **16 labels rather than four categories**, covering harassment, hate, threats, insults, scams,
  spam, promotional content, sexual content in three degrees, self-harm, medical, violence,
  sensitive content and illegal activity.
- **No scan rate limit.** Every message in a moderated channel goes through the model. The
  constraint is your monthly allowance, not a per-minute cap.
- **Over 100 languages**, with the same labels applied in all of them rather than full support in
  two.
- **Conversation context.** When a message is ambiguous alone, Supervisor can weigh recent channel
  history, and it has implicit moderation for harm that is implied rather than stated.
- **Images and video.** Supervisor reads what is in a picture, and analyses the changing frames of
  a video clip. Sapphire's documented automod works on message text, counts and joins.
- **Three model tiers**, so you can choose accuracy against cost per message.

## What Sapphire does that Supervisor does not

This list is long, and it matters.

- **Sapphire is free.** All of the above, at no cost, with paid plans only for raising limits and
  custom branding. Supervisor is £13.99 a month, or about £4.99 on the three year cycle.
- **Sapphire can ban, kick and mute** through moderation cases. Supervisor's actions are Delete,
  Timeout and Warn only.
- **Sapphire extends Discord's native AutoMod** rather than ignoring it. Supervisor runs alongside
  AutoMod but cannot attach actions to it.
- **Join Guard.** Supervisor has no join filtering, no account age checks and no raid protection
  of any kind.
- **Full regular expressions**, plus word group import and export. Supervisor's word filter does
  whole-word matching with a `*` wildcard.
- **Role actions.** Sapphire can add, remove or set roles as a moderation action. Supervisor
  cannot.
- **80+ log types.** Supervisor has an alerts channel.
- **Reaction roles, social notifications, welcome messages and the rest.** Supervisor has three
  slash commands.

## Coverage is the difference, not intelligence

This is the honest way to frame it. Both products use AI to read what a message means, and
Sapphire's implementation is a real one. The differences are how much it reads and how widely it
classifies: ten messages a minute against every message, four categories against sixteen, two
fully supported languages against over a hundred, and text only against text, images and video.

For a small or medium server that speaks English or German and is not posting faster than the
scan limit, Sapphire's AI moderation may well cover you completely, and it is free. That is a
genuinely good outcome and we are not going to pretend otherwise.

For a large, busy, multilingual server, or one where harmful content arrives as images, or where
you need scams and self-harm classified rather than filtered by word list, the coverage gap is
where Supervisor earns its price.

## For developers and platforms

Sapphire is a Discord bot, so it does not help you moderate your own product. Supervisor has a
REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and the current rates.

## So which should you use?

Unusually for this series, these two overlap enough that you might reasonably pick one.

Use Sapphire if you want a free, broad, well-built bot, your community is English or German
speaking, your channels are not busy enough to hit the scan limit, and you want reaction roles,
logging, join filtering and social notifications from the same tool. It is a lot of product for
nothing, and its Discord AutoMod integration is the smartest feature in this whole comparison.

Reach for Supervisor when coverage is the problem: every message checked rather than ten a minute,
sixteen labels rather than four, a hundred languages rather than two, and images and video read
rather than counted. Supervisor is the AI moderation layer, and it still sits alongside your
utility bot rather than replacing it, because it does not do reaction roles, logging or joins.

Running Sapphire for breadth and Supervisor for depth is a perfectly sensible setup, and so is
running Sapphire alone if it covers you.

Want to see the difference on your own content? Paste a message that gets past a keyword filter
into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
