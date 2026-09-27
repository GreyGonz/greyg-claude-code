# Changelog

## 2.0.0 — 2026-09-27

Breaking: skills-first, sonnet-first rewrite.

- Commands replaced by skills: `/plan-task`, `/review-diff`, `/test-fix`, `/commit`, `/explain`, `/docs`, `/project-init`, `/skills-sync`.
- Removed the Next.js/Supabase-specific commands (`api-*`, `component-new`, `page-new`, `types-gen`, `edge-function-new`); kept read-only under `legacy/commands/` until 2.1.
- Agents reduced from 12 to 8, all with restricted `tools`; `sonnet` everywhere except `system-architect` and `security-engineer` (`opus`). `orchestrator` became `/plan-task`; `learning-guide`, `deep-research-agent` and `backend-architect` merged into `/explain`, `tech-stack-researcher` and `system-architect`.
- MCP: only `context7` ships with the plugin. Playwright and Supabase moved to `templates/mcp/` for per-project `.mcp.json`.
- New `templates/` with `CLAUDE.md.tmpl`, per-stack conventions, settings and recommended community skills, consumed by `/project-init`.
- Removed `settings.template.json`, `.env.example`, `QUICK-START.md`, `PUBLISHING.md` (folded into README).

## 1.0.1

Last commands-based release (tag `v1.0.1`).
