---
name: clawpost
description: Publish social posts and comments from the user's own logged-in desktop Chrome through the Claw Post MCP server. Use when the user asks to post to X, LinkedIn, Facebook, TikTok or Instagram; reply on X/Facebook/LinkedIn/Reddit; send a LinkedIn DM; check notifications; or join a Facebook group they asked to join.
license: MIT
compatibility: Requires network access to https://mcp.clawpost.net/mcp, a Claw Post account (clawpost.net), and the Claw Post Chrome extension paired in the user's desktop Chrome, which must be running and logged in to the target platform.
metadata:
  author: Daydream Nation Tech Labs
  version: "1.1.0"
  homepage: https://clawpost.net
---

# Claw Post Skill

Use this skill when the user wants to post to social media, reply on X/Facebook/LinkedIn/Reddit, send LinkedIn DMs, check notifications, or join a Facebook group they asked to join.

## Setup

The user must have:
1. A Claw Post account at https://clawpost.net
2. The Chrome extension installed and paired (short video guides are built into setup)
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

### Post
- `list_platforms`
- `create_post`
- `get_upload_url`

### Comment/Reply
- `create_reddit_comment`
- `create_x_reply` (any x.com status URL)
- `create_linkedin_comment`
- `create_facebook_comment` (if `targetUrl` includes `comment_id=`, threaded reply under that parent; no top-level fallback)
- `reply_to_comment` (routes by URL)

### DMs
- `create_linkedin_message` (20/day). Reddit DMs are not supported.

### Notifications
- `check_notifications` → `list_replies` → reply → `mark_reply_read`

### Jobs / account
- `get_post_status`, `cancel_post`, `submit_job_input` (resume `needs_input`)
- `get_account_status`
- `join_facebook_group` when the user asks (5/day); do not auto-join

## Workflow

1. Call `get_account_status` to verify the extension is paired
2. Call `list_platforms` to see available platforms
3. For replies/notifications: `check_notifications` → `list_replies` → platform reply tool → `mark_reply_read`
4. If posting media, call `get_upload_url` first, upload the file, then include the URL in `create_post`
5. Call the appropriate create tool
6. Poll `get_post_status` for the live URL (or handle `needs_input` with `submit_job_input`)
