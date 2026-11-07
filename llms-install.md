# Installing the WaveForge MCP server in Cline

WaveForge is a hosted (remote) MCP server. There is nothing to clone, build, or run locally.

- Endpoint: `https://waveforge.net/mcp`
- Transport: Streamable HTTP (`"type": "streamableHttp"`)

## Steps for Cline

1. Open the Cline MCP settings file (`cline_mcp_settings.json`). In the IDE extension: MCP Servers icon > Configure > Configure MCP Servers. In the CLI: `~/.cline/data/settings/cline_mcp_settings.json`.
2. Add one of the entries below under `mcpServers`. Keep any existing servers.
3. Save. Cline connects automatically. Confirm the `waveforge` server shows as connected and lists its tools.

### Option A: free, no API key

Gives the `create_teaser` tool (a 30-second watermarked teaser video).

```json
{
  "mcpServers": {
    "waveforge": {
      "type": "streamableHttp",
      "url": "https://waveforge.net/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

### Option B: with a WaveForge API key

Adds the `create_render` tool (full-length video, no watermark, uses videos on your WaveForge account). Ask the user for their WaveForge API key (it starts with `wf_`). Do not invent one, and do not print it back.

```json
{
  "mcpServers": {
    "waveforge": {
      "type": "streamableHttp",
      "url": "https://waveforge.net/mcp",
      "headers": {
        "Authorization": "Bearer wf_YOUR_API_KEY"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

CLI alternative:

```bash
cline mcp add waveforge https://waveforge.net/mcp --transport http --yes
# with a key:
cline mcp add waveforge https://waveforge.net/mcp --transport http --header "Authorization: Bearer wf_YOUR_API_KEY" --yes
```

## Check it works

- Without a key, the tool list should contain `create_teaser`.
- With a valid key, `create_render` should also appear.
- `create_teaser` needs `title` and a public `audioUrl`; `artist` and `imageUrl` are optional.

## Troubleshooting

- Not connecting: make sure `"type": "streamableHttp"` is set. Without it Cline uses the legacy SSE transport.
- Auth errors: re-check the key and the `Authorization: Bearer ...` header.
- Render errors: check that the audio link points to a public audio file.
