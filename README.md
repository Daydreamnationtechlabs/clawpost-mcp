<p align="center">
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

**Platforms:** X, LinkedIn, Facebook (feed and groups), TikTok, Instagram. Comments/replies on X, Facebook, LinkedIn, and Reddit. LinkedIn DMs. Notification checks.

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
      "type": "http",
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

## Tools (17)

| Tool | What it does |
| --- | --- |
| `list_platforms` | Platforms available to your paired Chrome |
| `create_post` | Publish a post (text, optional media) |
| `create_reddit_comment` | Comment on a Reddit post or comment URL |
| `create_x_reply` | Reply to any x.com status URL, including other people's posts |
| `create_linkedin_comment` | Comment on a LinkedIn post URL |
| `create_linkedin_message` | Send a LinkedIn DM to a 1st-degree connection (20/day) |
| `create_facebook_comment` | Comment on a Facebook post; `comment_id=` in the URL = threaded reply |
| `reply_to_comment` | Route a reply to the right platform tool from the target URL |
| `join_facebook_group` | Join a Facebook group when the user asks (5/day); does not auto-join |
| `submit_job_input` | Resume a `needs_input` job (login ack or questionnaire answers) |
| `list_replies` | List Reddit/Facebook/LinkedIn replies already saved from a check |
| `check_notifications` | Ask the paired browser to read notifications once |
| `mark_reply_read` | Mark a `list_replies` row seen in Claw Post only |
| `cancel_post` | Cancel a queued, processing, or needs_input job |
| `get_upload_url` | Signed upload URL for media |
| `get_post_status` | Poll a job; returns the live post URL on success |
| `get_account_status` | Pairing and account status |

Typical notifications loop: `check_notifications` → `list_replies` → `reply_to_comment` (or the platform tool) → `mark_reply_read`.

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

## License

MIT License. See [LICENSE](LICENSE) for details.
