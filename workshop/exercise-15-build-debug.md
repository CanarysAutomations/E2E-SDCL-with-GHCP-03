# Exercise 15 — Build & Debug with the Local Agent

**Duration**: 4 minutes  
**Copilot Feature**: Local Agent + Terminal Tool  
**Goal**: Use Copilot to build the app, interpret errors, and iteratively fix them until all tests pass.

---

The local agent can run terminal commands, read output, diagnose errors, and edit code — all in one conversation. This creates a tight **build → error → fix → verify** loop.

---

## Step 1 — Build and Start the Application

In Copilot Chat (Agent mode), send:

```
Let's build and run the ITMS application.

1. Install all dependencies
2. Run the build/compile step (TypeScript tsc, Maven compile, etc.)
3. Start the application
4. For each error: show the exact error, identify root cause, apply fix, re-run. Continue until GET /api/v1/health returns { status: "ok" }.
```

The agent will loop autonomously: install → build → fix TypeScript/import errors → start → verify.

---

## Step 2 — Run All Tests to Completion

```
Run unit tests: npm run test:unit (or equivalent).

For any failing tests:
1. Show test name and failure message
2. Determine if it is a code bug or test bug
3. Fix the root cause — not just the test
4. Re-run until all pass

Then run integration tests: npm run test:integration
For any failures, reference the original Gherkin acceptance criteria in doc/frd.md for expected behavior.

Show the final coverage report.
```

---

## Step 3 — End-to-End Validation

```
Run an end-to-end flow using curl:
1. Login (POST /api/v1/auth/login) → get JWT
2. Create a task (POST /api/v1/tasks) → get task ID
3. Get task list (GET /api/v1/tasks) → confirm task is visible
4. Update task to In Progress (PATCH /api/v1/tasks/:id/status)
5. Verify task history shows the status progression

Show each curl command and response. The complete flow must work without errors.
```

---

## Debugging Tips

If Copilot loops on the same error:
```
Stop trying to fix [error]. What are the 3 most likely root causes based on the stack trace? Eliminate them one by one.
```

If a test keeps failing:
```
Read the acceptance criteria in doc/frd.md for [FR-ID]. Is the test or the implementation wrong? Tell me before making any changes.
```

---

## Verify

- [ ] Application starts and health check returns 200
- [ ] All unit tests pass with ≥ 80% coverage
- [ ] End-to-end task creation and status update flow works

---

**Next**: [Exercise 16 — IaC & CI/CD](exercise-16-iac-cicd.md)
