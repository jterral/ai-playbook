# Copilot Playbook

A comprehensive collection of custom agents and instructions for GitHub Copilot, including development best practices, quality standards, and automation tooling.

## 📋 Overview

This repository provides a curated set of custom agents and instructions to enhance GitHub Copilot's capabilities with:

- **Custom Agents**: Intelligent coding assistants tailored for specific development tasks
- **Custom Instructions**: Detailed guidelines for code quality, security, testing, and conventions

## 🎯 Features

- **[Auditor Agent](./agents/auditor.agent.md)**: An intelligent Copilot agent focused on code quality, security, testing, and architectural practices
- **[User Story Writer Agent](./agents/user-story-writer.agent.md)**: An agent that generates well-structured user stories and acceptance criteria
- **[Git Conventional Commits Instructions](./instructions/git-conventional-commit.instructions.md)**: Guidelines for writing standardized commit messages with mandatory scopes
- **[Git Pull Request Instructions](./instructions/git-pull-request.instructions.md)**: Best practices for writing standardized pull request titles, including Conventional Commit formatting and JIRA key usage

## 📁 Project Structure

```txt
copilot-playbook/
├── ...
├── agents/                          # Custom Copilot agents
│   └── *.agent.md                   # Agent definitions
├── instructions/                    # Custom Copilot instructions
│   └── *.instructions.md            # Instruction definitions
└── ...
```

## 🤝 Contributing

When contributing to this project:

1. Follow [Conventional Commits](instructions/conventional-commits.instructions.md) for all commits
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
