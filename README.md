# n8n Workflow Templates

Importable n8n workflows for content pipelines, monitoring, and AI-agent ops. Each ships as a self-contained JSON file you can drop into your own n8n instance, plus a README with what it does and which credentials it needs.

Most of these run in production as one system behind [alecfoster.com](https://www.alecfoster.com): the intake monitors below all write to a shared Notion database, `publish-social` fans posts out to social channels, and `error-handler-slack` catches failures across the whole set. The architecture is written up in [The Content Pipeline](https://www.alecfoster.com/guides/content-pipeline).

## Intake monitors

Each runs on its own schedule, pulls from its source type, dedupes, and writes normalized rows to the shared Notion intake database.

| Workflow | What it does | Status |
|---|---|---|
| [`rss-intake/`](rss-intake/) | Daily cron over core industry feeds (AdExchanger, IAB, Digiday, TechCrunch AI). Dedupes to a Notion database. The original intake workflow. | ready to import |
| [`reddit-rss-intake/`](reddit-rss-intake/) | Weekly cron over ~25 subreddit RSS feeds (AI, n8n, Claude, ML). Dedupes and files high-signal threads to Notion. | ready to import |
| [`reddit-ai-subreddits/`](reddit-ai-subreddits/) | Weekly cron over AI subreddits' top-of-week posts. Scores, filters, files keepers to Notion. | ready to import |
| [`reddit-ai-subreddits-monthly/`](reddit-ai-subreddits-monthly/) | Monthly cron (first Friday) over the month's top AI subreddit posts. Higher-bar companion to the weekly variant. | ready to import |
| [`news-web-monitor/`](news-web-monitor/) | Weekly cron over a dozen news/blog feeds, LLM-filtered for relevance, written to Notion. | ready to import |
| [`substack-monitor/`](substack-monitor/) | Weekly cron over AI + marketing Substack feeds. New issues filtered and filed to Notion. | ready to import |
| [`podcast-intake/`](podcast-intake/) | Twice-weekly: podcast RSS + Vimeo, transcribe, LLM topic extraction, write to Notion. Google Drive for transcripts. | ready to import |
| [`x-thought-leader-monitor/`](x-thought-leader-monitor/) | Weekly cron over a roster of X accounts, LLM relevance scoring, keepers to Notion. | ready to import |
| [`linkedin-profile-monitor/`](linkedin-profile-monitor/) | Weekly cron over a roster of LinkedIn profiles via a scraper API, new posts to Notion. | ready to import |
| [`web-capture-webhook/`](web-capture-webhook/) | Webhook for a browser extension/share target. Scrapes a URL (Reddit JSON, Firecrawl, WebCrawlerAPI fallback) to Notion. | ready to import |

## Publish + sync

| Workflow | What it does | Status |
|---|---|---|
| [`publish-social/`](publish-social/) | One webhook, publishes the same post to LinkedIn, X, Bluesky, Threads with per-channel formatting. | ready to import |
| [`linkedin-website-sync/`](linkedin-website-sync/) | Weekly cron that syncs recent LinkedIn posts to a JSON feed. Powers the activity feed on alecfoster.com. | ready to import |

## Ops

| Workflow | What it does | Status |
|---|---|---|
| [`error-handler-slack/`](error-handler-slack/) | Drop-in error workflow. Catches failures from any workflow and posts a formatted Slack alert. | ready to import |
| [`board-linkedin-monitor/`](board-linkedin-monitor/) | Weekly cron: scrapes LinkedIn posts from a roster, drafts comments via Claude, queues to Airtable. Cost-controlled. | coming soon |

## Why this exists

Every workflow here is something I built for myself, then sanitized so other people can fork and adapt. They are production pipelines, not no-code demos.

## How to import

1. Pick a workflow folder and download its `workflow.json`
2. n8n → **Workflows** → **Import from File**
3. The workflow imports with placeholder credential IDs (`REPLACE_WITH_*`) that won't resolve. Open each node that uses an external service, create the matching credential, and select it.
4. Point any Notion node at your own database ID.
5. Run once manually, then activate.

## What's been sanitized

- Credential references are placeholder IDs (`REPLACE_WITH_*`) — no API keys, OAuth tokens, or webhook secrets
- Workflow `id`/`versionId` and personal identifiers (Notion database IDs, monitored account rosters) are placeholders or samples
- Public source lists (RSS feeds, subreddits) are left in as working examples — swap them for your own

## License

MIT. Fork freely. If you ship something useful on top of these, a link back is appreciated.

