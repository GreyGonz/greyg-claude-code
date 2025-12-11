# MCP Servers Included

This plugin includes 3 pre-configured MCP servers that enhance Claude Code's capabilities.

## Included Servers

### 1. **Context7** (`@upstash/context7-mcp`)
**Purpose**: Access up-to-date, version-specific documentation for any library

**Usage**: Just mention "use context7" in your prompt when you need current library documentation

**Benefits**:
- Always up-to-date docs
- Version-specific information
- Works with thousands of libraries
- No manual searching required

### 2. **Playwright** (`@playwright/mcp`)
**Purpose**: Browser automation and web testing

**Capabilities**:
- Navigate websites
- Take screenshots
- Interact with web elements
- Generate test code
- Access accessibility trees

**Use Cases**:
- E2E testing
- Web scraping
- Browser automation
- Visual testing

### 3. **Supabase** (`@supabase/mcp-server-supabase`)
**Purpose**: Supabase database operations

**Capabilities**:
- Query databases
- Manage tables
- Execute SQL
- Handle authentication
- Work with storage

**Use Cases**:
- Database management
- Schema exploration
- Data queries
- Admin operations

**Required Setup**:
1. Generate a personal access token at https://supabase.com/dashboard/account/tokens
2. Find your project reference in your Supabase project dashboard URL: `https://supabase.com/dashboard/project/[PROJECT_REF]`
3. Set environment variables:
   ```bash
   export SUPABASE_ACCESS_TOKEN="your-personal-access-token"
   export SUPABASE_PROJECT_REF="your-project-ref"
   ```
4. Add to your shell config file (`~/.bashrc`, `~/.zshrc`, etc.) to persist
5. Restart Claude Code

**Security Notes**:
- Never commit access tokens to version control
- The MCP server is scoped to a specific project via `--project-ref` flag
- For read-only access, you can add `--read-only` flag to the args in `.mcp.json`

## Servers Not Included (Not Yet Available)

The following servers were requested but don't have official MCP implementations yet:

- **chrome-devtools** - No official MCP server found
- **stripe** - No official MCP server found (as of Oct 2025)
- **vercel** - No official MCP server found

## Using MCP Servers

After installing this plugin:

1. **Automatic Activation**: MCP servers start automatically when you use the plugin
2. **Restart Required**: Restart Claude Code after plugin installation
3. **Tool Access**: MCP tools appear in Claude's available tools list

## Adding More MCP Servers

You can add custom MCP servers to your local `.claude/.mcp.json`:

```json
{
  "server-name": {
    "command": "npx",
    "args": ["-y", "package-name"],
    "env": {
      "API_KEY": "your-key"
    }
  }
}
```

## Troubleshooting

**MCP servers not loading?**
1. Restart Claude Code
2. Check that npm/npx is installed
3. Verify network connection (MCP servers download on first use)

**Performance issues?**
- MCP servers run on-demand
- First use may be slower (package download)
- Subsequent uses are fast

## Learn More

- Official MCP Documentation: https://modelcontextprotocol.io
- Claude Code MCP Guide: https://docs.claude.com/en/docs/claude-code/mcp
- MCP Server Directory: https://mcpcat.io
