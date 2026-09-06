---
title: "Best Discord bots for multilingual servers in 2026"
date: 2026-09-06
description: "Most Discord moderation only works in English. Discord's own word lists are English only and the leading free AI bot covers two languages. Here is what each tool actually supports."
---

# Best Discord bots for multilingual servers in 2026

**Bottom line:** if your community speaks more than one language, almost every moderation tool on
Discord covers you in exactly one of them. Discord's own preset word lists and spam filter are
**English only**, by Discord's own statement. Sapphire's AI fully supports **English and German**.
Every rule-based bot covers whatever languages you personally write word lists for. **Supervisor**
is the only tool here that applies the same 16 labels across **over 100 languages** without you
writing anything, which is why it leads this list.

We make Supervisor, so read the sourcing section before taking our word for the ranking. Every
language claim below is quoted from the vendor's own documentation.

## Language support at a glance

| Tool | Languages actually covered | How |
| --- | --- | --- |
| **Supervisor** | **Over 100** | Same 16 labels applied in all of them |
| Sapphire | English and German fully, 6 more partly | AI classification |
| Discord AutoMod | English for presets, any language you type | Word lists |
| Dyno | Whatever you write | Word lists |
| Carl-bot | Whatever you write | Word lists |
| MEE6 | Whatever you write | Word lists |
| Wick | Whatever you write | Blacklists |

## 1. Supervisor, the only one that does not ask you to write lists

Supervisor classifies across 16 labels, harassment, hate, threats, insults, scams, spam,
promotional content, sexual content in three degrees, self-harm, medical, violence, sensitive
content and illegal activity, and applies them in **over 100 languages**. There is no list to
translate, no per-language rule set, and no separate configuration for each community you host.

It also weighs conversation context when a message is ambiguous alone, and reads images and video
rather than only text, both of which matter more in a multilingual server where the same content
arrives in more forms.

The honest limits, because they apply here too: three slash commands, no bans or kicks, no raid
protection, no utility features, and £13.99 a month with no free tier for new accounts, just a
seven day trial and £0.25 of moderation on signup.

**Best for:** any server where your members do not all speak the same language.

## 2. Sapphire, the best free option, in two languages

Sapphire has genuine AI moderation and gives it away, which makes it the strongest free entry
anywhere in this category. For a multilingual server the detail that decides it is in Sapphire's
own documentation:

> AI Moderation currently fully supports English and German. Other languages are supported as well,
> but do not support categorization of inappropriate language.

So insults, threats and identity attacks are classified in English and German. The broader "other
offensive language" category extends to Italian, French, Russian, Portuguese, Spanish and Turkish.
Anything outside that is uncategorised.

Its 12 rule modules do work in any language, with word groups, regular expressions and word list
import, but those are lists you maintain per language like everyone else's.

**Best for:** English or German communities, and a solid free base for others.

## 3. Discord AutoMod, English presets and your own keywords

AutoMod is free, native, and the only tool that blocks a message before it posts, so it belongs in
every server regardless of language. Its language position is stated plainly in Discord's own
AutoMod FAQ:

> AutoMod can detect words and phrases in any language from your Custom Keyword Rules. However, the
> word lists of Commonly Flagged Words, as well as the Spam Content filter, are currently only
> available in English.

So the ready-made protection is English, and every other language is a **Custom Keywords Rule** you
write, inside a budget of six rules per server. Each holds up to 1,000 keywords and 10 regex
patterns, which is real capacity, but it is capacity you fill yourself in every language your
members use.

**Best for:** the free floor under everything else, in any language you are willing to maintain.

## 4. The rule engines: Dyno, Carl-bot, MEE6 and Wick

Grouped, because their answer to multilingual moderation is identical: whatever you write down.

- **Dyno** has the most filters, nineteen, and its Banned Words setting offers exact or wildcard
  matching. Neither reads meaning, so both need a separate list per language.
- **Carl-bot** has the best responses, eleven punishments that combine in one rule plus the `defer`
  moderator queue, but its bad words module is a censor list you fill.
- **MEE6** has the enforcement ladder and audit log, with Bad Words as its only content filter.
- **Wick** scores blacklisted words into its Heat system, again from lists you write.

None of these are worse tools for being English-agnostic. They simply put the translation work on
you, and that work never finishes, because it repeats for every language and every spelling
variation within it.

**Best for:** countable problems, in any language, if you have someone to maintain the lists.

## Why this is harder than it looks

Three things make multilingual moderation different from moderating in one language, and they are
why list-based tools struggle.

**Lists multiply.** One banned term becomes one list per language, and each list needs the
leetspeak, homoglyph and spacing variants too. Ten languages is not ten times the work, it is more.

**Evasion is easier.** A member can simply switch language to get past a filter tuned for another.
`fr33 n1tr0` is one problem, the same scam in Portuguese is a different one.

**Context is language-specific.** Whether "do it then" is a joke or a threat depends on the
conversation, and the conversation is in whichever language the channel speaks.

## Why trust this ranking

Every language claim above is quoted from the vendor's own documentation, read on 29 August 2026:
Discord's AutoMod FAQ, which Discord last updated on 15 June 2026, for the English-only statement;
docs.sapph.xyz for Sapphire's English and German support and the partial list; plus Dyno's,
Carl-bot's, MEE6's and Wick's automod documentation for their list-based mechanisms.

We make Supervisor and we have ranked it first, so the reasoning should be checkable rather than
asserted. The axis of this list is language coverage, Supervisor is the only entry that applies
classification beyond two languages without you writing lists, and every other entry's coverage is
quoted from its own docs above. On a different axis it would not lead: it cannot ban or kick, has
no raid protection and no utility features, and it costs money where two entries here are free.

On our own side, the figures come from our evaluation set rather than marketing. Supervisor's
models are retrained on real moderation feedback, the thumbs up and thumbs down votes people leave
on live flags in their own servers. The last full retrain moved average F1 across the 16 labels
from 0.794 to 0.941 on our internal evaluation set, with errors on harmless messages down 44
percent, and version 2.2 improved macro-F1 again across all three model tiers. The method and
per-label numbers are in the [2.1 release post](/blog/supervisor-2-1).

We have no customer reviews or ratings to show you, because we have not collected any.

## What we would run on a multilingual server

1. **Discord AutoMod**, always, for the English presets and any keywords you are willing to
   maintain, plus the block-before-posting nothing else has.
2. **Supervisor**, for classification that does not care which language a message is in.
3. **A rule engine or utility bot** alongside, since Supervisor does not ban, kick or do anything
   beyond moderation.

There is a wider [roundup of moderation bots](/blog/best-discord-moderation-bots-2026), an audit of
[which bots actually use AI moderation](/blog/discord-bots-with-ai-moderation), and a
[head-to-head with Sapphire](/blog/supervisor-vs-sapphire-moderation), the only other classifier
here.

The quickest test is your own content in a language your current filters do not cover. Paste one
into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
