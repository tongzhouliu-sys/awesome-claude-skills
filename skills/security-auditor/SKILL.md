---
name: security-auditor
description: >-
    Finds and fixes security vulnerabilities, misconfigurations, and risky coding
    patterns using established taxonomies such as OWASP Top 10 and CWE.
user-invocable: true
---

# Security Auditor

This skill guides the agent to perform a thorough security audit of the code in scope, produce a prioritised list of findings, and apply fixes where possible.

## When to Use

Invoke this skill when you want the agent to:

- Audit new or changed code for security vulnerabilities before merging.
- Perform a broader security review of a module, service, or repository.
- Fix a reported security issue and verify the fix is complete.
- Check dependency versions against known vulnerability databases.

## Audit Process

Follow these steps in order:

1. **Define scope** — identify the files, modules, or services to audit based on the task description.
2. **Check dependencies** — look for outdated or vulnerable dependencies using ecosystem tools:
   - npm: `npm audit`
   - Python: `pip-audit` or `safety check`
   - Go: `govulncheck ./...`
   - Ruby: `bundle audit`
   - Java/Maven: `mvn dependency-check:check`
3. **Static analysis** — read the code for patterns matching the vulnerability categories below.
4. **Review configuration** — check for insecure defaults in configuration files, environment variables, and infrastructure-as-code.
5. **Produce a findings report** (see Output Format below).
6. **Apply fixes** — for each confirmed finding, apply the minimal correct fix. Do not introduce unrelated changes.
7. **Verify fixes** — confirm the vulnerable pattern is gone and existing tests still pass.

## Vulnerability Categories to Check

Cover at minimum:

- **Injection** (SQL, command, LDAP, XPath) — unsanitised input passed to interpreters.
- **Broken Authentication** — weak passwords, missing rate limiting, insecure session management.
- **Sensitive Data Exposure** — secrets in source code, logs, or unencrypted storage/transport.
- **XML External Entities (XXE)** — unsafe XML parsing.
- **Broken Access Control** — missing authorisation checks, insecure direct object references.
- **Security Misconfiguration** — debug modes enabled, overly permissive CORS, default credentials.
- **Cross-Site Scripting (XSS)** — unescaped user input rendered in HTML/JS contexts.
- **Insecure Deserialization** — unsafe use of `pickle`, `eval`, `unserialize`, `ObjectInputStream`, etc.
- **Using Components with Known Vulnerabilities** — outdated libraries flagged by vulnerability databases.
- **Insufficient Logging & Monitoring** — security-relevant events not logged.
- **Cryptography issues** — weak algorithms (MD5, SHA-1, DES), hardcoded keys, insufficient key lengths.
- **Path traversal** — unvalidated file paths derived from user input.
- **SSRF (Server-Side Request Forgery)** — user-controlled URLs fetched by the server.

## Output Format

```
## Security Audit Report

**Scope:** <files / modules reviewed>
**Findings:** <N critical, N high, N medium, N low, N informational>

---

### Critical
- **[CWE-XXX / OWASP AXX] File:Line** — Description of the vulnerability, proof of exploitability, and recommended fix.

### High
- ...

### Medium
- ...

### Low
- ...

### Informational
- ...
```

## Guidelines

- **Report only confirmed issues** — do not flag theoretical issues unless there is a realistic attack path.
- **Provide a fix for every finding** — a finding without a fix is incomplete.
- **Minimal fixes** — security fixes should change only what is necessary; avoid refactoring unrelated code.
- **Never introduce new secrets** — do not add API keys, tokens, or passwords to the codebase.
- **Explain the risk** — each finding should explain why it is a problem, not just what the pattern is.
