# Exercise 02 — Generate the Business Requirements Document

**Duration**: 3 minutes  
**Copilot Feature**: BRD Custom Agent  
**Goal**: Use the BRD agent to generate `doc/brd.md` from `requirement.md`.

---

## Step 1 — Select the BRD Agent and Send the Prompt

1. Open Copilot Chat (`Ctrl+Alt+I`)
2. Select **BRD Author** from the agent dropdown
3. Send this prompt:

```
Read the project requirements from #requirement.md and create a comprehensive Business Requirements Document. Save it as doc/brd.md.

- Number all requirements uniquely (BR-F-001, BR-NF-001, BR-R-001...)
- Include a stakeholder table with interests and influence levels
- Include a risks and mitigations table
- Add a glossary of domain terms
```

> **⚡ Tip:** While the agent generates the BRD (1–2 min), read the next exercise so you can immediately send the TSD prompt when the BRD is ready.

---

## Step 2 — Review the Output

When `doc/brd.md` appears, quickly verify:

- [ ] Functional requirements are numbered BR-F-001…
- [ ] Non-functional requirements have measurable acceptance criteria
- [ ] A stakeholder table and risks table are present

---

## Key Takeaway

> The BRD agent gives Copilot a **persistent, reusable role**. You never have to re-explain BA document structure — the agent encodes your standards once and applies them every time.

---

**Next**: [Exercise 03 — Generate TSD](exercise-03-tsd.md)
