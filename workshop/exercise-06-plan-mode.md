# Exercise 06 — Plan Mode: Generate Implementation Plan

**Duration**: 3 minutes  
**Copilot Feature**: Plan Mode  
**Goal**: Use Plan Mode to reason through the full implementation strategy before writing any code.

---

## Step 1 — Switch to Plan Mode

In Copilot Chat, click the mode selector at the bottom-left → **Plan**.

---

## Step 2 — Send the Planning Prompt

```
Read #frd.md and #tsd.md carefully.

Generate a complete, phased implementation plan for the ITMS:
- Phase 0: Project setup, folder structure, database migration tooling, CI skeleton
- Phase 1: Authentication & User Management (registration, login, JWT, RBAC)
- Phase 2: Task Management (creation, assignment, dependencies, status tracking)
- Phase 3: Reporting & Progress Summary (filters, export)
- Phase 4: Notifications (email via SendGrid, Teams webhooks)

For each phase, list tasks with:
- Task ID (T-001…), Title, Effort (S/M/L), FRD reference, Parallel or Sequential, Background Agent candidate?

Do NOT create any files yet. Show me the plan first.
```

> **⚡ Tip:** While reviewing the plan, have Exercise 07 open and ready — you'll create the prompt file immediately after approving.

---

## Step 3 — Approve and Save

Review the plan (check all phases covered, tasks reference FRD IDs), then switch back to **Agent mode** and send:

```
Save the implementation plan to doc/implementation-plan.md
```

---

## Verify

- [ ] `doc/implementation-plan.md` exists with all phases
- [ ] Tasks have IDs, effort estimates, and FRD references
- [ ] Some tasks are flagged as Background Agent candidates

---

## Key Takeaway

> Plan Mode prevents tunnel vision — Copilot shows its full strategy before writing a single line of code. A 3-minute review here saves hours of rework.

---

**Next**: [Exercise 07 — Create Implementation Prompt File](exercise-07-implementation-prompt.md)\n