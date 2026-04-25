# Contributing to Awesome Claude Skills

Thank you for wanting to contribute! This document explains how to add a new skill or improve an existing one.

---

## Table of Contents

- [Adding a New Skill](#adding-a-new-skill)
- [Skill File Format](#skill-file-format)
- [Writing Good Skill Instructions](#writing-good-skill-instructions)
- [Updating an Existing Skill](#updating-an-existing-skill)
- [Pull Request Guidelines](#pull-request-guidelines)

---

## Adding a New Skill

1. Fork this repository and create a feature branch.
2. Create a new directory under `skills/` whose name is the skill slug (lowercase, hyphen-separated):

   ```
   skills/
   └── my-skill/
       └── SKILL.md
   ```

3. Write the `SKILL.md` file (see [Skill File Format](#skill-file-format) below).
4. Add an entry for your skill in `README.md` under the appropriate category. If no category fits, propose a new one.
5. Open a pull request with a clear description of what the skill does and why it is useful.

---

## Skill File Format

Every skill is a single `SKILL.md` file with YAML front-matter followed by Markdown instructions.

```markdown
---
name: my-skill
description: >-
    One sentence that clearly describes what this skill does.
user-invocable: true
---

# My Skill

Brief paragraph explaining the skill's purpose.

## Instructions

Detailed instructions that the agent will follow...
```

### Front-matter fields

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | ✅ | `string` | Unique slug — must match the directory name. Use lowercase and hyphens. |
| `description` | ✅ | `string` | One-sentence description. Should complete the sentence "This skill …". |
| `user-invocable` | ✅ | `boolean` | `true` — user can request the skill explicitly. `false` — loaded automatically. |

---

## Writing Good Skill Instructions

Good skill instructions are **specific**, **actionable**, and **complete**.

### Do

- **State the goal clearly** — open the body with a short paragraph explaining what the skill achieves.
- **Use ordered lists for sequential steps** — if the agent should follow a specific workflow, number the steps.
- **Include examples** — concrete examples (code snippets, command lines) reduce ambiguity.
- **Define output format** — if you expect a specific output structure (e.g., a review grouped by severity), specify it explicitly.
- **Reference standards** — link to relevant specifications, style guides, or best-practice documents.
- **Handle edge cases** — tell the agent what to do when it encounters incomplete information, ambiguous code, or unsupported languages.

### Don't

- Don't repeat instructions that the agent already follows by default.
- Don't include sensitive data (API keys, passwords, internal hostnames).
- Don't make instructions so restrictive that the agent cannot adapt to the actual codebase.

---

## Updating an Existing Skill

- Open an issue first for significant rewrites so we can discuss the change.
- For small fixes (typos, clarifications, broken links), a pull request is welcome directly.
- Keep the `name` front-matter field **unchanged** — renaming a skill is a breaking change for repositories that depend on it.

---

## Pull Request Guidelines

- **One skill per PR** — keep changes focused so reviews are fast.
- **Test your skill** — assign a Copilot task that exercises the skill and paste a brief summary of the result in the PR description.
- **Match existing style** — look at the existing `SKILL.md` files to get a feel for tone and formatting.
- **Update `README.md`** — every new skill must have an entry in the index.
