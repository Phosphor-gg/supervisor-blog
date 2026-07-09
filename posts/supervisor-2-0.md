---
title: "Supervisor 2.0: smarter models, image moderation, and a lot more"
description: "Our biggest release yet. New 2.0 models with implicit moderation, 16 content labels, image moderation, a full Platform API, and the foundations for video moderation."
date: 2026-07-09
---

# Supervisor 2.0

Since April we have rebuilt almost every part of Supervisor, from the models that read your messages to the ways you can plug moderation into your own product. This is the biggest release since we launched, so we are calling it what it is: Supervisor 2.0.

Here is everything that has landed.

## New 2.0 models: Observer, Sentinel, and Arbiter

The heart of Supervisor is three moderation models, and all three have been retrained from the ground up for 2.0:

- **Observer** is fast and lightweight, built for high-volume real-time filtering.
- **Sentinel** adds sharper judgement for the cases Observer flags as borderline.
- **Arbiter** is our most capable model. In our own testing it holds a false positive rate below one percent, so it catches harmful content without punishing normal conversation.

Every 2.0 model is trained on significantly more data than before, which means better accuracy, fewer false positives, and stronger performance on the subtle cases that keyword filters and older classifiers miss. Each response now carries a model version, so you always know exactly what judged your content.

You do not have to pick a model by hand. Set the model to **Auto** and Supervisor routes each request to the right tier for you, escalating to a stronger model only when a message is genuinely ambiguous.

## Moderation that reads intent, not just words

The headline capability in 2.0 is **implicit moderation**. Most moderation tools only catch harm that is stated outright. Supervisor now understands harm that is implied: the message that is technically clean word by word but is clearly a threat, an insult, or a scam in context. Implicit detection runs alongside the standard labels and surfaces separately, so you can see both what a message says and what it means.

Paired with our context-aware analysis, which can check recent conversation history when a message is ambiguous on its own, this is what lets Supervisor catch the things that slip past everyone else.

## 16 content labels

We expanded our taxonomy to 16 distinct labels, giving you far more precise control over what gets flagged and why:

profanity, toxicity, harassment, hate, insult, sexual, sexual/unlawful, sexual/explicit, sensitive, violence, self-harm, medical, spam, promotional, scam, and illegal.

You choose which labels matter for your community, and Supervisor reports exactly which ones a message triggered rather than a single pass or fail.

## Image moderation

Supervisor now moderates images, not just text. Send an image and our vision-capable models analyze it directly against the same labels, so harmful pictures are caught the same way harmful words are. On Discord this happens automatically for attachments, and through the API you can moderate images alongside text in a single request. Batch moderation lets you check many images at once for high-volume workloads.

## Video moderation is next

The foundations for **video moderation** are now in place, and it is the next thing we are shipping. It will arrive in our next update, extending the same intent-aware analysis to video content. If moving imagery is part of what your community shares, this one is for you.

## Over 100 languages

All of this works in over 100 languages. Supervisor catches harmful content regardless of the language it is written in, including attempts to dodge filters with Unicode tricks, leetspeak, and creative spelling.

## A full Platform API

Supervisor is no longer just a Discord bot. With the new **Platform API**, you can build moderation directly into your own product and run it on behalf of your users. You get OAuth-style client credentials, a consent flow so users authorize your platform, per-user provisioning, and optional revenue-share billing so you can resell plans and credits to your own users.

To make integration painless, we shipped official SDKs for **Python, JavaScript, Go, Rust, and Java**, each with the full platform surface built in. The [Platform API documentation](https://supervisor.gg/docs/platform-api) has everything you need to get started.

## A better Discord bot

The Discord side got a lot of love too:

- **Verification**: gate your server behind a quick verification step, with automatic role assignment and optional vote-based verification.
- **Username moderation**: catch harmful usernames on join, not just messages.
- **Link filtering**: block unwanted links, invites, and media before they even reach the AI, with your own allow and block lists.
- **Image moderation** on attachments, with staff alerts when something is flagged.
- **Mental health support**: when self-harm content is detected, warnings now include support resources rather than just a removal.

## Verified: a lifetime tier built to keep bots out

Free tiers are a magnet for abuse. When credits are free, people spin up throwaway accounts and bots to farm them, which is unfair to real communities and expensive to absorb.

Verified is our answer. It is a one-time, lifetime purchase that proves there is a real person behind an account. Because it takes a genuine payment rather than a disposable signup, it raises the barrier for bots and automated abuse in a way a free tier never can.

In return, Verified boosts your monthly credit allowance to £5 of credits every month, for life, from a single payment. No subscription and no renewals. If you ever move to a paid plan, that plan takes over while it is active, and your Verified allowance is always there to fall back on.

## And a lot more

Alongside the big features, 2.0 brings a redesigned dashboard, a live [demo](https://supervisor.gg/demo), refreshed [documentation](https://supervisor.gg/docs), a [moderation glossary](https://supervisor.gg/glossary), and this blog.

## Try it

The best way to understand Supervisor 2.0 is to see it work. Paste a message into the [live demo](https://supervisor.gg/demo), or [get started for free](https://supervisor.gg) and add it to your own community in a couple of minutes.

As always, you can [join our Discord](https://discord.supervisor.gg) to follow what we are building next. Video moderation is coming soon.
