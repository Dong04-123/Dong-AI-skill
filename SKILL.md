---
name: dong-ai-company
description: "Your AI company — any domain, any output. Self-directed learning, column memory, governance pipeline, 7x24 company runtime. Make reports, comics, business plans, analysis, or code. pip install dong-ai."
tags: [ai-company, self-learning, governance, column-memory, metacognition, orchestration]
dong-plugin: true
---

# Dong AI Company — Hermes Skill

The universal interface to Dong AI is the `dong` CLI. Any agent that can run shell commands can
call it. This SKILL.md is the Hermes-specific binding; see CLAUDE.md / .cursorrules / README.md
for other platforms.

Install once, call from any agent:

```bash
pip install dong-ai
dong setup
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```

# ============================================
# TOOL INDEX (agent-agnostic)
# ============================================
# Each tool below works identically across all agents — just shell out to `dong <command>`.
# ============================================

# === Project Execution ===

- name: dong_make
  description: "Self-directed making for any domain. Tell the company what you want to make — a market report, a comic series, a business plan, a technical analysis, a marketing strategy. It researches the domain, proposes directions for your approval, deep-dives, executes, self-reviews, and delivers. Add --auto for fully autonomous mode."
  exec: "dong make '{{request}}' 2>&1 | tail -60"

- name: dong_run
  description: "Execute a complete project through the AI company governance pipeline. The CEO analyzes requirements, conducts red/blue team debate, recruits specialist workers, executes with self-healing and cross-review, then board-approves the result. The project is automatically debriefed afterward with lessons extracted and stored for future recall."
  exec: "dong run '{{request}}' 2>&1 | tail -50"

- name: dong_quick
  description: "Lightweight execution mode that bypasses the full CEO pipeline. Use for simple tasks that don't need debate, multiple workers, or board review. Direct LLM call with file read/write/run/web tools available. Faster than dong_run for straightforward requests."
  exec: "dong quick '{{request}}' 2>&1"

# === Code & File Workflow ===

- name: dong_analyze
  description: "Read and analyze any source file. Ask questions about code structure, logic, or behavior. Equivalent to dragging a file into a chat UI but runs in your terminal. Automatically reads .dong_rule for project context."
  exec: "dong analyze {{path}} '{{question}}' 2>&1 | tail -40"

- name: dong_edit
  description: "Read a file, propose changes based on your requirements, show a unified diff preview, and apply changes on confirmation. Includes syntax-aware code generation and respects project-level .dong_rule conventions."
  exec: "dong edit {{path}} '{{instruction}}' 2>&1"

- name: dong_debug
  description: "CI failure root cause analysis. Fetches logs from the latest failed GitHub Actions run, parses error locations, cross-references against graph memory for relevant symbols and dependencies, reads source code around failure points, and produces an LLM-generated root cause analysis with fix recommendations."
  exec: "dong debug 2>&1 | tail -80"

# === Company Runtime ===

- name: dong_company_start
  description: "Start a persistent 7x24 AI company instance in the background. Supports autonomous domain operation — describe any domain in natural language and the agent researches it, sets up monitoring strategies, and runs continuously. Configurable duration with --duration (30m/2h/1d) or --until (17:00)."
  exec: "dong company start --domain '{{domain}}' --duration {{duration}} 2>&1"

- name: dong_company_stop
  description: "Stop the running AI company instance. All domains are shut down, current state is saved."
  exec: "dong company stop 2>&1"

- name: dong_company_status
  description: "View the current status of the AI company — uptime, active domains, tasks completed, pending governance confirmations, and prediction accuracy statistics."
  exec: "dong company status 2>&1"

# === Metacognition & Governance ===

- name: dong_knowledge_map
  description: "Generate the organizational metacognition report. Shows what the AI company knows (domain expertise with scores), what it's learning (improvement trends), what strategies work best, and knowledge gaps (domains not yet explored)."
  exec: "dong company knowledge 2>&1"

- name: dong_governance_review
  description: "Run a governance self-review. Shows total decisions, confidence distribution, risk levels, and decision audit trail. Lists any pending high-risk actions that require human confirmation."
  exec: "dong company review 2>&1"

