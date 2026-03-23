# Useful AI MCP Server

Remote MCP server for [Useful AI](https://usefulai.fun), a shared tool library for AI agents.

Connect your agent and get two tools: `useful` (describe a task, send data, get the result) and `suggest` (request a tool that doesn't exist yet). Semantic matching finds the right tool automatically.

No keys, no auth. Free to use.

```
https://api.usefulai.fun/mcp
```

## Setup

### Claude Code

```bash
claude mcp add --transport http useful-ai https://api.usefulai.fun/mcp
```

### Gemini CLI

```bash
gemini mcp add --transport http useful-ai https://api.usefulai.fun/mcp
```

### Cursor

Add to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "useful-ai": {
      "url": "https://api.usefulai.fun/mcp"
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "useful-ai": {
      "type": "http",
      "url": "https://api.usefulai.fun/mcp"
    }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "useful-ai": {
      "serverUrl": "https://api.usefulai.fun/mcp"
    }
  }
}
```

### OpenCode

Add to `opencode.json`:

```json
{
  "mcp": {
    "useful-ai": {
      "type": "remote",
      "url": "https://api.usefulai.fun/mcp",
      "enabled": true
    }
  }
}
```

### Zed

Add to `.zed/settings.json`:

```json
{
  "context_servers": {
    "useful-ai": {
      "source": "custom",
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://api.usefulai.fun/mcp"],
      "env": {}
    }
  }
}
```

Requires Node.js. Uses mcp-remote as a bridge until Zed ships native HTTP support.

## Tools

### `useful`

Describe what you need and send your data. The server matches your task to the best tool and returns the result.

### `suggest`

Request a tool that doesn't exist yet. Popular suggestions get built first.

## Links

- **Website:** https://usefulai.fun
- **Docs:** https://usefulai.fun/docs
- **Skills (non-MCP):** https://github.com/uAI-solana/useful-ai-skills
