---
title: "Supervisor vs Carl-bot: AI moderation versus keyword automod"
date: 2026-07-16
description: "Carl-bot is a great all-round Discord bot, but its moderation is rule-based: keywords, regex, spam controls, and a honeypot channel. Here is an honest comparison with Supervisor, an AI moderation bot, so you can pick the right one, or run both."
---

# Supervisor vs Carl-bot: AI moderation versus keyword automod

Carl-bot is one of the most widely used Discord bots, and deservedly so. Reaction roles, logging, custom commands, tags, and a capable automod, all in one place. If you are here specifically about moderation, though, it is worth being clear about what Carl-bot's automod does and does not do, because that is exactly where Supervisor takes a different approach. This is an honest comparison, and the short version is that they are not really the same kind of tool.

## What Carl-bot's moderation actually is

Carl-bot's automod is rule-based. You give it rules, and it matches messages against those rules:

- Banned words and phrases, including regex and wildcard patterns.
- Invite and link filtering.
- Spam controls: mention spam, link spam, invite spam, excessive caps, and emoji spam, usually with a rate limit you set.
- Auto-warn or auto-mute when someone trips a rule.
- A honeypot channel: a decoy channel real members have no reason to post in, so anything that posts there is almost certainly a spam bot and gets kicked or banned automatically.
- Role and channel whitelisting so trusted people and channels are ignored.

This is genuinely useful, and the honeypot in particular is a smart, low-effort way to catch spam bots. For exact, predictable things (a specific banned word, an invite link, a bot flooding a channel), rules work well.

## Where keyword and regex moderation hits its ceiling

The catch with keywords and regex is that they only catch what you thought to write down, exactly as it was written. People who want to get past a filter do not type the banned word. They type around it:

- Leetspeak and substitutions: `fr33 n1tr0`, `h8`, `5c4m`.
- Unicode look-alikes: Cyrillic or Greek letters that read identically to a person but are different characters to a regex.
- Zero-width and invisible characters inserted mid-word.
- Spaced out or punctuated: `h a t e`, `s.c.a.m`.
- Implied harm with no banned word at all: a threat or an insult that is obvious in context but uses no word any list would contain.

Every one of those defeats a keyword or regex rule the moment it ships, and you end up in an arms race, adding pattern after pattern while the actual harmful content keeps getting through in new spellings. Rules also do not read tone, do not understand context, and need a fresh set for every language your community speaks.

## What Supervisor does differently

Supervisor moderates with purpose-built AI models instead of rules. It reads what a message means, not the exact characters, so the evasion tricks above have nothing to trick:

- It catches leetspeak, homoglyphs, invisible characters, and creative spelling, because it reads intent rather than strings.
- It has implicit moderation for harm that is implied rather than stated, and it can weigh recent conversation history when a message is ambiguous on its own.
- It classifies across 16 labels, including things a keyword list has no real way to handle: harassment, hate, threats, scams, spam, sexual content, self-harm, and more.
- It moderates images, not just text.
- It works in over 100 languages without a separate rule set per language.

You do not write or maintain any of it. There is no word list to keep current and no arms race to lose.

## Honeypot is for bots. Supervisor is for people.

This is the honest way to frame it. Carl-bot's honeypot is a good tool for catching spam bots, because bots behave predictably and a decoy channel exploits that. It does nothing for a real member posting harassment, a scam, hate, or a threat, because that person is never going to wander into a decoy channel. Catching spam bots and catching harmful human behaviour are different problems, and you can run a honeypot and Supervisor at the same time.

## So which should you use?

They solve different jobs, and for a lot of servers the answer is both.

Use Carl-bot for what it is great at: reaction roles, logging, custom commands, tags, and rule-based automod for the exact stuff and the spam bots. If that covers your moderation needs, Carl-bot on its own is fine and free to start.

Reach for Supervisor when rule-based automod is not catching the content that actually hurts your community: the harassment spelled to dodge the filter, the scams, the implied threats, the harmful images, the abuse in languages your rules do not cover. Supervisor is the AI moderation layer that reads meaning, and it sits alongside your existing setup rather than replacing your utility bot.

Want to see the difference on your own content? Paste a message that gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it get caught, or [add Supervisor to your server](https://invite.supervisor.gg).
