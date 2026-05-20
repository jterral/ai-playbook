# Copilot Playbook — Claude Code Guide

## Project Overview

The **Copilot Playbook** is a centralized collection of custom agents, instructions, and skills for GitHub Copilot. It provides standardized guidance for code review, workflow automation, development practices, and quality standards, designed to be reusable across multiple C# projects.

## Directory Structure

```
copilot-playbook/
├── skills/                         # Primary skill definitions
│   ├── auditor/SKILL.md            # Code quality review agent
│   ├── bruno-e2e/SKILL.md          # Run Bruno e2e tests
│   ├── bruno-generator/SKILL.md    # Generate Bruno API test files
│   ├── dotnet-check/SKILL.md       # Build & run unit tests
│   ├── git-conventional-commit/SKILL.md
│   ├── git-pull-request/SKILL.md
│   └── jira-create-ticket/SKILL.md
│
├── .github/
│   ├── copilot-instructions.md     # Repository governance & guidelines
│   ├── instructions/               # Base instructions (from APM)
│   └── workflows/                  # CI/CD pipelines
│
├── apm.yml                         # Agent Package Manager dependencies
└── mise.toml                       # Tool version management
```

## Skill Framework

### What is a Skill?

A skill is a reusable, self-contained capability that can be invoked from Claude Code or GitHub Copilot. Each skill is defined as a `SKILL.md` file containing:

- **YAML Frontmatter**: Metadata about the skill
- **Content**: Step-by-step instructions or guidelines

### SKILL.md Format

```yaml
---
name: skill-identifier
description: Brief description of what the skill does
user-invocable: true # Can be invoked from Claude Code
tools: [tool1, tool2] # Optional: tools this skill uses
---
# Step-by-step instructions or guidelines here
```

### Available Skills

| Skill                       | Purpose                                    | Category           |
| --------------------------- | ------------------------------------------ | ------------------ |
| **auditor**                 | Automated code review & quality assessment | Quality Review     |
| **bruno-e2e**               | Run Bruno API tests interactively          | Testing            |
| **bruno-generator**         | Generate Bruno .bru test files             | Code Generation    |
| **dotnet-check**            | Build C# project & run unit tests          | Build/Test         |
| **git-conventional-commit** | Conventional Commits format guide          | Documentation      |
| **git-pull-request**        | PR format for personal projects (scope)    | Documentation      |
| **git-pull-request-work**   | PR format for work projects (JIRA key)     | Documentation      |
| **jira-create-ticket**      | Generate Jira User Stories                 | Content Generation |
| **jira-plan-feature**       | Plan development tasks from Jira tickets   | Project Management |

### Conventions

#### English-Only Content

All skill content must be in English. Non-English text is not permitted.

#### Scope

- **Commits**: Use functional `scope` (e.g., `feat(auth): add login`)
  - File: `skills/git-conventional-commit/SKILL.md`
  - Why: Helps group related changes by domain
- **Pull Requests**: Use functional `scope` (e.g., `feat(auth): add login`)
  - File: `skills/git-pull-request/SKILL.md`
  - Why: Helps group related changes by domain

Both patterns are valid; use the appropriate one based on context.

#### Prerequisites

Each skill should document:

- Required CLI tools (e.g., `bru`, `dotnet`, `git`)
- Environment variables or configuration
- Access requirements (Jira credentials, etc.)

## Contributing

### Adding a New Skill

1. Create a new directory: `skills/{skill-name}/`
2. Add `SKILL.md` with frontmatter and content
3. Use this template:

```yaml
---
name: skill-name
description: One-line description of the skill's purpose
user-invocable: true
tools: []  # List any tools this skill uses
---

## Overview
Brief explanation of what the skill does and when to use it.

## Prerequisites
- CLI/tool requirements
- Environment setup
- Access requirements

## Steps
1. Step one
2. Step two
...
```

4. Ensure content is English-only
5. Test the skill in Claude Code
6. Create a PR with your new skill

### Updating Dependencies

Copilot Playbook uses APM (Agent Package Manager) to pull base instructions from `github/awesome-copilot`:

```bash
apm update  # Update dependencies from apm.yml
```

Changes are tracked in `apm.lock.yaml`.

## Tooling

### Pre-commit Hooks

Conventional Commits are enforced via pre-commit hooks (`.pre-commit-config.yaml`):

```bash
pre-commit install      # Install hooks
pre-commit run --all    # Validate all files
```

### Tool Versions

Managed via `mise.toml`:

```bash
mise install            # Install all tools from mise.toml
mise sync               # Update tool versions
```

### CI/CD

GitHub Actions workflows in `.github/workflows/`:

- `ci.yml` — Run tests and linting on push
- `pr-lint.yml` — Enforce conventional commits on PRs
- `release.yml` — Automated releases

## Validation

### SKILL.md Metadata Schema

All `SKILL.md` files must include:

- `name` — Kebab-case identifier matching directory name
- `description` — Concise one-line description
- `user-invocable` — Boolean (true for user-facing skills)

Optional fields:

- `tools` — Array of tool names used by the skill
- `category` — Semantic category (e.g., "Testing", "Git", "Jira")

### Pre-publication Checklist

- [ ] Content is English-only (no non-English text)
- [ ] File is named `SKILL.md` (not `README.md`)
- [ ] Frontmatter includes: `name`, `description`, `user-invocable`
- [ ] `name` matches directory name (kebab-case)
- [ ] Prerequisites section included (if applicable)
- [ ] Steps are numbered and clear
- [ ] Examples provided where helpful
- [ ] No console credentials or secrets included
- [ ] No French or other non-English content

## Maintenance

### Audit & Review

This playbook undergoes regular reviews to:

- Verify all skills use English-only content
- Remove duplicate files and consolidate utilities
- Update documentation for directory structure changes
- Standardize metadata formats
- Ensure prerequisites are clearly documented

### Troubleshooting

**Skill not appearing in Claude Code?**

- Ensure `user-invocable: true` in frontmatter
- Check skill `name` is correct (kebab-case)
- Verify file is at `skills/{name}/SKILL.md`

**Duplicate files between `skills/` and `instructions/`?**

- Skills directory is the source of truth
- Instructions directory is for reference only
- Use skills/ when invoking capabilities

## Related Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [APM (Agent Package Manager)](https://github.com/github/awesome-copilot)
- [Repository Governance](../.github/copilot-instructions.md)
