---
title: "AWS content moderation pricing: what Comprehend and Rekognition cost"
date: 2026-10-26
description: "How Amazon Comprehend toxicity detection and Amazon Rekognition content moderation are billed, with worked examples and an honest comparison against Supervisor's flat monthly plan."
---

# AWS content moderation pricing: what Comprehend and Rekognition cost

**Bottom line:** AWS moderation is pay per use with no subscription. Comprehend toxicity detection starts at $0.0001 per 100 characters with a 300 character minimum per request, so a short message costs $0.0003. Rekognition bills per image and per minute of video. Supervisor is a flat £13.99 a month with 90 million credits, which works out cheaper per short text message if you use the allowance and more expensive if you barely use it. Supervisor bills images by file size while AWS bills per image, so check your average image size.

AWS moderation is two services, so there are two price lists. This post covers only figures we checked against AWS's own pricing sources, and it names the places where AWS's pages disagree with each other so you can confirm them before budgeting.

## Amazon Comprehend toxicity detection

Comprehend measures toxicity requests in units of 100 characters, with a 3 unit (300 character) minimum charge per request, according to the [Comprehend pricing page](https://aws.amazon.com/comprehend/pricing/). Prices are in US dollars. The rates below are for US East (N. Virginia), taken from AWS's [published price list file](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/comprehend/current/index.json), where we also found identical rates for US West (Oregon), Europe (Ireland) and Asia Pacific (Sydney).

| Monthly volume (units of 100 characters) | Price per unit |
| --- | --- |
| First 10 million | $0.0001 |
| 10 million to 50 million | $0.00005 |
| 50 million to 100 million | $0.000025 |

AWS's own pages disagree about what happens above 100 million units a month: the pricing page says to contact AWS, while the price list file contains a further tier. We are not quoting a rate for that range. If you are anywhere near it, ask AWS.

Also worth knowing:

- **Short messages round up.** A 40 character chat message is billed as 3 units, the same as a 300 character one.
- **Request limits.** One request holds up to 10 strings of up to 1 KB each, per the [API reference](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html). The default quota is 25 requests per second per region, and it is [adjustable](https://docs.aws.amazon.com/general/latest/gr/comprehend.html).
- **Free tier.** Comprehend has a general free tier, but we could not confirm whether it covers toxicity detection, so do not assume it does.

### Worked example

Assuming one message of up to 300 characters per request, in the first volume tier (derived from the rates above):

| Messages per month | Units | Cost |
| --- | --- | --- |
| 10,000 | 30,000 | $3 |
| 100,000 | 300,000 | $30 |
| 1,000,000 | 3,000,000 | $300 |

A message of 301 to 400 characters is 4 units, and so on. If you batch several strings into one request, check how AWS meters the minimum before you rely on this table.

## Amazon Rekognition content moderation

Rekognition image moderation is billed per image, tiered by monthly volume, and stored video moderation is billed per minute.

- **Images.** We are not quoting a per-image rate. AWS's price list file and pricing page disagree on which pricing group `DetectModerationLabels` belongs to, and the tier boundaries differ between the two groups. Check the [Rekognition pricing page](https://aws.amazon.com/rekognition/pricing/) for the group your account falls under.
- **Stored video.** Content moderation on stored video is $0.10 per minute of video in US East (N. Virginia), per AWS's [price list file](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonRekognition/current/index.json). Other regions differ.
- **Custom moderation adapters.** Training a custom adapter is billed separately at $5 per hour of training in US East (N. Virginia), also from the price list file.
- **Free tier.** AWS lists a monthly free allowance for image and video analysis, but we could not confirm its duration or whether it applies to video moderation. Confirm on the pricing page.

Because Rekognition bills per image rather than per byte, a large image and a small image cost the same on the AWS side. That is useful for predicting your bill.

## What Supervisor costs

Supervisor has one plan, and it includes everything.

- **Premium: £13.99 a month**, £83.85 a year or £179.65 for three years, with 90,000,000 credits each month and all three models, context, image and video moderation.
- **£1 is 750,000 credits.** Text costs 1, 2 or 4 credits per byte on Observer, Sentinel and Arbiter, which the docs express as roughly £0.0014, £0.0027 and £0.0055 per KB.
- **Batches of two or more cost half.** Images are billed at 1 credit per byte, and video frames at a quarter of that.
- **New accounts** get 187,500 free credits, usable for 7 days from the first moderated message, and there is a 7 day Premium trial that needs a card.
- **When credits run out**, API requests return 402 Payment Required until they reset or you upgrade.

## Comparing the two honestly

The derived figures below use a 100 byte text message on Sentinel, which is 200 credits, or about £0.00027 at list rate.

| | AWS | Supervisor |
| --- | --- | --- |
| Billing model | Pay per use, no minimum | £13.99 a month flat, 90M credits |
| Short text message | $0.0003 (3 unit minimum) | 200 credits on Sentinel, 100 credits on Observer |
| Messages covered by one month | Unlimited, billed as you go | About 450,000 of that size on Sentinel, 900,000 on Observer, 225,000 on Arbiter |
| Effective cost if you use the whole allowance | Not applicable | About £0.00003 per message (£13.99 divided by 450,000, derived) |
| Images | Per image | By file size, about £0.14 for a 100 KB image per our docs |
| Stored video | $0.10 per minute | By frame size, up to 60 s and 10 MB |
| Currency | USD | GBP |

How to read it:

- **At low volume, AWS is cheaper.** At 10,000 messages a month, the AWS example above is about $3. Supervisor is £13.99 whether you send 10,000 or not.
- **At high text volume, Supervisor can be cheaper.** If you use most of the 450,000 Sentinel messages, the effective rate falls well below AWS's $0.0003 per short message. The currencies differ, so convert at the current rate. Past the allowance you need more credits, so model that before relying on it.
- **Images are where Supervisor's cost scales with file size.** A 100 KB image costs about £0.14, and the bill grows with the file. AWS bills per image. Work out your average image size against the AWS rate for your account before you decide, and expect Supervisor to be the more expensive option for large images.
- **Arbiter costs double Sentinel and four times Observer**, per byte. Choose the model per job.
- **Context and extra labels are not separate line items.** On Supervisor they are included in the plan. On AWS, getting scams, spam or self-harm coverage would mean another service, which this comparison does not price.

## Which should you pick on price?

Pick AWS if your volume is small or spiky, you are already billed through AWS, and Comprehend's seven toxicity labels and Rekognition's visual categories cover your problem. Pick Supervisor if your text volume is steady and high, you want 16 labels, context flagging and one API, and you would rather have one predictable bill. Many teams will use both.

You can test cost on real traffic before committing: [create a free account](https://supervisor.gg) for the signup credits, try the [live demo](https://supervisor.gg/demo), and see the [API reference](https://supervisor.gg/docs/integrations/api) for the billing rules.

## Sources

- [Amazon Comprehend pricing](https://aws.amazon.com/comprehend/pricing/) and [price list file](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/comprehend/current/index.json)
- [Comprehend DetectToxicContent API reference](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html) and [service quotas](https://docs.aws.amazon.com/general/latest/gr/comprehend.html)
- [Amazon Rekognition pricing](https://aws.amazon.com/rekognition/pricing/) and [price list file](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonRekognition/current/index.json)
- AWS prices were read on 26 October 2026 and change. Confirm them before budgeting.
