# Copilot Playbook

A comprehensive collection of custom agents and instructions for GitHub Copilot, including development best practices, quality standards, and automation tooling.

## 📋 Overview

This repository provides a curated set of custom agents and instructions to enhance GitHub Copilot's capabilities with:

- **Custom Agents**: Intelligent coding assistants tailored for specific development tasks
- **Custom Instructions**: Detailed guidelines for code quality, security, testing, and conventions

## 🎯 Features

- **[Auditor](./skills/auditor/SKILL.md)**: A demanding code review skill focused on code quality, security, testing, and architectural practices
- **[Git Conventional Commits](./skills/git-conventional-commit/SKILL.md)**: Guidelines for writing standardized commit messages with mandatory scopes
- **[Git Pull Request Formatting](./skills/git-pull-request-formatting/SKILL.md)**: Standardized pull request titles and descriptions with functional scope
- **[Bruno e2e](./skills/bruno-e2e/SKILL.md)** / **[Bruno Generator](./skills/bruno-generator/SKILL.md)**: Run Bruno API tests and generate `.bru` request files
- **[.NET Check](./skills/dotnet-check/SKILL.md)** / **[C# Conventions](./skills/csharp-conventions/SKILL.md)**: Build, test, and coding conventions for .NET projects
- **Flutter skills** ([architecture](./skills/flutter-architecture/SKILL.md), [style](./skills/flutter-style/SKILL.md), [Orient UI](./skills/flutter-orient-ui/SKILL.md)): Feature-first structure, Apple-compliant styling, and Orient UI component usage

## 📁 Project Structure

```txt
copilot-playbook/
├── ...
├── .claude-plugin/
│   └── marketplace.json             # Claude Code marketplace (5 plugins)
├── skills/                          # Skill definitions (APM-compatible layout)
│   └── {skill-name}/SKILL.md
└── ...
```

## 🔌 Use as Claude Code Plugins

This repository is a [Claude Code plugin marketplace](https://docs.claude.com/en/docs/claude-code/plugins) exposing five plugins that can be installed independently. From a Claude Code session:

```txt
/plugin marketplace add jterral/copilot-playbook
/plugin install git-workflow@copilot-playbook
/plugin install code-auditor@copilot-playbook
/plugin install bruno@copilot-playbook
/plugin install dotnet@copilot-playbook
/plugin install flutter@copilot-playbook
```

| Plugin           | Skills                                                       |
| ---------------- | ------------------------------------------------------------ |
| **git-workflow** | git-branch-naming, git-conventional-commit, git-pull-request-formatting |
| **code-auditor** | auditor                                                      |
| **bruno**        | bruno-e2e, bruno-generator                                   |
| **dotnet**       | csharp-conventions, dotnet-check                             |
| **flutter**      | flutter-architecture, flutter-orient-ui, flutter-style       |

Once installed, skills are namespaced by plugin (e.g. `git-workflow:git-conventional-commit`, `code-auditor:auditor`).

## 📦 Use with APM

Skills follow the [APM (Agent Package Manager)](https://github.com/github/awesome-copilot) layout and can be pulled individually into any project's `apm.yml`:

```yaml
dependencies:
  apm:
    - jterral/copilot-playbook/skills/git-conventional-commit
    - jterral/copilot-playbook/skills/csharp-conventions
```

Then run `apm update` to install them.

## 🤝 Contributing

When contributing to this project:

1. Follow [Conventional Commits](skills/git-conventional-commit/SKILL.md) for all commits
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

**Last Updated:** May 2026
