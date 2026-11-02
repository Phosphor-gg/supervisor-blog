---
title: "Wick vs Discord AutoMod vs Supervisor: three layers compared"
date: 2026-08-29
description: "The perimeter, the words, and the meaning. Here is what Wick, Discord AutoMod and Supervisor each cover now that Supervisor has its own security suite, and which combination makes sense."
---

# Wick vs Discord AutoMod vs Supervisor: three layers compared

*Updated 2 November 2026: Supervisor now includes anti-nuke, anti-raid and the rest of a
[security suite](/blog/supervisor-security-suite), so the Supervisor parts of this post have been
rewritten.*

**Bottom line:** AutoMod is free and is the only one that blocks a message before it posts, so
keep it on. Wick defends the structure of the server against nukes and raids. Supervisor now does
most of that too, free, with panic mode, raid detection and backups in Premium, and it is the only
one of the three that reads what legitimate members are saying. For most servers AutoMod plus
Supervisor covers all three layers. Wick still adds an appeals site, member reports, a 35-event
logger, an AutoMod panel and a rescue key.

When this post was first written the three tools barely overlapped: Wick protected the structure,
AutoMod blocked words, and Supervisor read meaning. Supervisor's security suite changed that. What
follows is what each one covers now, so you can tell which layers you are missing.

## The short answer

- **You already have AutoMod.** It is free, native, and the only one of the three that blocks a
  message before it is posted. Turn it on regardless of what else you run.
- **Add Supervisor** for structural risk (raids, nukes, rogue or compromised admins, alt-account
  floods) and for what legitimate members are saying to each other.
- **Add Wick** if you want its appeals site, member reports, event logging or rescue key, or a
  security bot with a long track record.

## At a glance

| | Discord AutoMod | Wick | Supervisor |
| --- | --- | --- | --- |
| Protects against | Listed words and spam | Structural attacks and spam | Structural attacks, spam and harmful meaning |
| Blocks before posting | **Yes** | No | No |
| Anti-nuke | No | **Yes** | Yes, free |
| Raid protection | Mention raid detection | **Yes, panic mode** | Auto lockdown free; join raid detection and panic mode in Premium |
| Verification gate | No | **Yes** | Yes, free |
| Server backup and restore | No | **Yes** | Yes, Premium |
| Reads what a message means | No | No | **Yes** |
| Conversation context | No | No | **Yes** |
| Images and video | Not documented | Attachment heat only | **Yes** |
| Harm categories | 3 presets | None | **16 labels** |
| Languages | Lists English only | Blacklists you write | **100+** |
| Can ban or kick | Blocks interactions | **Yes** | Yes |
| Appeals, member reports, event logger | No | **Yes** | No |
| Cost | Free | Free, or $5 / month Premium | Security free; AI and Advanced Security £13.99 / month |

## Layer one: Discord AutoMod

Free, built in, available for all servers rather than Community servers only.

It gives you the **Commonly Flagged Words Rule** with three ready-made categories, Insults and
Slurs, Sexual Content and Severe Profanity, plus a **Custom Keywords Rule** where you write your
own, capped at six keyword rules per server, each holding up to 1,000 keywords and 10 regex
patterns. On the spam side there is a **Block Spam Content Rule** and a **Block Mention Spam
Rule** with a limit up to 50 mentions per message and optional mention raid detection.

**Its unique property is that it blocks before the message is posted.** No bot can do this. A bot
sees a message after it has appeared and then deletes it, which always leaves a window where
members can read it. If the requirement is that a specific word never reaches the channel,
AutoMod is the correct and only tool.

Its documented limits: three built-in categories, six keyword rules, and Discord's own statement
that "the word lists of Commonly Flagged Words, as well as the Spam Content filter, are currently
only available in English". No documented image or video filter, and every rule judges one message
alone.

## Layer two: Wick

Wick's own documentation calls anti-nuke "the critical feature that differentiates Wick from all
other Discord Bots", and it is aimed at a completely different threat model to the other two: not
the ordinary member, but the person who already has permissions.

**Anti-nuke** monitors channel and role creation and deletion, bans and kicks, and webhook
creation and deletion. Attempts to bypass quarantine, to add dangerous permissions to any role, or
to change the vanity URL trigger quarantine themselves.

**Panic mode** locks the server down on detecting a nuke, hands authority to the owner and Wick,
and deploys a separate isolated "miniWick" to retrieve pre-attack state so the main bot is not
overloaded.

**The restore system** reloads the latest backup and reverts deletions made during the attack.
Wick is candid that without Imaging enabled this "is a finicky process and lacks a lot of
information and the server may not be restored properly".

**Verification and quarantine** control who gets in and strip power from suspected bad actors.

Its automod is the **Heat system**, where every action adds heat that decays over time rather than
tripping a fixed threshold. Heat comes from message repetition, emojis, characters, new lines,
mentions with `@everyone` weighted heavily, attachments, inactivity in quiet channels, blacklisted
words and links, advertisement, NSFW websites and malicious websites including IP-grabbers and
keyloggers.

