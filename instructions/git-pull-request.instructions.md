---
description: "Instructions for writing pull request titles following the Conventional Commits specification."
applyTo: '**'
---

# Pull Request Titles

## Titles

Follow the same overall Conventional Commits structure as commit messages, with one PR-specific difference:

- Format: `<type>(<jira-key>): <description>`
- Use the same types as commits
- For **pull request titles**, the value in parentheses is **MANDATORY** and must be the JIRA issue key, e.g., `SQACC-123`
- This is intentionally different from commit-message scopes in `git-conventional-commit.instructions.md`, where scope refers to a functional/codebase noun (for example `user`, `parser`, or `ci`)
- Description: imperative, lowercase, no period

## Examples

- feat(SQACC-123): add ability to parse arrays
- fix(SQACC-124): correct password validation
- chore(SQACC-125): migrate to github actions
