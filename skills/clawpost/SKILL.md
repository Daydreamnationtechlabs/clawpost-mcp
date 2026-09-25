# Claw Post Skill

Use this skill when the user wants to post to social media (X, LinkedIn, Facebook, TikTok, Instagram) or comment on Reddit.

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
      "url": "https://mcp.clawpost.net/mcp"
    }
  }
}
```

## Tools

- `list_platforms` - Check which platforms are available
- `create_post` - Publish a post with text and optional media
- `create_reddit_comment` - Comment on a Reddit post or comment
- `get_upload_url` - Get a signed URL for media uploads
- `get_post_status` - Check the status of a posting job
- `get_account_status` - Verify pairing and account status

## Workflow

1. Call `get_account_status` to verify the extension is paired
2. Call `list_platforms` to see available platforms
3. If posting media, call `get_upload_url` first, upload the file, then include the URL in `create_post`
4. Call `create_post` or `create_reddit_comment`
5. Poll `get_post_status` to get the live post URL
