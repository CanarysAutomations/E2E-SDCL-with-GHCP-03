# Exercise 04 — Generate the Functional Requirements Document

**Duration**: 4 minutes  
**Copilot Feature**: FRD Custom Agent  
**Goal**: Use the FRD agent to create testable user stories and use cases from the BRD and TSD.

---

## Background

The FRD is the document development teams and QA engineers work from directly. It breaks down business requirements into **use cases**, **user stories with Gherkin acceptance criteria**, and a **permissions matrix**. The FRD Author agent synthesizes the BRD and TSD into this developer-ready document.

---

## Step 1 — Switch to the FRD Agent

1. In Copilot Chat, click the agent selector
2. Select **FRD Author**

---

## Step 2 — Send the FRD Generation Prompt

Copy and paste this prompt:

```
Read #brd.md, #tsd.md, and #requirement.md. Create a comprehensive Functional Requirements Document saved as doc/frd.md.

Include:
- A User Roles & Permissions Matrix (Employee / Manager / HR Admin / IT Admin vs all features)
- Detailed use cases for: Leave Request (UC-001), Leave Approval (UC-002), Leave Cancellation (UC-003), Leave Balance Inquiry (UC-004), Attendance Check-In/Out (UC-005), HR Monthly Report (UC-006)
- User stories for each use case with Given/When/Then acceptance criteria in Gherkin format
- A complete Functional Requirements Catalogue with FR-IDs linked to BRD BR-IDs
- Data validation rules for all input fields
- All email/notification triggers with recipient and content
- Error scenarios and user-facing error messages
```

---

## Step 3 — Inspect the Output

Open `doc/frd.md` and verify:

- [ ] Permissions matrix table exists — each role has ✅ / ❌ for each feature
- [ ] At least 6 use cases with actor, preconditions, normal flow, and alternates
- [ ] User stories use "As a [role], I want [action], so that [benefit]" format
- [ ] Every user story has at least 2 Given/When/Then scenarios
- [ ] FR-IDs link back to BR-F-IDs from the BRD
- [ ] Story point estimates are assigned (1/2/3/5/8)

---

## Step 4 — Generate a Sprint Backlog View (Optional)

Send this follow-up to see the work broken into a sprint:

```
Based on doc/frd.md, create a Sprint 1 backlog containing the highest-priority user stories 
that deliver the core leave request and approval flow as a working end-to-end feature.
Format as a markdown table with columns: US-ID | Title | Story Points | Priority | Dependencies.
Append this as a "Sprint 1 Backlog" section at the end of doc/frd.md.
```

---

## Checkpoint — Docs Complete ✅

You should now have:

```
doc/
├── brd.md    ← Business requirements (from Exercise 02)
├── tsd.md    ← Technical architecture (from Exercise 03)
└── frd.md    ← Functional requirements + user stories (this exercise)
```

These three documents form the **specification foundation** for all remaining exercises. Every piece of code, database schema, test, and deployment script will trace back to one of these files.

---

## Key Takeaway

> Notice how each agent built on the previous output. BRD → TSD → FRD is the natural SDLC chain, and each agent was pre-wired to read the prior document. This is the power of **document-driven agentic workflows** — Copilot maintains context across the entire specification phase without you having to copy-paste content.

---

**Next**: [Exercise 05 — Create Custom Instructions](exercise-05-custom-instructions.md)
