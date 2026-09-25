<![CDATA[<p align="center">
  <img src="logo.png" alt="Claw Post" width="200" height="200" />
</p>

# Claw Post MCP

The third path for agent social posting. Not an API aggregator. Not a cloud VM browser.
Your agent calls our MCP, and your own logged-in desktop Chrome publishes. No platform API keys.

- **Homepage:** https://clawpost.net
- **Remote MCP:** `https://mcp.clawpost.net/mcp` (Streamable HTTP, OAuth)
- **Official MCP Registry:** `io.github.Daydreamnationtechlabs/clawpost`
- **Chrome extension:** [Install from Chrome Web Store](https://chromewebstore.google.com/detail/clawpost/gebmgifdmnflfcehpbepkdnndkhgkchh)
- **OpenClaw skill:** `openclaw skills install @daydreamnationtechlabs/clawpost`

**Platforms:** X, LinkedIn, Facebook (feed and groups you already belong to), TikTok, Instagram, plus Reddit comments.

## Setup

1. Sign up at https://clawpost.net
2. Install the Chrome extension, click its icon and sign in with Google (auto-pairs)
3. Stay logged in to the social sites in that Chrome profile
4. Connect your MCP client and complete OAuth

### Claude Code

```bash
claude mcp add --transport http clawpost https://mcp.clawpost.net/mcp
```

### Cursor

Add to your MCP settings (`.cursor/mcp.json` or global settings):

```json
{
  "mcpServers": {
    "clawpost": {
      "url": "https://mcp.clawpost.net/mcp"
    }
  }
}
```

### Cline

Add to your MCP settings:

```json
{
  "mcpServers": {
    "clawpost": {
      "url": "https://mcp.clawpost.net/mcp"
    }
  }
}
```

### Windsurf

Add to your MCP settings:

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

| Tool | What it does |
| --- | --- |
| `list_platforms` | Platforms available to your paired Chrome |
| `create_post` | Publish a post (text, optional media) |
| `create_reddit_comment` | Comment on a Reddit post or comment URL |
| `get_upload_url` | Signed upload URL for media |
| `get_post_status` | Poll a job; returns the live post URL on success |
| `get_account_status` | Pairing and account status |

## How it works

Your agent sends a job to our MCP. Our Chrome extension runs it inside your real desktop Chrome session. Your social logins never leave your browser, and nothing is shared with the model.

```
Agent  ──MCP call──▶  Claw Post Server  ──job──▶  Chrome Extension  ──post──▶  Social Platform
                            │
                      OAuth auth
```

The extension waits for jobs, executes them in the context of your logged-in tabs, and reports success or failure back to the MCP.

## Security

- Your social credentials never leave your browser
- OAuth authentication for the MCP connection
- No platform API keys required or stored
- Report security issues to human@daydreamnation.io

## Not affiliated with clawpost.dev

Claw Post (clawpost.net) is not affiliated with clawpost.dev, which is a different product.

## License

MIT License. See [LICENSE](LICENSE) for details.
]]>