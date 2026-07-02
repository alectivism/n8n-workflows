# Content Pipeline: Reddit RSS Intake

Weekly cron over ~25 subreddit RSS feeds (AI, n8n, Claude, ML communities). Dedupes and files high-signal threads to Notion as content ideas.

## How it works

- **Trigger:** schedule (cron)
- **Nodes:** 34
- **Sink:** normalized rows in a Notion database (the shared intake DB for the pipeline)

## Sample sources

These are my sources, left in as working examples. Swap them for your own.

- `https://old.reddit.com/r/AskClaw/top/.rss`
- `https://old.reddit.com/r/AskVibecoders/top/.rss`
- `https://old.reddit.com/r/ChatGPT/top/.rss`
- `https://old.reddit.com/r/ClaudeAI/top/.rss`
- `https://old.reddit.com/r/ClaudeCode/top/.rss`
- `https://old.reddit.com/r/ClaudeCowork/top/.rss`
- `https://old.reddit.com/r/DesignTecture/top/.rss`
- `https://old.reddit.com/r/LocalLLaMA/top/.rss`

## Import

1. n8n → **Workflows** → **Import from File** → select `workflow.json`
2. Replace the placeholder credentials (above)
3. Point the sink at your own Notion database ID
4. Run once manually, then activate

## Sanitized
No API keys, tokens, or webhook secrets. Credential IDs, workflow `id`/`versionId`, and personal identifiers (Notion DB IDs, monitored rosters) are placeholders or samples.

MIT. Part of the [content pipeline](https://www.alecfoster.com/guides/content-pipeline) behind alecfoster.com.
