---
name: jira-plan-feature
description: Plan development tasks for C# projects based on Jira tickets.
user-invocable: true
tools: [bash, jira-mcp]
---

## Prerequisites

- **Jira MCP**: Must be configured and accessible to fetch ticket details
- **Git**: Git must be installed and the working directory must be a git repository
- **Jira access**: User must have access to view Jira tickets
- **C# project**: Project must be a C# codebase with familiar structure
- **Environment**: Working directory should be the root of the C# project

## Steps

Given a Jira ticket ID $ARGUMENTS:

1. **Fetch the ticket** via Jira MCP
   - Retrieve: summary, description, acceptance criteria, issue type (Story/Bug/Task)

2. **Create the git branch**
   - Format: `{type}/{ticket-id}_{slug}`
   - Types:
     - `feature` — new functionality (default if unknown)
     - `fix` — bug fix
     - `chore` — maintenance, dependencies, config
     - `docs` — documentation only
   - Slug: kebab-case from summary, max 5 words
   - Example: `feature/PROJ-123_add-user-authentication`
   - Run `git switch -c {branchname}`

3. **Generate a development plan**
   - Analyze the existing codebase to identify impacted files/modules
   - List implementation steps in logical order
   - Flag any concerns: breaking changes, migrations, tests to write

4. **Final summary**
   - Display the created branch name
   - Display the plan as a checklist
   - Ask: "Where do you want to start?"
