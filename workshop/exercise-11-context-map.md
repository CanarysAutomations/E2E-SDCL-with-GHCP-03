# Exercise 11 — Create a Context Map Skill

**Duration**: 3 minutes  
**Copilot Feature**: Skills (`SKILL.md`)  
**Goal**: Generate a codebase map that improves accuracy of all subsequent Copilot interactions.

---

A **Skill** is an on-demand multi-step workflow in a `SKILL.md` file. The **Context Map** skill generates a structured map of your codebase — files, purposes, relationships, and patterns. Attaching this map to future prompts eliminates hallucinations (Copilot inventing wrong file paths or function names).

---

## Step 1 — Fetch the Skill

In Copilot Chat (Agent mode), send:

```
Fetch the Context Map skill from this URL and save it to .github/skills/context-map/SKILL.md:
https://raw.githubusercontent.com/github/awesome-copilot/main/skills/context-map/SKILL.md

Confirm the file was saved by showing me its first 10 lines.
```

> **If network access is unavailable**: Ask the instructor for the `SKILL.md` file, or create `.github/skills/context-map/SKILL.md` manually.

---

## Step 2 — Run the Skill

```
Follow the instructions in .github/skills/context-map/SKILL.md to generate a context map.

Save as .github/skills/context-map/context-map.md covering:
- All directories and their purpose
- Key source files and what they do
- Main data models and relationships
- API endpoints and handler locations
- Configuration patterns
```

---

## Step 3 — Use the Context Map

Test it with:

```
Using .github/skills/context-map/context-map.md, answer:
1. Which file handles task dependency blocking?
2. Where is the JWT authentication middleware?
3. What database tables are currently defined?
```

---

## Verify

- [ ] `.github/skills/context-map/context-map.md` exists
- [ ] Contains directory descriptions, key file purposes, and API routes

---

## Key Takeaway

> Prefix complex future prompts with `Reference the context map at .github/skills/context-map/context-map.md for codebase context, then...` — this single line dramatically reduces Copilot hallucinations.

---

**Next**: [Exercise 12 — Database & SQL](exercise-12-database-sql.md)
