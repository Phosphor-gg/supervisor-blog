---
title: "How to moderate in-game chat with an API"
date: 2026-10-26
description: "A practical pattern for moderating player chat and usernames from your game server: which labels to turn on, how to handle short replies with context, and what to do when credits run out."
---

# How to moderate in-game chat with an API

**Bottom line:** moderate chat on the server, not the client, send each message to a moderation API before you broadcast it, and decide in advance what happens when the API is unreachable. This guide shows the pattern in Go using the Supervisor SDK, with the same calls available over plain HTTP.

## The problem with word lists in game chat

Most games start with a banned word list. It works for a week. Then players type `f u c k`, swap letters for numbers, or just say something cruel that contains no banned word at all. Chat is also full of short replies like "do it" or "stop", which are harmless in one match and a threat in another.

Game chat has three constraints that a comment section does not:

- **Volume.** Messages are short and frequent, so the cost per message matters.
- **Timing.** Players see the message as it is sent, so the check sits in the send path.
- **Context.** A one word reply means nothing without the lines before it.

## What you will build

A function on your game server that takes a chat message and the last few lines from the same channel, and returns whether to hide it. It also checks usernames when a player joins.

## 1. Get an API key

Sign up at [supervisor.gg](https://supervisor.gg) with Discord, Google or GitHub, then go to **Dashboard > API Keys** and create a key. Keys look like `sk_prod_...`. Keep it on the server, never in the game client.

Install the Go SDK:

```bash
go get github.com/Phosphor-gg/supervisor-sdk-go
```

It needs Go 1.21 or later.

## 2. Check a message

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"os"
	"strings"
	"time"

	supervisor "github.com/Phosphor-gg/supervisor-sdk-go"
)

var client = supervisor.NewClient(
	os.Getenv("SUPERVISOR_API_KEY"),
	supervisor.WithTimeout(5*time.Second),
)

// Labels worth acting on in chat. Add or remove to suit your game.
var chatLabels = []supervisor.ModerationLabel{
	supervisor.LabelProfanity,
	supervisor.LabelToxicity,
	supervisor.LabelHarassment,
	supervisor.LabelHate,
	supervisor.LabelInsult,
	supervisor.LabelSexual,
	supervisor.LabelScam,
	supervisor.LabelSpam,
}

