---
title: "Price cuts: Sentinel and Arbiter are now much cheaper, and image pricing got fair"
description: "Sentinel drops 33% and Arbiter 56% per byte, and images now bill at a flat rate instead of the model rate — a large image on Arbiter costs 9x less than it did last week."
date: 2026-07-13
---

# Cheaper credits, fairer image pricing

We are cutting moderation prices today — significantly. Same models, same accuracy, same credits you already have: they just go a lot further now.

## The new text rates

| Model | Before | Now | Change |
| --- | --- | --- | --- |
| Observer | 1 credit/byte | 1 credit/byte | — |
| Sentinel | 3 credits/byte | **2 credits/byte** | **33% cheaper** |
| Arbiter | 9 credits/byte | **4 credits/byte** | **56% cheaper** |

In money terms, moderating a kilobyte of text with Arbiter used to cost about £0.0123. It now costs about £0.0055. Sentinel drops from ~£0.0041 to ~£0.0027 per KB.

We can do this because the 2.0 models run meaningfully more efficiently than the pricing they launched under, and we would rather pass that on than pad a margin. Arbiter in particular was priced for caution while we learned its real-world costs — we have now learned them.

## Image pricing that matches what actually happens

Until now, an image was billed like text: every byte at your model's rate. That never quite made sense — a photo is mostly pixels, and pixels don't go through Sentinel or Arbiter. The expensive text models only run when there is actual text in the image for our OCR to read.

So that's exactly how billing works now:

- **Every image bills at a flat 1 credit per byte**, regardless of which model you use.
- **If OCR finds readable text in the image**, that extracted text is billed at your model's normal per-byte rate — because it genuinely ran through the text model.
- No readable text, no text-model charge. A meme with no caption costs the same on Arbiter as on Observer.

The difference is dramatic for high-tier plans: a 500 KB image on Arbiter used to cost about £6.14. Today it costs about £0.68 — and usually much less than that, because our Discord bot now downscales and compresses images before sending them, so a typical photo arrives well under 300 KB.

## Nothing to do on your end

The new rates are live for every request from today, on every path — the Discord bot, the API, the Platform API, and batch moderation. Cached results remain free, credit allowances are unchanged, and your existing balance simply buys more moderation than it did yesterday.

Full pricing details are in the [API reference](https://supervisor.gg/docs/api), and plans are on the [pricing page](https://supervisor.gg/pricing). Questions? [Come ask in the Discord](https://discord.supervisor.gg).
