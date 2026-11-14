---
name: clawpost
description: Publish social posts and comments from the user's own logged-in desktop Chrome through the Claw Post MCP server and the paired Claw Post Chrome extension. Use when the user asks to post to X, LinkedIn, Facebook, TikTok or Instagram; to reply or comment on X, Facebook, LinkedIn, or Reddit; to send or read LinkedIn DMs; to check notifications; or to check whether a post went live.
license: MIT
compatibility: Requires network access to https://mcp.clawpost.net/mcp, a Claw Post account (clawpost.net), and the Claw Post Chrome extension paired in the user's desktop Chrome, which must be running and logged in to the target platform.
metadata:
  author: Daydream Nation Tech Labs
  version: "1.1.0"
  homepage: https://clawpost.net
---

# Claw Post Skill

Use this skill when the user wants to post to social media, comment or reply, send a LinkedIn DM, or check notifications.

## Setup

The user must have:
1. A Claw Post account at https://clawpost.net
2. The Chrome extension installed and paired
3. The MCP server connected with OAuth

## MCP Server

```json
{
  "mcpServers": {
    "clawpost": {
      "type": "http",
      "url": "https://mcp.clawpost.net/mcp"
    }
  }
}
```

## Tools (17)

- `list_platforms` - Check which platforms are available
- `create_post` - Publish a post with text and optional media
- `create_reddit_comment` - Comment on a Reddit post or comment URL
- `create_x_reply` - Reply to any x.com status URL
- `create_linkedin_comment` - Comment on a LinkedIn post URL
- `create_linkedin_message` - Send a LinkedIn DM (20/day)
- `create_facebook_comment` - Facebook comment; `comment_id=` = threaded reply
- `reply_to_comment` - Route a reply from the target URL
- `join_facebook_group` - Join a Facebook group when the user asks (5/day); do not auto-join
- `submit_job_input` - Resume a needs_input job
- `list_replies` - List saved replies from a check
- `check_notifications` - Read notifications once in the paired browser
- `mark_reply_read` - Mark a reply seen in Claw Post only
- `cancel_post` - Cancel a queued or processing job
- `get_upload_url` - Get a signed URL for media uploads
- `get_post_status` - Check the status of a posting job
- `get_account_status` - Verify pairing and account status

## Workflow

1. Call `get_account_status` to verify the extension is paired
2. Call `list_platforms` to see available platforms
3. Show the user the exact text, target platform and target URL, and wait for their approval
4. If posting media, call `get_upload_url` first, upload the file, then include the URL in `create_post`
5. Call the matching write tool (`create_post`, comment/reply tool, or `create_linkedin_message`)
6. Poll `get_post_status` to get the live post URL

Notifications loop: `check_notifications` → `list_replies` → `reply_to_comment` (or platform tool) → `mark_reply_read`.
