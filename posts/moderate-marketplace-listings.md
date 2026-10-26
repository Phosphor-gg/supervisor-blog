---
title: "How to moderate marketplace listings: text and images"
date: 2026-10-26
description: "Screen listings for scams, prohibited items and spam before they go live. Check titles, descriptions and photos with one API, and review a backlog of existing listings in bulk."
---

# How to moderate marketplace listings: text and images

**Bottom line:** a listing has text and photos, and either can break your rules. Check the title and description with the text endpoint and each photo with the image endpoint, then publish, hold or reject based on the labels. This guide uses TypeScript and the Supervisor SDK.

## The problem

Marketplaces get a particular mix of abuse: scams ("pay me outside the platform"), prohibited or illegal items, spam listings repeated across categories, and photos that contain things your text checks never see. A keyword list will not tell you that a polite description is a scam, and it cannot look at a photo.

## 1. Set up

Sign up at [supervisor.gg](https://supervisor.gg), create a key under **Dashboard > API Keys** (`sk_prod_...`), and install the SDK from GitHub (it is not on npm):

```bash
npm install github:Phosphor-gg/supervisor-sdk-js
```

## 2. Pick the labels that match your rules

Pass `enabled_labels` so a flag always maps to a rule you actually enforce. For a marketplace the useful ones are usually:

- `scam`: scam, phishing or incoherent content
- `illegal`: illegal activity
- `spam` and `promotional`: repeated or advertising content
- `sexual`, `sexual/explicit`, `sexual/unlawful`: depending on your category rules
- `hate`, `harassment`: in descriptions and seller messages

## 3. Check the text

```typescript
import {
  SupervisorClient,
  SupervisorError,
  ModerationLabel,
  ModerationModel,
} from "supervisor-sdk";

const client = new SupervisorClient({ apiKey: process.env.SUPERVISOR_API_KEY! });

const TEXT_LABELS = [
  ModerationLabel.Scam,
  ModerationLabel.Illegal,
  ModerationLabel.Spam,
  ModerationLabel.Promotional,
  ModerationLabel.Hate,
  ModerationLabel.Harassment,
  ModerationLabel.Sexual,
];

async function checkListingText(title: string, description: string) {
  return client.moderate({
    text: `${title}\n${description}`,
    model: ModerationModel.Sentinel,
    enabled_labels: TEXT_LABELS,
  });
}
```

Text is billed by the byte, so a long description costs more than a short one. Joining title and description into one request keeps it to one call per listing.

## 4. Check each photo

Send the image as base64 in the `image` field. Text and images go in separate requests.

```typescript
import { readFile } from "node:fs/promises";

async function checkListingPhoto(path: string) {
  const bytes = await readFile(path);
  return client.moderate({
    image: bytes.toString("base64"),
    model: ModerationModel.Sentinel,
  });
}
```

Notes on images:

- They are billed at a flat rate of about £0.0014 per KB of image data (the Observer rate), whichever model you choose.
- If the OCR finds readable text in the image, that text is billed in addition at the model's rate. That matters for listings, where photos often include text overlays or screenshots of messages.
- The SDK prepares images before upload: it strips any data URL prefix and, where it can (in a browser, or in Node with the optional `sharp` package installed), downsizes them to at most 1280 pixels on the longest edge. Without `sharp` in Node, the image is sent as it is.

## 5. Combine the verdicts

```typescript
type Decision = "publish" | "hold" | "reject";

const REJECT = new Set(["scam", "illegal", "sexual/unlawful", "sexual/explicit"]);

async function reviewListing(
  title: string,
  description: string,
  photoPaths: string[],
): Promise<{ decision: Decision; labels: string[] }> {
  try {
    const results = [
      await checkListingText(title, description),
      ...(await Promise.all(photoPaths.map(checkListingPhoto))),
    ];
    const labels = [...new Set(results.flatMap((r) => r.labels))];
    if (labels.some((l) => REJECT.has(l))) return { decision: "reject", labels };
    if (labels.length > 0) return { decision: "hold", labels };
    return { decision: "publish", labels };
  } catch (e) {
    if (e instanceof SupervisorError && e.statusCode === 402) {
      console.error("Moderation credits exhausted");
    }
    return { decision: "hold", labels: [] };
  }
}
```

When credits run out the API responds `402 Payment Required` until the monthly reset or an upgrade, and `SupervisorError` carries the status code. Holding on any error means an outage queues listings instead of publishing them unchecked. Choose the opposite if your business cannot tolerate delay, but make it a decision.

## 6. Re-check existing listings

For a backlog, `moderateBatch` takes an array of texts and returns one result per text. Batches of two or more are billed at 50% off.

```typescript
async function scanListings(listings: { id: string; text: string }[]) {
  const flagged: { id: string; labels: string[] }[] = [];
  // No maximum batch size is documented, so send chunks. 100 is our choice.
  for (let i = 0; i < listings.length; i += 100) {
    const chunk = listings.slice(i, i + 100);
    const results = await client.moderateBatch({
      texts: chunk.map((l) => l.text),
      model: ModerationModel.Observer,
      enabled_labels: TEXT_LABELS,
    });
    results.forEach((r, j) => {
      if (r.flagged) flagged.push({ id: chunk[j].id, labels: r.labels });
    });
  }
  return flagged;
}
```

## 7. Check seller names

`client.checkUsername("shop_name")` returns `{ flagged, score }`, which suits store and seller names.

## Summary

- Text and photos are separate requests, combine the labels.
- Scope with `enabled_labels`, and map labels to publish, hold or reject.
- Remember OCR text in photos is billed on top of the image.
- Hold on errors, and handle `402`.
- Use `moderateBatch` for backlogs.

Read the [API reference](/docs/integrations/api), try a listing in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
