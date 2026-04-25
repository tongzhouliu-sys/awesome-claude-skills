---
name: code-reviewer
description: >-
    Performs a thorough code review covering correctness, readability, performance,
    and adherence to team conventions, producing structured and actionable feedback.
user-invocable: true
---

# Code Reviewer

This skill guides the agent to perform a comprehensive, structured code review of the changes in the current task. Reviews are grouped by severity so authors can quickly triage feedback.

## When to Use

Invoke this skill when you want the agent to:

- Review a pull request or a set of uncommitted changes.
- Provide feedback before merging a branch.
- Check that changes conform to project conventions and best practices.

## Review Process

Follow these steps in order:

1. **Understand context** — read the task description, linked issue, and any existing tests to understand the intent of the changes.
2. **Check correctness** — identify logic errors, off-by-one mistakes, unhandled edge cases, and incorrect assumptions.
3. **Check security** — flag any input validation issues, unsafe data handling, hardcoded secrets, or patterns that match OWASP Top 10 vulnerabilities.
4. **Check performance** — identify unnecessary allocations, N+1 queries, blocking I/O in hot paths, and missing indexes.
5. **Check readability** — flag unclear variable names, missing or misleading comments, overly complex functions, and violations of the project's style guide.
6. **Check test coverage** — note any code paths that are not exercised by the existing or new tests.
7. **Summarise findings** — produce a structured report (see Output Format below).

## Output Format

Structure your review as follows:

```
## Code Review Summary

**Files reviewed:** <list of files>
**Overall assessment:** <one sentence>

---

### 🚫 Blocking Issues
<!-- Issues that must be resolved before merging -->
- **[File:Line]** Description of the issue and suggested fix.

### ⚠️ Non-Blocking Issues
<!-- Important improvements that should be addressed soon -->
- **[File:Line]** Description of the issue and suggested fix.

### 💡 Nits & Suggestions
<!-- Minor style, naming, or optional improvement suggestions -->
- **[File:Line]** Description.
```

If a category has no items, omit it entirely.

## Guidelines

- Be constructive and specific — every comment should include both the problem and a concrete suggestion.
- Prefer asking a clarifying question over making an assumption when the intent of code is genuinely unclear.
- Do not flag issues that are pre-existing and unrelated to the current change, unless they are security or correctness issues in code that the change touches.
- When suggesting a fix, provide a short code snippet if it makes the suggestion clearer.
