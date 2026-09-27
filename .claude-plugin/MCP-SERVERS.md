# MCP servers

The plugin bundles a single server, declared in `.mcp.json`:

| Server | Tools | Why it ships with the plugin |
|---|---|---|
| `context7` | `resolve-library-id`, `query-docs` | Current library docs for any stack; two tools, negligible context cost. |

Servers that are only useful in some projects are **not** bundled, because every bundled server adds its tool schemas to every session. Copy them per project from `templates/mcp/`:

| Snippet | Use in |
|---|---|
| `templates/mcp/playwright.mcp.json` | Repos with browser tests or scraping. |
| `templates/mcp/supabase.mcp.json` | Supabase projects; needs `SUPABASE_ACCESS_TOKEN` and `SUPABASE_PROJECT_REF` in the shell. |

Allow the context7 tools without prompts in your user settings:

```json
"permissions": { "allow": [
  "mcp__plugin_greyg-claude-code-config_context7__resolve-library-id",
  "mcp__plugin_greyg-claude-code-config_context7__query-docs"
] }
```
