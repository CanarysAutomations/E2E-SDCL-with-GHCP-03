# Exercise 10 — Assign an Independent Task to the Background Agent

**Duration**: 3 minutes  
**Copilot Feature**: Background Agent  
**Goal**: Delegate a long, self-contained coding task to the Background Agent and continue working while it runs.

---

## Background

The **Background Agent** runs Copilot tasks in the background — inside a sandboxed environment, asynchronously — while you keep working in your main VS Code session. It's perfect for:
- Long-running code generation tasks (generate all CRUD endpoints, write all tests)
- Tasks that don't need your immediate attention
- Parallel workstreams (you write one feature while Copilot writes another)

When the background agent finishes, it opens a pull request with the generated changes for you to review.

---

## Step 1 — Launch the Background Agent

In Copilot Chat:
1. Click the **`...` (More) menu** or look for the **Background Agent** option (cloud/async icon)
2. Select **Start Background Task** (or `New Background Agent Session`)

> **Alternative**: Use `Ctrl+Shift+P` → **GitHub Copilot: New Background Agent**

---

## Step 2 — Assign the Leave Approval API Task

This task is a good background candidate because it's:
- Self-contained (doesn't depend on your current work)
- Well-defined (we have the FRD and TSD to guide it)
- Time-consuming (multiple controllers, services, repositories)

Copy and paste this prompt into the Background Agent:

```
You are working in the LAMS (Leave & Attendance Management System) project.

Read:
- doc/tsd.md (API design section — Leave Approval endpoints)
- doc/frd.md (Use Cases UC-002 Leave Approval, UC-003 Leave Cancellation)
- .github/copilot-instructions.md (coding standards)
- The existing code in src/ to understand the folder structure and patterns

Implement the Leave Approval workflow:

1. PUT /api/v1/leave/requests/:id/approve
   - Auth required: Manager role only
   - Manager can only approve requests from their direct reports
   - Updates request status to "MANAGER_APPROVED"
   - Deducts from employee's leave balance
   - Triggers notification stub (log the notification event)

2. PUT /api/v1/leave/requests/:id/reject
   - Auth required: Manager or HR Admin role
   - Requires a rejection reason in the body
   - Updates request status to "REJECTED"
   - Does NOT deduct leave balance

3. PUT /api/v1/leave/requests/:id/hr-approve
   - Auth required: HR Admin only
   - Final approval step after manager approval
   - Updates request status to "APPROVED"

4. DELETE /api/v1/leave/requests/:id (Cancel)
   - Auth required: Employee (their own), Manager (team's), HR Admin (any)
   - Can only cancel PENDING or APPROVED requests
   - If cancelling APPROVED, restore the leave balance
   - Cannot cancel requests in the past

Follow the same patterns as the existing auth and leave request endpoints.
Create service, repository, and any new model files needed.
Open a pull request with all changes when done.
```

---

## Step 3 — Continue Working

While the background agent runs:
- **Continue in your local session** — move to Exercise 11 (Context Map)
- The background agent works independently and won't interrupt you

---

## Step 4 — Review the Pull Request

When the background agent finishes (typically 5–15 minutes for this task), it will:
1. Show a notification in VS Code
2. Open (or link to) the pull request it created

Review the PR:
- [ ] All 4 endpoints are implemented
- [ ] Role checks are correct (manager can't approve HR-level, employee can't approve own)
- [ ] Leave balance is adjusted on approval and restored on cancellation
- [ ] Code follows the same patterns as the existing `src/` files

Merge the PR if it looks correct.

---

## Key Takeaway

> Background Agent is a **parallel workstream**. On a real project, you might assign 4–5 long tasks to background agents (e.g., write all CRUD for users, write all CRUD for leave types, write all notifications, generate all tests) while you focus on the complex business logic. Each background agent opens a PR, you review and merge. This compresses days of work into hours.

---

**Next**: [Exercise 11 — Context Map Skill](exercise-11-context-map.md)
