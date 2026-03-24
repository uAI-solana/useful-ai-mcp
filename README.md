# Useful AI MCP Server

A fully dynamic MCP server for [Useful AI](https://usefulai.fun), a shared tool library for AI agents.

Your agent gets a curated, auto-updating list of tools as native MCP tools. The server tracks which tools are called most and promotes them automatically, so your agent always has the best tools available without any config changes.

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

## How it works

When your agent connects, the MCP server returns a dynamic list of individually named tools based on real usage data. Your agent sees tools like `useful_mock-data-generator`, `useful_batch-regex-tester`, and `useful_css-inline-tool` right in its tool list. It can call them directly with typed parameters, no dispatch step needed.

The tool list refreshes automatically. As new tools get built and used on the platform, they get promoted into the named list your agent receives.

## Tools

### Named tools (dynamic)

The server exposes 20+ of the most popular tools as individually named MCP tools. These change over time as usage patterns shift. Examples:

- `useful_mock-data-generator`
- `useful_batch-slug-generator`
- `useful_batch-regex-tester`
- `useful_address-string-parser`
- `useful_password-policy-validator`
- `useful_hallucination-tripwire`
- `useful_css-inline-tool`

Each named tool has a typed input schema, so your agent knows exactly what parameters to send.

### `useful_dispatch`

Catch-all for 200+ tools beyond the named ones. Describe what you need and send your data. The server matches your task to the best tool via semantic search and returns the result.

### `useful_suggest`

Request a tool that doesn't exist yet. Popular suggestions get built first.

## Why dynamic?

Static MCP servers give your agent a fixed tool list. If a new tool gets added, you have to update your config. With Useful AI, the server decides which tools to surface based on what people actually use. Your agent's capabilities grow without you touching anything.

This also saves tokens. When your agent sees a named tool like `useful_batch-regex-tester`, it calls it directly instead of reasoning about which tool to pick and writing a natural language description for a generic dispatch endpoint.

## Links

- **Website:** https://usefulai.fun
- **Docs:** https://usefulai.fun/docs
- **Skills (non-MCP):** https://github.com/uAI-solana/useful-ai-skills
