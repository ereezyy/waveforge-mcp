# WaveForge MCP server

WaveForge turns a song into a music video. This repo documents the hosted WaveForge MCP server. The server code itself is not in this repo; nothing here needs to be cloned or run.

- Endpoint: `https://waveforge.net/mcp`
- Transport: Streamable HTTP
- Website: https://waveforge.net

## Tools

| Tool | Key needed | What it does |
|---|---|---|
| `create_teaser` | No | 30-second teaser video, watermarked. Doesn't use any of your account's videos. |
| `create_render` | Yes (`wf_...`) | Full-length video with no watermark. Uses videos left on your account. |

## Use with Cline

WaveForge is a hosted MCP server at `https://waveforge.net/mcp` (Streamable HTTP). No install is needed.

Add this to `cline_mcp_settings.json` under `mcpServers`:

```json
"waveforge": {
  "type": "streamableHttp",
  "url": "https://waveforge.net/mcp",
  "disabled": false,
  "autoApprove": []
}
```

This gives the free `create_teaser` tool (30-second, watermarked). To also get `create_render` (full length, no watermark), add your WaveForge API key as a `headers` field inside the `waveforge` entry, next to `url`:

```json
"headers": { "Authorization": "Bearer wf_YOUR_API_KEY" }
```

See [llms-install.md](llms-install.md) for step-by-step instructions.

## Other MCP clients

Any client that supports Streamable HTTP can connect to `https://waveforge.net/mcp`, optionally with an `Authorization: Bearer wf_...` header.

## Support

See https://waveforge.net for support and terms.
