---
name: dong-ai-company
description: "Turn Hermes into an infinite-context AI company. Column memory, self-directed learning, governance pipeline, plugin ecosystem, and 7x24 company runtime. Your agent gains cross-project memory, metacognitive awareness, and autonomous operation capabilities."
tags: [ai-company, column-memory, metacognition, governance, mcp, self-learning, orchestration]
dong-plugin: true
---

# === 项目执行 ===

- name: dong_make
  description: "Self-directed making — tell the company what to make, and it researches the domain, proposes directions, lets you choose, deep-dives, plans, executes, self-reviews, and delivers. Works for any output: comics, reports, plans, analysis, designs, games, etc. Add --auto for fully autonomous mode."
  exec: "dong make '{{request}}' 2>&1 | tail -60"

- name: dong_run
  description: "Execute a complete project through the AI company governance pipeline. The CEO analyzes requirements, conducts red/blue team debate, recruits specialist workers, executes with self-healing and cross-review, then board-approves the result. The project is automatically debriefed afterward — lessons are extracted and stored for future recall. Supports software, novel, game, analysis, and audit project types."
  exec: "dong run '{{request}}' 2>&1 | tail -50"

- name: dong_quick
  description: "Lightweight execution mode that bypasses the full CEO pipeline. Use for simple tasks that don't need debate, multiple workers, or board review. Direct LLM call with file read/write/run/web tools available. Faster than dong_run for straightforward requests."
  exec: "dong quick '{{request}}' 2>&1"

# === 代码工作流 ===

- name: dong_analyze
  description: "Read and analyze any source file. Ask questions about code structure, logic, or behavior. Equivalent to dragging a file into Claude Chat but runs in your terminal. Automatically reads .dong_rule for project context."
  exec: "dong analyze {{path}} '{{question}}' 2>&1 | tail -40"

- name: dong_edit
  description: "Read a file, propose changes based on your requirements, show a unified diff preview, and apply changes on confirmation. Includes syntax-aware code generation and respects project-level .dong_rule conventions."
  exec: "dong edit {{path}} '{{instruction}}' 2>&1"

- name: dong_debug
  description: "CI failure root cause analysis. Fetches logs from the latest failed GitHub Actions run, parses error locations, cross-references against graph memory for relevant symbols and dependencies, reads source code around failure points, and produces an LLM-generated root cause analysis with fix recommendations."
  exec: "dong debug 2>&1 | tail -80"

# === 公司运营 ===

- name: dong_company_start
  description: "Start a persistent 7x24 AI company instance in the background. Supports autonomous domain operation — describe any domain in natural language and the agent researches it, sets up monitoring strategies, and runs continuously. Configurable duration with --duration (30m/2h/1d) or --until (17:00). Runs automatically: hourly health checks, daily reports at 9:00, backups at 3:00, webhook processing."
  exec: "dong company start --domain '{{domain}}' --duration {{duration}} 2>&1"

- name: dong_company_stop
  description: "Stop the running AI company instance. All domains are shut down, current state is saved."
  exec: "dong company stop 2>&1"

- name: dong_company_status
  description: "View the current status of the AI company — uptime, active domains, tasks completed, webhooks processed, pending governance confirmations, and prediction accuracy statistics."
  exec: "dong company status 2>&1"

# === 元认知与自省 ===

- name: dong_knowledge_map
  description: "Generate the organizational metacognition report. Shows what the AI company knows (domain expertise with scores), what it's learning (improvement trends), what strategies work best (learning strategy effectiveness), and knowledge gaps (domains not yet explored). Updated automatically after each project debrief."
  exec: "dong company knowledge 2>&1"

- name: dong_governance_review
  description: "Run a governance self-review. Shows total decisions, confidence distribution, risk levels, and decision audit trail. Lists any pending high-risk actions that require human confirmation."
  exec: "dong company review 2>&1"

- name: dong_governance_confirm
  description: "Confirm a pending high-risk decision. When the SafetyGovernor blocks an action due to low confidence or high risk, use this to explicitly authorize it."
  exec: "dong company confirm 2>&1"

# === 上下文管理 ===

- name: dong_graph_query
  description: "Query the cross-project graph memory. Lists all projects with their symbol and dependency counts, then drills into a specific project to show functions, classes, file locations, and dependency relationships. Persists across sessions — data indexed months ago is still searchable."
  exec: "dong graph list 2>&1 && echo '---' && dong graph view {{project_id}} 2>&1"

