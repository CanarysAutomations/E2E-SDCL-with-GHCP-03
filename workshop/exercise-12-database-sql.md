# Exercise 12 — Database Design, SQL Scripts & PL/SQL

**Duration**: 5 minutes  
**Copilot Feature**: Local Agent + Instructions  
**Goal**: Generate the full database schema, migration scripts, seed data, and stored procedures for the LAMS application.

---

## Background

Most business applications have critical business logic in the database layer — calculated leave balances, transactional approval workflows, audit triggers. This exercise generates the complete SQL layer for LAMS, including PL/SQL (Oracle) or PL/pgSQL (PostgreSQL) stored procedures.

> **If you don't have a database available**, follow the Mock Data path at the end of this exercise — Copilot will create JSON mock data with the same schema structure so your API can run without a real DB.

---

## Step 1 — Generate the Database Schema

In Copilot Chat (Agent mode), send:

```
Reference the ER diagram in doc/tsd.md and the context map at .github/skills/context-map/context-map.md.

Create the database schema migration files in db/migrations/:

1. db/migrations/001_create_users.sql — Users table
   Columns: id (UUID), email, password_hash, first_name, last_name, department, 
   manager_id (self-reference FK), role (ENUM: EMPLOYEE/MANAGER/HR_ADMIN/IT_ADMIN),
   is_active, created_at, updated_at

2. db/migrations/002_create_leave_types.sql — Leave Types table
   Columns: id, name, max_days_per_year, carry_forward_days, requires_document,
   requires_hr_approval, is_active

3. db/migrations/003_create_leave_balances.sql — Leave Balance per employee per year
   Columns: id, user_id (FK), leave_type_id (FK), year, allocated_days, used_days,
   carried_over_days, updated_at
   
4. db/migrations/004_create_leave_requests.sql — Leave Requests table
   Columns: id (UUID), user_id, leave_type_id, start_date, end_date, business_days,
   reason, status (ENUM: PENDING/MANAGER_APPROVED/APPROVED/REJECTED/CANCELLED),
   manager_id, manager_comment, hr_admin_id, hr_comment,
   created_at, updated_at, approved_at, cancelled_at

5. db/migrations/005_create_attendance.sql — Attendance records
   Columns: id, user_id, date, check_in_time, check_out_time, status 
   (ENUM: PRESENT/ABSENT/LATE/HALF_DAY/ON_LEAVE)

6. db/migrations/006_create_audit_log.sql — Audit trail
   Columns: id, table_name, record_id, operation (INSERT/UPDATE/DELETE),
   old_values (JSONB), new_values (JSONB), performed_by, performed_at

Add appropriate indexes on: email, user_id + date (attendance), user_id + year (balances), status + manager_id (requests).
Add foreign key constraints with ON DELETE RESTRICT.
Use PostgreSQL syntax.
```

---

## Step 2 — Create Stored Procedures / Functions

Send this prompt:

```
Create db/procedures/ with the following PL/pgSQL functions:

1. db/procedures/calculate_business_days.sql
   Function: calculate_business_days(start_date DATE, end_date DATE) RETURNS INTEGER
   - Count weekdays only (Mon–Fri) between the two dates inclusive
   - Exclude dates in a public_holidays table (create that table too)

2. db/procedures/apply_leave_request.sql
   Function: apply_leave_request(p_user_id UUID, p_leave_type_id INT, p_start_date DATE, p_end_date DATE, p_reason TEXT) RETURNS UUID
   - Calculates business days using calculate_business_days()
   - Checks leave balance availability; raises exception if insufficient
   - Inserts leave request record with status PENDING
   - Returns the new leave request ID
   - All in a single transaction

3. db/procedures/approve_leave_request.sql
   Function: approve_leave_request(p_request_id UUID, p_approver_id UUID, p_stage TEXT) RETURNS VOID
   - Validates approver role (MANAGER for first stage, HR_ADMIN for final)
   - Updates request status (MANAGER_APPROVED or APPROVED)
   - On final approval: deducts from leave_balances.used_days
   - Raises exception if already approved/rejected/cancelled

4. db/procedures/cancel_leave_request.sql
   Function: cancel_leave_request(p_request_id UUID, p_cancelled_by UUID) RETURNS VOID
   - Validates request can be cancelled (PENDING or APPROVED only)
   - Validates canceller permission (own request, team manager, or HR)
   - If APPROVED: restores balance
   - Updates status to CANCELLED

5. db/triggers/audit_trigger.sql
   Trigger: Create a generic audit trigger function that logs all INSERT/UPDATE/DELETE
   operations on leave_requests and leave_balances to the audit_log table.
   Apply the trigger to both tables.
```

---

## Step 3 — Create Seed Data

Send this prompt:

```
Create db/seeds/001_seed_data.sql with realistic test data:
- 4 leave types (Annual, Sick, Maternity, Paternity) with correct day limits
- 10 users: 1 HR Admin, 2 Managers, 7 Employees (with manager assignments)
- Leave balances for current year for all employees
- 5 sample leave requests in various statuses (PENDING, APPROVED, REJECTED, CANCELLED)
- A public_holidays table entry for common 2026 holidays

Use realistic names and UUIDs. Make sure the data is self-consistent (managers exist before employees reference them).
```

---

## Step 4 — Mock JSON Path (No Database Available)

> Skip this step if you have a working database.

If you don't have PostgreSQL available, send this prompt instead:

```
I don't have a database available. Create mock JSON data files in db/mock/ that replicate the database schema so the API can run with an in-memory data store.

Create:
- db/mock/users.json — 10 users matching the users table schema
- db/mock/leave_types.json — 4 leave types
- db/mock/leave_balances.json — balances for all users for 2026
- db/mock/leave_requests.json — 5 sample requests in different statuses
- db/mock/README.md — explains how to switch between real DB and mock data mode

Also create src/repositories/mock/ implementations of the repositories that read from these JSON files instead of querying the database.
```

---

## Verify

Check `db/` folder:

- [ ] Migration files are numbered and sequential (001_, 002_…)
- [ ] Each migration creates a table with all required columns
- [ ] Indexes are defined
- [ ] Stored procedures include transaction handling and exception raising
- [ ] Audit trigger is created for the correct tables
- [ ] Seed data is self-consistent

---

## Key Takeaway

> Copilot understands both SQL DDL and procedural SQL (PL/pgSQL/PL/SQL). By anchoring the prompt to the TSD's ER diagram and the business rules from the FRD, you get database code that actually matches your requirements — not generic boilerplate. The stored procedures encode business rules (leave balance checks, approval stages) in the database layer where they belong.

---

**Next**: [Exercise 13 — Unit & Functional Tests](exercise-13-testing.md)
