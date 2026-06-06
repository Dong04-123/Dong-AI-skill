<div align="center">

```
██████╗  ██████╗ ███╗   ██╗ ██████╗     █████╗ ██╗
██╔══██╗██╔═══██╗████╗  ██║██╔════╝    ██╔══██╗██║
██║  ██║██║   ██║██╔██╗ ██║██║         ███████║██║
██║  ██║██║   ██║██║╚██╗██║██║         ██╔══██║██║
██████╔╝╚██████╔╝██║ ╚████║╚██████╗    ██║  ██║██║
╚═════╝  ╚═════╝ ╚═╝  ╚═══╝ ╚═════╝    ╚═╝  ╚═╝╚═╝
```

# Dong AI — Hermes Skill

**Give your Hermes Agent enterprise-grade project governance.**

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Hermes](https://img.shields.io/badge/hermes-compatible-blue)](https://github.com/NousResearch/hermes-agent)
[![PyPI](https://img.shields.io/pypi/v/dong-ai)](https://pypi.org/project/dong-ai/)

</div>

---

## Overview

This Hermes skill connects your agent to [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company) — an AI orchestration engine with full organizational governance. Instead of single-turn LLM responses, you get:

- **Red/Blue team debate** on every design decision
- **Dynamic worker pools** recruited per-task with self-healing and cross-review
- **Graph memory** — structured symbol/dependency persistence, not window stuffing
- **Board review** with scoring and quality gates (≥ 6.0/10)
- **Multi-phase pipelines** with resume capability

## Install

```bash
pip install dong-ai[all]
dong setup

# Install the skill for Hermes
mkdir -p ~/.hermes/skills/dong-ai-company
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```

## Tools

| Tool | Description |
|------|-------------|
| `dong_run request="..."` | Full project lifecycle: debate → plan → execute → review → gate |
| `dong_chat message="..."` | Consult the AI CEO for architecture analysis |
| `dong_audit path="..."` | Board-reviewed codebase audit with severity-graded findings |
| `dong_status` | System health, available models, graph memory stats |

## Architecture

```
Hermes Agent ──→ [TOOL_CALL:dong_run] ──→ Dong AI API
                                              │
                                         ┌────┴────┐
                                         │  CEO    │
                                         │  ├─ Red/Blue Debate
                                         │  ├─ Project Pipeline
                                         │  └─ Board Review
                                         └────┬────┘
                                              │
                                         ┌────┴────┐
                                         │ Workers │
                                         │  ├─ Code/Test/Review
                                         │  ├─ Self-healing (×3)
                                         │  └─ Cross-review
                                         └─────────┘
                                              │
                                         ┌────┴────┐
                                         │  Graph  │
                                         │  Memory │
                                         └─────────┘
```

## Links

- **Core Engine**: [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company)
- **PyPI**: [dong-ai](https://pypi.org/project/dong-ai/)
- **Hermes Agent**: [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

## License

MIT
