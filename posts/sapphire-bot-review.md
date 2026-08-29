---
title: "Sapphire bot review: what it is good at and where it runs out"
date: 2026-08-29
description: "An honest review of Sapphire from a company that makes a competing AI moderation tool. Real AI moderation given away free, an unusually clever AutoMod integration, and one rate limit worth knowing about."
---

# Sapphire bot review: what it is good at and where it runs out

We make an AI moderation tool, so treat this as an interested party's assessment, and be aware
this is the review in our series where the other product competes with us most directly. Every
claim about Sapphire below comes from Sapphire's own documentation, and the rating comes from a
public page you can open yourself.

One disambiguation first: this is Sapphire the Discord bot at sapph.xyz, not sapphirejs.dev, which
is an unrelated framework for building Discord bots and often outranks it in search.

## What Sapphire is

Sapphire is a free multi-purpose Discord bot, operated by Xge Development, covering moderation,
auto moderation, reaction roles, join roles, welcome messages, role connections, social
notifications and logging. Its own home page states it is in over 1,788,200 servers reaching more
than 628.8 million users, and describes the product as "fully customizable, completely free".

## What Sapphire does well

**It has real AI moderation, and it gives it away.** Not a keyword list with a marketing label,
but a model that flags insults, threats, identity attacks and other offensive language, with
sensitivity configurable per category at low, medium or high. Of the major free Discord bots, this
is the only one we found doing genuine content classification, and that is worth saying plainly
even though it competes with what we sell.

**The Discord AutoMod integration is the smartest feature in this entire comparison series.**
Rather than ignoring or duplicating Discord's native AutoMod, Sapphire reads the rules you have
already configured under Server Settings and lets you attach additional actions and conditions to
them. You keep AutoMod's ability to block a message before it posts, which no bot can replicate,
and gain a richer response on top. Nobody else does this.

**The rule engine is properly designed.** Twelve modules built on explicit conditions: an operator
for exactly or at least, a message count, a time frame and a unit. Word groups bind lists of words
to specific conditions, with toggles for ignoring capitalisation and requiring whole words, nested
sub-groups, and import and export of word lists as text or JSON. That import path is a thoughtful
migration feature, since it accepts lists from other bots.

**It is honest about limitations in its own docs.** Sapphire states its regex support excludes
negative lookahead and lookbehind, and that attempting them produces an "Unknown Error". It also
publishes its scan rate limit rather than burying it.

**Join Guard is a solid gate.** Seven filters combined with AND logic: account age, account
creation date, default avatars, generated names, name content, guild tags and unverified bots.

**The action set is broad.** Report to moderators, delete, send a message, DM the user, open a
moderation case that warns, mutes, kicks or bans, add reactions, and add, remove or set roles.

## Where Sapphire runs out

**The AI scans 10 messages per server per minute.** Sapphire's documentation is explicit: "Sapphire
currently only scans 10 messages per server per minute. This limit can be increased with
Sapphire's Limit Increase plan." In a channel running at sixty messages a minute, that is roughly
one message in six reaching the model. This is the single most important number in this review,
and how much it matters depends entirely on how busy your server is.

**The AI covers four categories.** Insults, threats, identity attacks, and other offensive
language. Well chosen, but scams, self-harm, sexual content and illegal activity are not
classified categories, so those fall back to word groups you maintain.

**Full language support is English and German.** From the docs: "AI Moderation currently fully
supports English and German. Other languages are supported as well, but do not support
categorization of inappropriate language." Insults, threats and identity attacks are English and
German. The broader offensive language category adds Italian, French, Russian, Portuguese, Spanish
and Turkish.

**The 12 advanced modules are condition-based**, meaning they count messages within time frames.
That is a volume mechanism, so a single calm, correctly spelled harmful message satisfies no
condition.

**The documentation describes no image or video content analysis.** Attachments feature in
conditions as counts, not as content to read.

## What users say

| Source | Score | Sample | Checked |
| --- | --- | --- | --- |
| top.gg | 96 out of 100 | 215 ratings | 29 August 2026 |

That is the highest score of the five bots we checked on the same day and the same 0 to 100 scale,
where Dyno was 87, Wick 84 and Carl-bot 62. It is also the smallest sample of the four, at 215
ratings, so it is a strong signal on a narrower base. We did not find a Trustpilot profile, and we
could not systematically sample individual reviews from sources we can cite, so that aggregate is
what we are reporting rather than themes we cannot evidence.

## Where Supervisor fills the gaps, and where it does not

Since both products do AI moderation, the differences are specific rather than categorical:

- **16 labels rather than four**, adding scams, self-harm, sexual content in three degrees,
  violence, medical, spam, promotional and illegal activity.
- **No per-minute scan cap.** Every message in a moderated channel goes through a model; the
  constraint is a monthly allowance rather than a throughput ceiling.
- **Over 100 languages** with the same labels applied throughout.
- **Conversation context and implicit moderation** for messages that are ambiguous alone.
- **Images and video** read as content.

Where Supervisor does not fill the gap, and this list is long:

- **Supervisor is not free.** £13.99 a month, or about £4.99 on the three year cycle, with a seven
  day trial and £0.25 of moderation on signup. Sapphire's equivalent costs nothing.
- **Supervisor cannot ban, kick or mute.** Delete, Timeout and Warn are the whole list.
- **Supervisor cannot attach actions to Discord's AutoMod**, which is Sapphire's best trick.
- **Supervisor has no Join Guard**, no account age filtering and no raid protection.
- **Supervisor has no role actions**, no reaction roles, no logging suite and no social
  notifications.
- **Supervisor's word filter is not regex.** Whole-word matching with a `*` wildcard, and no word
  list import or export.

There is a [full comparison of the two moderation systems](/blog/supervisor-vs-sapphire-moderation)
if you want the mechanism in depth, and a look at
[what Sapphire's free model actually covers](/blog/sapphire-bot-pricing).

## Who Sapphire is right for

Sapphire is right for you if you want a lot of well-built product for nothing, if your community
speaks English or German, if your channels are not busy enough to run past the scan limit, and
especially if you already rely on Discord's native AutoMod and want to extend it rather than
replace it. For a great many servers that is an accurate description, and the honest recommendation
is to use Sapphire and not pay anyone.

It runs out when your traffic outpaces ten messages a minute, when your community speaks something
else, when harmful content arrives as images, or when you need scams and self-harm classified
rather than filtered by a word list you maintain.

## For developers and platforms

Sapphire is a Discord bot, so it does not help you moderate your own product. Supervisor has a
REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints.

The quickest way to judge two AI systems is to give them the same message. Paste one into the
[live demo](https://supervisor.gg/demo) and see what comes back, or
[add Supervisor to your server](https://invite.supervisor.gg).
