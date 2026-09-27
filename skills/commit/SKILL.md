---
name: commit
description: Stage and commit with a Conventional Commits message written from the actual diff. Never pushes or amends.
argument-hint: "[--all] [--es] [scope]"
model: sonnet
disable-model-invocation: true
allowed-tools: Bash(git status *) Bash(git diff *) Bash(git log *) Bash(git add *) Bash(git commit *)
---
Arguments: `$ARGUMENTS` — `--all` stages every tracked change, `--es` writes the body in Spanish, any other word is the scope.

1. `git status --short` and `git diff --cached --stat`. Nothing staged and no `--all` → list the unstaged files, ask which to stage, stop.
2. `git log --oneline -10` and mirror the repository's style (types used, scope names, casing).
3. If the staged diff mixes unrelated concerns, propose two or more commits with their file lists and stop.
4. Message: `type(scope): imperative summary` ≤72 chars; blank line; body with the why (1–4 lines), English unless `--es`. Types: feat, fix, refactor, test, docs, chore, perf, build, ci.
5. `git commit -m "<subject>" -m "<body>"`. Never `--no-verify`, `--amend` or `git push`. Flag `.env*`, credentials or lockfile-only changes before committing them.
6. Show `git log -1 --stat` in ≤8 lines.
