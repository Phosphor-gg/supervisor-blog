---
title: "Wick vs Discord AutoMod vs Supervisor: three layers, not three choices"
date: 2026-08-29
description: "These three protect against different things: the perimeter, the words, and the meaning. Here is what each one actually covers, and why the answer is usually all three rather than one."
---

# Wick vs Discord AutoMod vs Supervisor: three layers, not three choices

Most comparison posts end with a recommendation. This one ends with three, because these tools do
not overlap enough to compete. Wick protects the structure of your server, Discord AutoMod blocks
words before they post, and Supervisor reads what messages mean.

You can run all three at once, and for a large public server that is the correct answer rather
than a hedge. What follows is what each one actually covers, so you can tell which layers you are
missing.

Everything about Wick and AutoMod comes from their own documentation, checked on 29 August 2026.
We make Supervisor, so treat that section accordingly.

## The short answer

- **You already have AutoMod.** It is free, native, and the only one of the three that blocks a
  message before it is posted. Turn it on regardless of what else you run.
- **Add Wick** if your risk is structural: raids, nukes, rogue or compromised admins, alt-account
  floods.
- **Add Supervisor** if your risk is what legitimate members are saying to each other.

## At a glance

| | Discord AutoMod | Wick | Supervisor |
| --- | --- | --- | --- |
| Protects against | Listed words and spam | Structural attacks | Harmful meaning |
| Blocks before posting | **Yes** | No | No |
| Anti-nuke | No | **Yes** | No |
| Raid protection | Mention raid detection | **Yes, panic mode** | No |
| Verification gate | No | **Yes** | No |
| Server backup and restore | No | **Yes** | No |
| Reads what a message means | No | No | **Yes** |
| Conversation context | No | No | **Yes** |
| Images and video | Not documented | Attachment heat only | **Yes** |
| Harm categories | 3 presets | None | **16 labels** |
| Languages | Lists English only | Blacklists you write | **100+** |
| Can ban or kick | Blocks interactions | **Yes** | No |
| Cost | Free | $5 / month Premium | £13.99 / month |

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

**Its limits against the other two are substantial.** It deletes after a message posts rather than
blocking before, so it does not replace AutoMod. It has no anti-nuke, no anti-raid, no panic mode,
no backups, no restore, no quarantine and no verification, so it does not replace Wick. Its
actions are Delete, Timeout and Warn, so it cannot ban or kick, where AutoMod can block a member's
interactions entirely and Wick can ban.

## Where the layers do not overlap

The useful way to see this is by asking what each one misses that another catches.

**A slur typed in plain English.** AutoMod blocks it before it posts. Wick's blacklist may add
heat. Supervisor would catch it but only after posting. **AutoMod wins.**

**A raid of fifty accounts created yesterday.** AutoMod has mention raid detection. Wick has panic
mode, verification and account age filtering. Supervisor has nothing. **Wick wins.**

**An admin deleting every channel.** Only Wick sees it at all.

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
disaster:** add Wick. Nothing else in this comparison protects the structure of the server, and no
amount of content moderation helps once someone starts deleting channels.

**Servers where the members are legitimate and the problem is what they post:** add an AI layer.
That is the gap neither of the other two is designed to fill, and it is the one that produces the
harassment reports your moderators are actually handling.

**Budget order if you cannot do all three:** AutoMod first because it is free. Then whichever of
your two remaining risks is real, which is a question about your server rather than about the
tools. If you have never been raided but your mod team spends its time on harassment reports, the
content layer matters more. If you run a large server with many staff roles, the security layer
does.

The detail on each pairing is in
[Supervisor vs Discord AutoMod](/blog/supervisor-vs-discord-automod) and
[Supervisor vs Wick](/blog/supervisor-vs-wick-moderation), and there is a piece on whether
[AutoMod alone is enough](/blog/is-discord-automod-enough).

## For developers and platforms

AutoMod is a Discord feature and Wick is a Discord bot, so neither exists outside Discord. If you
are moderating your own product, Supervisor has a REST API with SDKs for Python, JavaScript, Go,
Rust and Java, plus a Platform API for provisioning moderation to your own users. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and rates.

The quickest way to find which layer you are missing is to take a message your current setup let
through and paste it into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
