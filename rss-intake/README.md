# Content Pipeline: RSS Intake

Daily cron over core industry feeds (AdExchanger, IAB, Digiday, TechCrunch AI). Dedupes and writes new items to a Notion content database. The original intake workflow.

## How it works

- **Trigger:** schedule (cron) — `0 14 * * *`
- **Nodes:** 19
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Credentials to replace

Every credential ID in the JSON is a placeholder (`REPLACE_WITH_*`). After import, open each flagged node, create the matching credential in your own instance, and select it.

- Notion API

## Sample sources

These are my sources, left in as working examples. Swap them for your own.

- `http://www.marketingaiinstitute.com/blog/rss.xml`
- `https://digiday.com/feed/`
- `https://iabtechlab.com/category/blog/feed/`
- `https://iapp.org/rss/daily-dashboard/`
- `https://techcrunch.com/category/artificial-intelligence/feed/`
- `https://tldr.tech/ai/rss`
- `https://venturebeat.com/category/ai/feed/`
- `https://www.adexchanger.com/feed/`

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
