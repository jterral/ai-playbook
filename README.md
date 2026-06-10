# Copilot Playbook

A comprehensive collection of custom agents and instructions for GitHub Copilot, including development best practices, quality standards, and automation tooling.

## 📋 Overview

This repository provides a curated set of custom agents and instructions to enhance GitHub Copilot's capabilities with:

- **Custom Agents**: Intelligent coding assistants tailored for specific development tasks
- **Custom Instructions**: Detailed guidelines for code quality, security, testing, and conventions

## 🎯 Features

- **[Auditor](./skills/auditor/SKILL.md)**: A demanding code review skill focused on code quality, security, testing, and architectural practices
- **[Git Conventional Commits](./skills/git-conventional-commit/SKILL.md)**: Guidelines for writing standardized commit messages with mandatory scopes
- **[Git Pull Request](./skills/git-pull-request/SKILL.md)**: Standardized pull request titles and descriptions with functional scope
- **[Bruno e2e](./skills/bruno-e2e/SKILL.md)** / **[Bruno Generator](./skills/bruno-generator/SKILL.md)**: Run Bruno API tests and generate `.bru` request files
- **[.NET Check](./skills/dotnet-check/SKILL.md)** / **[C# Conventions](./skills/csharp-conventions/SKILL.md)**: Build, test, and coding conventions for .NET projects
- **Flutter skills** ([architecture](./skills/flutter-architecture/SKILL.md), [style](./skills/flutter-style/SKILL.md), [Orient UI](./skills/flutter-orient-ui/SKILL.md)): Feature-first structure, Apple-compliant styling, and Orient UI component usage

## 📁 Project Structure

```txt
copilot-playbook/
├── ...
├── .claude-plugin/                  # Claude Code plugin & marketplace manifests
│   ├── plugin.json
│   └── marketplace.json
├── skills/                          # Skill definitions
│   └── {skill-name}/SKILL.md
└── ...
```

## 🔌 Install as Claude Code Plugin

This repository is also packaged as a [Claude Code plugin](https://docs.claude.com/en/docs/claude-code/plugins) and serves as its own marketplace. From a Claude Code session:

```txt
/plugin marketplace add jterral/copilot-playbook
/plugin install copilot-playbook@copilot-playbook
```

Once installed, skills are available under the `copilot-playbook:` namespace (e.g. `copilot-playbook:auditor`, `copilot-playbook:git-conventional-commit`).

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
