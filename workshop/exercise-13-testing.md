# Exercise 13 — Write Unit & Functional Tests

**Duration**: 4 minutes  
**Copilot Feature**: Local Agent + Prompt Files  
**Goal**: Generate comprehensive unit and integration tests from FRD acceptance criteria.

---

Tests are where FRD acceptance criteria become code. Each Gherkin **Given/When/Then** scenario in `doc/frd.md` maps to an automated test case.

---

## Step 1 — Setup Testing Infrastructure + Unit Tests

Send this combined prompt in Copilot Chat (Agent mode):

```
Reference .github/skills/context-map/context-map.md and .github/copilot-instructions.md.

First, set up the test infrastructure:
- Install and configure the test framework (Jest/pytest/JUnit — match the stack)
- Create tests/unit/ and tests/integration/ directories
- Create tests/helpers/ with: factory functions for test users (all 4 roles), authenticated request helper (JWT), and database cleanup helper
- Add test scripts: "test:unit", "test:integration", "test:all" with coverage

Then immediately generate unit tests for TaskService in tests/unit/:

Test createTask():
- Creates task with "To Do" status when all required fields are provided
- Throws ValidationError when title is missing
- Throws ValidationError when priority is not Low/Medium/High
- Throws NotFoundError when assignedUserId does not exist

Test updateTaskStatus():
- Updates To Do → In Progress when no blocking dependencies
- Sets status to Blocked when a dependency is not Completed
- Allows Completed when all dependencies are Completed
- Throws BlockedTaskError when starting a blocked task
- Records status change in task history

Use mocks for the repository layer. Each test must include Arrange/Act/Assert comments.
```

---

## Step 2 — Generate Integration Tests

```
Read doc/frd.md (Gherkin acceptance criteria US-001 to US-006).

Generate integration tests in tests/integration/:

POST /api/v1/tasks:
- "Developer creates a valid task" → 201, { success: true, data: { status: "To Do" } }
- "Task creation rejected when title is missing" → 400, { success: false, error: { code: "VALIDATION_ERROR" } }
- "Unauthenticated request is rejected" → 401

PATCH /api/v1/tasks/:id/status:
- "Updates To Do to In Progress with no blocking dependencies" → 200, history entry created
- "Blocked when dependency is incomplete" → 422, { error: { code: "TASK_BLOCKED" } }

POST /api/v1/tasks/:id/dependencies:
- "Add valid dependency" → 201
- "Circular dependency rejected" → 422
- "Adding dependency to incomplete task sets status to Blocked"

Each test resets database state using the helpers from Step 1.
```

---

## Step 3 — Run Tests and Check Coverage

```
Run the unit tests and show me the coverage report.
List any files in src/ with less than 80% test coverage.
```

---

## Verify

- [ ] Unit tests cover `TaskService` with at least 8 test cases
- [ ] Integration tests cover 3 main API endpoints
- [ ] Tests use the helper factory functions
- [ ] Coverage report is generated

---

> **⚡ Extension**: Test the SQL stored procedures: `Generate tests in tests/unit/database/ for the update_task_status and add_task_dependency PL/pgSQL functions — verify blocking logic, exceptions, and circular dependency detection.`

---

**Next**: [Exercise 14 — Security Review](exercise-14-security.md)
