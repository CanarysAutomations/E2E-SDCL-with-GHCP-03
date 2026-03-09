# Exercise 03 — Generate the Technical Specification Document

**Duration**: 4 minutes  
**Copilot Feature**: TSD Custom Agent  
**Goal**: Use the TSD agent to design the system architecture from the BRD.

---

## Background

The TSD bridges business requirements and engineering. Your **TSD Author** agent acts as a Solutions Architect — it reads the BRD, proposes technology choices, designs the data model and API contracts, and produces a document the development team can build from.

---

## Step 1 — Switch to the TSD Agent

1. In Copilot Chat, click the agent selector
2. Select **TSD Author**

---

## Step 2 — Send the TSD Generation Prompt

Copy and paste this prompt:

```
Read doc/brd.md and req.md, then create a complete Technical Specification Document saved as doc/tsd.md.

Requirements:
- Include a Mermaid system architecture diagram showing all major components
- Include a Mermaid ER diagram for the database schema (include all tables needed for leave management)
- Design REST API endpoints for: authentication, user management, leave requests, leave approvals, attendance, and reporting
- Recommend a technology stack with justifications (consider the Azure deployment constraint from req.md)
- Include security architecture addressing the OWASP Top 10
- Define a CI/CD pipeline architecture
- Trace every technical decision back to a BRD requirement ID
```

---

## Step 3 — Monitor the Plan

The TSD agent will plan its approach. Look for:
- It plans to read BOTH `doc/brd.md` AND `req.md`
- It mentions Mermaid diagrams
- It is NOT writing application code

Approve the plan.

---

## Step 4 — Inspect the Output

Open `doc/tsd.md` and verify:

- [ ] Mermaid architecture diagram renders correctly in VS Code preview (`Ctrl+Shift+V`)
- [ ] ER diagram includes tables: `users`, `leave_requests`, `leave_balances`, `leave_types`, `attendance_records` (or similar)
- [ ] At least 15 API endpoints are listed in the endpoint catalogue
- [ ] Security section mentions JWT, RBAC, and at least 3 OWASP categories
- [ ] Technology stack table exists with justifications

---

## Step 5 — Ask for a Specific Architecture Decision (Optional)

Try this follow-up to see how the agent reasons:

```
The system needs to handle email notifications and Teams webhook alerts. 
Update the Integration Points section in doc/tsd.md to cover:
- SendGrid for email (async via a message queue)
- Microsoft Teams webhook for manager alerts
- Include a sequence diagram showing the leave approval notification flow
```

---

## Key Takeaway

> The architecture designed here becomes the **source of truth** for the next exercises. Every API you build, every table you create, and every test you write will trace back to `doc/tsd.md`. This is how Copilot becomes a true SDLC co-pilot — not just a code generator, but an architectural collaborator.

---

**Next**: [Exercise 04 — Generate FRD](exercise-04-frd.md)
