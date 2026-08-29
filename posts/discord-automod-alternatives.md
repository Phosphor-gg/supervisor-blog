---
title: "Discord AutoMod alternatives: what to add when the built-in filter is not enough"
date: 2026-08-29
description: "Discord AutoMod is free, native and already on. The question is rarely what replaces it, but what to add. Here are the options and what each one covers that AutoMod does not."
---

# Discord AutoMod alternatives: what to add when the built-in filter is not enough

AutoMod is a Discord feature rather than a bot, so nothing genuinely replaces it. It is free, it
is in every server, and it can block a message before it is ever posted, which no third party can
do. Turning it off to run something else would be a strange trade.

So this post is about what to **add**. Here is what AutoMod covers, where it stops, and which
tools fill each gap.

## Why people look past AutoMod

Four limits, all documented by Discord and none of them faults.

**Three built-in categories.** The Commonly Flagged Words rule covers Insults and Slurs, Sexual
Content and Severe Profanity. There is no built-in category for harassment, threats, scams or
self-harm.

**Six custom keyword rules per server.** Each holds up to 1,000 keywords and 10 regex patterns,
but six rules is the ceiling.

**The ready-made lists and the spam filter are English only.** From Discord's own FAQ: "AutoMod
can detect words and phrases in any language from your Custom Keyword Rules. However, the word
lists of Commonly Flagged Words, as well as the Spam Content filter, are currently only available
in English."

**No documented image or video filter, and no conversation context.** Every documented rule type
works on message text, keywords, mentions or profile text, and judges one message on its own.

There is a longer piece on whether [AutoMod is enough for your server](/blog/is-discord-automod-enough)
if you want to work that out before adding anything.

## The options at a glance

| Tool | What it adds over AutoMod | Free tier | Best for |
| --- | --- | --- | --- |
| Sapphire | AI moderation, 12 rule modules, Join Guard, extends AutoMod itself | Yes, everything | The best free addition |
| Dyno | 19 rule filters, full ban and mute ladder | Yes, includes automod | Countable rules AutoMod lacks |
| Carl-bot | Flexible punishments, honeypot, moderator voting | Yes, includes automod | Humans in the loop |
| MEE6 | Warning escalation ladder, audit log, engagement features | Yes, includes automod | One bot for everything |
| Wick | Anti-nuke, panic mode, backups, verification | Yes | Structural threats |
| Supervisor | 16 labels, 100+ languages, images and video, context | No, 7 day trial | Contextual harm |

There is a wider roundup of the [best Discord moderation bots](/blog/best-discord-moderation-bots-2026)
if you want the category rather than AutoMod-shaped gaps.

## What to add, by the gap you have

### Sapphire, if you want the most for nothing

**The best free addition, and the only tool here that makes AutoMod itself better.** Sapphire
reads the AutoMod rules you have already configured under Server Settings and lets you attach
*additional* actions and conditions to them. You keep AutoMod's block-before-posting, which is its
best property, and gain a richer response on top. Nothing else in this list does that.

On top of the integration it brings genuine AI moderation for insults, threats, identity attacks
and offensive language, twelve condition-based rule modules with regex and word list import, and
Join Guard's seven account filters. All free, with paid add-ons only for custom branding from €5 a
month and higher limits.

The documented catch: it "only scans 10 messages per server per minute" without the paid Limit
Increase plan, and full AI language support is English and German.

**Best for:** almost every server that has outgrown AutoMod and does not want a bill.

### Dyno, if you want more countable rules

AutoMod gives you six keyword rules, mention limits and a spam filter. Dyno gives you nineteen
filters, including All Caps, Duplicate Text, Character Count, Emoji Spam, Image Spam, Links
Cooldown, Mentions Cooldown, Sticker Cooldown, Masked Links, Zalgo Text and Known Phishing Links.
It also brings the enforcement AutoMod lacks: Auto Mute, Auto Ban, Instant Mute and Instant Ban on
violation counts. All free.

**Best for:** servers whose problems are countable and who have run out of AutoMod's six rules.

### Carl-bot, if you want moderators involved

Brings a honeypot channel for catching spam bots, and the most flexible punishment set here:
delete, warn, tempmute, mute, timeout, kick, tempban, ban, message, DM and defer, combinable with
commas. Its `defer` action routes ambiguous cases to a channel where moderators decide with
reactions, which is a direct answer to AutoMod's all-or-nothing blocking.

**Best for:** servers that would rather route the grey areas to humans than tune a filter.

### MEE6, if you want an escalation ladder and an audit trail

Adds warning-count escalation, so ten warnings in fourteen days can be a permanent ban and two in
twenty four hours a one-day mute, plus around two dozen audit log event types. AutoMod can time
out and alert, but it does not keep an infraction history.

**Best for:** servers that need a documented enforcement record.

### Wick, if the threat is structural

AutoMod protects channels from messages. Wick protects the server from people with permissions:
anti-nuke monitoring of role and channel changes, panic mode lockdown, backups and restore,
quarantine and verification.

**Best for:** raids, nukes and compromised admin accounts, which AutoMod does not address.

## If the gap is what messages actually mean

This is the gap AutoMod's design cannot close, because three preset categories and a keyword list
are string matching. A targeted threat, a grooming attempt or a convincing scam is a single calm,
correctly spelled message containing no listed word.

Adding another rule engine does not close it either. Dyno's Banned Words and AutoMod's Custom
Keywords fail on the same message.

**Supervisor** is what we make, so weigh this accordingly. It reads what a message means: 16
labels including harassment, threats, scams, self-harm and illegal activity, conversation context
for ambiguous messages, implicit moderation for harm that is implied rather than stated, image and
video moderation, and over 100 languages rather than English-only lists. £13.99 a month, or about
£4.99 on the three year cycle, billed per account so one subscription covers every server you run.

Two honest caveats. **Supervisor deletes after a message posts**, where AutoMod blocks before, so
it does not replace AutoMod even on text. And it has no utility features at all, three slash
commands, no bans or kicks, and no raid protection.

**Best for:** running underneath AutoMod, catching what the presets and keyword rules cannot
express.

## Do you actually need to add anything?

Quite possibly not.

If your moderation problem is a list of words you never want posted, your community is mostly
English speaking, and nobody is systematically evading your filters, AutoMod covers it completely
and for free. Six keyword rules holding a thousand words each is a lot of rope. Spend an hour on
the Commonly Flagged Words exemptions and your custom rules before spending anything else.

Add something when the evidence says the gap is real: harmful messages your moderators catch that
AutoMod did not, content arriving in another language, harm arriving as images, or the same
content returning in new spellings faster than you can list them.

And whatever you add, leave AutoMod on. Free, native, and blocking before the message posts is a
combination nothing else offers.

## For developers and platforms

AutoMod is a Discord feature and does not exist outside Discord, so none of this applies if you are
moderating your own product. Supervisor has a REST API with SDKs for Python, JavaScript, Go, Rust
and Java, plus a Platform API for provisioning moderation to your own users. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and rates.

Whatever you add, test it on your own content rather than on a feature table. Paste a message that
gets past your keyword rules into the [live demo](https://supervisor.gg/demo) and see whether it
gets caught, or [add Supervisor to your server](https://invite.supervisor.gg).
