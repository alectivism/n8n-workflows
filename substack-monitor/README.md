# Content Pipeline: Substack Newsletters Monitor

Weekly cron over a set of AI and marketing Substack feeds. New issues get filtered and filed to Notion.

## How it works

- **Trigger:** schedule (cron) — `0 0 8 * * 1`
- **Nodes:** 13
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Credentials to replace

Every credential ID in the JSON is a placeholder (`REPLACE_WITH_*`). After import, open each flagged node, create the matching credential in your own instance, and select it.

- HTTP Header Auth (one per external service — the credential names on each node say which: Notion, Anthropic, Firecrawl, Apify, AssemblyAI, Vimeo)

## Sample sources

These are my sources, left in as working examples. Swap them for your own.

- `https://aisnakeoil.substack.com/feed',`
- `https://importai.substack.com/feed',`
- `https://www.latent.space/feed',`
- `https://www.marketingaiinstitute.com/blog/rss.xml',`
- `https://www.oneusefulthing.org/feed',`

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
