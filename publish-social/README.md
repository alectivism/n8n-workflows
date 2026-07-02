# Multi-Channel Social Publisher

One webhook → publishes the same post to X, Bluesky, Threads, and LinkedIn with per-channel formatting. The publish half of a content pipeline. Importable as a single n8n workflow JSON.

## What it does

A POST to the webhook (path `content-publish`) with a body like:

```json
{
  "slug": "2026-05-22-eval-rubric",
  "channels": ["x", "bluesky", "threads", "linkedin"],
  "posts": {
    "x": { "text": "<=280 chars>" },
    "bluesky": { "thread": ["<=300 chars>", "<optional continuation>"] },
    "threads": { "text": "<post>" },
    "linkedin": { "text": "<post>" }
  }
}
```

Routes per the `channels` array and posts to each enabled platform. Channels not listed are skipped, and each posts independently so one failed channel doesn't sink the others.

## Quick start

1. Import `workflow.json` (n8n → **Workflows** → **Import from File**).
2. **X** posts through an n8n OAuth2 credential. Create it and select it on the X node — the placeholder `REPLACE_WITH_*_CREDENTIAL_ID` won't resolve until you do.
3. **Bluesky**, **Threads**, and **LinkedIn** authenticate through n8n instance **Variables** read by Code nodes, not the credential store. Set: `BSKY_HANDLE`, `BSKY_APP_PASSWORD`, `THREADS_USER_ID`, `THREADS_ACCESS_TOKEN`, `LINKEDIN_ACCESS_TOKEN`, `LINKEDIN_AUTHOR_URN` (e.g. `urn:li:person:xxxx`).
4. Set the workflow **Active** and copy the production webhook URL from the trigger node.
5. POST to it from your content pipeline.

## Credentials and variables

| Channel | Auth | Where to get it |
|---|---|---|
| X (Twitter) | n8n OAuth2 credential | X Developer Portal → app with read + write |
| Bluesky | instance Variables (`BSKY_HANDLE`, `BSKY_APP_PASSWORD`) | bsky.app → Settings → App passwords |
| Threads | instance Variables (`THREADS_USER_ID`, `THREADS_ACCESS_TOKEN`) | Meta Developer Portal |
| LinkedIn | instance Variables (`LINKEDIN_ACCESS_TOKEN`, `LINKEDIN_AUTHOR_URN`) | LinkedIn Developer app with `w_member_social` (API access is gated by LinkedIn) |

Don't paste secrets into the JSON. Credential IDs and Variables are resolved by your own n8n instance.

## See also

Part of a personal content pipeline by [Alec Foster](https://www.alecfoster.com/guides/content-pipeline). The intake half is in [`../podcast-intake/`](../podcast-intake/), and the source monitors are the other folders in this repo.
