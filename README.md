# Copilot Playbook

A comprehensive collection of reusable agent skills for GitHub Copilot and Claude Code, including development best practices, quality standards, and automation tooling.

## 📋 Overview

This repository provides a curated set of skills, consumable two ways:

- **Claude Code plugins**: five plugins (git-workflow, code-auditor, bruno, dotnet, flutter) served from this repo's own marketplace
- **APM packages**: each skill can be pulled individually via [APM (Agent Package Manager)](https://github.com/github/awesome-copilot)

## 🎯 Features

- **Bruno**
  - [Bruno e2e](./plugins/bruno/skills/bruno-e2e/SKILL.md): Run Bruno API tests
  - [Bruno Generator](./plugins/bruno/skills/bruno-generator/SKILL.md): Generate `.bru` request files
- **Code Auditor**
  - [Code Auditor](./plugins/code-auditor/skills/)**: Demanding code review focused on code quality, security, testing, and architectural practices
- **Git Workflow**
  - [Branch Naming](./plugins/git-workflow/skills/git-branch-naming/SKILL.md): Standardized Git practices for branch naming
  - [Conventional Commits](./plugins/git-workflow/skills/git-conventional-commit/SKILL.md): Standardized Git practices for commit messages
  - [Pull Request Formatting](./plugins/git-workflow/skills/git-pull-request-formatting/SKILL.md): Standardized Git practices for pull request formatting
- **.NET**
  - [.NET Check](./plugins/dotnet/skills/dotnet-check/SKILL.md): Validate .NET project structure, dependencies, and build configuration
  - [C# Conventions](./plugins/dotnet/skills/csharp-conventions/SKILL.md): Enforce C# coding conventions and best practices
- **Flutter**
  - [Architecture](./plugins/flutter/skills/flutter-architecture/SKILL.md): Enforce Flutter architecture best practices
  - [Style](./plugins/flutter/skills/flutter-style/SKILL.md): Enforce Flutter styling conventions
  - [Orient UI](./plugins/flutter/skills/flutter-orient-ui/SKILL.md): Feature-first structure, Apple-compliant styling, and Orient UI component usage

## 📁 Project Structure

```txt
ai-playbook/
├── plugins/                         # All plugins (each self-contained)
│   ├── bruno/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/bruno-e2e/, bruno-generator/
│   ├── code-auditor/
│   │   ├── .claude-plugin/plugin.json
│   │   ├── commands/audit.md
│   │   ├── agents/auditor.md
│   │   └── skills/audit-architecture/, audit-security/, audit-quality/
│   ├── dotnet/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/csharp-conventions/, dotnet-check/
│   ├── flutter/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/flutter-architecture/, flutter-orient-ui/, flutter-style/
│   └── git-workflow/
│       ├── .claude-plugin/plugin.json
│       └── skills/git-branch-naming/, git-conventional-commit/, git-pull-request-formatting/
├── .claude-plugin/
│   └── marketplace.json             # Claude Code marketplace (5 plugins)
└── ...
```

## 🔌 Use as Claude Code Plugins

This repository is a [Claude Code plugin marketplace](https://docs.claude.com/en/docs/claude-code/plugins) exposing five plugins that can be installed independently. From a Claude Code session:

```txt
/plugin marketplace add jterral/ai-playbook
/plugin install git-workflow@ai-playbook
/plugin install code-auditor@ai-playbook
/plugin install bruno@ai-playbook
/plugin install dotnet@ai-playbook
/plugin install flutter@ai-playbook
```

| Plugin           | Skills                                                                               |
| ---------------- | ------------------------------------------------------------------------------------ |
| **bruno**        | bruno-e2e, bruno-generator                                                           |
| **code-auditor** | `/audit` command, `auditor` agent, audit-architecture, audit-security, audit-quality |
| **dotnet**       | csharp-conventions, dotnet-check                                                     |
| **flutter**      | flutter-architecture, flutter-orient-ui, flutter-style                               |
| **git-workflow** | git-branch-naming, git-conventional-commit, git-pull-request-formatting              |

Once installed, skills are namespaced by plugin (e.g. `git-workflow:git-conventional-commit`, `code-auditor:auditor`).

## 📦 Use with APM

Skills follow the [APM (Agent Package Manager)](https://microsoft.github.io/apm/) layout and can be pulled individually into any project's `apm.yml`:

```yaml
dependencies:
  apm:
    - jterral/ai-playbook/plugins/git-workflow
    - jterral/ai-playbook/plugins/dotnet
```

Then run `apm update` to install them.

## 🤝 Contributing

When contributing to this project:

1. Follow [Conventional Commits](plugins/git-workflow/skills/git-conventional-commit/SKILL.md) for all commits
2. Follow established code quality standards
3. Update documentation as needed

## 📄 License

See [LICENSE](LICENSE) file for full details.

## 🔗 Resources

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
- [mise Documentation](https://mise.jdx.dev/)
- [GitVersion Documentation](https://gitversion.net/)

---

**Last Updated:** June 2026
