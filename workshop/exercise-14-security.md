# Exercise 14 — Security Review

**Duration**: 3 minutes  
**Copilot Feature**: Security Prompt File  
**Goal**: Run a structured OWASP Top 10 security audit and fix critical findings.

---

Security is a gate before deployment, not an afterthought. By encoding the OWASP review in a prompt file, every team member runs the same consistent audit every sprint.

---

## Step 1 — Run the Security Review and Fix Critical Issues

In Copilot Chat (default Agent), send this combined prompt:

```
Run an OWASP Top 10 security review against src/.

For each category (A01 through A10):
- List every file and line with a potential vulnerability
- Explain the risk in plain language
- Rate severity: CRITICAL / HIGH / MEDIUM / LOW

Then immediately apply all CRITICAL and HIGH severity fixes:
- Show vulnerable code (before) and fixed code (after) for each fix
- For MEDIUM/LOW findings, add a comment: // SECURITY-TODO: [finding summary]

Prioritize: A01 (Broken Access Control), A03 (Injection), A07 (Auth failures).
```

> **⚡ Tip:** This combined prompt runs review + fix in one agent session, saving the context switch between separate "review" and "fix" passes.

---

## Step 2 — Audit SQL Injection Specifically

```
Audit every database query in src/repositories/ for SQL injection:
1. Are all queries using parameterized statements? (no template literals with user input)
2. Are user-supplied IDs validated as UUIDs before query use?
3. Are page/limit parameters bounds-checked before LIMIT/OFFSET?

Report each file as SAFE or VULNERABLE (with line number if vulnerable). Fix any VULNERABLE patterns.
```

---

## Step 3 — Generate a Security Report

```
Create doc/security-review-report.md with:
- Review date, reviewer: GitHub Copilot, files reviewed
- Findings summary table: Severity | OWASP Category | File | Status (Fixed/Open)
- Description of each fix applied
- Remaining MEDIUM/LOW items with recommended fixes
- Overall security posture assessment
```

---

## Verify

- [ ] All CRITICAL and HIGH findings are fixed
- [ ] `doc/security-review-report.md` exists with findings table
- [ ] No raw SQL string concatenation remains in `src/repositories/`

---

**Next**: [Exercise 15 — Build & Debug](exercise-15-build-debug.md)