- name: dong_session
  description: "List recent working sessions from persistent memory — session IDs, titles, message counts, timestamps. Then optionally view the last N messages of a specific session. Essential for resuming context across Hermes sessions."
  exec: "dong session list 2>&1 && echo '---' && dong session view {{session_id}} 2>&1 | tail -30"

# === 插件生态 ===

- name: dong_plugin_install
  description: "Install an MCP plugin from the Dong AI plugin registry. Available: filesystem (file I/O), github (PR/Issue), puppeteer (browser automation), web-search (Brave Search API), memory (knowledge graph), sequential-thinking (structured reasoning)."
  exec: "dong plugin install {{name}} 2>&1"

- name: dong_mcp_discover
  description: "Discover and test all configured MCP servers — scans .mcp.json and Hermes config, connects to each server, and lists available tools with descriptions."
  exec: "dong mcp 2>&1"

# === 系统 ===

- name: dong_status
  description: "Full system status: available models, Column Memory budget, graph memory statistics, active plugins, running company instances, and pending governance confirmations."
  exec: "dong detect 2>&1"

- name: dong_update
  description: "Check PyPI for a newer version and upgrade if available."
  exec: "dong update 2>&1"

---

## What Hermes Gains

| Capability | Without Dong AI | With Dong AI |
|------------|----------------|--------------|
| **Context** | Conversation window | Column Memory + cross-project graph |
| **Learning** | None per session | Experience Engine + Metacognition |
| **Autonomy** | Task-by-task | 7x24 company runtime |
| **Governance** | Direct execution | Confidence scoring + risk gates |
| **Debug** | Manual log reading | Automated CI root cause analysis |
| **Knowledge** | What the model knows | Organizational metacognition map |

## Architecture

```
Hermes Agent
  │
  ├── [TOOL_CALL:dong_run]         → CEO governance pipeline
  ├── [TOOL_CALL:dong_quick]       → Lightweight execution
  ├── [TOOL_CALL:dong_analyze]     → Code Q&A
  ├── [TOOL_CALL:dong_edit]        → File edit with diff
  ├── [TOOL_CALL:dong_debug]       → CI root cause analysis
  ├── [TOOL_CALL:dong_company_*]   → 7x24 company runtime
  ├── [TOOL_CALL:dong_knowledge_*] → Metacognition & governance
  ├── [TOOL_CALL:dong_graph_query] → Cross-project memory
  └── [TOOL_CALL:dong_plugin_*]    → MCP plugin management
```

## Installation

```bash
pip install dong-ai[all]
dong setup

mkdir -p ~/.hermes/skills/dong-ai-company
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```

## Daily Workflow

```bash
# Morning status
dong_status                          # system health + Column Memory budget
dong_knowledge_map                   # what the company knows and is learning

# Project work
dong_make request="一部3章科幻漫剧"         # self-directed: researches + proposes + executes
dong_run request="Build a CLI tool"           # full governance pipeline
dong_quick "fix this bug"                     # lightweight, no pipeline overhead

# Code analysis
dong_analyze path="src/main.py" question="Explain the auth flow"
dong_edit path="api.py" instruction="Add rate limiting"

# CI Debug
dong_debug                           # auto root cause analysis

# Persistent operation
dong_company_start domain="Monitor our e-commerce API" duration=8h
dong_company_status

# Meta-cognition
dong_governance_review               # decision audit trail
dong_knowledge_map                   # updated org knowledge map
```

## Tool Index

| Category | Tools | Count |
|----------|-------|-------|
| **Project execution** | dong_make, dong_run, dong_quick | 3 |
| **Code workflow** | dong_analyze, dong_edit, dong_debug | 3 |
| **Company runtime** | dong_company_start, dong_company_stop, dong_company_status | 3 |
| **Metacognition** | dong_knowledge_map, dong_governance_review, dong_governance_confirm | 3 |
| **Context** | dong_graph_query, dong_session | 2 |
| **Plugins** | dong_plugin_install, dong_mcp_discover | 2 |
| **System** | dong_status, dong_update | 2 |
| **Total** | | **18** |

## Links

- Engine: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
- Hermes: https://github.com/NousResearch/hermes-agent
