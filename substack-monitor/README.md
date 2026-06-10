# Substack Newsletters Monitor

Weekly cron over a set of AI/marketing Substack feeds. New issues get filtered and written to Notion.

Part of a personal content pipeline by [Alec Foster](https://www.alecfoster.com). Importable as a single n8n workflow JSON.

## What it does

Reads a roster of Substack `/feed` URLs (AI Snake Oil, Import AI, Nate's Note, and others), filters new issues, and files them to Notion.

## At a glance

| | |
|---|---|
| Trigger | Schedule (cron) |
| Schedule | Weekly, Mon 08:00 |
| Nodes | 13 |
| Destination | Notion content database |

## Quick start

1. Open your n8n instance → **Workflows** → **Import from File** → pick `workflow.json`.
2. Replace the placeholder credentials (see below). The imported file ships with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders that won't resolve until you create your own.
3. Repoint the Notion database: the workflow references placeholder database IDs (`aaaaaaaa-0000-...`). Open each Notion node, pick your own database, and remap the property fields.
4. Set the workflow **Active**. The cron will fire on the schedule above.

## Credentials needed

| Service | n8n credential type | Notes |
|---|---|---|
| HTTP Header Auth | `httpHeaderAuth` | Header-auth credential for the LLM/API used to filter issues |

Don't paste secrets into the JSON. n8n's credential store is encrypted; the JSON only references credential IDs.

## What's been sanitized

- Credential references replaced with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders
- All real Notion database/property IDs remapped to inert placeholder UUIDs (`aaaaaaaa-0000-4000-8000-…`)
- API tokens, Slack channel IDs, Google Drive folder IDs, and email addresses removed
- Environment-specific fields (`id`, `versionId`, `tags`, `active`, pinned data) stripped
