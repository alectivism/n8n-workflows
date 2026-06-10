# Web Capture Webhook

Webhook endpoint for a browser extension / share target. Scrapes a URL and saves structured content to Notion.

Part of a personal content pipeline by [Alec Foster](https://www.alecfoster.com). Importable as a single n8n workflow JSON.

## What it does

Receives a POST with a URL and routing flags from a browser extension or Android share target. Routes by source: Reddit posts use the native `.json` endpoint (full post + comments + images), general pages go through Firecrawl, with a WebCrawlerAPI fallback. Saves structured content to Notion.

Request body shape:
```json
{ "title": "", "url": "", "content": "", "contentType": "", "source": "", "sourceType": "", "capturedAt": "", "needsScrape": true, "isReddit": false }
```

## At a glance

| | |
|---|---|
| Trigger | Webhook |
| Schedule | Webhook (on demand) |
| Nodes | 9 |
| Destination | Notion content database |

## Quick start

1. Open your n8n instance → **Workflows** → **Import from File** → pick `workflow.json`.
2. Replace the placeholder credentials (see below). The imported file ships with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders that won't resolve until you create your own.
3. Repoint the Notion database: the workflow references placeholder database IDs (`aaaaaaaa-0000-...`). Open each Notion node, pick your own database, and remap the property fields.
4. Set the workflow **Active** and grab the production webhook URL from the trigger node.

## Credentials needed

| Service | n8n credential type | Notes |
|---|---|---|
| Notion | `notionApi` | Notion integration token |
| HTTP Header Auth | `httpHeaderAuth` | Header-auth credential for Firecrawl and WebCrawlerAPI (replace the `Bearer REPLACE_WITH_WEBCRAWLER_TOKEN` placeholder) |

Don't paste secrets into the JSON. n8n's credential store is encrypted; the JSON only references credential IDs.

## What's been sanitized

- Credential references replaced with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders
- All real Notion database/property IDs remapped to inert placeholder UUIDs (`aaaaaaaa-0000-4000-8000-…`)
- API tokens, Slack channel IDs, Google Drive folder IDs, and email addresses removed
- Environment-specific fields (`id`, `versionId`, `tags`, `active`, pinned data) stripped
