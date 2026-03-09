# Exercise 10 — Assign an Independent Task to the Background Agent

**Duration**: 2 minutes  
**Copilot Feature**: Background Agent  
**Goal**: Delegate a self-contained coding task to run asynchronously while you continue working.

---

The **Background Agent** runs tasks in a sandboxed environment asynchronously and opens a pull request with the changes when done. Use it for long, well-defined tasks that don't need your immediate attention.

---

## Step 1 — Launch the Background Agent

`Ctrl+Shift+P` → **GitHub Copilot: New Background Agent**

---

## Step 2 — Submit the Task Assignment & Dependency API Task

```
You are working in the ITMS project. Read:
- doc/tsd.md (Task Assignment and Dependency API sections)
- doc/frd.md (UC-002 Task Assignment, UC-003 Task Dependency Management)
- .github/copilot-instructions.md (coding standards)
- src/ to understand existing folder structure and patterns

Implement:

1. PATCH /api/v1/tasks/:id/assign
   - Accepts: { assignedUserId }, reassigns task, records previous assignee in history
   - Log the reassignment event as a notification stub

2. POST /api/v1/tasks/:id/dependencies
   - Accepts: { dependsOnTaskId }
   - If dependsOnTaskId is not Completed, marks the task as Blocked

3. DELETE /api/v1/tasks/:id/dependencies/:dependencyId
   - Removes dependency, re-evaluates blocked status

4. PATCH /api/v1/tasks/:id/status with allowed transition validation

Follow existing patterns. Create all needed service, repository, and model files.
Open a pull request when done.
```

---

## Step 3 — Continue Working

> **While this runs (5–15 min), proceed through Exercises 11–13 uninterrupted.**  
> You'll review and merge the PR after completing those exercises.

---

## Verify (after returning)

- [ ] All 4 endpoints are in the PR
- [ ] Dependency blocking logic sets task status to BLOCKED
- [ ] Task history records assignment and status changes
- [ ] Code follows the same patterns as `src/`

---

## Key Takeaway

> Background Agent is a **parallel workstream**. Assign 4-5 long, self-contained tasks to background agents simultaneously while you focus on complex business logic. Each opens a PR you review and merge.

---

**Next**: [Exercise 11 — Context Map Skill](exercise-11-context-map.md)
