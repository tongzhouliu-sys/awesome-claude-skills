# Awesome Claude Skills [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of skills for the [GitHub Copilot coding agent](https://docs.github.com/en/copilot/concepts/agents/copilot-coding-agent), powered by Claude.

Skills extend the Copilot coding agent with domain-specific knowledge, detailed instructions, and opinionated workflows — letting you codify your team's best practices and have Claude follow them automatically on every task.

---

## Contents

- [What is a Skill?](#what-is-a-skill)
- [How to Use a Skill](#how-to-use-a-skill)
- [Skills](#skills)
  - [Code Quality](#code-quality)
  - [Testing](#testing)
  - [Documentation](#documentation)
  - [Security](#security)
  - [Refactoring](#refactoring)
  - [Dependencies](#dependencies)
- [Contributing](#contributing)

---

## What is a Skill?

A **skill** is a directory containing a single `SKILL.md` file.  The file uses YAML front-matter to declare metadata and a Markdown body to provide instructions that Claude reads before starting work on a task.

```
skills/
└── my-skill/
    └── SKILL.md
```

`SKILL.md` front-matter fields:

| Field | Type | Description |
|---|---|---|
| `name` | `string` | Unique slug for the skill (matches the directory name). |
| `description` | `string` | One-sentence summary shown in skill-picker UIs. |
| `user-invocable` | `boolean` | When `true`, users can explicitly request the skill; when `false`, the skill is loaded automatically by the agent. |

---

## How to Use a Skill

1. **Copy** the skill directory you want into your repository under `.github/skills/` (or any path configured for skills in your repository settings).
2. **Commit** the skill to your default branch.
3. **Assign a task** to the Copilot coding agent — it will automatically pick up and follow the skill's instructions.

To invoke a user-invocable skill explicitly, mention it by name in your task description, e.g.:

> "Please review this PR. Use the `code-reviewer` skill."

---

## Skills

### Code Quality

#### [`code-reviewer`](skills/code-reviewer/SKILL.md)

> Performs a thorough code review covering correctness, readability, performance, and adherence to team conventions.

Guides the agent to produce structured, actionable review comments grouped by severity (blocking / non-blocking / nit).

---

### Testing

#### [`test-writer`](skills/test-writer/SKILL.md)

> Generates comprehensive, idiomatic tests that improve coverage and guard against regressions.

Instructs the agent to analyse existing test patterns, identify coverage gaps, and write tests that follow project conventions.

---

### Documentation

#### [`documentation-writer`](skills/documentation-writer/SKILL.md)

> Writes and updates documentation — READMEs, API docs, changelogs, and inline comments.

Guides the agent to produce clear, accurate, and consistently styled documentation aligned with the project's existing tone and format.

---

### Security

#### [`security-auditor`](skills/security-auditor/SKILL.md)

> Finds and fixes security vulnerabilities, misconfigurations, and risky coding patterns.

Instructs the agent to audit changes using established vulnerability taxonomies (OWASP Top 10, CWE) and produce fixes with explanations.

---

### Refactoring

#### [`refactoring-helper`](skills/refactoring-helper/SKILL.md)

> Guides safe, incremental refactoring while preserving existing behaviour and test coverage.

Provides a structured refactoring workflow: analyse → plan → apply small steps → verify.

---

### Dependencies

#### [`dependency-updater`](skills/dependency-updater/SKILL.md)

> Audits, updates, and consolidates project dependencies while checking for known vulnerabilities.

Instructs the agent to use ecosystem-native tooling (npm, pip, go mod, etc.) and validate that the project still builds and tests pass after updates.

---

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) to learn how to add or improve a skill.
