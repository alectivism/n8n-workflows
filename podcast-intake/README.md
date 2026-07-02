# Content Pipeline: Podcast RSS + Vimeo Intake

Twice-weekly cron: pulls podcast RSS and Vimeo, transcribes new media, extracts topic ideas with an LLM, and writes to Notion. Google Drive holds the transcripts.

## How it works

- **Trigger:** schedule (cron) — `0 0 10 * * 2,5`
- **Nodes:** 40
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Credentials to replace

Every credential ID in the JSON is a placeholder (`REPLACE_WITH_*`). After import, open each flagged node, create the matching credential in your own instance, and select it.

- Google Drive (OAuth2)
- HTTP Header Auth (one per external service — the credential names on each node say which: Notion, Anthropic, Firecrawl, Apify, AssemblyAI, Vimeo)

## Sample sources

These are my sources, left in as working examples. Swap them for your own.

- `https://api.vimeo.com/me/videos`
- `https://api.vimeo.com/videos/{{`
- `https://changelog.com/practicalai/feed',`
- `https://feeds.buzzsprout.com/2418777.rss',`
- `https://feeds.megaphone.fm/CSIS8973369418',`
- `https://feeds.megaphone.fm/PDP6186156462',`
- `https://feeds.megaphone.fm/buildingbettercmos',`
- `https://feeds.megaphone.fm/marketingai',`

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
