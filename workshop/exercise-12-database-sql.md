# Exercise 12 — Database Design, SQL Scripts & Stored Procedures

**Duration**: 4 minutes  
**Copilot Feature**: Local Agent + Instructions  
**Goal**: Generate the full database schema, migration scripts, stored procedures, and seed data.

---

## Step 1 — Generate the Database Schema

In Copilot Chat (Agent mode), send:

```
Reference the ER diagram in doc/tsd.md and the context map at .github/skills/context-map/context-map.md.

Create migration files in db/migrations/:

1. 001_create_users.sql — columns: id (UUID), email, password_hash, first_name, last_name, role (ENUM: DEVELOPER/TEAM_LEAD/PROJECT_MANAGER/QA_ENGINEER), is_active, created_at, updated_at

2. 002_create_tasks.sql — columns: id (UUID), title, description, priority (ENUM: LOW/MEDIUM/HIGH), status (ENUM: TO_DO/IN_PROGRESS/BLOCKED/COMPLETED), assigned_user_id (FK), estimated_completion_date, created_by (FK), timestamps

3. 003_create_task_dependencies.sql — columns: id, task_id (FK), depends_on_task_id (FK), created_by, created_at. Constraint: UNIQUE(task_id, depends_on_task_id), no self-referencing

4. 004_create_task_status_history.sql — columns: id, task_id (FK), previous_status, new_status, changed_by (FK), changed_at, note

5. 005_create_audit_log.sql — id, table_name, record_id, operation (INSERT/UPDATE/DELETE), old_values (JSONB), new_values (JSONB), performed_by, performed_at

Add indexes on assigned_user_id+status, task dependencies task_id, status+priority. Use PostgreSQL syntax.
```

---

## Step 2 — Create Stored Procedures and Seed Data

```
Create PL/pgSQL functions in db/procedures/:

1. create_task(p_title, p_description, p_priority, p_assigned_user_id, p_due_date, p_created_by) RETURNS UUID
   - Validates priority and assigned user, inserts task as TO_DO, logs initial status history. Single transaction.

2. update_task_status(p_task_id, p_new_status, p_changed_by, p_note) RETURNS VOID
   - Validates the transition; raise exception if task is BLOCKED by incomplete dependencies; updates status and logs history.

3. add_task_dependency(p_task_id, p_depends_on_task_id, p_created_by) RETURNS VOID
   - Checks for circular dependencies; inserts record; sets task to BLOCKED if dependency is not COMPLETED.

4. In db/triggers/audit_trigger.sql — a generic trigger logging INSERT/UPDATE/DELETE on tasks and task_dependencies to audit_log.

Then create db/seeds/001_seed_data.sql with:
- 10 users: 1 PM, 2 Team Leads, 7 Developers/QA
- 20 sample tasks across all statuses and priorities
- 5 dependency relationships (some blocking, some resolved)
```

> **No database available?** Add `— I don't have PostgreSQL available. Create mock JSON data files in db/mock/ instead, and create src/repositories/mock/ implementations that read from those JSON files.`

---

## Verify

- [ ] Migration files are numbered sequentially with all required columns
- [ ] Stored procedures handle transactions and raise exceptions for invalid transitions
- [ ] Seed data is self-consistent (FK references are valid)

---

**Next**: [Exercise 13 — Testing](exercise-13-testing.md)
