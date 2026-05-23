# Multi-Channel Social Publisher

One webhook → publishes the same post to **LinkedIn, X, Bluesky, and Threads** with per-channel formatting. The publish half of a content pipeline. Importable as a single n8n workflow JSON.

## What it does

A POST to the webhook with a body like:

```json
{
  "slug": "2026-05-22-eval-rubric",
  "channels": ["linkedin", "x", "bluesky", "threads"],
  "posts": {
    "linkedin": { "text": "<full post>", "image_url": "<optional>" },
    "x": { "text": "<280 chars>", "image_url": "<optional>" },
    "bluesky": { "text": "<300 chars>", "image_url": "<optional>" },
    "threads": { "text": "<post>", "image_url": "<optional>" }
  },
  "image_url": "<default if not in posts.*>"
}
```

…routes per `channels` array and posts to each enabled platform with the channel-specific text. Channels not listed are skipped.

## Quick start

1. Open your n8n instance → **Workflows** → **Import from File** → pick `workflow.json`
2. For each social node (X, Bluesky, Threads, LinkedIn), click → **Credentials** → create a new credential of the matching type. The placeholder IDs in the imported file (`REPLACE_WITH_*_CREDENTIAL_ID`) won't resolve until you do this.
3. Set the workflow to **Active**.
4. Get the production webhook URL from the trigger node.
5. POST to it from your content pipeline (curl, Claude Code, whatever).

## Credentials needed

| Channel | n8n credential type | How to create |
|---|---|---|
| LinkedIn | OAuth2 (Sign in with LinkedIn API) | LinkedIn Developer → Create app → add OAuth scope |
| X (Twitter) | OAuth2 | X Developer Portal → Create app with read+write |
| Bluesky | App password | bsky.app → Settings → App passwords |
| Threads | OAuth2 | Meta Developer Portal |

Don't paste your credentials into the JSON file. n8n's credential store is encrypted; the JSON only references credential IDs.

## Tested with

- n8n self-hosted v1.50+
- n8n cloud (any tier)
- Both single-account and multi-account workflows

## See also

This workflow is part of a larger personal content pipeline by [Alec Foster](https://www.alecfoster.com). The other half — podcast intake and idea extraction — is sketched in `../podcast-intake/`.
