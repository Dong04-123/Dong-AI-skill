<div align="center">

```
██████╗  ██████╗ ███╗   ██╗ ██████╗     █████╗ ██╗
██╔══██╗██╔═══██╗████╗  ██║██╔════╝    ██╔══██╗██║
██║  ██║██║   ██║██╔██╗ ██║██║         ███████║██║
██║  ██║██║   ██║██║╚██╗██║██║         ██╔══██║██║
██████╔╝╚██████╔╝██║ ╚████║╚██████╗    ██║  ██║██║
╚═════╝  ╚═════╝ ╚═╝  ╚═══╝ ╚═════╝    ╚═╝  ╚═╝╚═╝

# Dong AI — Hermes Skill

**Give your Hermes Agent a full AI Company backbone.**

Red/Blue debate · Dynamic workers · Graph memory · Board review  
7×24 project engineering, inside your Hermes.

</div>

---

## What is this?

A [Hermes Agent](https://github.com/NousResearch/hermes-agent) skill that connects your Hermes to [Dong AI Company](https://github.com/Dong04-123/Dong-AI-Company) — turning it from a personal assistant into an **AI-powered engineering enterprise**.

## Quick Install

```bash
# 1. Install Dong AI
pip install dong-ai

# 2. Configure
dong setup

# 3. Start API
dong serve &

# 4. Copy this skill to Hermes
cp SKILL.md ~/.hermes/skills/dong-ai-company/
```

## Available Commands

| Command | What it does |
|---------|--------------|
| `dong_run "build a config system"` | Full project lifecycle with governance |
| `dong_chat "review this architecture"` | Consult AI CEO |
| `dong_audit /path/to/project` | Automated codebase audit |
| `dong_schedule cmd="dong run audit" interval=1h` | Recurring tasks |

## Architecture

```
You → Hermes Agent → [TOOL_CALL:dong_*] → Dong AI API
                                             ↓
                                    CEO → Red/Blue Debate
                                        → Dynamic Pipeline
                                        → Board Review
                                        → Quality Gate
```

## Requirements

- Python 3.10+
- Dong AI (`pip install dong-ai`)
- Hermes Agent (any version with skill support)

## Links

- **This skill**: https://github.com/Dong04-123/Dong-AI-skill
- **Dong AI Core**: https://github.com/Dong04-123/Dong-AI-Company
- **Hermes Agent**: https://github.com/NousResearch/hermes-agent

## License

MIT
