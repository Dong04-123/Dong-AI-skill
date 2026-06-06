<div align="center">

```
██████╗  ██████╗ ███╗   ██╗ ██████╗     █████╗ ██╗
██╔══██╗██╔═══██╗████╗  ██║██╔════╝    ██╔══██╗██║
██║  ██║██║   ██║██╔██╗ ██║██║         ███████║██║
██║  ██║██║   ██║██║╚██╗██║██║         ██╔══██║██║
██████╔╝╚██████╔╝██║ ╚████║╚██████╗    ██║  ██║██║
╚═════╝  ╚═════╝ ╚═╝  ╚═══╝ ╚═════╝    ╚═╝  ╚═╝╚═╝
```

# Dong AI — Universal Agent Adapter

**Give any AI agent enterprise-grade project governance.** Works with Hermes, Claude Code,
Cursor, Copilot, Codex, or any agent that can run shell commands.

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![PyPI](https://img.shields.io/pypi/v/dong-ai)](https://pypi.org/project/dong-ai/)

</div>

---

## Overview

This repository ships **adapter files** that let any agent discover and use Dong AI Company's
18 tools. The adapter files are:

| File | Platform | Install |
|------|----------|---------|
| `SKILL.md` | **Hermes Agent** | `cp SKILL.md ~/.hermes/skills/dong-ai-company/` |
| `CLAUDE.md` | **Claude Code** | `cp CLAUDE.md ~/.claude/claude.md` |
| `.cursorrules` | **Cursor** | `cp .cursorrules .cursorrules` |
| `README.md` | **Any agent** | Read this file directly |

The engine behind all adapters is [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company) —
an AI orchestration engine with organizational governance.

## Install

```bash
pip install dong-ai
dong setup
```

That's it. Every `dong` command is now available from any shell.

## How Every Agent Calls Dong AI

The universal interface is `dong <command>`. Regardless of which agent you use, the
invocation is the same:

```bash
# Project execution
dong make "3-chapter sci-fi comic series"
dong run "Build a CLI tool for CSV parsing"
dong quick "fix this bug"

# Code analysis
dong analyze src/main.py "Explain the auth flow"
dong edit api.py "Add rate limiting"

# CI debugging
dong debug

# Long-running operation
dong company start --domain "Monitor our e-commerce API" --duration 8h
dong company status
dong company stop

# Memory & knowledge
dong graph list
dong graph view my-project
dong company knowledge
dong company review
```

## Capabilities

| Category | Tools | Details |
|----------|-------|---------|
| **Project execution** | dong_make, dong_run, dong_quick | Self-directed making, full governance pipeline, lightweight mode |
| **Code workflow** | dong_analyze, dong_edit, dong_debug | Code Q&A, file editing with diff, CI root cause analysis |
| **Company runtime** | company_start, company_stop, company_status | 7x24 background operation with autonomous domains |
| **Metacognition** | knowledge, governance_review, governance_confirm | Knowledge map, risk audit, decision confirmation |
| **Context** | graph_query, session | Cross-project graph memory, session recovery |
| **Plugins** | plugin_install, mcp_discover | MCP ecosystem integration |
| **System** | dong_status, dong_update | System health, auto-upgrade |

## Adapter Quick Reference

### Hermes Agent
```bash
mkdir -p ~/.hermes/skills/dong-ai-company
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```
Then use `dong_*` tool calls in your prompts.

### Claude Code
```bash
cp CLAUDE.md ~/.claude/claude.md
```
Then Claude Code knows `dong` commands are available.

### Cursor
```bash
cp .cursorrules .cursorrules
```
Then Cursor knows to use `dong` commands.

### GitHub Copilot
Create `.github/copilot-instructions.md` with:
```markdown
The @dong CLI provides project execution, code analysis, company runtime,
metacognition, and memory capabilities. Use `dong <command>` to invoke.
```

### Any Other Agent
Just document:
```
pip install dong-ai
dong <command>
```

## Architecture

```
Any Agent (Hermes / Claude Code / Cursor / Copilot / Codex / etc.)
  │  shell out via dong <command>
  │
  ▼
Dong AI Company Engine  ← pip install dong-ai
  ├── Column Memory       (cross-project context management)
  ├── Experience Engine   (debrief → skill → future recall)
  ├── SafetyGovernor      (confidence scoring + risk gates)
  ├── Metacognition       (knowledge map + strategy evolution)
  └── Domain Runtimes     (7x24 autonomous operation)
```

The `dong` CLI is the universal contract. The engine is the same regardless of which
agent wraps it.

## Links

- **Engine**: [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company)
- **PyPI**: [dong-ai](https://pypi.org/project/dong-ai/)
- **Hermes Agent**: [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

## License

MIT
