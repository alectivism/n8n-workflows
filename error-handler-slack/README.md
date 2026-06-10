# Error Handler → Slack Alert

Drop-in error workflow. Catches failures from any other workflow and posts a formatted alert to Slack. No auto-retry, no silent failures: you find out the moment something breaks.

Part of a personal content pipeline by [Alec Foster](https://www.alecfoster.com). Importable as a single n8n workflow JSON.

## What it does

Triggers on n8n's **Error Trigger**, which fires whenever a workflow that names this one as its error workflow fails. It formats the failing workflow's name, the error message, and the node that threw, then posts a single message to a Slack channel.

## At a glance

| | |
|---|---|
| Trigger | Error trigger |
| Schedule | On error (no cron) |
| Nodes | 3 |
| Destination | Slack |

## Quick start

1. Open your n8n instance → **Workflows** → **Import from File** → pick `workflow.json`.
2. Click the Slack node → **Credentials** → create a Slack OAuth2 credential (replace the `REPLACE_WITH_SLACKOAUTH2API_CREDENTIAL_ID` placeholder).
3. Set the channel: the node references a placeholder channel ID (`REPLACE_WITH_SLACK_CHANNEL_ID`). Pick your own.
4. Set the workflow **Active**.
5. On every other workflow you want monitored: **Settings** → **Error Workflow** → select this one.

## Credentials needed

| Service | n8n credential type | Notes |
|---|---|---|
| Slack | `slackOAuth2Api` | Slack app with `chat:write` scope, installed to your workspace |

Don't paste secrets into the JSON. n8n's credential store is encrypted; the JSON only references credential IDs.

## What's been sanitized

- Credential references replaced with `REPLACE_WITH_*_CREDENTIAL_ID` placeholders
- Slack channel ID replaced with `REPLACE_WITH_SLACK_CHANNEL_ID`
- Any Notion IDs remapped to inert placeholder UUIDs
- Environment-specific fields (`id`, `versionId`, `tags`, `active`, pinned data) stripped
