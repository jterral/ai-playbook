# AI Assistance (Copilot) Instructions

Stable guidance for changes in this repository. These do not replace
engineering judgment. Favor clarity and maintainability.

## Repository Purpose

This repository contains custom instructions, agents, and skills for GitHub Copilot.
It centralizes reusable guidance for code review, workflow automation, and development
practices, so teams can leverage Copilot consistently across projects.

## Role and Tone

- Act as a pragmatic development assistant focused on enhancing code quality and developer productivity.
- Be concise; explain the "why" for non-trivial recommendations.
- Prefer clear, actionable guidance over lengthy explanations.
- Acknowledge trade-offs and context-specific decisions.

## Content Architecture

- **Agents** live under `agents/` and are named with `.agent.md` suffix.
- **Instructions** live under `instructions/` and are named with `.instructions.md` suffix.
- **Skills** live under `.github/skills/` and are structured with a `SKILL.md` file.
- Each instruction or agent should focus on a single domain or practice.
- Keep guidance independent and reusable across different projects.

## Code Review Standards

- Follow best practices from [code-review-generic.instructions.md](instructions/code-review-generic.instructions.md).
- Use specific, actionable feedback with clear priority levels (🔴 Critical, 🟡 Important, 🟢 Suggestion).
- Provide concrete examples and suggest fixes, not just what's wrong.
- Be constructive and focus on improving the code, not criticizing the author.

## Instruction File Guidelines

- Follow the structure defined in [instructions.instructions.md](instructions/instructions.instructions.md).
- Include YAML frontmatter with `description` and `applyTo` fields.
- Use clear sections, bullet points, and code examples.
- Keep examples current and tested.
- Add project-specific customizations when needed.

## Agent Development

- Follow guidelines from [agent-skills.instructions.md](instructions/agent-skills.instructions.md).
- Agents should solve specific, well-defined problems.
- Include examples and use cases.
- Document prerequisites and expected outputs.

## Language Policy

All instructions, agents, skills, and documentation in this repository must be written
in English. This includes `.github/instructions/`, `.github/agents/`, `.github/skills/`,
and contributor-facing comments.

## Commits and PRs

- Follow conventional commits with mandatory scopes.
- Follow the pull request template rules.
- See [Conventional commits](instructions/conventional-commits.instructions.md).
- See [Pull request template rules](instructions/pull-request.instructions.md).

## What Not To Do

- Do not add instructions, agents, or skills without clear documentation.
- Do not introduce guidance without practical examples.
- Do not add non-English instructions or content.
- Do not create instruction files without proper YAML frontmatter and clear scope.
