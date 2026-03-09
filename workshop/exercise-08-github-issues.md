# Exercise 08 — Create GitHub Issues via MCP

**Duration**: 4 minutes  
**Copilot Feature**: GitHub MCP Server  
**Goal**: Connect the GitHub MCP and convert the implementation plan into GitHub Issues automatically.

---

## Part A — Setup (one-time)

> **Skip to Part B if GitHub MCP is already configured in your workspace.**

Open (or create) `.vscode/mcp.json`:

```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}" }
    }
  },
  "inputs": [
    { "id": "github_token", "type": "promptString", "description": "GitHub Personal Access Token", "password": true }
  ]
}
```

Create a PAT at https://github.com/settings/tokens (scopes: `repo`, `issues`, `read:org`) and reload VS Code.

---

## Part B — Create a Repository

```
Using the GitHub MCP, create a repository named "itms-app":
- Description: "Intelligent Task Management System — Workshop App"
- Private, initialized with README
```

Note your repo as `[your-username]/itms-app`.

---

## Part C — Generate Issues from the Implementation Plan

```
Read doc/implementation-plan.md and convert it into GitHub Issues for [your-username]/itms-app.

For each task:
- Clear title and description
- Acceptance criteria as checkboxes
- Labels: backend, database, testing, infrastructure, security
- Milestone matching the Phase

Create milestones first, then create issues for Phase 0 and Phase 1 tasks.
Use the GitHub MCP to create them directly.
```

---

## Verify

- [ ] Milestones created for each Phase
- [ ] Issues have labels and acceptance criteria checkboxes
- [ ] Issues are assigned to the correct milestone

---

> **⚡ Extension**: `Using the GitHub MCP, add all Phase 1 issues to a new Project board "ITMS Sprint 1" with columns: To Do / In Progress / Done.`

---

**Next**: [Exercise 09 — Build APIs with the Local Agent](exercise-09-api-local-agent.md)