# n8n Workflow Templates

Importable n8n workflows for content pipelines, monitoring, and AI agent ops. Each workflow ships as a self-contained JSON file you can drop into your own n8n instance, plus a README explaining what it does and what credentials it needs.

## Available workflows

| Workflow | What it does | Status |
|---|---|---|
| [`publish-social/`](publish-social/) | One webhook → publishes the same post to LinkedIn, X, Bluesky, Threads with per-channel formatting | ✅ ready to import |
| [`board-linkedin-monitor/`](board-linkedin-monitor/) | Weekly cron: scrapes LinkedIn posts from a roster, generates draft comments via Claude, queues to Airtable for review. Cost-controlled with kill-switch. | ✅ ready to import (sanitize roster + IDs first) |
| [`podcast-intake/`](podcast-intake/) | Twice-weekly cron: pulls podcast RSS feeds → transcribes via OpenAI Whisper → extracts topic ideas via Claude → writes to Notion | ⚠️ coming soon |

## Why this exists

Every workflow here is something I built for myself, then sanitized so other people can fork and adapt. They are not no-code demos — they are battle-tested pipelines running in production for [me](https://www.alecfoster.com) or my org.

Each workflow includes:
- The exported JSON (one file, importable directly)
- A README with: what it does, request/response schema (for webhook-triggered ones), credentials list, and tested-with notes
- A `spec.md` documenting design decisions

## How to import a workflow

1. Pick a workflow folder
2. Open your n8n instance (cloud or self-hosted)
3. **Workflows** → **Import from File** → select the `.json`
4. The workflow appears with **placeholder credential IDs** that won't resolve until you replace them. Click each node that uses external services, hit **Credentials**, create new credentials of the matching type, save.
5. Test the workflow manually before turning on the active toggle.

## What's been sanitized

- All credential references have placeholder IDs (`REPLACE_WITH_X_CREDENTIAL_ID`, etc.)
- No real API keys, OAuth tokens, or webhook secrets
- Workflow `id`, `versionId`, `tags`, and `active` flags stripped (these are environment-specific)
- For workflows that reference internal datasets (e.g., board roster), the data is replaced with a sample so you can see the shape

## License

MIT. Fork freely. If you ship something useful built on top of these, link back.

## Credit

Built by [Alec Foster](https://www.alecfoster.com), Chief Agent Officer & Responsible AI Lead at the Marketing + Media Alliance.
