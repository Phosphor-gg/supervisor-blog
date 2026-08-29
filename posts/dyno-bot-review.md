---
title: "Dyno bot review: what it is good at and where it runs out"
date: 2026-08-29
description: "An honest review of Dyno, the Discord moderation bot, from a company that makes a competing tool. What its nineteen automod filters cover, what the public ratings say, and where a rule engine stops."
---

# Dyno bot review: what it is good at and where it runs out

We make an AI moderation tool, so treat this as an interested party's assessment. Every claim
about Dyno below comes from Dyno's own documentation, and every rating comes from a public
page you can open yourself. Where we could not verify something, we say so instead of guessing.

## What Dyno is

Dyno is a long-standing general purpose Discord bot with a large module set: automod,
moderation commands, action logging, autoroles, custom commands, tickets, levels, giveaways,
starboard, reaction roles, social feeds and more. It is configured through a web dashboard
rather than in Discord, and its automod module is one of the most configurable rule engines
you can put in a server.

Setting it up means enabling the Automod module, choosing a default log channel, optionally
setting ignored channels and roles, then creating individual rules. Dyno needs a fairly broad
permission set to work: Manage Webhooks, Manage Roles, Ban Members and Timeout Members at the
server level, plus View Channel, Send Messages, Send Messages in Threads, Manage Messages and
Read Message History in channels. That is the direct consequence of it being able to ban and
assign roles, not bloat.

## What Dyno does well

**The filter list is genuinely comprehensive.** Dyno documents nineteen automod filters: All
Caps (default 70%), Bad Words, Chat Clearing Newlines, Duplicate Text, Character Count, Emoji
Spam, Fast Message Spam, Image Spam, Invite Links, Known Phishing Links, Links, Links Cooldown,
Mass Mentions, Mentions Cooldown, Spoilers, Masked Links, Stickers, Sticker Cooldown and Zalgo
Text. If a thing can be counted or matched, Dyno probably has a filter for it.

**It escalates properly.** The actions are Warn, Delete, Auto Mute, Auto Ban, Instant Mute and
Instant Ban, with Auto Mute and Auto Ban firing after a violation count you set. That is a real
enforcement ladder, and it is more than most moderation tools offer, ours included.

**The scoping model is thorough.** Every rule takes Affected Roles, Affected Channels, Ignored
Roles and Ignored Channels, and Automod automatically ignores the server owner, administrators,
and manager and moderator roles. You can also create several rules for the same filter with
different actions, which is how you build a graduated policy rather than a single blunt one.

**Its documentation is honest about its own edges.** The docs state plainly that the Automod
Warn action "is not a `?warn` and will not dm the user, be logged in the Modlog channel, appear
on `?warnings` or `?modlogs`, or go toward any Autopunish settings", and that automod violations
expire after 5 minutes. That is the kind of detail most products leave you to discover after an
incident, and Dyno writes it down.

**Known Phishing Links is a maintained detection**, not something you have to keep a list for.
That is a category of harm handled for you rather than delegated to your moderators.

**Link matching is sensibly designed.** You do not need to add a protocol prefix, and adding a
domain covers its paths, with an allow list available even when deleting all links.

## Where Dyno runs out

Every one of those nineteen filters is either a string match or a counter, and that is the
ceiling.

**A word list only matches what you wrote down.** Dyno gives you two modes, and the trade-off
between them is the clearest illustration of the problem in any product we have looked at.
Banned Words (exact) matches only the exact word, so `fr33 n1tr0`, `h8` and `s.c.a.m` walk
straight past. Banned Words (wildcard) matches the word inside other words, and Dyno's own
documentation gives the example that banning "hi" also matches "high". One setting misses the
evasions, the other flags innocent members, and there is no third setting that reads intent.

**Counters measure volume, never meaning.** Fast Message Spam, Mass Mentions, Emoji Spam, Image
Spam and the various cooldowns all ask "how many" and never "what". A targeted threat, a
grooming attempt or a convincing scam is a single, calmly written, correctly spelled message. It
contains no banned word, no mention flood, no caps, no emoji. Every counter reads zero.

**No filter classifies harm by category.** There is nothing in the documented list that
identifies harassment, hate, threats, self-harm or scams as categories. Those become word lists
you write and maintain, in every language your community speaks.

