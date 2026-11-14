# Installing Claw Post MCP

This is a remote MCP server. Nothing to clone or build.

## Quick Start

1. Add a remote server named `clawpost` with URL `https://mcp.clawpost.net/mcp` (Streamable HTTP).
2. Complete the OAuth prompt in the browser.
3. Tell the user to install the [Claw Post Chrome extension](https://chromewebstore.google.com/detail/clawpost/gebmgifdmnflfcehpbepkdnndkhgkchh), click its icon, sign in with Google, and stay logged in to the target social site. Short video guides are built into setup.
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

### Post
- `list_platforms`
- `create_post`
- `get_upload_url`

### Comment/Reply
- `create_reddit_comment`
- `create_x_reply` (any x.com status URL)
- `create_linkedin_comment`
- `create_facebook_comment` (`comment_id=` in targetUrl = threaded reply under that parent)
- `reply_to_comment` (routes by URL)

### DMs
- `create_linkedin_message` (20/day)

### Notifications
- `check_notifications` → `list_replies` → reply → `mark_reply_read`

### Jobs
- `get_post_status`
- `cancel_post`
- `submit_job_input` (resume `needs_input`)

### Account / groups
- `get_account_status`
- `join_facebook_group` (when the user asks, 5/day; do not auto-join)

## Troubleshooting

If `get_account_status` reports not paired:

1. Ensure the Chrome extension is installed and the icon shows as active
2. Click the extension icon and sign in with Google, or use the Dashboard 6-digit code
3. Stay logged in to your target social platforms in that Chrome profile
4. Retry the MCP connection

Support: https://clawpost.net/faq or mailto:leo@clawpost.net
