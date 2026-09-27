# Project templates

Consumed by `/project-init`; usable by hand.

| File | Copy to | Notes |
|---|---|---|
| `CLAUDE.md.tmpl` | `<repo>/CLAUDE.md` | Replace `{{...}}` placeholders; keep it under ~35 lines. |
| `<stack>/conventions.md` | inlined into CLAUDE.md `## Convenciones` | Drop lines that do not apply to the repo. |
| `<stack>/settings.json` | `<repo>/.claude/settings.json` | Only rules the global settings do not already cover. |
| `<stack>/skills.txt` | run each line | Community skills via `npx skills add … --copy`; lock lands in `skills-lock.json`. |
| `docs/agents-and-skills.md.tmpl` | `<repo>/docs/agents-and-skills.md` | Delegation table; only if the repo keeps a `docs/`. |
| `mcp/*.mcp.json` | `<repo>/.mcp.json` | Per-project MCP servers (see `mcp/README.md`). |

Stack conventions that apply everywhere (type hints, gofmt, `<script setup>`…) live in the dotfiles `~/.claude/rules/`, not here.
