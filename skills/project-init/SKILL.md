---
name: project-init
description: Scaffold CLAUDE.md, .claude/settings.json and docs/agents-and-skills.md for this repo from the plugin templates, detecting the stack. Use in a repo without CLAUDE.md.
argument-hint: "[python|vue|java-quarkus|go|ts-node] [--dry-run]"
model: sonnet
disable-model-invocation: true
allowed-tools: Read Write Edit Glob Grep Bash(ls *) Bash(cat *) Bash(git status *) Bash(mkdir *) Bash(jq *) Bash(npx skills add *)
---
Templates live in `${CLAUDE_PLUGIN_ROOT}/templates` (see its `README.md`).
Arguments: `$ARGUMENTS` — optional stack override and `--dry-run` (print what you would write; write nothing).

1. **Detect the stack** unless given: `pyproject.toml`/`requirements*.txt` → python; `go.mod` → go; `build.gradle*`/`pom.xml` containing `quarkus` → java-quarkus; `package.json` with a `vue` dependency → vue; `package.json` with `typescript` → ts-node. Several matches (e.g. python plus `web/package.json`): primary = backend; list the secondary's commands too.
2. **Collect real commands**: `package.json` scripts; `pyproject` `[project.scripts]`, extras, `[tool.*]`; `Makefile` targets; gradle tasks and Java/Quarkus versions from `build.gradle*`/`gradle.properties`; `go.mod` module and version. Take the one-line purpose and any hard constraint from `README*`.
3. **CLAUDE.md**: fill `templates/CLAUDE.md.tmpl` with those commands and the stack's `templates/<stack>/conventions.md`, dropping lines that do not apply. ≤35 lines. Do not repeat what `~/.claude/rules` already says.
4. **.claude/settings.json**: from `templates/<stack>/settings.json`; if it exists, merge (union of arrays, existing keys kept). If `.claude/settings.local.json` has `permissions.allow`, list the entries already covered by global or project settings and suggest removing them.
5. **docs/agents-and-skills.md**: only if the repo has `docs/`; from the template, with project agents (`.claude/agents/*.md` frontmatter) and skills (`skills-lock.json` or `.claude/skills/*`).
6. **Existing files** are never overwritten silently: for an existing `CLAUDE.md` show the sections you would add and ask first.
7. Print `templates/<stack>/skills.txt` and offer to run the lines (each `npx skills add` asks for permission). If `@playwright/*` or `@supabase/*` are dependencies, point to `templates/mcp/`.
8. Report: files written, files skipped, follow-ups.
