---
title: "Underrated Discord bots and features in 2026"
date: 2026-09-06
description: "The best thing in Discord moderation right now is free and most servers have never heard of it. Six tools, features and gaps that deserve more attention than they get, with the evidence for each."
---

# Underrated Discord bots and features in 2026

**Bottom line:** the most underrated thing in Discord moderation is **Sapphire**, which gives away
genuine AI moderation for free and holds the highest public rating of any bot we checked, 96 out of
100 on top.gg. Close behind are three features hiding inside bots people already run,
**Carl-bot's `defer`**, **Wick's Heat system** and **Discord AutoMod's regex support**, plus one
capability gap almost nobody has measured: **nothing on Discord reads what is inside a picture**
except Supervisor.

"Underrated" is a subjective word, so each entry below says what the evidence actually is and where
it came from. We make a competing paid product, and five of the six entries are not ours.

## The list at a glance

| What | Where it lives | Why it is underrated |
| --- | --- | --- |
| Sapphire | Free bot at sapph.xyz | Free AI moderation, highest rating we found |
| `defer` | Carl-bot premium | The only human-in-the-loop moderation queue |
| Heat system | Wick, free tier | Adaptive spam scoring, not fixed thresholds |
| AutoMod regex | Discord, free | 10 regex patterns per rule, already in your server |
| AutoMod integration | Sapphire, free | Extends AutoMod rather than duplicating it |
| Image and video moderation | Supervisor, paid | Nobody else reads what is in a picture |

## 1. Sapphire, the free bot with real AI moderation

Most servers have never heard of it, and it is the most capable free tool in this category.

Sapphire's Auto Moderation module includes genuine AI classification, flagging **insults, threats,
identity attacks and other offensive language**, with sensitivity set per category. Of the seven
moderation tools we audited, only two classify what a message means, and Sapphire is the free one.
On top of that it gives away reaction roles, join roles, welcome messages, social notifications,
moderation cases and logging with over 80 log types.

The evidence for "underrated" rather than just "good": on top.gg's 0 to 100 scale, checked 29
August 2026, Sapphire scored **96 from 215 ratings**. That is the highest of the four bots we
checked that publish a rating, above Dyno's 87 from 373, Wick's 84 from 259 and Carl-bot's 62 from
594. It is also the smallest sample of the four, which is rather the point: a very high score on a
comparatively small number of ratings is what an under-discovered product looks like.

Two limits it documents honestly: the AI "only scans 10 messages per server per minute" without its
paid Limit Increase plan, and "AI Moderation currently fully supports English and German".

One disambiguation, because it costs people time: the bot is **sapph.xyz**. The `sapphirejs.dev`
that often outranks it is an unrelated framework for building Discord bots.

## 2. Carl-bot's `defer`, the only human-in-the-loop queue

Every automod in this category makes the same forced choice: act automatically and accept false
positives, or set thresholds loose and miss things. Carl-bot has a third option and almost nobody
talks about it.

The **`defer`** punishment does not punish. It sends the offending context to a drama channel where
your moderators decide with reactions. Ambiguity becomes a queue for humans instead of a guess by a
bot.

It sits alongside a punishment set nothing else matches, delete, warn, tempmute, mute, timeout,
kick, tempban, ban, message and DM, which **combine with commas**, so `delete, tempmute 20m` is one
rule with durations written as `3h42m`.

Why it is underrated: Carl-bot is famous for reaction roles, so its moderation gets overlooked, and
`defer` needs premium, which puts it behind a wall most people never look over. It is the most
thoughtful moderation design in this whole category.

## 3. Wick's Heat system, adaptive instead of fixed

Nearly every anti-spam feature on Discord is a fixed threshold: five messages in five seconds, ten
mentions in one message. Tuned tight it punishes enthusiasm, tuned loose it misses the raid.

Wick does it differently. Every action adds **heat** that decays over time, and enough accumulated
heat triggers a punishment. Wick describes it as "an adaptive algorithm that adjusts to the user's
current actions and scales properly with an increase in members and their activity", with the
analogy of a machine gun that overheats then cools. Heat comes from message repetition, emojis,
characters, new lines, mentions with `@everyone` weighted heavily, attachments, inactivity in quiet
channels, blacklisted words and links, advertisement, and NSFW or malicious sites including
IP-grabbers and keyloggers. Auto Timeouts then escalate with a **Multiplier** so raiders cannot
simply wait out a fixed cap.

