# Authentication

## Getting Your Credentials

1. Log in to [voizematic.ai](https://voizematic.ai)
2. Go to **Settings → API / MCP**
3. Copy your **Client ID** and **Client Secret** — treat these like a password, never commit them to version control

## Using Your Credentials

Pass your Client ID and Client Secret as headers when configuring the MCP server:

```json
{
  "mcpServers": {
    "voizematic": {
      "type": "url",
      "url": "https://voizematic.ai/mcp",
      "headers": {
        "X-Client-ID": "YOUR_VOIZEMATIC_CLIENT_ID",
        "X-Client-Secret": "YOUR_VOIZEMATIC_CLIENT_SECRET"
      }
    }
  }
}
```

## Security Best Practices

- **Never commit your credentials** to version control
- Use environment variables when building custom integrations
- Rotate your Client Secret regularly from the dashboard
- Both credentials are scoped to your account — anyone with them has full access

## Scopes

All credentials currently have full access to your Voizematic account. Granular scopes (read-only, campaign-only, etc.) are on the roadmap.

## Rate Limits

| Plan | Requests/min |
|---|---|
| Free | 30 |
| Pro | 120 |
| Enterprise | Unlimited |

If you hit rate limits, Claude will surface the error and suggest retrying.
