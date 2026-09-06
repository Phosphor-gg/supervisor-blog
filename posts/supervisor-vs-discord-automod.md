---
title: "Supervisor vs Discord AutoMod: AI moderation versus built-in keyword rules"
date: 2026-08-29
description: "Discord AutoMod is free, native and already in your server, with three ready-made word lists and six keyword rules. An honest comparison with Supervisor, including what AutoMod does better."
---

# Supervisor vs Discord AutoMod: AI moderation versus built-in keyword rules

**Bottom line:** keep AutoMod on, because it is free and it is the only tool that stops a
message before it is posted. Add Supervisor when the harm in your server is not a word you can
write down: AutoMod classifies three preset categories in English, Supervisor classifies 16
across more than 100 languages and reads images and video. Most servers should run both.

AutoMod is the moderation tool every Discord server already has. It is free, it is built into
the platform, there is no bot to invite, and it is almost always the first thing a server
turns on. If you are comparing it to a paid AI moderation bot, it is worth being precise
about what AutoMod does and does not do, because that is exactly where Supervisor takes a
different approach. This is an honest comparison, and the short version is that they are not
really the same kind of tool.

## Quick comparison

| | Discord AutoMod | Supervisor |
| --- | --- | --- |
| Mechanism | 3 preset word lists, 6 keyword rules | 16 AI labels |
| Blocks before posting | **Yes** | No, deletes after |
| Reads what a message means | No | **Yes** |
| Conversation context | No | **Yes** |
| Images and video | Not documented | **Yes** |
| Languages | Preset lists English only | **Over 100** |
| Ban or kick | Can block all interactions | No |
| Member profiles | **Yes** | No |
| Price | **Free** | £13.99 a month, per account |

## What Discord AutoMod actually is

AutoMod is a rule engine built into Discord itself, configured at Server Settings >
AutoMod, and it is available for all servers rather than Community servers only. It gives you
two groups of filters.

Keyword Filters:

- **Commonly Flagged Words Rule**, which switches on Discord's own ready-made word lists in
  three categories: **Insults and Slurs**, **Sexual Content** and **Severe Profanity**. You
  can exempt individual words you want to allow.
- **Custom Keywords Rule**, your own list of words and phrases. Discord's API documentation
  caps these at **six keyword rules per server**, each holding up to 1,000 keywords of 60
  characters or less, plus up to 10 regular expression patterns of 260 characters or less.
- Words can also be blocked in member usernames and nicknames.

Spam Filters:

- **Block Spam Content Rule**, aimed at "unsolicited messages or advertisements (free Nitro)"
  and invite spam. Discord is refreshingly straight about how it works: it is "powered by
  machine learning that is informed by spammy messages users have previously reported to us",
  and "this filter is not perfect so it might not catch everything that you may consider
  spam".
- **Block Mention Spam Rule**, with a limit you set up to a maximum of 50 mentions per
  message.

When a rule matches, AutoMod can block the message so it is never posted, log the content to
a channel you choose, time the member out, or block that member from using text, voice and
other interactions. Roles and channels can be exempted, and exempting a channel also exempts
its threads and text chat in voice.

This is genuinely good tooling, and one part of it is better than anything a bot can do.
AutoMod runs inside Discord, so blocking a message means the message never appears. A bot,
Supervisor included, sees a message after it has posted and then deletes it, which leaves a
window where people can read it. If your single most important requirement is that certain
words never reach the channel at all, AutoMod is the correct tool and no third party can
match it.

## Where a keyword list and three presets hit their ceiling

The limits are in the two mechanisms AutoMod has.

**A word list only catches what you wrote down, spelled the way you wrote it.** People who
want past a filter do not type the banned word. They type around it:

- Leetspeak and substitutions: `fr33 n1tr0`, `h8`, `5c4m`.
- Unicode look-alikes: Cyrillic or Greek letters that read identically to a person but are
  entirely different characters to a filter.
- Zero-width and invisible characters inserted mid-word.
- Spaced out or punctuated: `h a t e`, `s.c.a.m`.

Regex buys you some of this back, and ten patterns per rule is a real tool in skilled hands.
It is also a maintenance job that never ends, and a pattern loose enough to catch the
variations tends to be loose enough to catch innocent messages too.

**The built-in categories cover three things.** AutoMod's presets are profanity, sexual
content and slurs. That is the whole list. There is no built-in category for harassment, none
for threats, none for scams, none for self-harm, and none for spam beyond the generic spam
rule. If the content hurting your community is a targeted campaign against one member, a
convincing crypto scam, or someone in crisis, AutoMod has no category that describes it, so
you are back to writing keywords for it yourself.

