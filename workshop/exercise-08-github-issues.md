# Exercise 08 — Create GitHub Issues via MCP

**Duration**: 5 minutes  
**Copilot Feature**: GitHub MCP Server + Prompt File  
**Goal**: Convert the implementation plan into GitHub Issues using the GitHub MCP and the pre-built issues prompt file.

---

## Background

The **Model Context Protocol (MCP)** lets Copilot interact with external systems. The **GitHub MCP server** gives Copilot the ability to create issues, pull requests, branches, and more — directly from chat.

In this exercise, you'll connect the GitHub MCP and use the `github-issues.prompt.md` file to automatically create work items from your implementation plan.

---

## Part A — Install the GitHub MCP Server (One-Time Setup)

### Step 1 — Install the GitHub MCP

> **If GitHub MCP is already configured in your workspace, skip to Part B.**

Open VS Code Command Palette (`Ctrl+Shift+P`) and search for:
```
MCP: Add Server
```

Select **GitHub MCP** from the list, or add it manually:

1. Open (or create) `.vscode/mcp.json` in your workspace
2. Add the following configuration:

```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
      }
    }
  },
  "inputs": [
    {
      "id": "github_token",
      "type": "promptString",
      "description": "GitHub Personal Access Token",
      "password": true
    }
  ]
}
```

3. Create a GitHub Personal Access Token at https://github.com/settings/tokens
   - Required scopes: `repo`, `issues`, `read:org`
4. Reload the VS Code window — GitHub MCP will start automatically

---

## Part B — Create a GitHub Repository (if not already done)

If you don't have a repository yet, create one:

```
Using the GitHub MCP, create a new repository named "lams-app" with:
- Description: "Leave & Attendance Management System — Workshop App"
- Private repository
- Initialize with a README
```

Note your repository as `[your-username]/lams-app` — you'll need this.

---

## Part C — Generate Issues from the Implementation Plan

### Step 1 — Run the Issues Prompt File

In Copilot Chat, type `/` and select **GitHub Issues Generator** (from `.github/prompts/github-issues.prompt.md`).

Or manually send this prompt:

```
Read doc/implementation-plan.md and convert it into GitHub Issues for the repository [YOUR-USERNAME]/lams-app.

For each task in the implementation plan, create a GitHub issue with:
- A clear title
- A description explaining what needs to be done
- Acceptance criteria as checkboxes
- Appropriate labels: backend, database, testing, infrastructure, security
- Milestone matching the Phase (Phase 0, Phase 1, etc.)

Start by creating the milestones first, then create issues for Phase 0 and Phase 1 tasks.
Use the GitHub MCP to create them directly.
```

> Replace `[YOUR-USERNAME]` with your actual GitHub username.

---

## Step 2 — Verify on GitHub

Open your repository on GitHub (https://github.com/[your-username]/lams-app/issues) and verify:

- [ ] Milestones created for each Phase
- [ ] Issues have labels (backend, database, etc.)
- [ ] Issues have acceptance criteria as checkboxes
- [ ] Issues are assigned to the correct milestone

---

## Step 3 — Create a Project Board (Optional)

```
Using the GitHub MCP, add all the Phase 1 issues to a new GitHub Project board 
called "LAMS Sprint 1". Set up three columns: To Do, In Progress, Done.
```

---

## Key Takeaway

> The MCP transforms Copilot from a **code editor tool** into a **project management tool**. Going from a Functional Requirements Document to a structured, labelled, milestoned GitHub issue backlog in under 5 minutes is the kind of productivity multiplier that changes how teams operate. The same MCP can later be used to track progress, comment on issues, and link PRs — all from chat.

---

**Next**: [Exercise 09 — Build APIs with Local Agent](exercise-09-api-local-agent.md)
