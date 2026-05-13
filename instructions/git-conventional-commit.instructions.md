---
description: "Instructions for writing commit messages following the Conventional Commits specification."
---

# Conventional Commits

## Commit messages

Follow Conventional Commits specification:

- Format: `<type>(<scope>): <description>`
- **Scope is mandatory** — never omit it
- Types: feat, fix, docs, style, refactor, perf, test, chore
- Scope: a noun describing the section of the codebase affected (e.g., user, parser, ci)
- Description: imperative, lowercase, no period

## Examples

- feat(parser): add ability to parse arrays
- fix(user): correct password validation
- chore(ci): migrate to github actions
