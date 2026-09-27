---
name: review-diff
description: Review the working-tree diff (or a ref range) for bugs, missing tests, security and convention issues. Use before committing.
argument-hint: "[base-ref]"
model: sonnet
context: fork
agent: Explore
disable-model-invocation: true
allowed-tools: Read Grep Glob Bash(git diff *) Bash(git log *) Bash(git status *) Bash(git show *)
---
Review the change set and report findings. Never edit files.

Base ref: `$0` (empty → uncommitted changes).
- No base: `git status --short`, then `git diff HEAD`; read untracked files listed by status.
- With base: `git diff $0...HEAD` and `git log --oneline $0..HEAD`.

Check in this order: correctness (logic, edge cases, error handling), security (injection, secrets, authz, unsafe deserialization), tests (missing or weakened), project conventions (CLAUDE.md, `.claude/rules`), performance only when obvious. Read surrounding code when the diff alone is ambiguous; do not review unchanged code.

Output in the user's language, ≤20 lines:
`## Review: <n> files, +<a>/-<b>`
Findings ordered by severity, one line each: `[high|medium|low] path:line — problem → fix`.
End with `LGTM` if nothing above low, otherwise `Bloqueantes: <n>`.
