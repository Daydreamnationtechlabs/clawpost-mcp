---
name: clawpost
description: Publish social posts and Reddit comments from the user's own logged-in desktop Chrome through the Claw Post MCP server and the paired Claw Post Chrome extension. Use when the user asks to post to X, LinkedIn, Facebook (their feed or a group they already belong to), TikTok or Instagram, to comment on a Reddit post, or to check whether a post went live.
license: MIT
compatibility: Requires network access to https://mcp.clawpost.net/mcp, a Claw Post account (clawpost.net), and the Claw Post Chrome extension paired in the user's desktop Chrome, which must be running and logged in to the target platform.
metadata:
  author: Daydream Nation Tech Labs
  version: "1.0.0"
  homepage: https://clawpost.net
---

# Claw Post Skill

Use this skill when the user wants to post to social media (X, LinkedIn, Facebook, TikTok, Instagram) or comment on a Reddit post.

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

## Tools

- `list_platforms` - Check which platforms are available
- `create_post` - Publish a post with text and optional media
- `create_reddit_comment` - Comment on a Reddit post
- `get_upload_url` - Get a signed URL for media uploads
- `get_post_status` - Check the status of a posting job
- `get_account_status` - Verify pairing and account status

## Workflow

1. Call `get_account_status` to verify the extension is paired
2. Call `list_platforms` to see available platforms
3. Show the user the exact text, target platform and target URL, and wait for their approval
4. If posting media, call `get_upload_url` first, upload the file, then include the URL in `create_post`
5. Call `create_post` or `create_reddit_comment`
6. Poll `get_post_status` to get the live post URL
