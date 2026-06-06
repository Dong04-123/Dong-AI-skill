# Dong AI Company — Claude Code Adapter

Install once, use from any Claude Code session:

```bash
pip install dong-ai
dong setup
cp CLAUDE.md ~/.claude/claude.md   # optional: user-level availability
```

## Available Commands

All tools are `dong <command>` shell invocations. Call them from any Claude Code session.

### Project Execution

- **`dong make "what to make"`** — Self-directed making for any domain.
  Researches the domain, proposes directions for approval, deep-dives, executes, self-reviews.
  Add `--auto` for fully autonomous mode.
- **`dong run "project description"`** — Full governance pipeline.
  CEO analyzes → red/blue debate → dynamic workers → board review → debrief.
- **`dong quick "task description"`** — Lightweight, no pipeline overhead.

### Code & File Workflow

- **`dong analyze <path> 'question'`** — Read and analyze any source file.
- **`dong edit <path> 'instruction'`** — Edit file with diff preview + confirmation.
- **`dong debug`** — CI failure root cause analysis from latest GitHub Actions run.

### Company Runtime

- **`dong company start --domain 'description' --duration 8h`** — 7x24 background operation.
- **`dong company stop`** — Shut down running company instance.
- **`dong company status`** — Current state: uptime, domains, pending confirmations.

### Metacognition & Governance

- **`dong company knowledge`** — Knowledge map: what the company knows and is learning.
- **`dong company review`** — Governance self-review: confidence, risk, decision audit.
- **`dong company confirm`** — Authorize a pending high-risk decision.

### Context & Memory

- **`dong graph list && dong graph view <project_id>`** — Query cross-project graph memory.
- **`dong session list`** — List past working sessions from persistent memory.

### Plugins

- **`dong plugin install <name>`** — Install MCP plugin.
- **`dong mcp`** — Discover and test configured MCP servers.

### System

- **`dong detect`** — Full system status: models, memory, plugins, company instances.
- **`dong update`** — Check PyPI for newer version and upgrade.

## Usage Rules for Claude Code

1. When the user asks to make something (report, comic, analysis, plan), use `dong make`.
2. For complex multi-step projects with governance, use `dong run`.
3. For simple tasks (fix a bug, one-shot analysis), use `dong quick`.
4. For code analysis questions, use `dong analyze <path> 'question'`.
5. For CI debugging, use `dong debug`.
6. For long-running monitoring/operation tasks, use `dong company start`.

## Architecture

```
Claude Code
  │  shell out
  ├── dong make "report"
  ├── dong run "build CLI"
  ├── dong company start --domain "monitor"
  │
  ▼
Dong AI Company Engine  ← pip install dong-ai
  ├── Column Memory       (cross-project context)
  ├── Experience Engine   (learns from past projects)
  ├── SafetyGovernor      (confidence + risk gates)
  ├── Metacognition       (knowledge map + strategy evolution)
  └── Domain Runtimes     (7x24 autonomous operation)
```

## Links

- Engine: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
- Skill Repo: https://github.com/Dong04-123/Dong-AI-skill
