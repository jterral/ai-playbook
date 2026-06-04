---
name: jira-plan-feature
description: Plan development tasks based on Jira tickets.
user-invocable: true
tools: [bash, jira-mcp]
---

# Plan Feature from Jira Ticket

## Prerequisites

- **Jira MCP**: Must be configured and accessible to fetch ticket details
- **Git**: Git must be installed and the working directory must be a git repository
- **Jira access**: User must have access to view Jira tickets
- **C# project**: Project must be a C# codebase with familiar structure
- **Environment**: Working directory should be the root of the C# project

## Steps

Given a Jira ticket ID:

1. **Fetch the ticket** via Jira MCP
   - Retrieve: summary, description, acceptance criteria, issue type (Story/Bug/Task)

2. **Create the git branch**
   - Use the `git-branch-naming-jira` skill conventions
   - Run `git pull` to ensure the local repository is up to date
   - Run `git switch -c {branchname}` from the master/main branch

3. **Generate a development plan**
   - Analyze the existing codebase to identify impacted files/modules
   - List implementation steps in logical order
   - Flag any concerns: breaking changes, migrations, tests to write

4. **Execute the plan**
   - Implement all changes
   - Build and run tests to verify
   - Commit using the `git-conventional-commit` skill conventions
   - Create the PR using the `git-pull-request-jira` skill conventions
