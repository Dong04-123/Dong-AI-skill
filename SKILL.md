---
name: dong-ai-company
description: "Give your Hermes Agent a full AI Company backbone — red/blue debate, dynamic worker pools, graph memory, board review. 7x24 project engineering powerhouse."
tags: [ai-agent, multi-agent, orchestration, company, governance, project-management]
---

# Dong AI Company Skill

Turn your Hermes Agent into an AI-powered engineering enterprise.  
This skill adds enterprise-grade project governance to Hermes:

- **Red/Blue team debate** on design decisions
- **Dynamic worker pools** recruited per-task from 160+ roles
- **Graph memory** — structured symbol/dependency persistence across phases
- **Board review** — every phase scored 1–10, gate at 6.0
- **Requirement locks** — design checklist enforced per phase

## Prerequisites

```bash
pip install dong-ai
dong setup        # Interactive configuration
dong serve        # Start API → http://localhost:8648
```

## Tools

### `dong_run`
Execute a full project lifecycle in Dong AI. Returns a structured report.

- **request** (required): Project description

```
[TOOL_CALL:dong_run] request=Build a configuration management system with YAML/JSON support [/TOOL_CALL]
```

### `dong_chat`
Consult the Dong AI CEO for design decisions and architecture analysis.

- **message** (required): Your question or requirement

```
[TOOL_CALL:dong_chat] message=Review this architecture for security risks [/TOOL_CALL]
```

### `dong_audit`
Trigger an automated codebase audit with board-level findings.

- **path** (required): Project path to audit

```
[TOOL_CALL:dong_audit] path=/home/user/project [/TOOL_CALL]
```

### `dong_schedule`
Schedule recurring project tasks.

- **command** (required): Command to run
- **interval** (required): 30m / 1h / 1d

```
[TOOL_CALL:dong_schedule] command=dong run "System health check" interval=1h [/TOOL_CALL]
```

## Capabilities

| Capability | Description |
|------------|-------------|
| 🏛️ **Governance** | Full corporate decision pipeline: debate → design → execute → review → gate |
| 🧠 **Graph Memory** | Persistent symbol/dependency graph — cross-phase context without window limits |
| 👥 **Dynamic Workers** | LLM-recruited specialists per task — self-healing, cross-review |
| 📋 **Requirement Locks** | Design → checklist → per-phase coverage scoring |
| 🔌 **20+ Providers** | DeepSeek / OpenAI / Claude / Groq / Local Qwen — auto failover |
| ⚙️ **Dual Mode** | API (256K context) / Local (64K context) — freely switchable |
| 🕐 **Cron** | `dong cron add --cmd "dong run audit" --every 1h` |
| 📡 **Webhook** | `POST /webhook` triggers automated audit |

## Architecture

```
User → Hermes Agent → [TOOL_CALL:dong_*] → Dong AI API
                                               │
                                          ┌────┴────┐
                                          │  CEO    │
                                          │  ├─ Red/Blue Debate
                                          │  ├─ Dynamic Pipeline
                                          │  └─ Board Review
                                          └────┬────┘
                                               │
                                          ┌────┴────┐
                                          │ Workers │
                                          │  ├─ Code
                                          │  ├─ Test
                                          │  └─ Review
                                          └─────────┘
```

## Quick Start

```bash
# Install Dong AI
pip install dong-ai

# Configure
dong setup

# Start API (Hermes connects here)
dong serve --port 8648

# In Hermes, use [TOOL_CALL:dong_run] to execute projects
```

## Links

- GitHub: https://github.com/Dong04-123/Dong-AI-skill
- Dong AI Core: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
