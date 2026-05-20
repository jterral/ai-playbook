---
name: git-pull-request-work
description: PR title and description format for work projects — uses JIRA ticket key as scope.
user-invocable: true
tools: [git, github]
---

## Prerequisites

- **Git**: Branch must be pushed to remote before creating a PR
- **GitHub access**: Must have write access to the repository
- **JIRA ticket**: A valid JIRA issue key (e.g., `JIRA-123`) must be available
- **PR template**: `.github/PULL_REQUEST_TEMPLATE.md` should exist in the repository

## Titles

- Format: `<type>(<jira-key>): <description>`
- Use the same types as commits: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`
- The JIRA key in parentheses is **MANDATORY** (e.g., `JIRA-123`)
- Description: imperative, lowercase, no period

### Examples

- `feat(JIRA-123): add ability to parse arrays`
- `fix(JIRA-124): correct password validation`
- `chore(JIRA-125): migrate to github actions`

## Technical Requirements

When creating a PR via the GitHub MCP `create_pull_request` tool:

- The `body` parameter MUST use real line breaks (multi-line string), NOT escaped `\n` sequences
- Markdown formatting must be preserved as-is with actual newlines between sections
- Use the `gh` CLI with a HEREDOC as fallback if MCP tool does not render markdown correctly

## Description

The PR description should use the template found in `.github/PULL_REQUEST_TEMPLATE.md`.

If the template is not present, use the following template:

```markdown
# Description

<!--- Describe your changes in detail -->

- TODO: describe your changes in detail

## Related Issue

- [JIRA-XXXX](https://<my_domain>.atlassian.net/browse/JIRA-XXXX)

## Types of changes

<!--- Put an `x` in all the boxes that apply. -->

- [ ] 🐛 Bug fix (non-breaking change which fixes an issue).
- [ ] 🚀 New feature (non-breaking change which adds functionality).
- [ ] ⚠️ Breaking change (fix or feature that would cause existing functionality to change).
- [ ] 📖 Documentation (change or add documentation).
- [ ] 🧰 Tools (fix or add tools in the repository to build / lint / ...).
- [ ] 🧹 Clean code (refactor code without changing functionality).

## Checklist

<!--- Put an `x` in all the boxes that apply. -->

- [ ] I have added tests to cover my changes.
- [ ] All new and existing unit tests passed.
- [ ] All new and existing integration tests passed.
```
