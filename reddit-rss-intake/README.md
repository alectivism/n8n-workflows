# Reddit RSS Intake

Weekly cron over ~25 subreddit RSS feeds. Dedupes and files high-signal threads to Notion.

Part of a personal content pipeline by [Alec Foster](https://www.alecfoster.com). Importable as a single n8n workflow JSON.

## What it does

Reads the `.rss` feed for a roster of subreddits (AI, n8n, Claude, vibecoding, ML communities), normalizes each post, removes duplicates against prior runs, and writes new threads to Notion as content ideas.

## At a glance

| | |
|---|---|
| Trigger | Schedule (cron) |
| Schedule | Weekly, Mon 14:00 |
| Nodes | 34 |
| Destination | Notion content database |

## Quick start

1. Open your n8n instance → **Workflows** → **Import from File** → pick `workflow.json`.
2. Replace the placeholder credentials (see below). The imported file ships with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders that won't resolve until you create your own.
3. Repoint the Notion database: the workflow references placeholder database IDs (`aaaaaaaa-0000-...`). Open each Notion node, pick your own database, and remap the property fields.
4. Set the workflow **Active**. The cron will fire on the schedule above.

## Credentials needed

| Service | n8n credential type | Notes |
|---|---|---|
| Notion | `notionApi` | Notion integration token (or swap the HTTP node for the native Notion node) |

Don't paste secrets into the JSON. n8n's credential store is encrypted; the JSON only references credential IDs.

## What's been sanitized

- Credential references replaced with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders
- All real Notion database/property IDs remapped to inert placeholder UUIDs (`aaaaaaaa-0000-4000-8000-…`)
- API tokens, Slack channel IDs, Google Drive folder IDs, and email addresses removed
- Environment-specific fields (`id`, `versionId`, `tags`, `active`, pinned data) stripped