Why it is underrated: Wick is known as the anti-nuke bot, so its spam handling gets ignored, and
the heat model is mechanically better than a counter for exactly the case where counters annoy your
regulars. It is on the free tier.

## 4. Discord AutoMod's regex, already in your server

AutoMod is famous for its three ready-made word lists and dismissed as basic. The part people skip
is that each **Custom Keywords Rule** holds up to **10 regular expression patterns of 260
characters**, alongside up to 1,000 keywords, and you get six such rules per server.

That is a genuine pattern-matching engine, free, native, and applied **before a message is posted**
rather than after. No bot can block a message; AutoMod can.

Why it is underrated: the regex support is documented in Discord's developer documentation rather
than shouted about in the settings UI, so most admins never find it. If you know regex, six rules
with ten patterns each is far more rope than "three preset lists" suggests.

Worth knowing the limits too: the preset lists and the spam filter are English only, and no
documented rule type reads images or video.

## 5. Sapphire's AutoMod integration, the best idea nobody copied

This one deserves its own entry because of what it implies rather than what it does.

Every other bot in this category either ignores Discord AutoMod or quietly duplicates it. Sapphire
reads the AutoMod rules you have already configured under Server Settings and lets you attach
**additional actions and conditions** to them.

So you keep AutoMod's block-before-posting, which is the one thing no third party can replicate,
and gain a richer response on top of it. It is free, and as far as our audit found, unique.

Why it is underrated: it requires understanding that AutoMod and a bot are complementary rather
than competing, which is not how this category usually markets itself.

## 6. Image and video moderation, the gap nobody notices

This is ours, so treat it accordingly, and note carefully what the claim is. We are not saying
Supervisor is underrated, because it is new and we have no ratings to point at. The **underrated
thing** is the gap it fills, which almost nobody realises is open.

Audit what the tools in your server do with a picture. Dyno's Image Spam counts multiple images
within ten seconds. Carl-bot rate limits attachments and filters file types, with a safe list of
png, jpg, gif and the rest. Wick folds attachments into its Heat score. Discord AutoMod documents no
image rule type at all, and neither Sapphire's nor MEE6's documentation describes reading image
content.

So every one of them counts pictures, and none of them looks at one. A slur typed in chat trips a
word list; a screenshot of the same slur, a meme, a scam QR code or a clip touches nothing.

Supervisor applies the same 16 labels to images, extracts and moderates any readable text in them,
and for video decodes the clip and analyses only the frames where the picture actually changes,
returning a timestamp for each flagged moment. It is the only tool in this comparison that does,
and it costs money where five entries above are free.

Why it is underrated: it is a gap most servers have never measured. Your moderators are probably
removing images your automod never flagged, and that never shows up as a filter failure because no
filter was ever looking.

## What we deliberately left off

**MEE6 AI.** MEE6 markets an AI product separately from its Moderator plugin. We did not read its
documentation, so we cannot tell you whether it belongs on a list like this.

## Why trust this list

Every claim above was read from the vendor's own documentation on 29 August 2026: docs.sapph.xyz
and sapph.xyz for Sapphire's AI categories, scan limit and language support, quoted directly;
docs.carl.gg for Carl-bot's punishments and `defer`; docs.wickbot.com for the Heat model and its
quotes; and Discord's auto moderation developer documentation for the regex and keyword limits. The
ratings came from each bot's top.gg listing on the same date, on top.gg's 0 to 100 scale, quoted
with their sample sizes.

We make Supervisor, a paid competitor to several of the tools praised above, and five of the six
entries are not ours. The one that is makes a claim about a capability gap rather than about our
reputation, and every tool's handling of images is quoted from its own documentation so you can
check it.

We have no customer reviews or ratings to show you, because we have not collected any.

## What to do with this

If you run a Discord server and have not looked at any of the first five, the cheapest experiments
in order are: turn on AutoMod's regex if you know regex, add Sapphire, and add Wick if raids are a
real risk. All free. Then check what your automod has been doing with images, which is the sixth.

There is a fuller [roundup of moderation bots](/blog/best-discord-moderation-bots-2026) if you want
them ranked, an audit of
[which bots actually use AI moderation](/blog/discord-bots-with-ai-moderation), and a
[pricing comparison](/blog/discord-bot-pricing-compared) covering what each paid tier really buys.

If you get through all of that and messages are still getting past your filters, that is the gap we
built for. Paste one into the [live demo](https://supervisor.gg/demo) and see whether it gets
caught, or [add Supervisor to your server](https://invite.supervisor.gg).
