# Exercise 04 — Generate the Functional Requirements Document

**Duration**: 3 minutes  
**Copilot Feature**: FRD Custom Agent  
**Goal**: Use the FRD agent to create testable user stories and use cases from the BRD and TSD.

---

## Step 1 — Select the FRD Agent and Send the Prompt

1. Switch to **FRD Author** in the agent selector
2. Send this prompt:

```
Read #requirement.md, #brd.md and #tsd.md. Create a comprehensive Functional Requirements Document saved as doc/frd.md.

Include:
- A User Roles & Permissions Matrix (Developer / Team Lead / Project Manager / QA Engineer vs all features)
- Use cases for: Task Creation (UC-001), Task Assignment (UC-002), Task Dependency Management (UC-003), Task Status Tracking (UC-004), Task Listing and Filtering (UC-005), Project Progress Summary (UC-006)
- User stories with Given/When/Then acceptance criteria in Gherkin format
- Functional Requirements Catalogue with FR-IDs linked to requirement sections
- Data validation rules for all input fields
- Notification triggers for task reassignment, dependency blocking, and status changes
- Error scenarios and user-facing error messages
```

> **⚡ Tip:** While the agent generates the FRD, set up your tech stack choice for Exercise 05.

---

## Step 2 — Verify Docs Are Complete

You should now have:

```
doc/
├── brd.md    ← Business requirements (Exercise 02)
├── tsd.md    ← Technical architecture (Exercise 03)
└── frd.md    ← Functional requirements + user stories (this exercise)
```

- [ ] Six use cases (UC-001 to UC-006) with Gherkin scenarios
- [ ] FR-IDs can be traced back to BRD requirement IDs

---

## Key Takeaway

> BRD → TSD → FRD is the natural SDLC chain. Each agent read the previous document as its input. This is **document-driven agentic workflow** — Copilot maintains context across the entire specification phase.

---

**Next**: [Exercise 05 — Custom Instructions](exercise-05-custom-instructions.md)
