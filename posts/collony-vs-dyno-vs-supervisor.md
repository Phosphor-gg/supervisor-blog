---
title: "collony.ai vs Dyno vs Supervisor: rules, an AI manager, or AI moderation"
date: 2026-11-16
description: "Dyno enforces filters you configure, collony.ai enforces plain-language rules with an outside AI, and Supervisor classifies harm with its own models and adds a free security suite. An honest comparison for Discord servers."
---

# collony.ai vs Dyno vs Supervisor: rules, an AI manager, or AI moderation

**Bottom line:** **Dyno** is the best free rules bot, with nineteen automod filters. **collony.ai**
is the pick for Telegram, or if you want a bot that answers member questions. For a Discord server
that needs harmful messages caught and the server itself protected, **Supervisor** covers the
most: 16 AI labels in over 100 languages, images and video, a free security suite, and roughly
900,000 messages a month for £13.99.

collony.ai details come from its pricing page, docs and privacy policy, read on 16 November 2026.
Dyno details come from its own automod, moderation and pricing documentation, as covered in our
[MEE6 vs Dyno comparison](/blog/mee6-vs-dyno-vs-supervisor). We make Supervisor.

## At a glance

| | Dyno | collony.ai | Supervisor |
| --- | --- | --- | --- |
| How it moderates | 19 rule filters you configure | An AI reading your plain-language rules | **16 AI labels, purpose-built models** |
| Reads meaning | No | Yes | **Yes** |
| Known phishing links | Yes | Yes, link and scam sources | Yes, before the AI runs |
| Languages | Word lists you write | Replies in the member's language | **Over 100 moderated** |
| Images and video | Image spam counts only | Images; GIFs, video, stickers optional | **Images and video** |
| Anti-nuke, join gate, verification | No | No | **Yes, free** |
| Answers questions | No | **Yes, on Grow** | No |
| Telegram | No | **Yes** | No |
| AI runs on | No AI | Outside providers such as OpenAI | **Self-hosted models** |
| Entry price | Free, or $5.99 a month | $29 a month for 500 messages a day | **£13.99 a month, about 900,000 messages** |

## Dyno: rules you control

Dyno documents nineteen automod filters, from all caps and duplicate text to masked links, known
phishing links and zalgo text, each with its own action, all free. If your server's problems can
be counted or listed, Dyno has a filter for it.

collony.ai's own comparison page makes the fair point about this approach: every new scam pattern
needs a new rule. A calm message with no banned word and no link passes every filter.

## collony.ai: plain-language rules, read by an AI

collony.ai answers that problem by letting an AI enforce rules you write in a sentence, with
presets for phishing, wallet spam and DM solicitation, after Surge Guard, impersonation checks and
blocklists. Its impersonation protection, comparing members against your team's names and
pictures, is a real strength.

The trade-offs for Discord are volume, privacy and security. Protect checks 500 messages a day at
one credit per message. Moderation runs through outside AI providers, with OpenAI named in its
privacy policy, and messages are kept in a searchable history, with logs typically up to 90 days.
There is no anti-nuke, join gate or verification.

## Supervisor: AI moderation with security built in

Supervisor solves the same problem as collony.ai, reading meaning instead of matching rules, but
with its own classifiers trained for moderation rather than a general chatbot. It classifies 16
labels including harassment, hate, threats, scams, spam, sexual content and self-harm, in over 100
languages, with conversation context and image and video moderation. Message text is not stored.

It also does what neither Dyno nor collony.ai does: a **free security suite** with anti-nuke
watching the audit log, a join gate, Heat spam filtering, auto lockdown, quarantine, verification
and numbered moderation cases. Premium adds panic mode, join raid detection and backups.

Premium is £13.99 a month, £6.99 annually or £4.99 over three years, with £120 of moderation a
month, roughly 900,000 messages at 100 bytes on the Observer model, across every server you run.

## Which should you pick?

- **You want free, predictable filters and your problems are countable:** Dyno.
- **You are on Telegram, or want the bot to answer questions too:** collony.ai.
- **You want harmful messages caught by meaning and your server protected from nukes and raids:**
  Supervisor.

Dyno and Supervisor complement each other well, Dyno's filters for the countable rules and
Supervisor for everything they cannot see.

See what Supervisor catches that a filter misses in the [live demo](https://supervisor.gg/demo),
or [add Supervisor to your server](https://invite.supervisor.gg).

## Frequently asked questions

### Is Dyno or collony.ai better?

Dyno is the better free rules bot with nineteen filters. collony.ai reads meaning with an AI and supports Telegram, but starts at $29 a month for 500 messages a day.

### Does Dyno have anti-nuke?

No. Dyno is a general purpose bot with automod and moderation commands. Supervisor includes anti-nuke free.

### Can I use Dyno and Supervisor together?

Yes. Dyno's filters handle countable rules, and Supervisor catches what those filters cannot see and protects the server from nukes and raids.
