---
title: "How to moderate forum posts and threads"
date: 2026-10-26
description: "Forum posts are long, threaded and full of context. Here is how to moderate them with an API: choose labels, use context for replies, keep cost predictable, and scan an existing archive."
---

# How to moderate forum posts and threads

**Bottom line:** forum posts are longer than chat messages and depend on the thread, so check each post when it is submitted, think about cost per byte, and send the thread context only when the API asks for it. This guide uses Go and the Supervisor SDK.

## The problem

A forum is where arguments run long. The usual failures are a pile-on that stays just under your word list, promotional posts disguised as helpful answers, and links to scams in replies to old threads. Posts are also long: a few paragraphs of text is far more than a chat line, and the cost of moderating it is billed by size.

## 1. Set up

Sign up at [supervisor.gg](https://supervisor.gg), create a key under **Dashboard > API Keys** (`sk_prod_...`), and add the SDK (Go 1.21 or later):

```bash
go get github.com/Phosphor-gg/supervisor-sdk-go
```

## 2. Understand the cost of long posts

Text is billed by the byte at the model's rate: roughly £0.0014 per KB on Observer, £0.0027 on Sentinel and £0.0055 on Arbiter. From the credit rates, a 2 KB post on Sentinel is about £0.0054. Multiply by your posts per month to budget, rather than guessing.

Two levers keep cost down:

- Use Observer for the first pass and reserve Arbiter for appeals.
- Moderate the text a user actually wrote, not the quoted text they are replying to. Quotes are already moderated, and you pay by the byte.

Identical repeated requests within the cache window consume no credits, per the API reference.

## 3. Check a post

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"os"
	"strings"

	supervisor "github.com/Phosphor-gg/supervisor-sdk-go"
)

var client = supervisor.NewClient(os.Getenv("SUPERVISOR_API_KEY"))

var forumLabels = []supervisor.ModerationLabel{
	supervisor.LabelToxicity,
	supervisor.LabelHarassment,
	supervisor.LabelHate,
	supervisor.LabelInsult,
	supervisor.LabelSpam,
	supervisor.LabelPromotional,
	supervisor.LabelScam,
	supervisor.LabelIllegal,
}

// reviewPost returns the labels that fired, and whether the post needs a human.
// threadTail holds the last few posts in the thread, oldest first.
func reviewPost(ctx context.Context, body string, threadTail []string) ([]string, error) {
	model := supervisor.ModelSentinel
	res, err := client.Moderate(ctx, &supervisor.ModerationRequest{
		Text:           &body,
		Model:          &model,
		EnabledLabels:  forumLabels,
		IncludeContext: true,
	})
	if err != nil {
		return nil, err
	}
	if res.Flagged {
		return res.Labels, nil
	}
	if res.NeedsContext != nil && *res.NeedsContext && len(threadTail) > 0 {
		combined := strings.Join(append(append([]string{}, threadTail...), body), "\n")
		res, err = client.Moderate(ctx, &supervisor.ModerationRequest{
			Text:          &combined,
			Model:         &model,
			EnabledLabels: forumLabels,
		})
		if err != nil {
			return nil, err
		}
	}
	return res.Labels, nil
}
```

For a reply such as "you clearly have no idea", `include_context` lets the API tell you the post is ambiguous on its own (`needs_context: true` with `context_labels`). The follow-up then sends the thread tail with it. Context-aware moderation is included with Premium.

## 4. Handle failures

```go
func submitPost(ctx context.Context, body string, tail []string) {
	labels, err := reviewPost(ctx, body, tail)
	if err != nil {
		var apiErr *supervisor.Error
		if errors.As(err, &apiErr) && apiErr.StatusCode == 402 {
			fmt.Println("moderation credits exhausted")
		}
		queueForReview(body, nil) // hold: nothing publishes unreviewed
		return
	}
	if len(labels) > 0 {
		queueForReview(body, labels)
		return
	}
	publish(body)
}
```

`queueForReview` and `publish` are your own functions. A `402` means credits have run out; requests fail until the monthly reset or an upgrade.

## 5. Check usernames and thread titles

New accounts are where forum abuse starts. `client.CheckUsername(ctx, "user123")` returns `Flagged` and a `Score`. Thread titles are short text and can go through `Moderate` like any other post.

## 6. Scan the archive

For an existing forum, send old posts through `ModerateBatch`. It returns one result per text and batches of two or more are billed at 50% off.

```go
func scanArchive(ctx context.Context, posts []string) ([]int, error) {
	model := supervisor.ModelObserver
	var flagged []int
	// No maximum batch size is documented, so send chunks. 100 is our choice.
	for start := 0; start < len(posts); start += 100 {
		end := min(start+100, len(posts))
		results, err := client.ModerateBatch(ctx, &supervisor.BatchModerationRequest{
			Texts:         posts[start:end],
			Model:         &model,
			EnabledLabels: forumLabels,
		})
		if err != nil {
			return flagged, err
		}
		for i, r := range results {
			if r.Flagged {
				flagged = append(flagged, start+i)
			}
		}
	}
	return flagged, nil
}
```

## 7. Keep a human in the loop

Treat flagged posts as a queue for moderators, with the labels attached, rather than deleting automatically. See the glossary entry on [false positives](/glossary/false-positive) for why this matters.

## Summary

- Posts are billed by size, so budget from bytes and pick the model by volume.
- Scope with `enabled_labels`, use `include_context` for replies.
- Hold on errors, handle `402`.
- Use `ModerateBatch` for archives.

Read the [API reference](/docs/integrations/api), try a thread in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
