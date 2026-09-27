---
name: plan-task
description: Analyze a task, produce a phased implementation plan and a delegation map to the plugin agents. Use for non-trivial features before writing code.
argument-hint: "<task description>"
disable-model-invocation: true
---
Plan the task below before any code is written. Stay in the main context so you can delegate; do not implement.

## Task
$ARGUMENTS

## Steps
1. Understand: goal, definition of done, constraints from CLAUDE.md, what already exists. Delegate broad searches to an Explore subagent instead of reading whole files yourself.
2. If scope or acceptance criteria are ambiguous, ask at most 3 questions, then continue.
3. Classify complexity: S (≤2 files), M (one module), L (several modules or a new dependency), XL (architecture change). For L/XL consult `system-architect` once with a precise question; if the change touches auth, secrets, data exposure or input handling also consult `security-engineer`.
4. Write the plan: ordered steps, files to touch, existing helpers to reuse (with paths), tests to add or run, risks and rollback.
5. Stop and wait for approval.

## Delegation map (sonnet unless noted)
| Need | Agent |
|---|---|
| Ambiguous requirements, acceptance criteria | `requirements-analyst` |
| Library or technology choice, current docs | `tech-stack-researcher` |
| System, API or data design (L/XL) | `system-architect` (opus) |
| Auth, secrets, input handling, exposed surface | `security-engineer` (opus) |
| UI structure, accessibility, Vue/React patterns | `frontend-architect` |
| Slow paths, profiling, caching | `performance-engineer` |
| Tech debt, safe restructuring | `refactoring-expert` |
| README, API docs | `technical-writer` |

## Output
In the user's language: `## Plan: <title>` → **Contexto** (≤3 lines) → **Pasos** (numbered, each naming its files) → **Verificación** (commands) → **Riesgos**.
