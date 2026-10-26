---
title: "How to detect toxicity in JavaScript and TypeScript"
date: 2026-10-26
description: "Detect toxic, abusive and spammy text in Node, Bun, Deno or the browser with the Supervisor SDK: install from GitHub, moderate text, scope labels, use context and batches, handle errors."
---

# How to detect toxicity in JavaScript and TypeScript

**Bottom line:** install the Supervisor SDK from GitHub, create a `SupervisorClient`, and `await client.moderate({ text })`. You get `flagged` and `labels` back. The client has no dependencies and works in Node, Bun, Deno and the browser (but keep your API key on a server).

## The problem

Client-side word filters are trivial to bypass and visible to anyone who opens dev tools. Toxicity detection belongs on your server, behind your own API route, where you can keep the key private and decide what happens to a flagged message.

## Install

The package is installed from GitHub, not npm:

```bash
npm install github:Phosphor-gg/supervisor-sdk-js
```

It builds on install, so it works with npm, pnpm and yarn straight from GitHub, and ships with full type definitions. Create a key at **Dashboard > API Keys** after signing up at [supervisor.gg](https://supervisor.gg). Keys look like `sk_prod_...`.

## Your first check

```typescript
import { SupervisorClient } from "supervisor-sdk";

const client = new SupervisorClient({ apiKey: process.env.SUPERVISOR_API_KEY! });

const result = await client.moderate({ text: "text to check" });
console.log(result.flagged, result.labels);
```

The result is a `ModerationResponse` with `flagged`, `labels`, `implicit_labels`, `model_version`, and optional `needs_context` and `context_labels`. Content that triggers returns labels such as `["toxicity", "insult"]`.

## Labels and models

`toxicity` is one of 16 labels: profanity, toxicity, harassment, hate, insult, sexual, sexual/unlawful, sexual/explicit, sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. Scope a check with `enabled_labels`, and choose a model:

```typescript
import { ModerationLabel, ModerationModel } from "supervisor-sdk";

const result = await client.moderate({
  text: "text to check",
  model: ModerationModel.Sentinel,
  enabled_labels: [
    ModerationLabel.Toxicity,
    ModerationLabel.Insult,
    ModerationLabel.Harassment,
    ModerationLabel.Hate,
  ],
});
```

Observer costs roughly £0.0014 per KB of text, Sentinel (the default) roughly £0.0027 and Arbiter roughly £0.0055.

## An Express route

```typescript
import express from "express";
import { SupervisorClient, SupervisorError } from "supervisor-sdk";

const client = new SupervisorClient({ apiKey: process.env.SUPERVISOR_API_KEY! });
const app = express();
app.use(express.json());

app.post("/comments", async (req, res) => {
  try {
    const result = await client.moderate({ text: req.body.text });
    if (result.flagged) {
      return res.status(422).json({ error: "rejected", labels: result.labels });
    }
    // ...save the comment
    return res.status(201).json({ ok: true });
  } catch (e) {
    if (e instanceof SupervisorError && e.statusCode === 402) {
      console.error("Supervisor credits exhausted");
    }
    return res.status(503).json({ error: "moderation unavailable" });
  }
});

app.listen(3000);
```

Whether you answer `503` (fail closed, as here) or save the comment for later review is your policy decision.

## Short replies: use context

```typescript
const first = await client.moderate({ text: "stop it", include_context: true });
// { flagged: false, needs_context: true, context_labels: ["harassment"] }
if (!first.flagged && first.needs_context) {
  const full = await client.moderate({ text: [...history, "stop it"].join("\n") });
}
```

If `needs_context` is true, send the history in a follow-up request. Context-aware moderation is included with Premium.

## Batches

```typescript
const results = await client.moderateBatch({
  texts: ["First message", "Second message", "Third message"],
  model: ModerationModel.Observer,
});
results.forEach((r, i) => console.log(i, r.flagged, r.labels));
```

`moderateBatch` returns one `ModerationResponse` per text. Batches of two or more are billed at 50% off. The docs state no maximum batch size, so chunk large jobs.

## Errors

The SDK exports `SupervisorError` and three subclasses, all with a `statusCode`:

| Class | Status |
| --- | --- |
| `AuthenticationError` | 401 |
| `RateLimitError` | 429 |
| `ValidationError` | 400 or 422 |
| `SupervisorError` | anything else, including `402` |

A `402` means credits are exhausted until the monthly reset or an upgrade. Check `e.statusCode === 402` on the base class.

## Other checks

- Images: `client.moderate({ image: base64 })`. See [moderating user-uploaded images](/blog/moderate-user-uploaded-images).
- Videos: `client.moderateVideo(videoBytes)`. See [moderating user-uploaded videos](/blog/moderate-user-uploaded-videos).
- Usernames: `client.checkUsername("user123")` returns `{ flagged, score }`.

## Summary

- Install from GitHub, call `moderate({ text })`.
- Read `flagged` and `labels`.
- Scope with `enabled_labels`, use `include_context` for short replies.
- Use `moderateBatch` for volume, and handle `402`.

See the [JavaScript SDK docs](/docs/sdks/javascript) and [API reference](/docs/integrations/api), try the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