**Every rule judges one message, or one profile, on its own.** Nothing in AutoMod's rule set
considers the conversation a message sits in. So the messages that need context are exactly
the ones it cannot weigh: "do it then", "nobody would miss you", "stop pretending", all
harmless in one thread and serious in another.

**The ready-made lists and the spam filter are English only.** This one comes straight from
Discord's own AutoMod FAQ: "AutoMod can detect words and phrases in any language from your
Custom Keyword Rules. However, the word lists of Commonly Flagged Words, as well as the Spam
Content filter, are currently only available in English." Your custom rules work in any
language, but you write and maintain those yourself, in every language your community speaks,
inside a budget of six rules.

**There is no documented image or video filter.** Every rule type Discord documents operates
on message text, keywords, mentions or profile text. If someone posts the same content as a
picture, the rules have nothing to match on.

## What Supervisor does differently

Supervisor moderates with purpose-built AI models instead of keyword lists and presets. It
reads what a message means, so the evasion tricks have nothing to trick and the single
harmful message is not invisible:

- It catches leetspeak, homoglyphs, invisible characters, and creative spelling, because it
  reads intent rather than exact strings.
- It has implicit moderation for harm that is implied rather than stated, and it can weigh
  recent conversation history when a message is ambiguous on its own.
- It classifies across 16 labels, covering the things no preset expresses: harassment, hate,
  threats, scams, spam, promotional content, sexual content, self-harm, illegal activity and
  more.
- It moderates images and video, reading what is in the picture rather than only what is in
  the text.
- It works in over 100 languages without a separate rule set per language, and without you
  writing a word list for each one.

You do not write or maintain any of it. There is no word list to keep current, no regex to
re-tune after every false positive, and no arms race to lose.

## What AutoMod does that Supervisor does not

Being straight about this matters more than winning the comparison, because you will find out
either way.

- **AutoMod blocks before posting. Supervisor deletes after.** Covered above, and it is the
  real one.
- **AutoMod scans member profiles.** Supervisor moderates messages, images and video. It does
  not scan profiles.
- **AutoMod has mention raid detection.** Supervisor has no raid protection, no anti-nuke, no
  verification gate and no captcha. If raids are your problem, you need something else, and
  there are bots that specialise in exactly that.
- **AutoMod supports full regular expressions.** Supervisor's word filter does
  case-insensitive whole-word matching with a `*` wildcard for partial matches, which is
  simpler on purpose but genuinely less powerful.
- **AutoMod can block a member from text, voice and other interactions.** Supervisor's
  actions are Delete, Timeout and Warn. It cannot ban or kick.
- **AutoMod is free.** Supervisor is £13.99 a month, or about £4.99 a month on the three year
  cycle, with a seven day free trial and £0.25 of moderation free on signup so you can watch
  it work before deciding anything.

## Presets are for words. Supervisor is for meaning.

This is the honest way to frame it. AutoMod's keyword rules and presets are the right tool
for the things you can write down: slurs you never want in the channel, invite spam, mention
floods, a profile naming something you do not allow. Those are string and volume problems,
and AutoMod solves them for free, inside the platform, before the message posts.

They do nothing about the quietly written message that contains no listed word and trips no
counter, because that message is not a string problem. Catching a slur and catching a
grooming attempt are different problems, and you can run both tools at once.

## Why trust this comparison

Everything above about AutoMod comes from Discord's own material: the auto moderation section of
the developer documentation for the rule types, action types and per-guild caps, and the AutoMod
FAQ, which Discord last updated on 15 June 2026, for the admin-facing rule names and the language
support quote. Both read on 29 August 2026.

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

If you are moderating your own product rather than a Discord server, AutoMod is not available
to you at all, since it is a Discord feature. Supervisor has a REST API with SDKs for Python,
JavaScript, Go, Rust and Java, and a Platform API for provisioning moderation to your own
users. The [API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and
the current rates.

## So which should you use?

They solve different jobs, and for most servers the answer is both.

Leave AutoMod on. It costs nothing, it runs inside Discord, and for the exact strings you
never want posted it does something no bot can do. Set up your keyword rules, turn on the
presets, cap your mentions, and let it handle the string and volume problems.

Reach for Supervisor when the content hurting your community is not a string: the harassment
spelled to dodge the word list, the scams, the implied threats, the harmful images and video,
the abuse in languages your keywords do not cover, and the single calmly written message that
matches nothing. Supervisor is the AI moderation layer that reads meaning, and it sits
alongside your existing setup rather than replacing your utility bot.

Want to see the difference on your own content? Paste a message that gets past a keyword
filter into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
