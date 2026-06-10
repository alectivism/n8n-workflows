# n8n Workflow Templates

Importable n8n workflows for content pipelines, monitoring, and AI agent ops. Each workflow ships as a self-contained JSON file you can drop into your own n8n instance, plus a README explaining what it does and what credentials it needs.

These are the actual workflows running my personal content pipeline, sanitized so you can fork and adapt them. Not no-code demos: production pipelines, exported and scrubbed.

## Intake (RSS → Notion)

These read feeds on a cron, dedupe, filter, and write new items to a Notion content database.

| Workflow | What it does | Cadence |
|---|---|---|
| [`rss-intake/`](rss-intake/) | Core industry feeds (AdExchanger, IAB, Digiday, TechCrunch AI, …) → Notion | Daily |
| [`reddit-rss-intake/`](reddit-rss-intake/) | ~25 subreddit RSS feeds → Notion | Weekly |
| [`reddit-ai-subreddits/`](reddit-ai-subreddits/) | Top-of-week posts from AI subreddits → Notion | Weekly |
| [`reddit-ai-subreddits-monthly/`](reddit-ai-subreddits-monthly/) | Top-of-month posts from AI subreddits → Notion | Monthly |
| [`news-web-monitor/`](news-web-monitor/) | Industry news/blog feeds, LLM-filtered → Notion | Weekly |
| [`substack-monitor/`](substack-monitor/) | AI/marketing Substack feeds → Notion | Weekly |
| [`podcast-intake/`](podcast-intake/) | Podcast RSS + Vimeo → transcribe → LLM topic extraction → Notion | Twice weekly |

## Monitors (social → Notion)

| Workflow | What it does | Cadence |
|---|---|---|
| [`x-thought-leader-monitor/`](x-thought-leader-monitor/) | Pulls posts from a roster of X accounts, scores relevance, files keepers | Weekly |
| [`linkedin-profile-monitor/`](linkedin-profile-monitor/) | Monitors LinkedIn profiles via a scraper API → Notion | Weekly |
| [`board-linkedin-monitor/`](board-linkedin-monitor/) | Scrapes a roster's LinkedIn posts, drafts comments via Claude, queues to Airtable | ⚠️ coming soon |

## Publish & infrastructure

| Workflow | What it does | Trigger |
|---|---|---|
| [`publish-social/`](publish-social/) | One webhook → publishes to LinkedIn, X, Bluesky, Threads with per-channel formatting | Webhook |
| [`web-capture-webhook/`](web-capture-webhook/) | Browser-extension capture endpoint: scrape a URL (Reddit JSON / Firecrawl / WebCrawlerAPI) → Notion | Webhook |
| [`linkedin-website-sync/`](linkedin-website-sync/) | Syncs recent LinkedIn posts to a JSON feed consumed by a personal website | Weekly cron |
| [`error-handler-slack/`](error-handler-slack/) | Drop-in error workflow: catches failures from any workflow and alerts Slack | Error trigger |

## How to import a workflow

1. Pick a workflow folder.
2. Open your n8n instance (cloud or self-hosted) → **Workflows** → **Import from File** → select the `.json`.
3. The workflow appears with **placeholder credential IDs** (`REPLACE_WITH_*_CREDENTIAL_ID`) that won't resolve until you replace them. Click each node that uses an external service → **Credentials** → create a new credential of the matching type → save.
4. For workflows that write to Notion, repoint the database: the JSON references inert placeholder IDs (`aaaaaaaa-0000-…`). Open each Notion node, select your own database, and remap the property fields.
5. Test the workflow manually before turning on the **Active** toggle.

## What's been sanitized

Every workflow here was exported from a live n8n instance and run through a scrubber that:

- Replaces all credential references with placeholder IDs (`REPLACE_WITH_X_CREDENTIAL_ID`, etc.)
- Removes real API keys and tokens (no OAuth tokens, no `Bearer` secrets, no webhook secrets)
- Remaps every real Notion database and property ID to an inert placeholder UUID (`aaaaaaaa-0000-4000-8000-…`) so structure is preserved but nothing real leaks
- Strips Slack channel IDs, Google Drive folder IDs, and email addresses
- Strips environment-specific fields (`id`, `versionId`, `tags`, `active`, pinned data)

If you find something that slipped through, open an issue.

## License

MIT. Fork freely. If you ship something useful built on top of these, link back.

## Credit

Built by [Alec Foster](https://www.alecfoster.com), Chief AI Architect & Responsible AI Lead at the Marketing + Media Alliance.
