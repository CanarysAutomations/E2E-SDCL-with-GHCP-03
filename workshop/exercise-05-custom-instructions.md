# Exercise 05 — Create Custom Instructions for Your Language

**Duration**: 3 minutes  
**Copilot Feature**: Workspace Instructions (`copilot-instructions.md`)  
**Goal**: Set always-on coding standards that Copilot follows in every conversation.

---

## Step 1 — Choose Your Tech Stack

Pick one option for the rest of the workshop:

| Option | Language | Framework | Database |
|--------|----------|-----------|----------|
| A | TypeScript / Node.js | Express | PostgreSQL or your choice |
| B | Python | FastAPI | PostgreSQL or your choice |
| C | Java | Spring Boot | PostgreSQL or your choice |
| D | C# / .NET | ASP.NET Core | SQL Server or your choice |

> **Default**: Option A (TypeScript/Node.js/PostgreSQL) if unsure.

---

## Step 2 — Generate the Instructions File

Switch to the **default Copilot agent**. Send this prompt (replace `[YOUR CHOICE]`):

I am building a REST API application using [YOUR CHOICE — e.g., TypeScript with Express and PostgreSQL].

Create .github/copilot-instructions.md with workspace-wide coding standards.

Include:
1. Language & framework conventions (naming, file structure)
2. API: versioning (/api/v1/), response envelope { success, data, error, meta }
3. Error handling: custom error classes, centralized middleware, proper HTTP codes
4. Security: always validate input with a schema library, parameterized queries only
5. Database: use migrations, use ORM/query builder — no raw string SQL
6. Testing: unit test every function, integration test all API endpoints
7. Logging: structured JSON logs with request ID, user ID, operation name
8. Code style: no console.log in production, functions under 30 lines
9. Git: conventional commits (feat:, fix:, docs:, test:, chore:)

## Step 3 — Verify

- [ ] File exists at `.github/copilot-instructions.md`
- [ ] Contains input validation and parameterized query rules
- [ ] Has the `/api/v1/` URL convention


## Key Takeaway

> Instructions set the **floor** for code quality. You define your standards once — Copilot applies them automatically to every piece of code it generates in this workspace.

---

**Next**: [Exercise 06 — Plan Mode](exercise-06-plan-mode.md)