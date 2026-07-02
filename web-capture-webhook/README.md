# Content Pipeline: Web Capture Webhook

Webhook endpoint for a browser extension or share target. Scrapes a URL (Reddit JSON, Firecrawl, WebCrawlerAPI fallback) and saves structured content to Notion.

## How it works

- **Trigger:** webhook — POST to `/content-capture`
- **Nodes:** 9
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Credentials to replace

Every credential ID in the JSON is a placeholder (`REPLACE_WITH_*`). After import, open each flagged node, create the matching credential in your own instance, and select it.

- Notion API

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
