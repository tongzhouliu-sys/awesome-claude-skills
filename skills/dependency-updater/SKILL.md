---
name: dependency-updater
description: >-
    Audits, updates, and consolidates project dependencies, checking for known
    vulnerabilities and ensuring the project builds and tests pass after changes.
user-invocable: true
---

# Dependency Updater

This skill guides the agent to safely audit and update project dependencies, resolve vulnerabilities, and remove unused packages — using the ecosystem's native tooling at every step.

## When to Use

Invoke this skill when you want the agent to:

- Update all or specific dependencies to their latest compatible versions.
- Resolve a known vulnerability reported by a security scanner or advisory.
- Remove unused dependencies.
- Consolidate duplicate transitive dependencies.
- Migrate from a deprecated or unmaintained package to a maintained alternative.

## Update Process

Follow these steps in order:

1. **Identify the ecosystem(s)** — detect package managers from manifest files:
   - `package.json` → npm / yarn / pnpm
   - `requirements.txt` / `pyproject.toml` / `Pipfile` → pip / pipenv / poetry / uv
   - `go.mod` → Go modules
   - `Gemfile` → Bundler
   - `pom.xml` / `build.gradle` → Maven / Gradle
   - `Cargo.toml` → Cargo
   - `*.csproj` / `packages.config` → NuGet

2. **Audit for known vulnerabilities** — run the ecosystem's audit command:
   - npm: `npm audit`
   - yarn: `yarn audit`
   - pip: `pip-audit` or `safety scan`
   - Go: `govulncheck ./...`
   - Ruby: `bundle audit`
   - Cargo: `cargo audit`

3. **Identify outdated packages** — list packages with available updates:
   - npm: `npm outdated`
   - pip: `pip list --outdated`
   - Go: `go list -u -m all`
   - Ruby: `bundle outdated`

4. **Categorise updates** — group packages into:
   - **Security fixes** — versions that resolve a CVE or advisory (highest priority).
   - **Patch updates** (`1.2.3` → `1.2.4`) — low risk; update all.
   - **Minor updates** (`1.2.x` → `1.3.0`) — moderate risk; update unless CHANGELOG indicates breaking changes.
   - **Major updates** (`1.x.x` → `2.0.0`) — higher risk; check migration guide before updating.

5. **Apply updates** — use the package manager to update, preferring scoped commands:
   - Apply security fixes first, then patch, then minor, then major (one at a time for large updates).
   - Commit lock files (`package-lock.json`, `Pipfile.lock`, `go.sum`, `Gemfile.lock`, etc.) alongside manifest files.

6. **Build and test** — after each group of updates, run the full build and test suite to confirm nothing regressed.

7. **Remove unused dependencies** — if a package is imported nowhere in the codebase, remove it.

8. **Summarise changes** — produce a brief summary listing each updated package, the old version, the new version, and the reason for the update.

## Summary Format

```
## Dependency Update Summary

| Package | Old Version | New Version | Type | Reason |
|---------|-------------|-------------|------|--------|
| express | 4.17.1 | 4.21.0 | minor | Security fix (CVE-2024-XXXX) + latest stable |
| lodash  | 4.17.20 | 4.17.21 | patch | Security fix (CVE-2021-23337) |
| webpack | 4.46.0 | 5.94.0 | major | End of life; migration guide followed |

**Removed (unused):** <package-name>
**Audit result after updates:** 0 vulnerabilities found
```

## Guidelines

- **Always use the lock file** — never update `package-lock.json`, `go.sum`, or equivalent files by hand; let the package manager regenerate them.
- **Do not pin to exact versions unless necessary** — prefer semver ranges (`^`, `~`) that allow patch updates.
- **Read migration guides for major updates** — do not blindly bump a major version without understanding breaking changes.
- **One ecosystem at a time** — if the project has multiple package managers, update and test each one separately.
- **Do not change source code** — the only files that should change are manifests, lock files, and (if necessary) import paths when migrating from a renamed package.
- **Check the project's security policy** — some projects have a `SECURITY.md` that specifies which vulnerability severities require a patch release.
