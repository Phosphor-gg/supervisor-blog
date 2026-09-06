---
title: "Sapphire vs MEE6 vs Supervisor: free, paid, or specialist"
date: 2026-08-29
description: "Sapphire gives away most of what MEE6 charges for, including AI moderation. Here is the honest comparison from both bots' own docs, and where a specialist layer fits."
---

# Sapphire vs MEE6 vs Supervisor: free, paid, or specialist

**Bottom line:** on moderation Sapphire beats MEE6 and costs nothing, including real AI
detection MEE6 does not have. MEE6 wins on levels and engagement. Add Supervisor when Sapphire's
documented cap of 10 messages per server per minute, or its two fully supported languages, stops
covering your traffic.

Sapphire is the bot people find when they go looking for a free MEE6. It covers a lot of the same
ground, it does not charge for it, and it has one thing MEE6 does not: genuine AI moderation.

That makes this a real comparison rather than a price argument, so this post resolves Sapphire
against MEE6 first, then covers where a specialist moderation layer fits.

One disambiguation: Sapphire here is the Discord bot at sapph.xyz, not sapphirejs.dev, which is an
unrelated framework for building bots.

## The short answer

- **Pick Sapphire** if you want MEE6's breadth without the bill, and your server is not busy
  enough to hit its AI scan limit.
- **Pick MEE6** if you specifically want levels, economy and social alerts across six platforms,
  a full audit log, or a lifetime purchase.
- **Add Supervisor** if AI moderation is the point and you need it to see every message, across
  more categories and more languages.

## At a glance

| | Sapphire | MEE6 | Supervisor |
| --- | --- | --- | --- |
| Price | Free | £11.99 / month per server | £13.99 / month per account |
| Paid add-ons | Custom branding from €5, limit increase | Premium tiers | None, one plan |
| Lifetime option | No | Yes, £89.99 | No |
| AI moderation | **Yes, 4 categories** | No | **Yes, 16 labels** |
| AI scan limit | **10 messages / server / minute** | Not applicable | None |
| AI languages | English and German fully | Not applicable | 100+ |
| Rule modules | 12, condition-based | 8 checks | Link and word filters |
| Extends Discord AutoMod | **Yes** | No | No |
| Join filtering | Join Guard, 7 filters | No | No |
| Can ban or kick | Yes | Yes | No |
| Logging | 80+ log types | ~2 dozen event types | Alerts channel only |
| Images and video | Not documented | Not documented | Yes, reads content |

## Sapphire vs MEE6: the differences that actually matter

### Price, and what it actually changes

**Sapphire's entire feature set is free.** Its home page says "completely free", and the paid
products are Custom Branding from €5 a month and a Limit Increase plan, neither of which unlocks a
feature you otherwise cannot use.

**MEE6 is per server**, in its own words: "A subscription is valid for a single Discord server."
Standard rates are £11.99 a month, £49.99 a year, or £89.99 once for lifetime.

But the honest comparison is narrower than "free versus paid", because **MEE6's automod is also
free**. What MEE6 charges for is enhanced limits and engagement features. So if moderation is your
only concern, both cost nothing and the decision is about capability, not price.

Where price genuinely decides it: **levels**. MEE6 gives you levels, and Sapphire does not
advertise a levelling system at all. If levels are why you want a bot, Sapphire does not replace
MEE6 at any price.

### AI moderation, which only one of them has

This is the real differentiator and it runs the opposite way to the price.

**Sapphire has genuine AI moderation.** A model that flags insults, threats, identity attacks and
other offensive language, with sensitivity configurable per category at low, medium or high. MEE6's
Moderator plugin has nothing equivalent: its eight checks are Bad Words, Repeated Text, Server
Invites, External Links, Excessive Caps, a combined emoji, spoiler and mention check, Zalgo, and
Anti-Spam. All string matches and counters.

So the free bot has the more advanced detection mechanism. That is worth stating plainly.

Sapphire documents two limits on it: it "only scans 10 messages per server per minute" without the
paid Limit Increase plan, and "AI Moderation currently fully supports English and German", with
other languages supported but without categorisation.

### The AutoMod integration

**Sapphire's single best feature**, and nothing else in this comparison has it. Sapphire reads the
Discord AutoMod rules you have already configured under Server Settings and lets you attach
*additional* actions and conditions to them. You keep AutoMod's ability to block a message before
it posts, which no bot can replicate, and gain a richer response on top.

MEE6 runs alongside AutoMod but does not extend it.

### Enforcement and record keeping

**MEE6 wins on records.** Its audit log covers around two dozen event types delivered by webhook
every one to five minutes, plus a per-member infractions system, and automated actions that
escalate on accumulated warnings: ten warnings in fourteen days for a permanent ban, five in seven
days for a three-day ban, two in twenty four hours for a one-day mute.

**Sapphire counters with breadth.** Over 80 log types, moderation cases that warn, mute, kick or
ban, and an action set that also adds reactions and adds, removes or sets roles, which MEE6 does
not do as automod actions.

**Sapphire also has Join Guard**, seven filters combined with AND logic covering account age,
account creation date, default avatars, generated names, name content, guild tags and unverified
bots. MEE6 has no equivalent join gate.

### Verdict on Sapphire versus MEE6

