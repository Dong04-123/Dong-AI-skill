---
name: dong-ai-company
description: "Equip Hermes with a complete AI Company — full project lifecycle with red/blue debate, dynamic worker pools, graph memory, board review, plugin ecosystem, and MCP integration. Software, novels, games, analysis — any project type."
tags: [ai-company, project-management, orchestration, governance, mcp, plugins]
dong-plugin: true
---

# === 项目管理 ===

- name: dong_run
  description: "Execute a complete project using Dong AI Company's full governance pipeline. The CEO analyzes requirements, conducts red/blue team debate, recruits specialist workers, executes with self-healing and cross-review, then board-approves the result. Supports software, novel, game, analysis, and audit project types. Response includes the full execution report and file paths."
  exec: "dong run '{{request}}' 2>&1 | tail -50"

- name: dong_audit
  description: "Run an automated codebase audit with full AI Company governance. Scans the target project for architecture issues, security risks, code quality, and generates a board-reviewed findings report with severity ratings and fix recommendations."
  exec: "dong run 'Audit the project at {{path}}' 2>&1 | tail -50"

- name: dong_quick_analysis
  description: "Quick one-shot code analysis without the full CEO pipeline. Ask questions about a code file, a design decision, or get an instant expert opinion. Lightweight alternative to dong_run for single-shot queries."
  exec: "dong chat --one-shot '{{prompt}}' 2>&1 | tail -40"

# === 日常巡检 ===

- name: dong_status
  description: "Check the current status of the Dong AI Company — available models, running projects, system health, graph memory statistics, and installed plugins."
  exec: "dong detect 2>&1"

- name: dong_config
  description: "View the current configuration at a glance — which provider is active, API vs local mode, context window sizes, temperature, and all tunable parameters. Use before switching models or debugging poor responses."
  exec: "dong config list 2>&1"

- name: dong_help
  description: "List all available dong commands with brief descriptions. Quick reference for what Dong AI can do."
  exec: "dong help 2>&1"

- name: dong_logs
  description: "Check the most recent structured log entries from Dong AI operations. Shows timestamp, level, event type, and logger name. Useful for debugging failed runs, API errors, or just checking what happened recently."
  exec: "tail -30 /home/administrator/.dong/logs/$(date +%Y-%m-%d).jsonl 2>/dev/null | python3 -c '
