---
name: dong-ai-company
description: "Equip Hermes with a complete AI Company — full project lifecycle with red/blue debate, dynamic worker pools, graph memory, and board review. Software, novels, games, analysis — any project type."
tags: [ai-company, project-management, orchestration, governance]
dong-plugin: true
---

- name: dong_run
  description: "Execute a complete project using Dong AI Company's full governance pipeline. The CEO analyzes requirements, conducts red/blue team debate, recruits specialist workers, executes with self-healing and cross-review, then board-approves the result. Supports software, novel, game, analysis, and audit project types. Response includes the full execution report and file paths."
  exec: "dong run '{{request}}' 2>&1 | tail -50"

- name: dong_chat
  description: "Consult the Dong AI CEO for real-time architecture analysis, design review, or strategic planning. Gets an instant expert opinion backed by graph memory of the project context."
  exec: "dong chat --one-shot '{{message}}' 2>&1 | tail -30"

- name: dong_audit
  description: "Run an automated codebase audit with full AI Company governance. Scans the target project for architecture issues, security risks, code quality, and generates a board-reviewed findings report with severity ratings and fix recommendations."
  exec: "dong run 'Audit the project at {{path}}' 2>&1 | tail -50"

- name: dong_status
  description: "Check the current status of the Dong AI Company — available models, running projects, system health, and graph memory statistics."
  exec: "dong detect 2>&1"

---

## 🏛️ What This Gives Hermes

| Capability | Without Dong AI | With Dong AI |
|------------|----------------|--------------|
| Design | Single LLM response | Red/Blue team debate with scoring |
| Execution | Single response | Dynamic worker pool + self-healing + cross-review |
| Memory | Conversation window | Graph memory (symbols + deps + requirements) |
| Quality | Human judgment | Board review + phase gate ≥ 6.0 |
| Projects | One-off tasks | Multi-phase pipeline with resume |

## 🧠 Graph Memory Architecture

Dong AI's graph memory doesn't "remember" by stuffing text into a context window. It maintains a structured, queryable knowledge graph of:

- **Symbols**: Every function, class, interface extracted with exact signatures
- **Dependencies**: Call graphs, inheritance chains, module relationships
- **Requirements**: Design-phase checklist linked to each task's output
- **Decisions**: Every board review score and its rationale

When Hermes calls `dong_run`, the CEO injects relevant graph context into worker prompts — not raw conversation history.

## 🔌 Provider Support

| Provider | Type | Context |
|----------|------|---------|
| DeepSeek | Cloud API | 1M tokens |
| OpenAI | Cloud API | 128K tokens |
| Claude (Anthropic) | Cloud API | 200K tokens |
| Groq | Cloud API | 128K tokens |
| Together | Cloud API | 128K tokens |
| Fireworks | Cloud API | 128K tokens |
| Cerebras | Cloud API | 128K tokens |
| Cohere | Cloud API | 128K tokens |
| Local (llama.cpp) | Local GPU | 64K–400K |
| Ollama | Local CPU/GPU | 32K–128K |
| DashScope (Qwen) | Cloud API | 128K tokens |
| GLM | Cloud API | 128K tokens |
| MiniMax | Cloud API | 128K tokens |
| xAI (Grok) | Cloud API | 128K tokens |
| HuggingFace | Cloud API | 128K tokens |
| Kimi (Moonshot) | Cloud API | 128K tokens |
| OpenRouter | Cloud aggregate | varies |
| Xiaomi MiMo | Cloud API | 128K tokens |
| DeepInfra | Cloud API | 128K tokens |

All providers use OpenAI-compatible protocol. Auto failover: if one fails, the next takes over mid-stream.

## 🚀 Hermes Integration

```bash
# 1. Install Dong AI
pip install dong-ai[all]

# 2. Configure (detects hardware, selects mode, sets context)
dong setup

# 3. Install this skill
cp SKILL.md ~/.hermes/skills/dong-ai-company/SKILL.md

# 4. Start using in Hermes
#    [TOOL_CALL:dong_run] request=Build a CLI tool [/TOOL_CALL]
#    [TOOL_CALL:dong_chat] message=Review this architecture [/TOOL_CALL]
```

## Links

- Core Engine: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
- Hermes Agent: https://github.com/NousResearch/hermes-agent
