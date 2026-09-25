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

## Available Tools

- `list_platforms` - Platforms available to the paired Chrome
- `create_post` - Publish a post (text, optional media)
- `create_reddit_comment` - Comment on a Reddit post or comment URL
- `get_upload_url` - Signed upload URL for media
- `get_post_status` - Poll a job; returns the live post URL on success
- `get_account_status` - Pairing and account status

## Troubleshooting

If `get_account_status` reports not paired:

1. Ensure the Chrome extension is installed and the icon shows as active
2. Click the extension icon and sign in with Google
3. Stay logged in to your target social platforms in that Chrome profile
4. Retry the MCP connection
