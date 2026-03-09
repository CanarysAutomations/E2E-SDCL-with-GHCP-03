# Exercise 09 — Build APIs with the Local Agent

**Duration**: 4 minutes  
**Copilot Feature**: Local (Default) Agent — Agentic Coding  
**Goal**: Scaffold the project and implement core REST API endpoints end-to-end.

---

## Step 1 — Scaffold the Project

Switch to **Agent mode** (default agent). Send this prompt:

```
Read #tsd.md and the API Design section. Scaffold the initial ITMS REST API project:
- Root config files (match stack from copilot-instructions.md)
- Folder structure: src/routes/, src/controllers/, src/services/, src/repositories/, src/models/, src/middleware/, src/config/
- App entry point on port 3000 (or 8000 for Python)
- Environment variable loading (.env.example with all required vars)
- Health check: GET /api/v1/health → { status: "ok", timestamp, version: "1.0.0" }
- README.md with setup instructions

Do NOT implement business logic — scaffolding only.
```

> **⚡ Tip:** While the agent scaffolds, copy the Background Agent prompt from Exercise 10 — you can submit it immediately after Step 3 so it runs in parallel.

---

## Step 2 — Implement the Authentication API

```
Implement the Authentication API from #tsd.md:

1. POST /api/v1/auth/login
   - Accepts: { email, password }
   - Validates input (reject invalid email format, password < 8 chars)
   - Returns: { success: true, data: { token, refreshToken, expiresIn, user: { id, name, email, role } } }
   - On failure: { success: false, error: { code: "INVALID_CREDENTIALS", message: "..." } }
   - Rate limit: 5 attempts per minute per IP

2. POST /api/v1/auth/logout — requires JWT, invalidates token

3. POST /api/v1/auth/refresh — accepts { refreshToken }, returns new access token

Apply all standards from .github/copilot-instructions.md.
```

---

## Step 3 — Implement the Task Management API

```
Implement the Task Management API from doc/tsd.md:

1. POST /api/v1/tasks
   - Auth required
   - Accepts: { title, description, priority, assignedUserId, dueDate }
   - Validates: title required, priority is Low/Medium/High, dueDate is valid
   - Returns: created task with status "To Do"

2. GET /api/v1/tasks
   - Auth required, query params: status, priority, assignedUserId, page, limit

3. PATCH /api/v1/tasks/:id/status
   - Accepts: { status } (To Do / In Progress / Blocked / Completed)
   - Records status change in history

Create corresponding service, repository, and model/schema files.
```

> **⚡ Now launch the Background Agent from Exercise 10** with the task assignment endpoints — it will run while you continue with subsequent exercises.

---

## Verify

- [ ] `GET /api/v1/health` returns `{ status: "ok" }`
- [ ] `POST /api/v1/auth/login` and `POST /api/v1/tasks` are implemented
- [ ] Folder structure matches `src/routes/, src/services/, src/repositories/`

---

**Next**: [Exercise 10 — Background Agent](exercise-10-background-agent.md)
