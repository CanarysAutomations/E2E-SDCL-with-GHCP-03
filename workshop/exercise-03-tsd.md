# Exercise 03 — Generate the Technical Specification Document

**Duration**: 3 minutes  
**Copilot Feature**: TSD Custom Agent  
**Goal**: Use the TSD agent to design system architecture from the BRD.

---

## Step 1 — Select the TSD Agent and Send the Prompt

1. Switch to **TSD Author** in the agent selector
2. Send this prompt:

```
Read #brd.md and #requirement.md, then create a complete Technical Specification Document saved as doc/tsd.md.

- Include a Mermaid system architecture diagram showing all major components
- Include a Mermaid ER diagram for the database schema
- Design REST API endpoints for: authentication, user management, task management, task assignment, task dependencies, and reporting
- Recommend a technology stack with justifications
- Include security architecture addressing the OWASP Top 10
- Define a CI/CD pipeline architecture
- Trace every technical decision back to a BRD requirement ID
```

> **⚡ Tip:** While the agent generates the TSD, read Exercise 04 and have the FRD prompt ready.

---

## Step 2 — Review the Output

- [ ] Mermaid diagrams are present (architecture + ER)
- [ ] REST API endpoints are documented in a table
- [ ] Technology stack has justifications

---

## Key Takeaway

> The TSD becomes the **source of truth** for every subsequent exercise — the API design drives Ex09 coding, the ER diagram drives Ex12 database work, and the deployment architecture drives Ex16 IaC.

---

> **⚡ Extension** (skip if short on time): Add notification architecture with a follow-up prompt:
> ```
> Update the Integration Points section in doc/tsd.md to cover SendGrid email
> (async via message queue) and Microsoft Teams webhook. Include a sequence diagram
> showing the task status update → notification flow.
> ```

---

**Next**: [Exercise 04 — Generate FRD](exercise-04-frd.md)
