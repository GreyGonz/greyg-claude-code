---
name: skills-sync
description: Check and update the community skills installed in this repo (skills-lock.json) and refresh docs/agents-and-skills.md.
disable-model-invocation: true
model: sonnet
allowed-tools: Read Edit Write Glob Grep Bash(npx skills *) Bash(cat *) Bash(git diff *) Bash(git status *)
---
1. Locate `skills-lock.json` (repo root or `.agents/`). None → say so and suggest `/project-init`.
2. `npx skills check` (fallback `npx skills list`) to see outdated entries.
3. Before updating, `git status --short .claude/skills .agents/skills`: any locally modified skill is listed and excluded, because `npx skills update` overwrites local edits.
4. Update the rest, then `git diff --stat`; regenerate the skills table in `docs/agents-and-skills.md` if it exists (name, origin repo, one-line purpose from each `SKILL.md` description).
5. Report in ≤10 lines.
