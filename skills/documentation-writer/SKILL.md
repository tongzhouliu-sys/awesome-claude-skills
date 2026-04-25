---
name: documentation-writer
description: >-
    Writes and updates documentation — READMEs, API references, changelogs, and inline
    comments — that is clear, accurate, and consistent with the project's existing style.
user-invocable: true
---

# Documentation Writer

This skill guides the agent to produce high-quality documentation that serves the actual audience (contributors, API consumers, end users) and stays consistent with the tone and format already present in the project.

## When to Use

Invoke this skill when you want the agent to:

- Write or update a `README.md`.
- Add or update inline code comments and docstrings.
- Generate API reference documentation (JSDoc, docstring, godoc, etc.).
- Update a `CHANGELOG.md` or release notes.
- Write a `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, or similar community document.

## Documentation Process

Follow these steps in order:

1. **Identify the audience** — determine who will read this documentation (end users, API consumers, contributors) and calibrate the language and level of detail accordingly.
2. **Audit existing documentation** — read any existing docs in the same file or directory to understand the current tone, terminology, and format before writing anything new.
3. **Gather facts from the code** — read the implementation (not just signatures) to ensure all documented behaviour is accurate. Never document behaviour that is not reflected in the code.
4. **Draft the documentation** — follow the format guidelines below.
5. **Cross-check accuracy** — re-read the relevant code after drafting. Fix any inconsistencies.
6. **Check links** — ensure any hyperlinks or cross-references point to real files or anchors.

## Format Guidelines

### READMEs

Include in this order (omit sections that are not applicable):

1. Project name and one-line description
2. Badges (CI status, license, version)
3. Quick-start / installation instructions
4. Usage examples (prefer runnable code snippets)
5. Configuration reference
6. Contributing section (or link to `CONTRIBUTING.md`)
7. License

### Inline Comments and Docstrings

- Describe **why**, not just **what** — the code already shows what it does.
- Document every public function, method, class, and module.
- Follow the project's docstring format (JSDoc, NumPy, Google, etc.). If none is established, use the most common format for the language.
- Include `@param` / `@returns` / `@throws` (or equivalents) for every public API.
- Keep comments up to date — update or remove comments that no longer reflect the code.

### Changelogs

Follow [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) conventions unless the project already uses a different format:

- Group entries under: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`.
- Write entries from the user's perspective ("Users can now …", not "We added …").

## Guidelines

- **Accuracy over completeness** — a missing section is better than an incorrect one.
- **Match the existing voice** — if the project uses informal language, stay informal; if it is formal, stay formal.
- **Use active voice and present tense** — prefer "Returns the user ID" over "The user ID is returned".
- **Avoid jargon** unless it is standard in the project's domain and already used in existing docs.
- **Short paragraphs and bullet points** — documentation is usually scanned, not read linearly.
