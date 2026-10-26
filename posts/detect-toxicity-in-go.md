---
title: "How to detect toxicity in Go"
date: 2026-10-26
description: "Detect toxic, abusive and spammy text in Go with the Supervisor SDK: standard library only, context aware, with label scoping, batches, usernames and error handling."
---

# How to detect toxicity in Go

**Bottom line:** `go get` the Supervisor SDK, create a client with your API key, and call `client.Moderate`. It is standard library only and takes a `context.Context`, so timeouts and cancellation work the way you expect.

## The problem

Go services tend to sit in the hot path: a chat gateway, a comment API, a game server. You want a moderation call that respects your context deadlines, returns a typed result, and does not drag in a dependency tree.

## Install

```bash
go get github.com/Phosphor-gg/supervisor-sdk-go
```

It requires Go 1.21 or later. Sign up at [supervisor.gg](https://supervisor.gg), then create a key at **Dashboard > API Keys**. Keys look like `sk_prod_...`.

## Your first check

```go
package main

import (
	"context"
	"fmt"
	"os"

	supervisor "github.com/Phosphor-gg/supervisor-sdk-go"
)

func main() {
	client := supervisor.NewClient(os.Getenv("SUPERVISOR_API_KEY"))
	text := "text to check"
	res, err := client.Moderate(context.Background(), &supervisor.ModerationRequest{Text: &text})
	if err != nil {
		panic(err)
	}
	fmt.Println(res.Flagged, res.Labels)
}
```

Fields are pointers where optional, so `Text` is a `*string`. The `ModerationResponse` has `Flagged`, `Labels`, `ImplicitLabels`, `ModelVersion`, `NeedsContext` and `ContextLabels`.

## Client options

```go
client := supervisor.NewClient(
	os.Getenv("SUPERVISOR_API_KEY"),
	supervisor.WithTimeout(5*time.Second),
)
```

`WithBaseURL(url)` and `WithTimeout(d)` are available, as is `WithHTTPClient`.

## Labels and models

Toxicity is one of 16 labels. Scope a check with `EnabledLabels` and pick a model:

```go
model := supervisor.ModelSentinel
res, err := client.Moderate(ctx, &supervisor.ModerationRequest{
	Text:  &text,
	Model: &model,
	EnabledLabels: []supervisor.ModerationLabel{
		supervisor.LabelToxicity,
		supervisor.LabelInsult,
		supervisor.LabelHarassment,
		supervisor.LabelHate,
	},
})
```

Observer is roughly £0.0014 per KB of text, Sentinel (the default) roughly £0.0027 and Arbiter roughly £0.0055.

## Short replies: use context

```go
res, err := client.Moderate(ctx, &supervisor.ModerationRequest{
	Text:           &text,
	IncludeContext: true,
})
if err == nil && !res.Flagged && res.NeedsContext != nil && *res.NeedsContext {
	// Send the recent history with the message in a follow-up request.
	combined := strings.Join(append(history, text), "\n")
	res, err = client.Moderate(ctx, &supervisor.ModerationRequest{Text: &combined})
}
```

`NeedsContext` is a `*bool`, so check for nil. Context-aware moderation is included with Premium.

## Batches and usernames

```go
results, err := client.ModerateBatch(ctx, &supervisor.BatchModerationRequest{
	Texts: []string{"First message", "Second message", "Third message"},
})
// results is []ModerationResponse, one per text.

name, err := client.CheckUsername(ctx, "user123")
// name.Flagged, name.Score
```

Batches of two or more are billed at 50% off. The docs state no maximum batch size, so chunk large jobs.

## Errors

API errors are `*supervisor.Error` with a `StatusCode`, plus helpers:

```go
var apiErr *supervisor.Error
if errors.As(err, &apiErr) {
	switch {
	case apiErr.StatusCode == 402:
		// credits exhausted until the monthly reset or an upgrade
	case apiErr.IsRateLimit():
		// 429: back off and retry later
	case apiErr.IsAuthError():
		// 401: bad or missing key
	case apiErr.IsValidationError():
		// 400 or 422
	}
}
```

There is no `Is402` helper, so compare `StatusCode` directly.

## Other media

`client.ModerateVideo(ctx, videoBytes)` takes the clip as bytes and checks the 10 MB limit locally. Images go in the `Image` field as base64. See the posts on [images](/blog/moderate-user-uploaded-images) and [videos](/blog/moderate-user-uploaded-videos).

## Summary

- `go get`, then `client.Moderate(ctx, ...)`.
- Read `Flagged` and `Labels`.
- Scope with `EnabledLabels`, use `IncludeContext` for short replies.
- Batch for volume, and compare `StatusCode` for `402`.

See the [Go SDK docs](/docs/sdks/go) and [API reference](/docs/integrations/api), try the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
