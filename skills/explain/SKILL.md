---
name: explain
description: Explain a file, symbol or behaviour of this codebase concisely with file:line references, in a cheap isolated subagent.
argument-hint: "<file | symbol | question>"
model: sonnet
context: fork
agent: Explore
allowed-tools: Read Grep Glob Bash(git log *)
---
Explain: $ARGUMENTS

- Locate with Grep/Glob first; read only the relevant line ranges.
- Structure: what it is (1–2 lines) → how it works (flow, key decisions) → where it is used and what depends on it → gotchas.
- Cite `path:line` for every claim. ≤30 lines, in the user's language, no code excerpt longer than 6 lines.
- For a *why* question, use `git log -S` only when the code itself does not answer.
