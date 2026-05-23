# Podcast Intake

Twice-weekly cron that pulls a configurable list of podcast RSS feeds, transcribes new episodes via OpenAI Whisper, asks Claude to extract topic ideas in your voice, and writes structured rows to a Notion intake database.

Inputs: list of RSS URLs + Notion database ID.
Output: ranked content ideas in Notion, ready for triage.

## Status

⚠️ Workflow JSON not yet sanitized for public release. See [content-pipeline](https://github.com/alectivism/) for the architecture.

## What it does

```
Tue + Fri 10am PT cron
  → For each RSS feed: get new episodes since last run
  → For each episode: download MP3, transcribe via Whisper API
  → Send transcript chunks to Claude with extraction prompt
  → Extract: topic_idea, hot_take_potential, relevance, utility, key_points
  → Write to Notion: one row per idea, status="not_started", score auto-computed
```

Then in Claude Code or your editor, you `/triage` the Notion queue and `/draft` the best ideas into LinkedIn / newsletter / blog posts.

## Coming soon

- Sanitized `workflow.json`
- Sample RSS list (5-10 AI/marketing podcasts)
- Notion database schema (intake row template)
- Extraction prompt template
