# greyg-claude-code

Personal Claude Code plugin: cost-aware skills, focused agents and project templates for Python, Vue 3 + PrimeVue, Java Quarkus, Go and TypeScript. Machine-specific settings (permissions, hooks, status line, global CLAUDE.md) live in a separate dotfiles repo.

## Install

```
/plugin marketplace add GreyGonz/greyg-claude-code
/plugin install greyg-claude-code-config@greyg-claude-code
```

Update: `/plugin marketplace update greyg-claude-code` then `/plugin update greyg-claude-code-config@greyg-claude-code`, restart Claude Code.

## Skills

| Skill | Model | What it does |
|---|---|---|
| `/plan-task <task>` | session model | Phased plan plus delegation map; stops for approval. The only place worth an expensive model. |
| `/review-diff [base]` | sonnet, forked | Reviews the diff for bugs, security, tests and conventions. Read-only. |
| `/test-fix [cmd]` | sonnet | Runs lint/tests from CLAUDE.md (or detects the stack), fixes, re-runs; max 3 rounds. |
| `/commit [--all] [--es] [scope]` | sonnet | Conventional Commits from the staged diff. Never pushes or amends. |
| `/explain <target>` | sonnet, forked | Explains a file, symbol or behaviour with `file:line` references. |
| `/docs <target>` | sonnet | Writes or refreshes docs from the code (Spanish by default). |
| `/project-init [stack] [--dry-run]` | sonnet | Scaffolds `CLAUDE.md`, `.claude/settings.json`, `docs/agents-and-skills.md` from `templates/`. |
| `/skills-sync` | sonnet | Checks/updates community skills from `skills-lock.json`; protects local edits. |

## Agents

| Agent | Model | Use for |
|---|---|---|
| `system-architect` | opus | System, API and data design for medium/large changes (read-only). |
| `security-engineer` | opus | Vulnerability review of code or a diff (read-only). |
| `frontend-architect` | sonnet | UI structure, state, accessibility, performance (Vue/React). |
| `requirements-analyst` | sonnet | Scope, acceptance criteria, open questions. |
| `tech-stack-researcher` | sonnet | Library/approach comparisons with current docs (context7 + web). |
| `performance-engineer` | sonnet | Measured bottleneck analysis and targeted fixes. |
| `refactoring-expert` | sonnet | Behaviour-preserving restructuring backed by tests. |
| `technical-writer` | sonnet | README, guides, ADRs, API docs. |

Subagents without an explicit model follow `CLAUDE_CODE_SUBAGENT_MODEL` from your settings; the two `opus` agents are pinned on purpose.

## MCP servers

The plugin ships only `context7`. For browser automation or Supabase, copy the matching file from `templates/mcp/` to `<project>/.mcp.json` (see `templates/mcp/README.md`).

## Templates

`templates/` holds `CLAUDE.md.tmpl`, per-stack `conventions.md`, `settings.json` and `skills.txt`, plus MCP snippets. `/project-init` fills them in; they can also be copied by hand.

## Development

```
claude plugin validate .
claude --plugin-dir . # try the working copy without installing
```

Release: bump `version` in `.claude-plugin/plugin.json` and `marketplace.json`, add a `CHANGELOG.md` entry, commit, `claude plugin tag .`, push with tags.

## Legacy

`legacy/commands/` keeps the 1.x Next.js/Supabase commands for reference only; nothing loads them. Tag `v1.0.1` is the last commands-based release.
