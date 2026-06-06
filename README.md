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
- **Graph memory** — persistent symbol/dependency persistence across ALL past projects
- **Experience Engine** — debriefs every project, extracts lessons, injects them into future CEO prompts
- **Board review** with scoring and quality gates (≥ 6.0/10)
- **Multi-phase pipelines** with resume capability
- **MCP plugin ecosystem** — 8+ servers installable with one command
- **Session recovery** — search past sessions and graph memory across all work
- **Enterprise features** — API auth, multi-tenancy, Prometheus metrics, structured logs

## Install

```bash
pip install dong-ai[all]
dong setup

mkdir -p ~/.hermes/skills/dong-ai-company
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```

## Tools (19 total)

### 项目管理
| Tool | Description |
|------|-------------|
| `dong_run request="..."` | Full project lifecycle: debate → plan → execute → review → gate |
| `dong_audit path="..."` | Board-reviewed codebase audit with severity-graded findings |
| `dong_quick_analysis prompt="..."` | One-shot code/file analysis, lightweight alternative to dong_run |

### 日常巡检
| Tool | Description |
|------|-------------|
| `dong_status` | System health, available models, graph memory stats, installed plugins |
| `dong_config` | View current configuration — provider, mode, context size, temperature |
| `dong_logs` | Check recent structured log entries for debugging |
| `dong_help` | List all available dong commands |

### 图记忆
| Tool | Description |
|------|-------------|
| `dong_graph_query project_id="..."` | List projects and drill into graph memory |
| `dong_graph_search keyword="..."` | Search symbol/dependency graphs across all projects |

### 模型与配置
| Tool | Description |
|------|-------------|
| `dong_model_switch provider="deepseek" mode="api"` | Switch between providers/modes on the fly |

### 会话恢复
| Tool | Description |
|------|-------------|
| `dong_session session_id="..."` | List and view past working sessions |

### 自动化
| Tool | Description |
|------|-------------|
| `dong_cron_list` | List scheduled cron tasks |
| `dong_webhook_list` | List configured webhook endpoints |

### 插件生态
| Tool | Description |
|------|-------------|
| `dong_plugin_install name="..."` | Install MCP plugin from registry |
| `dong_plugin_search query="..."` | Search plugin registry |
| `dong_plugin_list` | List installed plugins |
| `dong_mcp_discover` | Discover and test MCP servers |

### 服务
| Tool | Description |
|------|-------------|
| `dong_serve` | Start API server with auth, metrics, health checks |

### 统计
| Tool | Description |
|------|-------------|
| `dong_project_stats path="..."` | Quick codebase file/line counts by language |

## Daily Workflow

```bash
# Morning check
dong_status       # what's running?
dong_logs         # any overnight errors?
dong_cron_list    # scheduled tasks ok?

# Context recovery from yesterday
dong_session      # find yesterday's session
dong_graph_search keyword="auth redesign"  # find that function

# Switch to cloud for heavy task
dong_model_switch provider="deepseek" mode="api"

# Project work
dong_run request="Build a CLI tool for CSV parsing"

# Extend capabilities
dong_plugin_install name=filesystem
dong_plugin_install name=github
dong_mcp_discover  # verify
```

## Architecture

```
Hermes Agent ──→ [TOOL_CALL:dong_run] ──→ Dong AI CLI
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
                                              │
                                         ┌────┴──────┐
                                         │   MCP     │
                                         │  Plugins  │
                                         │ (8+servers)│
                                         └───────────┘
```

## Links

- **Core Engine**: [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company)
- **PyPI**: [dong-ai](https://pypi.org/project/dong-ai/)
- **NPM**: [@dong-ai/sdk](https://www.npmjs.com/package/@dong-ai/sdk)
- **Hermes Agent**: [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
- **MCP Spec**: [modelcontextprotocol.io](https://modelcontextprotocol.io)

## License

MIT