**Nothing weighs conversation context.** Each filter judges one message on its own, so the
messages that most need judgement are the ones no rule can make.

None of that makes Dyno a bad tool. It makes it a rule engine, which is what it says it is.

## What the public ratings say

We could not systematically sample user reviews, so rather than characterise themes we cannot
evidence, here are the public aggregates with their full provenance, and their caveats.

| Source | Score | Sample | Checked |
| --- | --- | --- | --- |
| top.gg | 87 out of 100 | 373 ratings | 29 August 2026 |
| Trustpilot | 4.2 out of 5 | 68 reviews | 29 August 2026 |

Two things worth stating rather than glossing. top.gg rates on a 0 to 100 scale, not out of
five, so 87 there is not comparable to 4.2 here. And Trustpilot displays its own caution on this
profile: "This company hasn't invited their customers, so reviews may not be representative."
The profile is also unclaimed. The Trustpilot distribution is polarised, with 84% at five stars
and 10% at one star and very little in between, which is a common shape for a free product with
a large user base and is an observation about the data rather than a conclusion about the
product.

Both aggregates are positive. We are not going to pretend otherwise.

## What Dyno costs

We are not quoting Dyno's prices, because we could not read Dyno's pricing page from our
tooling and we do not publish figures we have not verified. What the documentation does tell us
is the shape of the paywall.

Dyno documents two separate subscription products, which are easy to confuse: a **Dyno Premium**
subscription, with named plans including **Standard Premium** and **Custom Premium**, and a
separate **Dyno Membership** subscription. Documented as requiring Standard Premium: a per-rule
automod log channel, a per-rule custom response, and custom moderation responses. Custom Emojis
requires Custom Premium. On the free tier, a server can have a maximum of three autopunishments,
mutes cap at 14 days, bans at 3 months and role additions at 30 days.

The automod engine itself, and the nineteen filters, are available without paying.

## Where Supervisor fills the gaps, and where it does not

Supervisor is an AI moderation bot. Instead of matching strings and counting events, it reads
what a message means, which addresses the specific ceilings above:

- The evasion trade-off disappears, because there is no word list to spell around. Leetspeak,
  homoglyphs, invisible characters and creative spelling are read as what they mean.
- It classifies across 16 labels, including harassment, hate, threats, scams, self-harm and
  illegal activity, which is the category coverage a filter list does not provide.
- It can weigh recent conversation history when a message is ambiguous on its own.
- It moderates images and video, reading the content rather than counting the attachments.
- It works in over 100 languages without a word list per language.

Where it does not fill the gap, plainly:

- **Supervisor cannot ban or mute.** Its actions are Delete, Timeout and Warn. Dyno's
  enforcement ladder, with Auto Ban and Instant Ban on a violation count, has no equivalent.
- **Supervisor has no counters.** Newlines, character count, sticker spam, zalgo, all caps
  percentage and duplicate text are not things it measures. For those, a rule engine is the
  right tool.
- **Supervisor has no dedicated phishing link detection.** Its link filter covers Discord
  invites, media, Nitro gift links and your own domain allow and block lists.
- **Supervisor has no modules.** No levels, tickets, custom commands, autoroles, giveaways or
  social feeds. Three slash commands, and everything else on the web dashboard.
- **Supervisor is paid**, at £13.99 a month or about £4.99 a month on the three year cycle, with
  a seven day trial and £0.25 of moderation free on signup.

There is a [full comparison of the two approaches](/blog/supervisor-vs-dyno-moderation) if you
want the mechanism side in depth.

## Who Dyno is right for

Dyno is right for you if you want one bot doing many jobs, if your moderation problems are
countable or matchable, and if you want a real enforcement ladder with bans and mutes attached
to violation counts. For a very large number of servers that is an accurate description, and
Dyno will serve them well for free.

It is not sufficient on its own if the content actually hurting your community is contextual,
multilingual, image-based, or written by someone deliberately spelling around your filters.
That is not a criticism of Dyno so much as a description of what rule engines are for. Running
both is the normal answer: Dyno for the countable problems and the enforcement, an AI layer for
the meaning.

## For developers and platforms

Dyno is a Discord bot, so it does not help you moderate your own product. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api)
has the endpoints and the current rates.

The quickest way to see where the two approaches differ is on your own content. Paste a message
that gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it
get caught, or [add Supervisor to your server](https://invite.supervisor.gg).
