---
title: "Discord bots that moderate images and video in 2026"
date: 2026-09-06
description: "Almost every Discord moderation tool counts attachments rather than looking at them. Here is what each one actually does with a picture, and the one option that reads the content."
---

# Discord bots that moderate images and video in 2026

**Bottom line:** almost nothing on Discord looks at what is inside a picture. Every major
moderation tool we audited handles images by **counting** them, rate limiting them, or filtering
their file type. Discord AutoMod documents no image or video rule at all. **Supervisor** is the
only option here that reads image content and analyses video frames, which is why it leads this
list, and it is worth knowing that the list is genuinely this short.

We make Supervisor, so the sourcing section at the end names every page this was read from. If you
know of a tool we have missed, that is a gap in our research rather than a claim that none exists.

## What each tool does with an image

| Tool | Images | Video | Mechanism |
| --- | --- | --- | --- |
| **Supervisor** | **Reads content** | **Reads changed frames** | AI classification |
| Discord AutoMod | Not documented | Not documented | No image rule type |
| Sapphire | Not documented | Not documented | Attachments appear in conditions as counts |
| Dyno | Image Spam | No | Counts multiple images within 10 seconds |
| Carl-bot | Attachment spam, `deletefiles` | No | Rate limits, plus a safe file type list |
| MEE6 | Not documented | Not documented | Plugin docs describe text checks only |
| Wick | Attachment heat | No | Attachments contribute to a rate score |

## 1. Supervisor, the only one reading content

Supervisor applies the same 16 labels to images that it applies to text, so a picture is classified
for harassment, hate, threats, sexual content in three degrees, violence, self-harm, scams and the
rest, rather than counted. If the image contains readable text, that text is extracted and
moderated too.

Video works by decoding the clip and analysing **only the frames where the picture actually
changes**, rather than every frame, so a sixty second clip costs a handful of frames instead of
hundreds. The response carries a `timestamp_ms` per analysed frame, so a flagged moment can be
located inside the clip rather than only reported for the video as a whole. The documented limits
are 10 MB, 60 seconds and 20 frames maximum, all enforced server-side.

Pricing for the media side, since it differs from text: images bill at a flat rate regardless of
model, with any OCR-extracted text billed at the model rate on top, and video frames bill at a
quarter of the image rate. Both are included in the £13.99 a month plan's £120 of monthly
moderation.

Honest limits: image moderation and video moderation are both toggles that are off until you turn
them on, video is off by default deliberately, attachments over 10 MB are skipped without being
downloaded, and clips longer than 60 seconds are rejected once decoded.

**Best for:** any server where harmful content arrives as a picture rather than a sentence.

## 2. Dyno, Carl-bot and Wick, the rate limiters

These three do something with images, and it is worth being precise that the something is not
looking at them.

**Dyno** has an **Image Spam** filter that detects multiple images sent at once or within a ten
second window. That is a genuine anti-flood tool and it does not examine any image.

**Carl-bot** has **attachment spam** rate limiting, plus a `deletefiles` toggle that deletes unsafe
file types, with the safe list spelled out in its docs: png, jpg, jpeg, gif, svg, bmp, tif, webp,
webm, mp4, mov, pdf, txt, mp3, flac and wav. File type is not content.

**Wick** folds attachments into its **Heat** system, where they contribute to an accumulating score
that decays over time. Again, the count and the pace, not the picture.

**Best for:** image floods and raids, which they handle well and which classification does not
solve.

## 3. Discord AutoMod, Sapphire and MEE6, text only

None of these three documents an image or video rule.

**Discord AutoMod** has five documented trigger types: keyword, keyword preset, spam, mention spam
and member profile. Every one operates on message text, keywords, mentions or profile text. If the
same content arrives as a picture, no rule has anything to match on. This is the notable one,
because AutoMod is otherwise the strongest free tool on Discord and the only one that blocks before
a message posts.

**Sapphire** has genuine AI moderation for text, insults, threats, identity attacks and other
offensive language, and its 12 rule modules take attachments as a condition, meaning a count within
a time frame. Its documentation does not describe reading image content.

**MEE6's** Moderator plugin documents eight automod checks, all of them string matches or counters
over message text.

We are phrasing all three as "not documented" rather than "cannot", because a feature could have
shipped since we read the docs, and we would rather be checkable than definitive.

**Best for:** everything they are actually built for, which is text.

## Why this gap exists, and why it matters

Text moderation is a solved shape: match strings, count events, or classify meaning. Image
moderation needs a vision model per image, which costs real compute per attachment, and video
multiplies that by frame count. So most bots reasonably decided not to.

The gap matters because the content that most often gets a server in trouble is increasingly not
text. A slur typed in a channel trips a word list. The same slur in a meme, a screenshot of a
threat, a scam QR code, or a clip does not touch any filter in the table above except ours.

If your moderators are removing images your automod never flagged, that is the gap, and no amount
of keyword tuning closes it.

## Why trust this list

Every entry was read from the vendor's own documentation on 29 August 2026: Discord's auto
moderation developer documentation for the five trigger types and the absence of an image rule;
docs.sapph.xyz for Sapphire's automod conditions; Dyno's automod documentation for Image Spam;
docs.carl.gg for attachment spam and the `deletefiles` safe list; wiki.mee6.xyz for MEE6's eight
checks; and docs.wickbot.com for Wick's Heat factors. Supervisor's limits and pricing come from our
own documentation and billing system.

We make Supervisor and it is first on this list, which on a list this short deserves a plain
justification rather than a claim. The axis here is whether a tool reads image or video content.
Everything else in the table is quoted doing something different with attachments, counting them,
rate limiting them or filtering file types, and those quotes are from their own docs. On any other
axis this ranking would change: Wick beats us on raids, Dyno on countable filters, Carl-bot on
responses, AutoMod on blocking before a message posts, and Sapphire on being free.

On our own side the numbers come from our evaluation set rather than marketing. Supervisor's models
are retrained on real moderation feedback, the thumbs up and thumbs down votes people leave on live
flags in their own servers. The last full retrain moved average F1 across the 16 labels from 0.794
to 0.941 on our internal evaluation set, with errors on harmless messages down 44 percent, and
version 2.2 improved macro-F1 again across all three model tiers. The method and per-label numbers
are in the [2.1 release post](/blog/supervisor-2-1).

We have no customer reviews or ratings to show you, because we have not collected any.

## What to run

For image floods, a rate limiter, and Dyno's Image Spam or Wick's Heat both do it free. For what is
actually in the picture, Supervisor is the only option in this comparison, and the honest way to
find out whether you need it is to test it on an image your current setup let through.

There is a wider [roundup of moderation bots](/blog/best-discord-moderation-bots-2026), an audit of
[which bots actually use AI moderation](/blog/discord-bots-with-ai-moderation), and the
[video moderation launch post](/blog/video-moderation) with the frame selection detail.

Paste an image or a clip into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
