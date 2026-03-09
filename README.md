# E2E SDLC with GitHub Copilot — Workshop

> **Audience**: Developers, Tech Leads, Architects  
> **Total Duration**: ~90 minutes (16 exercises × 3–5 min each)  
> **Pre-requisites**: VS Code with GitHub Copilot Chat extension, Node/Python/Java runtime, Git CLI, GitHub Copilot access, GitHub MCP.

---

## What You Will Build

An **Intelligent Task Management System (ITMS)** — a realistic business application that covers every phase of the Software Development Life Cycle, all guided by GitHub Copilot.

The system enables teams to create, assign, and track tasks, manage task dependencies, monitor project progress, and identify bottlenecks — all key pain points for software teams working across multiple members and workstreams.

**Core capabilities from [`requirement.md`](requirement.md):**

| Capability | Description |
|---|---|
| **Task Creation** | Create tasks with ID, title, priority, status, assignee, and due date |
| **Task Assignment** | Assign or reassign tasks to team members |
| **Dependency Management** | Link tasks with dependencies; auto-mark blocked tasks |
| **Status Tracking** | Track To Do / In Progress / Blocked / Completed with history |
| **Filtering & Listing** | Query tasks by status, priority, assignee, or due date |
| **Progress Summary** | Dashboard showing total, completed, in-progress, and blocked counts |

> The requirement is already in [`requirement.md`](requirement.md). You do **not** need to write the application yourself — Copilot does the heavy lifting. Your job is to learn how to **direct Copilot effectively** through each SDLC phase.

---

## Workshop Map

| # | Exercise | Copilot Feature | Duration |
|---|----------|----------------|----------|
| 01 | [Setup & Custom Agents](workshop/exercise-01-setup-agents.md) | Custom Agents (`.agent.md`) | 5 min |
| 02 | [Generate BRD](workshop/exercise-02-brd.md) | BRD Custom Agent | 4 min |
| 03 | [Generate TSD](workshop/exercise-03-tsd.md) | TSD Custom Agent | 4 min |
| 04 | [Generate FRD](workshop/exercise-04-frd.md) | FRD Custom Agent | 4 min |
| 05 | [Custom Instructions](workshop/exercise-05-custom-instructions.md) | `.instructions.md` | 3 min |
| 06 | [Plan Mode – Implementation Plan](workshop/exercise-06-plan-mode.md) | Plan Mode | 4 min |
| 07 | [Create Implementation Prompt File](workshop/exercise-07-implementation-prompt.md) | Prompt Files | 3 min |
| 08 | [Create GitHub Issues via MCP](workshop/exercise-08-github-issues.md) | GitHub MCP + Prompt File | 5 min |
| 09 | [Build APIs with Local Agent](workshop/exercise-09-api-local-agent.md) | Local (Default) Agent | 5 min |
| 10 | [Background Agent Task](workshop/exercise-10-background-agent.md) | Background Agent | 3 min |
| 11 | [Context Map Skill](workshop/exercise-11-context-map.md) | Skills (`SKILL.md`) | 4 min |
| 12 | [Database & SQL / PL/SQL](workshop/exercise-12-database-sql.md) | Local Agent + Instructions | 5 min |
| 13 | [Unit & Functional Tests](workshop/exercise-13-testing.md) | Local Agent + Prompt File | 5 min |
| 14 | [Security Review](workshop/exercise-14-security.md) | Security Prompt File | 4 min |
| 15 | [Build & Debug](workshop/exercise-15-build-debug.md) | Local Agent + Terminal | 5 min |
| 16 | [IaC & CI/CD](workshop/exercise-16-iac-cicd.md) | Custom Agent + Prompt File | 5 min |

---

## Workspace Structure After Workshop

```
SDLC2/
├── req.md                          ← Starting requirement (provided)
├── doc/
│   ├── brd.md                      ← Generated in Exercise 02
│   ├── tsd.md                      ← Generated in Exercise 03
│   └── frd.md                      ← Generated in Exercise 04
├── .github/
│   ├── copilot-instructions.md     ← Created in Exercise 05
│   ├── agents/
│   │   ├── brd.agent.md            ← Created in Exercise 01
│   │   ├── tsd.agent.md            ← Created in Exercise 01
│   │   ├── frd.agent.md            ← Created in Exercise 01
│   │   └── devops.agent.md         ← Created in Exercise 16
│   └── prompts/
│       ├── implementation-plan.prompt.md  ← Created in Exercise 07
│       ├── github-issues.prompt.md        ← Created in Exercise 08
│       └── security-review.prompt.md      ← Created in Exercise 14
├── .github/skills/context-map/     ← Created in Exercise 11
├── src/                            ← API code created in Exercise 09+
├── tests/                          ← Tests created in Exercise 13
├── db/                             ← SQL scripts created in Exercise 12
└── infra/                          ← IaC scripts created in Exercise 16
```

---

## Key GitHub Copilot Features Covered

| Feature | Description |
|---------|-------------|
| **Custom Agents** | Scoped AI personas with tool restrictions and domain prompts |
| **Plan Mode** | Pre-execution planning before Copilot takes action |
| **Local Agent** | Default interactive coding agent in VS Code |
| **Background Agent** | Runs long tasks asynchronously while you work |
| **Prompt Files** | Reusable, parameterized prompt templates (`.prompt.md`) |
| **Instructions** | Always-on context injected into every Copilot conversation |
| **Skills** | On-demand workflow bundles loaded from `SKILL.md` |
| **GitHub MCP** | Model Context Protocol server for GitHub integration |

---

## Getting Started

[![Use this Template](https://img.shields.io/badge/Use%20this%20Template-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/new?template_owner=CanarysAutomations&template_name=speckit-and-beyond&owner=%40me&name=speckit-and-beyond&description=Agent-Driven+Spec+Development:+The+FlavorHub+Crisis&visibility=public)

1. Configure your GitHub token for MCP access by setting `GITHUB_TOKEN` in your environment
1. Open the cloned repository in VS Code
1. Ensure **GitHub Copilot** and **GitHub Copilot Chat** extensions are installed and signed in
1. Open the Copilot Chat panel (`Ctrl+Alt+I`)
1. Start with [Exercise 01](workshop/exercise-01-setup-agents.md)
---

> **Instructor Note**: Each exercise has a `> Instructor Guide` section visible only in the markdown source. Exercises are designed so attendees never need to copy code — they copy **prompts** and let Copilot generate the output.