**Its limit is that heat measures behaviour, not content.** A single calm, correctly spelled
message sent at a normal pace generates almost no heat regardless of what it says.

## Layer three: Supervisor

This is ours, so weigh it accordingly.

Supervisor moderates with AI models that read what a message means rather than matching strings or
measuring rate. It classifies across 16 labels including harassment, hate, threats, insults,
scams, spam, sexual content, self-harm, violence and illegal activity. It weighs recent
conversation history when a message is ambiguous on its own, has implicit moderation for harm that
is implied rather than stated, moderates images and video by reading content, and works in over
100 languages without a word list per language. £13.99 a month, or about £4.99 on the three year
cycle, billed per account so one subscription covers every server.

Since 2 November 2026 it also has a security suite that uses no credits. Free for every server:
anti-nuke with per-minute and per-hour limits, quarantine hold, vanity URL protection and
dangerous permission monitoring; a join gate; Heat spam filtering; auto lockdown and `/lock`;
quarantine; verification by web, captcha or button; and `/ban`, `/kick`, `/timeout`, `/warn` and
other commands with numbered cases. Panic mode, join raid detection, backups and heat tuning are
in Advanced Security, included in Premium.

**Its limits against the other two.** It deletes after a message posts rather than blocking
before, so it does not replace AutoMod. Against Wick, it has no appeals site, no member reports,
no 35-event logger or message edit and delete logs, no AutoMod panel and no rescue key, its vanity
URL protection cannot set the old URL back, and its security suite is new where Wick's has years
behind it.

## Where the layers do not overlap

The useful way to see this is by asking what each one misses that another catches.

**A slur typed in plain English.** AutoMod blocks it before it posts. Wick's blacklist may add
heat. Supervisor would catch it but only after posting. **AutoMod wins.**

**A raid of fifty accounts created yesterday.** AutoMod has mention raid detection. Wick has panic
mode, verification and account age filtering. Supervisor has a join gate with account age
filtering and verification free, and join raid detection in Premium. **Wick and Supervisor both
cover it.**

**An admin deleting every channel.** Wick and Supervisor's anti-nuke both see it. AutoMod does not.

**A calmly written threat to one member, correctly spelled, no listed words.** AutoMod matches no
keyword and has no threat category. Wick's heat barely moves. **Supervisor is the only one that
reads it.**

**A scam in Portuguese.** AutoMod's presets are English only. Wick's blacklists are what you
wrote. Supervisor works across over 100 languages. **Supervisor wins.**

**Harm posted as an image.** Neither AutoMod nor Wick documents reading image content.
**Supervisor is the only one.**

**A member spelling around your filters with `fr33 n1tr0` or `h a t e`.** Both lists miss it.
**Supervisor reads the intent.**

## So which should you use?

**Every server:** AutoMod, on, configured. It costs nothing and it is the only thing that stops a
message appearing at all.

**Large public servers, or any server where a moderator account being compromised would be a
disaster:** you need anti-nuke. Supervisor's is free; Wick's is too, with a longer track record
and extras such as appeals and a rescue key. No amount of content moderation helps once someone
starts deleting channels.

**Servers where the members are legitimate and the problem is what they post:** add an AI layer.
That is the gap neither AutoMod nor Wick is designed to fill, and it is the one that produces the
harassment reports your moderators are actually handling.

**Budget order:** AutoMod first because it is free. Supervisor's security suite is also free, so
the base security layer costs nothing either way. The paid decision is whether you need AI
content moderation (Supervisor Premium, which also unlocks Advanced Security) or Wick's advanced
security tier.

The detail on each pairing is in
[Supervisor vs Discord AutoMod](/blog/supervisor-vs-discord-automod) and
[Supervisor vs Wick](/blog/supervisor-vs-wick-moderation), and there is a piece on whether
[AutoMod alone is enough](/blog/is-discord-automod-enough).

## Why trust this comparison

Everything above comes from the vendors' own material: Discord's auto moderation developer
documentation and its AutoMod FAQ, last updated 15 June 2026, and Wick's features page and command
reference on docs.wickbot.com. All read on 29 August 2026. Wick's public rating on top.gg was 84
out of 100 from 259 ratings that day, on top.gg's 0 to 100 scale.

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
100 languages, conversation context, and the only one that reads images and video. It now also
has a free security suite with anti-nuke, raid protection, bans and case tracking, but it has no
utility features such as levels, tickets or reaction roles, which is why most posts here recommend
running it alongside a general purpose bot rather than instead of one.

We have no customer reviews, ratings or testimonials to show you, because we have not collected
any. Judge it on your own content in the [live demo](https://supervisor.gg/demo) rather than on
our word for it.

## For developers and platforms

AutoMod is a Discord feature and Wick is a Discord bot, so neither exists outside Discord. If you
are moderating your own product, Supervisor has a REST API with SDKs for Python, JavaScript, Go,
Rust and Java, plus a Platform API for provisioning moderation to your own users. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and rates.

The quickest way to find which layer you are missing is to take a message your current setup let
through and paste it into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
