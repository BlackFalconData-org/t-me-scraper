# Telegram Channel Scraper [Just 💰$0.68]

Extract structured data from [t.me](https://t.me) — t.me — public Telegram channel posts with post text, publish date, view counts, photos, videos and links, plus channel title, description and subscriber count. Search inside a channel, paste channel links, and get only new posts in incremental mode.

**[Telegram Channel Scraper [Just 💰$0.68] on Apify →](https://apify.com/blackfalcondata/t-me-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword. Filter by 📝 description format, and more.

**Incremental mode** — Only get new or changed posts since your last run. Content hash per post — no duplicates, no re-processing.

**Change classification** — Track cross-run duplicate detection across runs. Build audit trails of how posts evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N posts (up to 10.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every post returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured posts from t.me on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor posts, track trends, and analyze market dynamics with structured, deduplicated data from t.me.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per post is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "telegram",
  "maxResults": 100,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Public channel to scrape: `telegram`, `@telegram`, or `https://t.me/telegram`. Add an in-channel search with `?q=`, e.g. `telegram?q=update`. Use a JSON array for several channels, e.g. ["telegram","durov"]. |
| `maxResults` | integer | `100` | Maximum total posts, newest first (0 = unlimited). |
| `descriptionMaxLength` | integer | `0` | Truncate each post's text to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state and return only new or changed posts. stateKey is optional — defaults to a value derived from the channel(s) requested. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked channel universe. Leave empty to auto-generate from the inputs. |
| `skipReposts` | boolean | `false` | When incremental, skip posts whose content matches a post seen (and since removed) in a prior run. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED posts. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of posts included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results. Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `startUrls` | array | — | One or more public Telegram channel links, such as https://t.me/s/durov or https://t.me/durov. Add ?q=word to a link to search inside that channel. When set, the channel field is ignored. |

---

## Output fields

Every post returns the same 41-field schema. Missing values are `null` — never omitted.

- `listingId`
- `postKey`
- `postId`
- `channel`
- `url`
- `portalUrl`
- `title`
- `text`
- `date`
- `edited`
- `views`
- `viewsText`
- `author`
- `forwardedFrom`
- `forwardedFromUrl`
- `replyToUrl`
- `replyToText`
- `isServiceMessage`
- `mediaType`
- `photos`
- `videos`
- `documents`
- `links`
- `hashtags`
- `linkPreview`
- `channelUsername`
- `channelTitle`
- `channelVerified`
- `channelDescription`
- `channelPhotoUrl`
- `channelSubscribers`
- `channelPhotos`
- `channelVideos`
- `channelLinks`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per post. Here is a real example from a production run:

```json
{
  "listingId": "1f9b4d8f559a21438b11aa79808bd494a587d759f549f26bfb391781db31fb37",
  "postKey": "telegram/441",
  "postId": 441,
  "channel": "telegram",
  "url": "https://t.me/telegram/441",
  "portalUrl": "https://t.me/telegram/441",
  "title": "Bot-to-Bot Communication. Bots are now able to respond to other bots, not just users.",
  "text": "Bot-to-Bot Communication. Bots are now able to respond to other bots, not just users.\n\nAI enthusiasts can utilize this to create custom workflows with autonomous agents.\n\nMay Featu…",
  "date": "2026-05-14T16:08:31+00:00",
  "edited": false,
  "views": 1590000,
  "viewsText": "1.59M"
}
```

*Truncated — full records contain 41 fields. See Output fields for the complete schema.*

**[Try Telegram Channel Scraper [Just 💰$0.68] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/t-me-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0045 |
| Result | $0.000675 |

See the [actor on Apify](https://apify.com/blackfalcondata/t-me-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape t.me?**
Use this actor on Apify to extract structured data from t.me. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get t.me data as JSON, CSV, or Excel?**
The actor writes each post to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape t.me?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check t.me's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each post gets a content hash. On subsequent runs, only new or changed posts are emitted — saving time, compute, and storage. Expired posts can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Telegram Channel Scraper [Just 💰$0.68]](https://apify.com/blackfalcondata/t-me-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
