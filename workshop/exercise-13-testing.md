# Exercise 13 — Write Unit & Functional Tests

**Duration**: 5 minutes  
**Copilot Feature**: Local Agent + Prompt Files  
**Goal**: Generate comprehensive unit and integration/functional tests for the LAMS API.

---

## Background

Tests are where the FRD's acceptance criteria become code. Each **Given/When/Then** scenario in `doc/frd.md` maps to an automated test. Copilot can read those acceptance criteria and write tests that verify them — turning the FRD into a living test suite.

---

## Step 1 — Generate the Test Configuration

Send this prompt in Copilot Chat (Agent mode):

```
Reference the context map at .github/skills/context-map/context-map.md and .github/copilot-instructions.md.

Set up the testing infrastructure for the LAMS project:
1. Install and configure the appropriate test framework for the tech stack (Jest for Node.js, pytest for Python, JUnit for Java)
2. Create tests/unit/ and tests/integration/ directory structure
3. Set up a test database configuration (use the mock data from db/mock/ if real DB is unavailable)
4. Create a tests/helpers/ folder with:
   - A factory function to create test users with different roles
   - A function to create authenticated test requests (with valid JWT)
   - A database cleanup helper to reset state between tests
5. Add test scripts to package.json / pyproject.toml:
   - "test:unit" — runs unit tests only
   - "test:integration" — runs integration tests
   - "test:all" — runs everything with coverage report
```

---

## Step 2 — Generate Unit Tests for the Service Layer

Send this prompt:

```
Read doc/frd.md (focus on FR-IDs for leave management) and the service files in src/services/.

Generate unit tests in tests/unit/ for the Leave Service:

Test Suite: LeaveService.applyForLeave()
- Test: Should create a PENDING leave request when employee has sufficient balance
  (maps to Given employee has 15 annual days remaining When they apply for 5 days Then a PENDING request is created)
- Test: Should throw InsufficientBalanceError when leave balance is 0
- Test: Should throw ValidationError when start_date is in the past
- Test: Should throw ValidationError when end_date is before start_date
- Test: Should calculate business days correctly (skip weekends)
- Test: Should allow unpaid leave even with 0 balance

Test Suite: LeaveService.approveLeave()
- Test: Manager can approve a PENDING request for a direct report
- Test: Manager cannot approve a request from an employee not in their team
- Test: HR Admin can give final approval after manager approval
- Test: Cannot approve an already-approved request (idempotency check)
- Test: Cannot approve a cancelled request

Use mocks for the repository layer in all unit tests.
Each test must include Arrange / Act / Assert structure as comments.
```

---

## Step 3 — Generate Integration Tests for the API

Send this prompt:

```
Read doc/frd.md (focus on the Gherkin acceptance criteria in user stories US-001 to US-006).

Generate integration tests in tests/integration/ for the Leave Request API:

Test Suite: POST /api/v1/leave/requests
- Scenario: "Employee submits a valid annual leave request"
  Given: Authenticated as employee with 20 days balance
  When: POST /api/v1/leave/requests with { leaveTypeId, startDate, endDate, reason }
  Then: 201 Created, response has { success: true, data: { id, status: "PENDING", businessDays } }

- Scenario: "Request rejected when leave balance insufficient"
  Given: Employee with 0 days balance
  When: POST request for 3 days
  Then: 422 Unprocessable Entity, { success: false, error: { code: "INSUFFICIENT_BALANCE" } }

- Scenario: "Unauthenticated request is rejected"
  Given: No JWT token
  When: POST request
  Then: 401 Unauthorized

Test Suite: PUT /api/v1/leave/requests/:id/approve
- Scenario: "Manager approves a team member's leave request"
- Scenario: "Manager cannot approve request outside their team" → 403 Forbidden
- Scenario: "HR Admin gives final approval on manager-approved request"

Test Suite: DELETE /api/v1/leave/requests/:id (Cancel)
- Scenario: "Employee cancels their own PENDING request" → balance restored: No change
- Scenario: "Employee cancels their APPROVED request" → balance restored: Yes
- Scenario: "Cannot cancel a past-date approved request"

Each integration test should start with a clean database state using the test helpers from Step 1.
```

---

## Step 4 — Generate a Test for a SQL Stored Procedure

Send this prompt:

```
The calculate_business_days() PostgreSQL function in db/procedures/ needs tests.

Create tests/unit/database/test_calculate_business_days.sql (or a test file appropriate for the stack) that verifies:
- Mon to Fri of the same week = 5 business days
- Sat to Fri of next week = 5 business days (skips weekend)
- Single day (Mon) = 1 business day  
- Range that includes a public holiday = correct count minus holiday
- Same day = 1 business day

If not using a real database, create an equivalent unit test using the JavaScript/Python implementation of business day calculation.
```

---

## Step 5 — Run Tests and Check Coverage

Send this prompt:

```
Run the unit tests using the terminal and show me the coverage report.
Identify any files in src/ that have less than 80% test coverage and list them.
```

---

## Verify

- [ ] Unit tests exist for `LeaveService` with at least 8 test cases
- [ ] Integration tests cover the 3 main API endpoints
- [ ] Tests use the test helpers (factory functions, auth helper)
- [ ] Each test follows Arrange/Act/Assert structure
- [ ] Coverage report is generated

---

## Key Takeaway

> When Copilot writes tests from the FRD's Gherkin criteria, the tests become a **living specification**. Every test failure tells you exactly which user story is broken. This is the promise of Behavior-Driven Development — and Copilot makes it practical by eliminating the tedious work of writing the test boilerplate.

---

**Next**: [Exercise 14 — Security Review](exercise-14-security.md)
