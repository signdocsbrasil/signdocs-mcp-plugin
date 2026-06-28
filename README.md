# SignDocs Brasil — Claude plugin & desktop extension

One-step ways to give Claude the [SignDocs Brasil](https://signdocs.com.br)
e-signature tools (create signing sessions, manage multi-signer envelopes, verify
documents, manage webhooks). Powered by
[`@signdocs-brasil/mcp-server`](https://www.npmjs.com/package/@signdocs-brasil/mcp-server).

This repo is **both** a Claude Code plugin and a Claude Code plugin marketplace,
plus the source for the Claude Desktop extension.

---

## Claude Code (CLI / IDE / web) — plugin

Connects to the **hosted** SignDocs MCP endpoint (nothing to run locally).

```
/plugin marketplace add signdocsbrasil/signdocs-mcp-plugin
/plugin install signdocs-brasil@signdocs-brasil
/plugin enable signdocs-brasil
```

On enable you're prompted for:

- **API credentials (Base64)** — base64 of `clientId:clientSecret` (from
  app.signdocs.com.br → API). Generate it with:
  ```bash
  printf '%s' "YOUR_CLIENT_ID:YOUR_CLIENT_SECRET" | base64
  ```
- **MCP endpoint URL** — defaults to homologação (`https://mcp-hml.signdocs.com.br/mcp`);
  set `https://mcp.signdocs.com.br/mcp` for production.

Credentials are stored in your OS keychain. Then just ask Claude, e.g. *"create a
SignDocs signing session for …"*.

### Stdio fallback (run the server locally)

Prefer to run the server yourself (no hosted endpoint, e.g. air-gapped or custom
build)? Skip the plugin and add the stdio server directly:

```bash
claude mcp add signdocs \
  -e SIGNDOCS_CLIENT_ID=your_client_id \
  -e SIGNDOCS_CLIENT_SECRET=your_client_secret \
  -e SIGNDOCS_ENVIRONMENT=hml \
  -- npx -y @signdocs-brasil/mcp-server
```

This requires Node.js locally and uses the exact same tools as the hosted endpoint.

---

## Claude Desktop — extension (.mcpb)

A one-click bundle that runs the server **locally via stdio** (the idiomatic mode
for Desktop). Download the `.mcpb` from
[Releases](https://github.com/signdocsbrasil/signdocs-mcp-plugin/releases),
double-click it, and enter your Client ID + Secret. Build instructions:
[`desktop-extension/`](./desktop-extension).

---

## What Claude can do

23 tools across signing sessions, multi-signer envelopes, documents,
transactions, evidence, public verification, and webhooks. Binding/quota actions
(create session, cancel, verify-document) are marked so clients confirm before
firing. See the [server README](https://www.npmjs.com/package/@signdocs-brasil/mcp-server)
for the full catalog.

> Start in `hml` (sandbox); switch to production only when you intend to create
> real, legally-binding signatures.

## License

MIT
