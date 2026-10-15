# gopuff-plugin

Team marketplace with one plugin, `gopuff`, that connects Grok Bot to
Gopuff's official MCP server.

## Plugins

| Plugin | MCP server | Clients |
|---|---|---|
| `gopuff` | `https://mcp.gopuff.com/mcp` | Grok Bot only (`cursor: "never"`) |

The MCP config is URL-only with `"placement": "server"`, so sign-in uses
standard MCP OAuth with dynamic client registration at
`https://goauth.gopuff.com/oauth/register`.

## Sign-in status

As of 2026-10-15, Gopuff's registration endpoint only accepts
`http://127.0.0.1:<port>/callback` redirect URIs, so sign-in fails until
Gopuff allowlists the Cursor and Grok Bot callbacks:

- `https://www.cursor.com/agents/mcp/oauth/callback` and
  `http://localhost:8787/callback` (sent together in one registration)
- `https://www.cursor.com/bot/mcp/oauth/callback` and
  `grokbot://mcp/oauth/callback` (Grok Bot mobile)

## Using it

1. Cursor dashboard → Plugins → Marketplaces → import from repository, URL
   `https://github.com/minupalaniappan/gopuff-plugin`. Registering it for a
   team requires team admin (or the team's "allow third-party plugin imports"
   setting). The Cursor GitHub App must have access to this repository.
2. Set the team marketplace policy for `gopuff` (Required, Default or
   Optional), or install it per user from Settings → Plugins.
3. Members governed by an MCP allowlist also need
   `https://mcp.gopuff.com/mcp` admitted by the team's MCP policy.
4. Fully relaunch Grok Bot, open the plugin, and authenticate under Accounts.

## Updating

Edit `third_party/gopuff`, bump `version` in
`third_party/gopuff/.cursor-plugin/plugin.json`, add a CHANGELOG entry, run
the validator, and push to `main`.

## Validation

```
npm install --no-save ajv ajv-formats
node scripts/validate-plugins.mjs
```
