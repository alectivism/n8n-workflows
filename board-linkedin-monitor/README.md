# Board LinkedIn Monitor

Weekly cron that scrapes LinkedIn posts from a configurable roster of accounts (board members, key prospects, partner orgs, etc.) and uses Claude to generate 2-3 draft comments per post. Drafts queue to Airtable for human review — **no auto-posting**.

Built around a strict cost ceiling. See `spec.md` for full design.

## Status

Sanitized export coming soon. The workflow currently lives in [board-linkedin-monitor](https://github.com/alectivism/board-linkedin-monitor) (private). Open an issue or DM if you want early access to a sanitized version.

## What it does

```
Weekly cron (Mon 8am ET)
  → Load roster from Code node
  → For each member: scrape latest LinkedIn post via Apify
  → For each post: ask Claude for 3 candidate comments in your CEO/voice
  → Write to Airtable: post URL, comments, status="ready_for_review"
```

Cost-controlled:
- `limit=1` per Apify scrape (latest post only) → $0.005/event
- Roster Code node has `ENABLED_TIERS = []` kill switch
- Weekly cadence, not daily
- Math: ~$0.25/week at 50 members, ~$0.55/week at 110 members

## Coming soon

- Sanitized `workflow.json`
- Sample 10-person roster (replace with your own)
- Airtable base template with the right field schema
- Voice prompt template (replace `{{LEADER_VOICE_DESCRIPTION}}`)
