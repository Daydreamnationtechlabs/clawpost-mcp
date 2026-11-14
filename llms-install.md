# Installing Claw Post MCP

This is a remote MCP server. Nothing to clone or build.

## Quick Start

1. Add a remote server named `clawpost` with URL `https://mcp.clawpost.net/mcp` (Streamable HTTP).
2. Complete the OAuth prompt in the browser.
3. Tell the user to install the [Claw Post Chrome extension](https://chromewebstore.google.com/detail/clawpost/gebmgifdmnflfcehpbepkdnndkhgkchh), click its icon, sign in with Google, and stay logged in to the target social site.
4. Verify with `get_account_status`. If it reports not paired, the user must finish step 3.

## MCP Configuration

```json
{
  "mcpServers": {
    "clawpost": {
      "url": "https://mcp.clawpost.net/mcp"
    }
  }
}
```

## Available Tools (17)

- `list_platforms` - Platforms available to the paired Chrome
- `create_post` - Publish a post (text, optional media)
- `create_reddit_comment` - Comment on a Reddit post or comment URL
- `create_x_reply` - Reply to any x.com status URL
- `create_linkedin_comment` - Comment on a LinkedIn post URL
- `create_linkedin_message` - LinkedIn DM to a 1st-degree connection (20/day)
- `create_facebook_comment` - Facebook comment; `comment_id=` = threaded reply
- `reply_to_comment` - Route a reply from the target URL
- `join_facebook_group` - Join a Facebook group when the user asks (5/day)
- `submit_job_input` - Resume a needs_input job
- `list_replies` - List saved replies from a check (never loads a page)
- `check_notifications` - Read Reddit/Facebook/LinkedIn notifications once
- `mark_reply_read` - Mark a reply seen in Claw Post only
- `cancel_post` - Cancel a queued, processing, or needs_input job
- `get_upload_url` - Signed upload URL for media
- `get_post_status` - Poll a job; returns the live post URL on success
- `get_account_status` - Pairing and account status

Notifications loop: `check_notifications` → `list_replies` → `reply_to_comment` → `mark_reply_read`.

## Troubleshooting

If `get_account_status` reports not paired:

1. Ensure the Chrome extension is installed and the icon shows as active
2. Click the extension icon and sign in with Google
3. Stay logged in to your target social platforms in that Chrome profile
4. Retry the MCP connection