**For moderation, Sapphire wins**, and it is free. AI detection MEE6 lacks, more rule modules, a
join gate, more logging, and the AutoMod integration.

**For engagement, MEE6 wins.** Levels, economy, giveaways, birthdays and social alerts across six
platforms are the reason MEE6 is on so many servers, and Sapphire does not match that side.

The honest recommendation for most servers weighing these two on moderation grounds: try Sapphire
first, because it costs nothing to find out.

Full breakdowns: [what Sapphire's free model covers](/blog/sapphire-bot-pricing),
[what MEE6 costs](/blog/mee6-pricing), and our [Sapphire review](/blog/sapphire-bot-review) and
[MEE6 review](/blog/mee6-review).

## Where both hit the same ceiling

They hit it in different places, which is unusual for this series.

**MEE6 hits it everywhere**, because all eight checks are strings and counters. `fr33 n1tr0`, `h8`
and `s.c.a.m` walk past Bad Words, and a calm targeted threat trips no counter.

**Sapphire hits it at the edges of its AI.** Four categories means scams, self-harm, sexual content
and illegal activity are not classified and fall back to word groups you maintain. Two fully
supported languages means a multilingual server is partly uncovered. And the ten messages per
minute cap means that in a busy channel, most messages never reach the model at all, so the
mechanism is sound but the coverage is thin exactly when the server is most active.

Neither reads what is inside an image. Neither weighs conversation context.

## What Supervisor adds, and what it does not

Since Sapphire also does AI moderation, the differences here are specific rather than categorical:

- **16 labels rather than four**, adding scams, self-harm, sexual content in three degrees,
  violence, spam, promotional and illegal activity.
- **No per-minute scan cap.** Every message in a moderated channel goes through a model; the
  constraint is a monthly allowance rather than throughput.
- **Over 100 languages** with the same labels throughout, rather than two fully supported.
- **Conversation context and implicit moderation** for messages ambiguous on their own.
- **Images and video** read as content.

What it does not do:

- **It is not free**, where Sapphire's equivalent is. £13.99 a month, or about £4.99 on the three
  year cycle, with a seven day trial and £0.25 of moderation on signup.
- **No bans, kicks or mutes.** Delete, Timeout and Warn only, where both other bots can ban.
- **No levels, economy, social alerts, reaction roles, join roles or logging suite.** Three slash
  commands.
- **It cannot extend Discord AutoMod** the way Sapphire does, and cannot block before posting.
- **No Join Guard** and no raid protection.

The pairings in depth: [Supervisor vs Sapphire](/blog/supervisor-vs-sapphire-moderation) and
[Supervisor vs MEE6](/blog/supervisor-vs-mee6-moderation).

## So which should you use?

**Leaving MEE6 to stop paying:** Sapphire, and it is the recommendation in our
[MEE6 alternatives](/blog/mee6-alternatives) piece too.

**Want levels and engagement:** MEE6, since Sapphire does not replace that side.

**Want the best free moderation:** Sapphire, comfortably.

**Busy server, multilingual, or harm arriving as images:** this is where Sapphire's documented
limits bite and where a dedicated layer earns its price. Running Sapphire for breadth and a
moderation layer for depth is a sensible pairing, and so is running Sapphire alone if it covers
you.

**Running several servers:** MEE6 multiplies per server, Sapphire is free everywhere, Supervisor
is one subscription for the account.

## Why trust this comparison

Everything above comes from the vendors' own material: the auto moderation page of
docs.sapph.xyz, including the scan limit and language quotes, and MEE6's Moderator plugin
documentation and premium pages. All read on 29 August 2026. Sapphire's top.gg rating was 96 out
of 100 from 215 ratings that day; MEE6 publishes no top.gg rating, and its Trustpilot score was
4.8 out of 5 from 7,217 reviews.

We make Supervisor, so this is not a neutral comparison and we have not written it as one. What we
have done instead is put the other side's advantages in their own section above, in plain terms,
and say where we could not read something rather than guessing at it.

On our own side, the figures come from our source and our evaluation set rather than from
marketing copy. Supervisor's models are retrained on real moderation feedback, the thumbs up and
thumbs down votes people leave on live flags in their own servers, which is the closest thing to
customer research this category has. The last full retrain moved average F1 across the 16 labels
from 0.794 to 0.941 on our internal evaluation set, with errors on harmless messages down 44
percent, and version 2.2 improved macro-F1 again across all three model tiers. The method and the
per-label numbers are in the [2.1 release post](/blog/supervisor-2-1).

**Where Supervisor leads, and where it does not.** On moderation coverage specifically it is the
most complete tool in this series: 16 labels where nothing else classifies more than four, over
100 languages, conversation context, and the only one that reads images and video. It is also the
narrowest, with no bans, no raid protection and no utility features, which is why every post here
recommends running it alongside another bot rather than instead of one.

We have no customer reviews, ratings or testimonials to show you, because we have not collected
any. Judge it on your own content in the [live demo](https://supervisor.gg/demo) rather than on
our word for it.

## For developers and platforms

Both are Discord bots, so neither helps you moderate your own product. Supervisor has a REST API
with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and rates.

Whichever you pick, and it may well be the free one, test it on your own content. Paste a message
that gets past a keyword filter into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