// shouldHide reports whether a chat line should be hidden. recent holds the
// previous lines in the same channel, oldest first.
func shouldHide(ctx context.Context, msg string, recent []string) (bool, []string, error) {
	model := supervisor.ModelObserver
	res, err := client.Moderate(ctx, &supervisor.ModerationRequest{
		Text:           &msg,
		Model:          &model,
		EnabledLabels:  chatLabels,
		IncludeContext: true,
	})
	if err != nil {
		return false, nil, err
	}
	if res.Flagged {
		return true, res.Labels, nil
	}

	// The message looked fine alone but may not be fine in conversation.
	if res.NeedsContext != nil && *res.NeedsContext && len(recent) > 0 {
		combined := strings.Join(append(append([]string{}, recent...), msg), "\n")
		res, err = client.Moderate(ctx, &supervisor.ModerationRequest{
			Text:          &combined,
			Model:         &model,
			EnabledLabels: chatLabels,
		})
		if err != nil {
			return false, nil, err
		}
	}
	return res.Flagged, res.Labels, nil
}
```

A few choices in that code are worth explaining.

**`EnabledLabels` scopes the check.** Without it every one of the 16 labels is checked. In a game you probably do care about `scam` and `spam` (account sellers, boosting offers), and you might not care about `medical`. Pick the labels that match your community rules so a flag always means something you would act on.

**`IncludeContext` handles short replies.** With `include_context` set, the response can carry `needs_context` and `context_labels`. For `"stop it"` the API returns `flagged: false` with `needs_context: true` and `context_labels: ["harassment"]`: on its own the message is fine, but it might not be. The docs say to include message history in a follow-up request, and the code above does that by joining the recent lines with the new one last. Context-aware moderation is included with Premium.

**The follow-up only runs when it needs to.** A flagged message is already a decision, so the code returns straight away. Most messages are neither flagged nor ambiguous, so most messages cost one request.

**Choose the model for your volume.** The example uses Observer, the cheapest model, at roughly £0.0014 per KB of text. Sentinel (the default, roughly £0.0027 per KB) and Arbiter (roughly £0.0055 per KB) cost more. Text is billed by the byte, so a 100 byte chat line on Observer costs about £0.00013. Premium includes £120 of credits a month, which works out at about 900,000 lines of that size. Batching halves the cost again. Work out your own numbers from your average message length and traffic.

## 3. Wire it into the send path

```go
func onChatMessage(ctx context.Context, player, msg string, recent []string) {
	hide, labels, err := shouldHide(ctx, msg, recent)
	if err != nil {
		handleModerationError(err)
		// Decide your policy: here we let the message through and log it.
		broadcast(player, msg)
		return
	}
	if hide {
		fmt.Printf("hid message from %s: %v\n", player, labels)
		sendToPlayerOnly(player, "Your message was not sent.")
		return
	}
	broadcast(player, msg)
}
```

`broadcast` and `sendToPlayerOnly` are your game's own functions. Showing the sender their own message while hiding it from everyone else ("shadow muting") is an option if you do not want to tell abusive players what tripped the filter. That is a game design call, not an API feature.

## 4. Handle errors and running out of credits

When your balance is exhausted the API returns `402 Payment Required` until credits are replenished by the monthly reset or an upgrade. The Go SDK gives you the status code on its error type:

```go
func handleModerationError(err error) {
	var apiErr *supervisor.Error
	if errors.As(err, &apiErr) {
		switch {
		case apiErr.StatusCode == 402:
			fmt.Println("out of moderation credits: alert the team")
		case apiErr.IsRateLimit():
			fmt.Println("rate limited: back off and retry later")
		case apiErr.IsAuthError():
			fmt.Println("bad API key")
		default:
			fmt.Println("moderation error:", apiErr)
		}
		return
	}
	fmt.Println("moderation request failed:", err)
}
```

The bigger question is what your game does when moderation fails. There are two honest options:

- **Fail open.** Let the message through and alert someone. Chat keeps working, but unmoderated lines get out during an outage.
- **Fail closed.** Hold or drop messages. Safer for a game with young players, but chat stops when the API call fails.

Pick one deliberately and test it. Also set a client timeout you can live with, as the example does with `WithTimeout`, so a slow request cannot stall your game loop.

## 5. Check usernames on join

Usernames are chat too, and they sit on screen all the time. There is a separate endpoint for them:

```go
func usernameAllowed(ctx context.Context, name string) (bool, error) {
	res, err := client.CheckUsername(ctx, name)
	if err != nil {
		return false, err
	}
	return !res.Flagged, nil
}
```

The response is `{ "flagged": false, "score": 0.12 }`, a flag plus a confidence score.

## 6. Review backlogs in bulk

If you keep chat logs and want to review a week of them, do not loop over single requests. `ModerateBatch` takes a list of texts and returns one result per text, and batches of two or more are billed at 50% off:

```go
func reviewLog(ctx context.Context, lines []string) error {
	model := supervisor.ModelObserver
	results, err := client.ModerateBatch(ctx, &supervisor.BatchModerationRequest{
		Texts:         lines,
		Model:         &model,
		EnabledLabels: chatLabels,
	})
	if err != nil {
		return err
	}
	for i, r := range results {
		if r.Flagged {
			fmt.Printf("line %d flagged: %v\n", i, r.Labels)
		}
	}
	return nil
}
```

The docs do not state a maximum batch size, so send large logs in chunks rather than one enormous request.

## Raw HTTP

If you are not using Go, the same check is one request:

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "stop it",
    "model": "observer",
    "include_context": true
  }'
```

There are also SDKs for [Python](/docs/sdks/python), [JavaScript](/docs/sdks/javascript), [Rust](/docs/sdks/rust) and [Java](/docs/sdks/java), which suits Minecraft style servers on the JVM.

## Summary

- Moderate on the server, before broadcast.
- Use `enabled_labels` to match your community rules.
- Use `include_context` and a single follow-up request for short replies.
- Use `CheckUsername` for names and `ModerateBatch` for logs.
- Treat `402` and timeouts as a policy decision made in advance, not an exception to discover in production.

Read the [API reference](/docs/integrations/api), try messages from your own game in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key.
