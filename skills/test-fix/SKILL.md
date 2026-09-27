---
name: test-fix
description: Run the project's lint and tests, fix failures, re-run (max 3 rounds). Use after a change or when the suite is red.
argument-hint: "[test command or path]"
model: sonnet
allowed-tools: Read Edit Grep Glob Bash
---
Goal: a green run with the fewest code changes.

1. Command: `$ARGUMENTS` if given; else the Tests/Lint lines of CLAUDE.md; else detect: `pyproject.toml` → `.venv/bin/pytest -q` (plus `.venv/bin/ruff check .` if ruff is configured); `go.mod` → `go vet ./... && go test ./...`; `build.gradle*` → `./gradlew test`; `package.json` → `npm test` (plus `npx vue-tsc --noEmit` when vue-tsc is a dependency).
2. Run once. Read only the failing tests and the code they exercise.
3. Fix the code, not the test. Edit a test only when the test itself is wrong, and say so explicitly.
4. Re-run the failing subset first (`pytest path::name`, `go test -run`, `--tests 'Class'`, `vitest run <file>`), then the full command. Maximum 3 rounds.
5. Still red: stop and report what fails, why, what you tried and the smallest next step.

Report in ≤10 lines: command, before/after counts, files changed.