import sys, json
for line in sys.stdin:
    try:
        r = json.loads(line.strip())
        print(f\"[{r.get(\"level\",\"?\"):5s}] {r.get(\"event\",\"\"):30s}  {r.get(\"logger\",\"\"):8s}  {r.get(\"t\",\"\")[:19]}\")
        if r.get(\"error\"): print(f\"       error: {r[\"error\"][:80]}\")
    except: pass
' 2>&1"

# === 图记忆 ===

- name: dong_graph_query
  description: "Query Dong AI's persistent graph memory — list all projects with their symbol/dependency counts, then drill into a specific project to see functions, classes, and cross-module dependencies."
  exec: "dong graph list 2>&1 && echo '---' && dong graph view {{project_id}} 2>&1"

- name: dong_graph_search
  description: "Search all graph memory projects for a keyword — finds matching functions, classes, and dependencies across every project Dong AI has worked on. Useful when you vaguely remember a function name or concept and want to trace it back."
  exec: "dong graph list 2>&1 && echo '---' && dong graph list 2>&1 | python3 -c '
import sys, subprocess, re
lines = [l.strip() for l in sys.stdin if l.strip()]
for l in lines:
    m = re.match(r\"^(\S+)\s+\d+\", l)
    if m:
        pid = m.group(1)
        r = subprocess.run([\"dong\", \"graph\", \"view\", pid], capture_output=True, text=True, timeout=10)
        out = r.stdout + r.stderr
        if \"{{keyword}}\".lower() in out.lower():
            print(f\"== {pid} ==\"); print(out[:500])
' 2>&1"

# === 模型与配置 ===

- name: dong_model_switch
  description: "Switch between models and providers on the fly. Change provider (deepseek, openai, local, ollama, etc.), switch mode (api/local/auto), then verify with a detection scan. Useful when one provider is rate-limited or you want to switch between cheap/fast and powerful models."
  exec: "dong config set provider={{provider}} 2>&1 && dong config set mode={{mode}} 2>&1 && echo '  → 验证:' && dong detect 2>&1"

# === 会话恢复 ===

- name: dong_session
  description: "List recent working sessions from Dong AI's persistent memory — shows session IDs, titles, message counts, and timestamps. Then optionally view the last N messages of a specific session. Essential for resuming context across work sessions."
  exec: "dong session list 2>&1 && echo '---' && dong session view {{session_id}} 2>&1 | tail -30"

# === 自动化管理 ===

- name: dong_cron_list
  description: "List all scheduled cron tasks managed by Dong AI — shows task names, schedules, commands, and next run time. Use before adding or removing automated jobs."
  exec: "dong cron list 2>&1"

- name: dong_webhook_list
  description: "List all configured webhook endpoints — shows registered URLs that Dong AI will respond to. Useful for checking CI/CD integration status."
  exec: "dong webhook list 2>&1"

# === 上网工具 ===

- name: dong_web_search
  description: "Search the internet via DuckDuckGo. No API key needed. Returns titles, URLs, and snippets. Supports Chinese and English queries. Useful for finding latest news, documentation, facts, and code references."
  exec: "dong chat --one-shot '搜索互联网: {{query}}' 2>&1 | tail -30"

- name: dong_web_fetch
  description: "Fetch and read the content of any public web page. Strips HTML, scripts, and styles to return clean readable text. Useful for reading documentation, articles, news, or API responses."
  exec: "dong chat --one-shot '获取网页内容: {{url}}' 2>&1 | tail -50"

# === 插件生态 ===
# 安装/搜索/管理 MCP 插件
- name: dong_plugin_install
  description: "Install an MCP plugin from the Dong AI plugin registry to extend agent capabilities. Available plugins include: filesystem (file I/O), github (PR/Issue management), fetch (web scraping), puppeteer (browser automation), sqlite (database), memory (knowledge graph), sequential-thinking (multi-step reasoning), brave-search (web search)."
  exec: "dong plugin install {{name}} 2>&1"

- name: dong_plugin_search
  description: "Search the Dong AI plugin registry for available MCP plugins. Pass a keyword to filter results."
  exec: "dong plugin search {{query}} 2>&1"

- name: dong_plugin_list
  description: "List currently installed plugins — shows which MCP servers are configured and ready to use."
  exec: "dong plugin list 2>&1"

- name: dong_mcp_discover
  description: "Discover and test all configured MCP servers — scans .mcp.json and Hermes config, connects to each server, and shows the tools they expose with descriptions."
  exec: "dong mcp 2>&1"

# === 服务 ===

- name: dong_serve
  description: "Start the Dong AI API server on port 8648 with OpenAI-compatible endpoints, API key authentication, Prometheus metrics, and health checks. The server supports chat completions (streaming and non-streaming), CEO project execution, and webhook receiving. Set DONG_API_KEY env var for auth."
  exec: "dong serve --host 0.0.0.0 --port 8648 2>&1 &"

# === 快速统计 ===

- name: dong_project_stats
  description: "Quick codebase statistics — counts source files by language, total lines, and file count. Supports Python, JavaScript, TypeScript, Rust, Go and other common languages."
  exec: "echo '--- 源文件 ---' && find {{path}} -type f \( -name '*.py' -o -name '*.js' -o -name '*.ts' -o -name '*.rs' -o -name '*.go' -o -name '*.java' -o -name '*.c' -o -name '*.cpp' -o -name '*.h' \) 2>/dev/null | head -40 && echo '---' && echo \"文件总数: $(find {{path}} -type f 2>/dev/null | wc -l)\" && echo \"代码行数: $(find {{path}} -type f \( -name '*.py' -o -name '*.js' -o -name '*.ts' -o -name '*.rs' -o -name '*.go' \) -exec cat {} + 2>/dev/null | wc -l)\""

---

## 🏛️ What This Gives Hermes

| Capability | Without Dong AI | With Dong AI |
|------------|----------------|--------------|
| Design | Single LLM response | Red/Blue team debate with scoring |
| Execution | Single response | Dynamic worker pool + self-healing + cross-review |
| Memory | Conversation window | Graph memory (symbols + deps + requirements) |
| Quality | Human judgment | Board review + phase gate ≥ 6.0 |
| Projects | One-off tasks | Multi-phase pipeline with resume |
| Extensibility | Static | MCP plugin ecosystem with 8+ servers |
| Observability | None | Structured logs + Prometheus metrics + health API |
| Context recovery | None | Session history + graph search across all past work |

## 🔌 Plugin Ecosystem

Dong AI ships with a built-in plugin registry — install MCP servers with one command:

```bash
# List installed plugins
dong plugin list

# Search the registry
dong plugin search browser

# Install a plugin
dong plugin install puppeteer

# Remove a plugin
dong plugin remove puppeteer
```

Available plugins out of the box:

| Plugin | Description | Command |
|--------|-------------|---------|
| `filesystem` | Secure file read/write/search | npx @mcp/filesystem |
| `github` | PR, Issue, code search | npx @mcp/github |
| `fetch` | Web scraping to markdown | npx @mcp/fetch |
| `puppeteer` | Browser automation | npx @mcp/puppeteer |
| `sqlite` | Database query & explore | uvx mcp-server-sqlite |
| `memory` | Knowledge graph persistence | npx @mcp/memory |
| `sequential-thinking` | Multi-step reasoning chains | npx @mcp/seq-thinking |
| `brave-search` | Web + news search | npx @mcp/brave-search |

## 📊 Enterprise Features

### API Authentication
```bash
# Start with auth enabled
DONG_API_KEY=*** dong serve

# Client
curl -H "Authorization: Bearer *** http://localhost:8648/health
```

### Multi-tenancy
Multiple API keys → isolated data namespaces:
```bash
DONG_API_KEYS='{"sk-tenant-a": "team-alpha", "sk-tenant-b": "team-beta"}' dong serve
```

### Metrics & Observability
```bash
# Prometheus-format metrics
curl http://localhost:8648/metrics

# Structured JSON logs
tail -f ~/.dong/logs/$(date +%Y-%m-%d).jsonl | jq .
```

### Docker Deployment
```bash
docker compose up -d
# → http://localhost:8648
# → Health check auto-monitors the container
```

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

## 👨‍💻 Daily Workflow Examples

```bash
# Morning: check status and logs
dong_set_status                          # what model, what plugins
dong_logs                                # any errors overnight?
dong_cron                                # scheduled tasks status

# Context recovery
dong_session                             # find yesterday's session
dong_graph_search keyword="auth redesign" # find that function you wrote

# Switching gears
dong_model_switch provider="deepseek" mode="api"  # switch to cloud for speed
dong_quick_analysis prompt="Review the error handling in api.py"

# Project work
dong_run request="Build a CLI tool for CSV analysis"
dong_graph_query project_id=my_project   # check graph memory afterward

# Extending capabilities
dong_plugin_search browser               # find browser automation
dong_plugin_install puppeteer            # install it
dong_mcp_discover                        # verify it works
```

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
#    [TOOL_CALL:dong_session] session_id=abc123 [/TOOL_CALL]
#    [TOOL_CALL:dong_plugin_install] name=filesystem [/TOOL_CALL]
```

## TypeScript SDK

For Node.js/TypeScript projects, install the official SDK:

```bash
npm install @dong-ai/sdk
# or from source: npm run build in sdks/typescript/
```

```typescript
import { DongAI } from "@dong-ai/sdk";

const dong = new DongAI({ apiKey: "sk-..." });
const resp = await dong.run("Audit the current project");
console.log(resp.log);
```

## Tool Index

| Category | Tools | Count |
|----------|-------|-------|
| **项目管理** | dong_run, dong_audit, dong_quick_analysis | 3 |
| **日常巡检** | dong_status, dong_config, dong_help, dong_logs | 4 |
| **图记忆** | dong_graph_query, dong_graph_search | 2 |
| **模型与配置** | dong_model_switch | 1 |
| **会话恢复** | dong_session | 1 |
| **自动化** | dong_cron_list, dong_webhook_list | 2 |
| **上网工具** | dong_web_search, dong_web_fetch | 2 |
| **插件生态** | dong_plugin_install, dong_plugin_search, dong_plugin_list, dong_mcp_discover | 4 |
| **服务** | dong_serve | 1 |
| **统计** | dong_project_stats | 1 |
| **总计** | | **21** |

## Links

- Core Engine: https://github.com/Dong04-123/Dong-AI-Company
- PyPI: https://pypi.org/project/dong-ai/
- NPM: https://www.npmjs.com/package/@dong-ai/sdk
- Hermes Agent: https://github.com/NousResearch/hermes-agent
- MCP Spec: https://modelcontextprotocol.io
