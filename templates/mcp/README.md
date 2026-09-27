# Per-project MCP servers

Copy the file you need to `<repo>/.mcp.json` (or merge its `mcpServers` block). They load only in that project, keeping other sessions' context small.

- `playwright.mcp.json`: browser automation for UI tests and scraping.
- `supabase.mcp.json`: needs `SUPABASE_ACCESS_TOKEN` and `SUPABASE_PROJECT_REF` exported in your shell (token from https://supabase.com/dashboard/account/tokens). Never commit the values.
