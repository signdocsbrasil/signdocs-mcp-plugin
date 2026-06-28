# SignDocs Brasil — Claude Desktop extension (.mcpb)

One-click Claude Desktop install for the SignDocs MCP server. Unlike the Claude
Code plugin (which talks to the hosted endpoint), this extension runs the
`@signdocs-brasil/mcp-server` **locally via stdio** — the idiomatic mode for
Claude Desktop extensions.

## Build the .mcpb

```bash
cd desktop-extension
npm install                      # populates node_modules (bundled into the .mcpb)
npx @anthropic-ai/mcpb validate manifest.json
npx @anthropic-ai/mcpb pack      # → signdocs-brasil-0.1.0.mcpb
```

Publish the resulting `.mcpb` on GitHub Releases (and link it from the site with
an "Add to Claude Desktop" button).

## Install (end user)

1. Download `signdocs-brasil-<version>.mcpb`.
2. Double-click it (or Claude Desktop → Settings → Extensions → Install from file).
3. Enter **Client ID** + **Client Secret** (from app.signdocs.com.br → API) and
   pick the environment (`hml` to start). Credentials are stored in the OS keychain.

Requires Node.js on the machine (Claude Desktop uses it to launch the server).
