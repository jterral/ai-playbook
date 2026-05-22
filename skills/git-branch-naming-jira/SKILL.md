---
name: git-branch-naming-jira
description: Git branch naming convention. Use automatically when creating a git branch for a JIRA ticket.
---

# Branch Naming Convention

Format: `{type}/{ticket-id}_{slug}`

## Types

- `feature` — new functionality (default if unknown)
- `fix` — bug fix
- `chore` — maintenance, dependencies, config
- `docs` — documentation only

## Rules

- Default to `feature` if the type cannot be determined
- Ticket ID in uppercase: `JIRA-1234`
- Slug in kebab-case from the ticket summary, max 5 words
- Example: `feature/JIRA-1234_get-user-address`
