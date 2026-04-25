---
name: refactoring-helper
description: >-
    Guides safe, incremental refactoring while preserving existing behaviour,
    maintaining test coverage, and following established patterns in the codebase.
user-invocable: true
---

# Refactoring Helper

This skill guides the agent through a disciplined, incremental refactoring workflow. The goal is to improve code structure, readability, or performance without changing observable behaviour.

## When to Use

Invoke this skill when you want the agent to:

- Extract duplicated logic into shared utilities.
- Break up large functions or classes into smaller, focused units.
- Rename symbols for clarity.
- Replace an ad-hoc pattern with an established one (e.g., replace manual retry loops with a library).
- Improve the layering or organisation of a module.
- Address tech-debt flagged in a code review.

## Refactoring Workflow

Follow this workflow strictly — **do not skip steps**:

1. **Understand the goal** — read the task description and identify the specific structural improvement requested.
2. **Read the code** — fully read all files that will be touched before making any changes.
3. **Run the existing tests** — confirm the test suite passes before you start. If tests are failing, note it and do not proceed until the cause is understood.
4. **Plan the changes** — write out a brief, numbered plan of the steps you will take. For large refactors, prefer smaller sequential commits over one large change.
5. **Apply the changes incrementally** — make one logical change at a time:
   - Extract / inline a function or variable.
   - Rename a symbol across all its usages.
   - Move code to a new file/module.
   - Replace one pattern with another.
6. **Run the tests after each step** — confirm nothing regressed before continuing.
7. **Review the diff** — re-read your own changes before finalising to catch unintended modifications.
8. **Summarise the refactor** — briefly describe what was changed and why it is an improvement.

## Refactoring Patterns

Apply these patterns as appropriate:

- **Extract Function / Method** — move a self-contained block of code into a named function.
- **Inline Function** — remove a function whose body is as clear as its name.
- **Rename Variable / Function / Class** — choose a name that clearly communicates intent.
- **Replace Magic Number / String with Named Constant** — improves readability and centralises values.
- **Extract Class / Module** — split a class or file that has grown beyond a single responsibility.
- **Consolidate Duplicate Code** — extract shared logic into a single utility.
- **Replace Conditional with Polymorphism** — replace complex if/else or switch chains with a strategy or visitor pattern where appropriate.
- **Introduce Parameter Object** — replace a long parameter list with a single structured object.
- **Replace Nested Callbacks with Promises / async-await** — modernise asynchronous code.

## Guidelines

- **Behaviour must be preserved** — if a refactor changes observable behaviour, it is not a refactor, it is a feature change. Stop and clarify with the user.
- **Do not mix refactoring with feature work** — if you notice a bug or missing feature while refactoring, open a separate issue rather than fixing it inline.
- **Keep diffs reviewable** — pure renames (which produce large mechanical diffs) should be in separate commits from logic changes.
- **Do not reduce test coverage** — if a refactor changes the public API, update the tests to match. Do not delete tests.
- **Respect existing patterns** — match the naming, structure, and idioms already used in the codebase. Do not introduce patterns that are foreign to the project.
