# Content Pipeline Error Handler — Slack Alert

Drop-in error workflow. Catches failures from any other workflow and posts a formatted alert to Slack. Set it as the error workflow on everything else.

## How it works

- **Trigger:** error trigger
- **Nodes:** 3
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Credentials to replace

Every credential ID in the JSON is a placeholder (`REPLACE_WITH_*`). After import, open each flagged node, create the matching credential in your own instance, and select it.

- Slack (OAuth2)

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
