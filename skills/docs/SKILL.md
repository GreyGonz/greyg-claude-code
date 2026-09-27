---
name: docs
description: Write or update repository documentation (README, docs/, API reference) from the actual code. Use when docs are missing or stale.
argument-hint: "<README | docs/<file> | module path>"
model: sonnet
allowed-tools: Read Write Edit Grep Glob Bash(git log *) Bash(ls *)
---
Target: $ARGUMENTS

Documentation in Spanish unless the project CLAUDE.md says otherwise; commands, code and identifiers verbatim in English.
1. Read the existing document (if any) and the code it must describe. Never document from memory.
2. Short and true: only commands that exist and options that are parsed; one source per fact, link instead of duplicating across files.
3. Preserve structure and tone; update only stale or missing sections; remove what no longer matches the code and say what you removed.
4. For an API: a table of endpoints/functions (name, input, output, errors) derived from the source.
5. Finish with a 3-line summary of what changed.