- name: dong_governance_confirm
  description: "Confirm a pending high-risk decision. When the SafetyGovernor blocks an action due to low confidence or high risk, use this to explicitly authorize it."
  exec: "dong company confirm 2>&1"

# === Context & Memory ===

- name: dong_graph_query
  description: "Query the cross-project graph memory. Lists all projects with their symbol and dependency counts, then drills into a specific project to show functions, classes, file locations, and dependency relationships."
  exec: "dong graph list 2>&1 && echo '---' && dong graph view {{project_id}} 2>&1"

- name: dong_session
  description: "List recent working sessions from persistent memory — session IDs, titles, message counts, timestamps. Then optionally view the last N messages of a specific session."
  exec: "dong session list 2>&1 && echo '---' && dong session view {{session_id}} 2>&1 | tail -30"

# === Plugins ===

- name: dong_plugin_install
  description: "Install an MCP plugin from the Dong AI plugin registry."
  exec: "dong plugin install {{name}} 2>&1"

- name: dong_mcp_discover
  description: "Discover and test all configured MCP servers — scans .mcp.json and Hermes config, connects to each server, and lists available tools with descriptions."
  exec: "dong mcp 2>&1"

# === System ===

- name: dong_status
  description: "Full system status: available models, Column Memory budget, graph memory statistics, active plugins, running company instances, and pending governance confirmations."
  exec: "dong detect 2>&1"

- name: dong_update
  description: "Check PyPI for a newer version and upgrade if available."
  exec: "dong update 2>&1"

---

## Architecture

```
Any Agent (Hermes / Claude Code / Cursor / Copilot / Codex / etc.)
  │
  ├── shell out: dong make "a report"
  ├── shell out: dong run "build a CLI"
  ├── shell out: dong quick "fix this"
  ├── shell out: dong analyze path question
  └── shell out: dong company start --domain "monitor API"
        │
        ▼
   Dong AI Company Engine  ← pip install dong-ai
        │
        ├── Column Memory      (cross-project context)
        ├── Experience Engine  (learns from past projects)
        ├── SafetyGovernor     (confidence + risk gates)
        ├── Metacognition      (knowledge map + strategy evolution)
        └── Domain Runtimes    (7x24 autonomous monitoring)
```

The `dong` CLI is the universal contract. The Engine is the same regardless of which
agent wraps it.

## What Your Agent Gains

| Capability | Without Dong AI | With Dong AI |
|------------|----------------|--------------|
| Context | Conversation window only | Column Memory + cross-project graph |
| Learning | Per-session only | Experience Engine + Metacognition |
| Autonomy | Task-by-task | 7x24 company runtime |
| Governance | Direct execution | Confidence scoring + risk gates |
| Debug | Manual log reading | Automated CI root cause analysis |
| Knowledge | What the model knows | Organizational metacognition map |

## Calling from Any Agent

All tools are `dong <command>` shell invocations. Template parameters use {{ }}
syntax — substitute with your agent's template engine.

**Claude Code** — copy CLAUDE.md from this repo:
```bash
cp CLAUDE.md .claude/
```

**Cursor** — copy .cursorrules from this repo:
```bash
cp .cursorrules .cursorrules
```

**GitHub Copilot** — create a .github/copilot-instructions.md:
```markdown
The @dong CLI provides project execution, code analysis, company runtime,
metacognition, and memory capabilities. Use `dong <command>` to invoke.
See README.md for full tool documentation.
```

**Any agent** — shell out directly:
```bash
pip install dong-ai
dong make "a quarterly market report"
dong analyze path="src/main.py" question="What does this do?"
```

## Capabilities Summary

| Category | Tools | Count |
|----------|-------|-------|
| Project execution | dong_make, dong_run, dong_quick | 3 |
| Code workflow | dong_analyze, dong_edit, dong_debug | 3 |
| Company runtime | dong_company_start, dong_company_stop, dong_company_status | 3 |
| Metacognition | dong_knowledge_map, dong_governance_review, dong_governance_confirm | 3 |
| Context | dong_graph_query, dong_session | 2 |
| Plugins | dong_plugin_install, dong_mcp_discover | 2 |
| System | dong_status, dong_update | 2 |
| **Total** | | **18** |

## Links

- Engine: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
- Hermes: https://github.com/NousResearch/hermes-agent
