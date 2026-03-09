# Exercise 07 — Create an Implementation Prompt File

**Duration**: 2 minutes  
**Copilot Feature**: Prompt Files (`.prompt.md`)  
**Goal**: Package the implementation plan workflow into a reusable `/command` the whole team can invoke.

---

## What is a Prompt File?

A `.prompt.md` file stored in `.github/prompts/` is a saved, reusable prompt. Team members invoke it from Copilot Chat by typing `/` followed by the prompt name — no need to remember or re-type the full prompt.

---

## Step 1 — Create a Project-Specific Prompt File

In Copilot Chat (default Agent), send:

```
Create a prompt file at .github/prompts/itms-implementation-plan.prompt.md

When invoked, this prompt should:
1. Read #frd.md and #tsd.md
2. Generate a phased implementation plan for our stack: [YOUR STACK from Exercise 05]
3. Reference folder structure: src/routes/, src/services/, src/repositories/, src/models/
4. Include database migration tasks
5. Flag tasks suitable for background agent execution

Format: phases as H2 headers, tasks as a table: ID | Task | Effort | FRD Ref | Parallel? | Background Agent?
```

---

## Step 2 — Test the Prompt File

1. In Copilot Chat, type `/`
2. Type `itms` — you should see **itms-implementation-plan** appear
3. Select it and press Enter — Copilot re-runs the plan generation

---

## Key Takeaway

> Prompt files scale Copilot adoption across a team. Instead of one person knowing "the right prompt," everyone has a `/itms-implementation-plan` command they invoke consistently.

---

**Next**: [Exercise 08 — Create GitHub Issues via MCP](exercise-08-github-issues.md)\n