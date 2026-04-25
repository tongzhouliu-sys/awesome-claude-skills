---
name: test-writer
description: >-
    Generates comprehensive, idiomatic tests that improve coverage and guard against
    regressions, following the project's existing test patterns and conventions.
user-invocable: true
---

# Test Writer

This skill guides the agent to analyse existing test infrastructure, identify coverage gaps, and write high-quality tests that fit naturally alongside the project's existing suite.

## When to Use

Invoke this skill when you want the agent to:

- Add tests for new code that was written without them.
- Increase coverage for an under-tested module or function.
- Write regression tests for a bug that was just fixed.
- Refactor or improve existing tests.

## Test-Writing Process

Follow these steps in order:

1. **Discover the test framework** — look for configuration files (`jest.config.*`, `pytest.ini`, `go.mod`, `Gemfile`, `build.gradle`, etc.) and existing test files to identify the framework, assertion style, and directory conventions.
2. **Understand the code under test** — read the implementation to understand its public interface, inputs, outputs, and side effects.
3. **Identify coverage gaps** — if a coverage tool is available (`npm test -- --coverage`, `pytest --cov`, `go test -cover`), run it. Otherwise, reason about which paths, branches, and edge cases are untested.
4. **Plan test cases** — before writing code, list the test cases you will add:
   - Happy path(s)
   - Edge cases (empty input, zero, null/nil, max values, etc.)
   - Error / failure paths
   - Boundary conditions
5. **Write the tests** — follow the project's naming conventions, file placement, and assertion style exactly.
6. **Run the tests** — execute the test suite to confirm all new tests pass and no existing tests regress.
7. **Report coverage improvement** — briefly state the before/after coverage delta if measurable.

## Guidelines

- **Match existing conventions exactly** — file names, describe/it block nesting, assertion library, mock patterns, fixture setup, etc.
- **One assertion per test when possible** — tests that assert a single behaviour are easier to diagnose when they fail.
- **Avoid testing implementation details** — test public interfaces and observable outputs, not internal state.
- **Use descriptive test names** — a failing test name should tell the developer what broke without needing to read the test body.
- **Keep tests independent** — each test should be able to run in isolation without relying on the side effects of another test.
- **Do not delete or weaken existing tests** — if a test appears incorrect, flag it in a comment rather than removing it.
- **Mock external dependencies** — database calls, HTTP requests, file system access, and time-dependent behaviour should be mocked or stubbed.
