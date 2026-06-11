# Copilot Playbook — Claude Code Guide

## Project Overview

The **Copilot Playbook** is a centralized collection of custom agents, instructions, and skills for GitHub Copilot. It provides standardized guidance for code review, workflow automation, development practices, and quality standards, designed to be reusable across multiple C# projects.

## Directory Structure

```txt
copilot-playbook/
├── skills/                         # Primary skill definitions
│   ├── auditor/SKILL.md
│   ├── bruno-e2e/SKILL.md
│   ├── bruno-generator/SKILL.md
│   ├── csharp-conventions/SKILL.md
│   ├── dotnet-check/SKILL.md
│   ├── flutter-architecture/SKILL.md
│   ├── flutter-orient-ui/SKILL.md
│   ├── flutter-style/SKILL.md
│   ├── git-branch-naming/SKILL.md
│   ├── git-conventional-commit/SKILL.md
│   └── git-pull-request-formatting/SKILL.md
│
├── .claude-plugin/
│   └── marketplace.json            # Claude Code marketplace (5 plugins defined inline)
│
├── .github/
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
description: Brief description of what the skill does and when to use it
---
# Step-by-step instructions or guidelines here
```

### Available Skills

| Skill                       | Purpose                                       | Category        |
| --------------------------- | --------------------------------------------- | --------------- |
| **auditor**                 | Automated code review & quality assessment    | Quality Review  |
| **bruno-e2e**               | Run Bruno API tests interactively             | Testing         |
| **bruno-generator**         | Generate Bruno .bru test files                | Code Generation |
| **csharp-conventions**      | C# and .NET coding conventions (auto)         | Conventions     |
| **dotnet-check**            | Build C# project & run unit tests             | Build/Test      |
| **flutter-architecture**    | Flutter feature-first architecture (auto)     | Conventions     |
| **flutter-orient-ui**       | Orient UI component usage in Flutter (auto)   | Conventions     |
| **flutter-style**           | Flutter styling for Apple compliance (auto)   | Conventions     |
| **git-branch-naming**       | Git branch naming convention (auto)           | Documentation   |
| **git-conventional-commit** | Conventional Commits format guide             | Documentation   |
| **git-pull-request-formatting** | PR title and description format           | Documentation   |

### Claude Code Marketplace Plugins

Skills are grouped into five plugins defined inline in `.claude-plugin/marketplace.json` (`source: "./"` with explicit `skills` paths — no per-plugin `plugin.json` needed):

| Plugin           | Skills                                                                   |
| ---------------- | ------------------------------------------------------------------------ |
| **bruno**        | bruno-e2e, bruno-generator                                               |
| **code-auditor** | auditor                                                                  |
| **dotnet**       | csharp-conventions, dotnet-check                                         |
| **flutter**      | flutter-architecture, flutter-orient-ui, flutter-style                   |
| **git-workflow** | git-branch-naming, git-conventional-commit, git-pull-request-formatting  |

When adding or renaming a skill directory, update the matching `skills` paths in `marketplace.json` — `claude plugin validate` does not check that these paths exist.

### Conventions

#### English-Only Content

All skill content must be in English. Non-English text is not permitted.

#### Scope

- **Commits**: Use functional `scope` (e.g., `feat(auth): add login`)
  - File: `skills/git-conventional-commit/SKILL.md`
  - Why: Helps group related changes by domain
- **Pull Requests**: Use functional `scope` (e.g., `feat(auth): add login`)
  - File: `skills/git-pull-request-formatting/SKILL.md`
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
description: One-line description of the skill's purpose and when to use it
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

1. Ensure content is English-only
2. Test the skill in Claude Code
3. Create a PR with your new skill

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
- `description` — Concise one-line description stating what the skill does and when to use it

Optional fields:

- `license` — Reference to license terms or SPDX identifier
- `allowed-tools` — Restrict which tools are available while the skill is active (use sparingly)

### Pre-publication Checklist

- [ ] Content is English-only (no non-English text)
- [ ] File is named `SKILL.md` (not `README.md`)
- [ ] Frontmatter includes: `name`, `description`
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

- Check skill `name` is correct (kebab-case) and matches the directory name
- Verify file is at `skills/{name}/SKILL.md`
- Ensure the `description` states when to use the skill (it drives automatic activation)

**Duplicate files between `skills/` and `instructions/`?**

- Skills directory is the source of truth
- Instructions directory is for reference only
- Use skills/ when invoking capabilities

## Related Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [APM (Agent Package Manager)](https://github.com/github/awesome-copilot)
