---
title: "Carl-bot review: what it is good at and where it runs out"
date: 2026-08-29
description: "An honest review of Carl-bot from a company that makes a competing moderation tool. Its automod modules, the unusually rich punishment set, what its public rating says, and where a rule engine stops."
---

# Carl-bot review: what it is good at and where it runs out

**Bottom line:** Carl-bot has the best moderation responses of any bot here, eleven punishments
that combine in one rule plus a `defer` action that routes ambiguous cases to a human vote, and
automod is free. Its detection is still lists and rate limits, so add Supervisor when what is
hurting your community is contextual rather than countable.

We make an AI moderation tool, so treat this as an interested party's assessment. Every claim
about Carl-bot below comes from Carl-bot's own documentation, and the rating comes from a public
page you can open yourself. Where we could not verify something, we say so instead of guessing.

## What Carl-bot is

Carl-bot is a general purpose Discord bot best known for reaction roles, with a substantial
moderation side alongside logging, embeds, feeds, greetings, starboard, suggestions, tags and
triggers. It is configured mostly through a web dashboard, and its own documentation says it is
"highly recommended to use the Dashboard for setting up automod".

## What Carl-bot does well

**The punishment set is the richest of any bot we have looked at.** Automod can respond with
delete, warn, tempmute, mute, timeout, kick, tempban, ban, message, DM, or defer. Durations are
written naturally as `3h42m`, and crucially **you can combine punishments by separating them with
commas**, so `delete, tempmute 20m` is a single valid response. Most bots give you one action per
rule. Carl-bot gives you a policy.

**Defer is a genuinely original idea.** Instead of acting automatically, the `defer` punishment
sends the offending context to a drama channel where moderators vote with reactions. That turns
the ambiguous cases into a queue for humans rather than forcing you to choose between
over-blocking and under-blocking. It is a premium feature, and it is the most thoughtful design
in the category.

**The module coverage is broad.** Automod covers message spam, attachment spam, bad words, caps
limit, invites, links, mentions, and a honeypot. Each has its own rate limits and its own
punishments.

**The rate limit model is honest about needing configuration.** Message spam "will not be active
without setting a rate limit of at least 1+ messages in 1+ seconds first", and the docs warn that
once active, the triggering message is deleted even if `delete` is not among the punishments. That
is the kind of side effect most products let you discover in production.

**Whitelisting and scoping are well thought out.** Roles and channels can be whitelisted so
automod ignores them, channels can be set media-only, and there is a `deletefiles` toggle for
unsafe file types with the safe list spelled out: png, jpg, jpeg, gif, svg, bmp, tif, webp, webm,
mp4, mov, pdf, txt, mp3, flac and wav.

**Warn thresholds are persistent by design.** Warns do not automatically expire, and the threshold
punishment triggers on every new warning while a member is above the limit, which is a deliberate
and defensible choice rather than an oversight.

## Where Carl-bot runs out

Every automod module is a string match, a rate limit, or a trap. That is the ceiling.

**Bad words only catches what you wrote down.** Not the leetspeak version, not the homoglyph
version, not the one with a zero-width character in the middle, and not the same idea in another
language. The usual evasions apply: `fr33 n1tr0`, `h8`, `5c4m`, `h a t e`, `s.c.a.m`.

**Rate limits measure volume, never meaning.** Message spam, attachment spam, caps and mentions
all ask how many and how fast. A targeted threat, a grooming attempt or a convincing scam is one
calm, correctly spelled message that trips none of them.

**The honeypot catches bots, not people.** It is an excellent trap for automated spam accounts,
and a member deliberately making one person's life miserable will never post in it.

**There are no harm categories.** Nothing identifies harassment, hate, threats or self-harm as
categories in their own right, so each becomes a censor list you maintain.

**Nothing weighs conversation context.** Each module judges one message alone.

**The documentation describes no image or video content analysis.** Attachments are rate limited
and unsafe file types can be deleted, but what is inside a picture is not examined.

## What users say

| Source | Score | Sample | Checked |
| --- | --- | --- | --- |
| top.gg | 62 out of 100 | 594 ratings | 29 August 2026 |

Two things about that number. top.gg rates on a 0 to 100 scale rather than out of five. And it is
lower than the other bots we checked on the same scale and the same day, where Dyno was 87, Wick
84 and Sapphire 96.

We are reporting it because leaving it out would be dishonest, and we are not going to build a
narrative on it, because we cannot tell you why it is what it is. We could not systematically
sample the reviews behind it from sources we can cite, so we do not know whether it reflects the
moderation features, an outage, a pricing change, or something else entirely. A rating is not an
explanation. Carl-bot remains one of the most widely used bots on Discord and the feature work
described above is genuinely good.

## Where Supervisor fills the gaps, and where it does not

Supervisor reads what a message means rather than matching strings and counting events:

- No censor list to spell around, so leetspeak, homoglyphs and invisible characters are read as
  what they mean.
- 16 labels including harassment, hate, threats, scams, self-harm and illegal activity.
- Conversation context weighed when a message is ambiguous alone.
- Images and video moderated on content, not just rate limited by count.
- Over 100 languages without a list per language.

Where it does not fill the gap, plainly:

- **Supervisor cannot ban, kick, mute or tempban.** Its actions are Delete, Timeout and Warn.
  Carl-bot's punishment set is far richer, and there is no Supervisor equivalent of combining
  several punishments in one rule.
- **Supervisor has nothing like defer.** There is no moderator voting queue.
- **Supervisor has no honeypot**, no persistent warn threshold system, and no rate limits.
- **Supervisor has no reaction roles, embeds, feeds, starboard, tags or triggers.** Three slash
  commands, and everything else on the dashboard.
- **Supervisor is paid**, at £13.99 a month or about £4.99 a month on the three year cycle, with
  a seven day trial and £0.25 of moderation free on signup.

There is a [full comparison of the two approaches](/blog/supervisor-vs-carl-bot-moderation) if you
want the mechanism side in depth.

## Who Carl-bot is right for

Carl-bot is right for you if you want reaction roles done properly, a genuinely flexible
punishment system, and automod modules you can tune precisely. The combination of composable
punishments and the defer queue makes it the best choice in this category for a server that wants
moderators in the loop rather than fully automated enforcement.

It is not sufficient on its own if the content hurting your community is contextual, multilingual,
image-based, or written by someone deliberately spelling around your censor list. That is a
description of what rule engines are for rather than a criticism. Running both is the normal
answer.

## For developers and platforms

Carl-bot is a Discord bot, so it does not help you moderate your own product. Supervisor has a
REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints.

The quickest way to judge any of this is on your own content. Paste a message that gets past a
keyword filter into the [live demo](https://supervisor.gg/demo) and see whether it gets caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
