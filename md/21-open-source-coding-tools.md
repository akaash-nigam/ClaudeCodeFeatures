# Open-Source AI Coding Tools: Comprehensive Architecture Guide

> **Last updated:** March 25, 2026
> **Scope:** All major open-source AI coding CLIs, IDE extensions, editors, and agent platforms

---

## Table of Contents

1. [Comparison Table](#comparison-table)
2. [CLI Tools](#1-cli-tools)
   - [Aider](#11-aider)
   - [OpenCode (sst)](#12-opencode-sst)
   - [Goose (Block)](#13-goose-block)
   - [SWE-agent (Princeton)](#14-swe-agent-princeton)
   - [Gemini CLI (Google)](#15-gemini-cli-google)
3. [IDE Extensions](#2-ide-extensions)
   - [Cline](#21-cline)
   - [Continue.dev](#22-continuedev)
   - [Roo Code](#23-roo-code)
   - [Kilo Code](#24-kilo-code)
   - [Cody (Sourcegraph)](#25-cody-sourcegraph)
4. [Full IDEs / Self-Hosted Platforms](#3-full-ides--self-hosted-platforms)
   - [Void](#31-void)
   - [Pear AI](#32-pear-ai)
   - [Tabby](#33-tabby)
5. [Agent Platforms](#4-agent-platforms)
   - [OpenHands](#41-openhands)
   - [Devon](#42-devon)
   - [Sweep AI](#43-sweep-ai)
   - [bolt.diy](#44-boltdiy)
6. [Archived / Inactive](#5-archived--inactive)
   - [Mentat](#51-mentat)
   - [CodeGeeX](#52-codegeex)
7. [Ecosystem Analysis](#ecosystem-analysis)
8. [Recommendations by Use Case](#recommendations-by-use-case)

---

## Comparison Table

| Tool | Category | Stars | License | Language | Models | MCP | Active | Last Commit |
|------|----------|------:|---------|----------|--------|-----|--------|-------------|
| **OpenCode** | CLI | 130,096 | MIT | TypeScript | 75+ (all major) | Yes | Very Active | Mar 25, 2026 |
| **Gemini CLI** | CLI | 99,036 | Apache-2.0 | TypeScript | Gemini family | Yes | Very Active | Mar 25, 2026 |
| **OpenHands** | Agent Platform | 69,738 | MIT | Python | All major LLMs | Yes | Very Active | Mar 25, 2026 |
| **Cline** | IDE Extension | 59,338 | Apache-2.0 | TypeScript | All major + local | Yes | Very Active | Mar 25, 2026 |
| **Aider** | CLI | 42,366 | Apache-2.0 | Python | All via LiteLLM | No | Very Active | Mar 17, 2026 |
| **Tabby** | Self-Hosted | 33,050 | Apache-2.0 | Rust | CodeLlama, StarCoder, etc. | No | Active | Mar 2, 2026 |
| **Goose** | CLI/Desktop | 33,554 | Apache-2.0 | Rust | All major LLMs | Yes | Very Active | Mar 25, 2026 |
| **Continue** | IDE Extension | 32,047 | Apache-2.0 | TypeScript | All major + local | Yes | Very Active | Mar 25, 2026 |
| **Void** | Full IDE | 28,469 | Apache-2.0 | TypeScript | All major + local | No | Paused | Jan 12, 2026 |
| **Roo Code** | IDE Extension | 22,830 | Apache-2.0 | TypeScript | All major + local | Yes | Very Active | Mar 19, 2026 |
| **bolt.diy** | Agent Platform | 19,204 | MIT | TypeScript | 19+ providers | Yes | Active | Feb 5, 2026 |
| **SWE-agent** | CLI/Research | 18,844 | MIT | Python | GPT-4o, Claude, etc. | No | Active | Mar 24, 2026 |
| **Kilo Code** | IDE Extension | 17,177 | MIT | TypeScript | All major + local | Yes | Very Active | Mar 25, 2026 |
| **bolt.new** | Agent Platform | 16,265 | MIT | TypeScript | Anthropic (hosted) | No | Moderate | Dec 2024 |
| **Sweep AI** | IDE Plugin | 7,655 | Proprietary (OSS core) | Jupyter/Python | Own LLMs | No | Active | Sep 2025 |
| **Cody** | IDE Extension | 3,794 | Apache-2.0 | TypeScript | Claude, GPT-4o, Gemini | No | Pivoted | Mar 24, 2026 |
| **Devon** | Agent Platform | 3,454 | AGPL-3.0 | Python | Anthropic, OpenAI, Groq | No | Stale | Jul 2024 |
| **Mentat** | CLI | 2,559 | Apache-2.0 | Python | OpenAI, Anthropic | No | Archived | 2024 |
| **CodeGeeX** | IDE Plugin | 7,593 | Apache-2.0 | Python | CodeGeeX (13B) | No | Low | 2025 |
| **Pear AI** | Full IDE | 670 | MIT | TypeScript | GPT-4, Claude, Llama | No | Low | May 2025 |

---

## 1. CLI Tools

### 1.1 Aider

| Field | Value |
|-------|-------|
| **Repo** | [github.com/Aider-AI/aider](https://github.com/Aider-AI/aider) |
| **Stars** | 42,366 |
| **License** | Apache-2.0 |
| **Language** | Python |
| **Created by** | Paul Gauthier |
| **Latest commit** | Mar 17, 2026 |

**What it does:** AI pair programming in the terminal. Aider lets you collaboratively edit code with LLMs by adding files to a chat session, making multi-file edits, and auto-committing changes with descriptive git messages.

**Architecture:**

```
Terminal Input
    |
    v
+-------------------+     +--------------------+
| Chat Interface    |---->| Repository Mapper  |
| (code/architect/  |     | (AST-based)        |
|  ask modes)       |     | - Function sigs    |
+-------------------+     | - Dependency graph  |
    |                      | - Relevance scoring |
    v                      +--------------------+
+-------------------+              |
| Edit Formats      |<-------------+
| - whole file      |
| - unified diff    |     +--------------------+
| - search/replace  |---->| Git Integration    |
+-------------------+     | - Auto commits     |
    |                      | - Undo support     |
    v                      +--------------------+
+-------------------+
| Lint & Test Loop  |
| - Auto-fix errors |
| - Re-run tests    |
+-------------------+
```

**Key architectural innovations:**
- **Repository Map:** Uses Abstract Syntax Trees (AST) to create a structural map of the entire codebase -- function signatures, class hierarchies, import relationships. This map is used to prioritize which context to send to the LLM.
- **Architect/Editor dual-model system:** An "Architect" model (e.g., Claude Sonnet) designs the solution, then an "Editor" model translates that into precise code edits. Each model specializes in its strength.
- **Multiple edit formats:** Supports whole-file replacement, unified diffs, and search/replace blocks. The format is auto-selected based on the model's capabilities.
- **Auto lint & test:** After every edit, Aider runs your linter and test suite, then automatically attempts to fix any failures.

**Models supported:** All major LLMs via LiteLLM -- OpenAI (GPT-4o, o1, o3-mini), Anthropic (Claude Sonnet 4, Opus 4), Google (Gemini 2.5), DeepSeek (R1, V3), xAI, Azure, OpenRouter, Bedrock, Vertex AI, local models via Ollama. Works best with Claude Sonnet 4 and DeepSeek.

**Key features:**
- Multi-file coordinated edits across 100+ programming languages
- Voice-to-code via microphone input
- In-chat commands (/add, /drop, /undo, /diff, /test, /lint)
- Git integration with auto-commits and undo
- Architect mode for planning before coding
- Watch mode for continuous development
- Web content scraping for context
- `.aider.conf.yml` for project-specific configuration

**Strengths:**
- Most mature CLI coding tool in the ecosystem (started 2023)
- Excellent multi-file editing with structural awareness
- Model-agnostic with deep LiteLLM integration
- Strong SWE-bench scores, regularly benchmarked
- Clean git history with descriptive auto-commits
- Active solo maintainer with frequent releases

**Weaknesses:**
- No MCP support (as of March 2026)
- No built-in browser automation
- Python-only (slower startup than Go/Rust alternatives)
- No persistent sessions (restarts lose context)
- No native subagent/parallel execution
- UI is basic terminal text (no TUI)

**Community:** 42K+ stars, 4,068 forks, 1,455 open issues. Very active solo-maintainer project with strong community contributions.

---

### 1.2 OpenCode (sst)

| Field | Value |
|-------|-------|
| **Repo** | [github.com/sst/opencode](https://github.com/sst/opencode) |
| **Stars** | 130,096 |
| **License** | MIT |
| **Language** | TypeScript |
| **Created by** | SST (Anomaly) |
| **Latest commit** | Mar 25, 2026 |

**What it does:** The most-starred open-source coding agent. A terminal-native AI coding tool with a rich TUI, persistent sessions, multi-agent system, and support for 75+ LLMs across all major providers.

**Architecture:**

```
+------------------+     +--------------------+     +------------------+
| TUI Client       |     | Desktop App        |     | VS Code Extension|
| (Ink/React)      |     | (Electron)         |     |                  |
+--------+---------+     +--------+-----------+     +--------+---------+
         |                        |                           |
         +------------------------+---------------------------+
                                  |
                    +-------------v--------------+
                    | Persistent Background      |
                    | Server (HTTP/SSE)           |
                    | - SessionPrompt orchestrator|
                    | - ToolRegistry              |
                    | - Provider.getModel()       |
                    +-------------+--------------+
                                  |
              +-------------------+-------------------+
              |                   |                   |
    +---------v-------+  +-------v--------+  +-------v--------+
    | Agent System     |  | Tool System    |  | Skills System  |
    | - Build (default)|  | - File ops     |  | - .opencode/   |
    | - Plan (readonly)|  | - Shell exec   |  |   skills/      |
    | - @general sub   |  | - Code search  |  | - Custom cmds  |
    +------------------+  | - Task delegate|  +----------------+
                          +----------------+
```

**Key architectural innovations:**
- **Persistent background server:** Sessions survive terminal disconnects, SSH drops, and machine sleeps. You reconnect and pick up where you left off.
- **Multi-interface:** Same backend serves TUI (terminal), desktop app (Electron), VS Code extension, and web interface.
- **7 native agents:** Build, Plan, and specialized subagents with predefined permissions and tool access. Agents can delegate to other agents.
- **Layered tool system:** Tools from various sources registered in ToolRegistry, resolved per-agent and per-model capabilities, transformed for the AI model by ProviderTransform.
- **Skills system:** First-class skill definitions in `.opencode/skills/` that integrate with the execution pipeline.

**Models supported:** 75+ models -- OpenAI, Anthropic, Google Gemini, AWS Bedrock, Azure OpenAI, Groq, OpenRouter, local models via Ollama and LM Studio, and essentially any OpenAI-compatible API.

**Key features:**
- Rich TUI with session management
- Persistent sessions that survive disconnects
- MCP server support for extensibility
- Skills system for reusable prompts/workflows
- Custom commands via Markdown files
- LSP integration for code intelligence
- Privacy-first (no code/context data stored by OpenCode)
- File operations, shell execution, code search built-in

**Strengths:**
- Largest open-source coding agent by stars (130K+)
- Multi-interface (CLI, desktop, IDE extension, web)
- Persistent sessions are a killer feature for long tasks
- Massive model support (75+)
- Very active development and large community (800+ contributors)
- Privacy-focused architecture

**Weaknesses:**
- Relatively new (viral growth in late 2025 / early 2026)
- Still pre-1.0 in many interfaces
- TypeScript-based (heavier than Go/Rust alternatives)
- Community documentation still catching up to rapid feature development

**Community:** 130K+ stars, 13,793 forks, 800+ contributors, 10K+ commits, 5M+ monthly developers. The fastest-growing open-source coding project in 2025-2026.

---

### 1.3 Goose (Block)

| Field | Value |
|-------|-------|
| **Repo** | [github.com/block/goose](https://github.com/block/goose) |
| **Stars** | 33,554 |
| **License** | Apache-2.0 |
| **Language** | Rust |
| **Created by** | Block (Square, Cash App) |
| **Latest commit** | Mar 25, 2026 |

**What it does:** An extensible AI agent from Block that goes beyond code suggestions -- it can install dependencies, execute code, edit files, run tests, and orchestrate workflows. Built on the Model Context Protocol (MCP) for deep tool integration.

**Architecture:**

```
+------------------+     +------------------+
| Desktop App      |     | CLI Interface    |
| (native)         |     | (terminal)       |
+--------+---------+     +--------+---------+
         |                        |
         +------------------------+
                    |
         +----------v-----------+
         | Goose Core (Rust)    |
         | - Agent orchestrator |
         | - Session manager    |
         +----------+-----------+
                    |
    +---------------+---------------+
    |               |               |
+---v---+     +-----v-----+   +----v----+
| LLM   |     | MCP Server|   | Tool    |
| Router |     | Registry  |   | System  |
| (any)  |     | (plugins) |   | (native)|
+--------+     +-----------+   +---------+
```

**Key architectural innovations:**
- **MCP-native:** Built from the ground up on the Model Context Protocol (co-developed with Anthropic). Every external integration is an MCP server, making Goose infinitely extensible.
- **Rust core:** Fast startup, low memory footprint, and reliable cross-platform binaries.
- **Enterprise-grade:** Backed by Block (a $40B+ company), designed for enterprise workflows from day one.

**Models supported:** Any LLM -- supports multi-model configuration to optimize performance and cost. OpenAI, Anthropic, Google, local models, and any OpenAI-compatible endpoint.

**Key features:**
- MCP-first architecture with plugin ecosystem
- Desktop app and CLI interfaces
- Multi-model configuration for cost optimization
- File editing, terminal execution, test running
- Workflow orchestration beyond just coding
- Can interact with external APIs autonomously

**Strengths:**
- Rust-based (fast, efficient, reliable)
- MCP-native gives it the best extensibility story
- Enterprise backing from Block
- Free and fully open source
- Active development (commits daily)

**Weaknesses:**
- Narrower community compared to OpenCode/Aider
- Still evolving rapidly (API surface changing)
- Less coding-specific benchmarking data than Aider
- Documentation could be more comprehensive

**Community:** 33.5K stars, 3,124 forks, 368+ contributors. Backed by Block with dedicated engineering team.

---

### 1.4 SWE-agent (Princeton)

| Field | Value |
|-------|-------|
| **Repo** | [github.com/princeton-nlp/SWE-agent](https://github.com/princeton-nlp/SWE-agent) |
| **Stars** | 18,844 |
| **License** | MIT |
| **Language** | Python |
| **Created by** | Princeton & Stanford researchers |
| **Latest commit** | Mar 24, 2026 |

**What it does:** An autonomous agent that takes a GitHub issue and attempts to fix it automatically. Designed primarily as a research tool for the SWE-bench benchmark, it also supports offensive cybersecurity testing and competitive coding challenges. Published at NeurIPS 2024.

**Architecture:**

```
+------------------+
| GitHub Issue     |
| (input)          |
+--------+---------+
         |
+--------v---------+
| Agent-Computer   |
| Interface (ACI)  |
| - Custom commands|
| - LM-centric I/O |
+--------+---------+
         |
+--------v---------+     +------------------+
| Agent Loop       |---->| Docker Sandbox   |
| - Navigate repo  |     | - File editing   |
| - View/edit code |     | - Test execution |
| - Execute tests  |     | - Command shell  |
+--------+---------+     +------------------+
         |
+--------v---------+
| LLM (configurable)|
| - GPT-4o         |
| - Claude Sonnet  |
+------------------+
```

**Key architectural innovations:**
- **Agent-Computer Interface (ACI):** Custom-designed commands and feedback formats that make it easier for LLMs to navigate repositories, view/edit code, and execute tests. The ACI is the key insight -- the interface design matters as much as the model.
- **YAML-governed:** The entire agent behavior is controlled by a single YAML configuration file.
- **mini-SWE-agent:** A simplified 100-line version that scores >74% on SWE-bench verified, proving the core ideas are sound.

**Models supported:** GPT-4o, Claude Sonnet 4, and any LLM that supports function calling. Configured per-run via YAML.

**Key features:**
- Autonomous GitHub issue resolution
- Docker-sandboxed execution
- SWE-bench benchmarking built-in
- Cybersecurity vulnerability finding
- Competitive coding challenge solving
- Configurable via single YAML file
- Minimal, research-oriented design

**Strengths:**
- Academic rigor (Princeton/Stanford, NeurIPS 2024)
- State-of-the-art SWE-bench performance
- Clean, well-documented architecture
- The ACI concept is influential across the ecosystem
- mini-SWE-agent proves simplicity works

**Weaknesses:**
- Research-first, not production-ready for daily development
- No interactive mode (batch processing only)
- No MCP or plugin system
- Requires Docker for sandboxing
- Not designed for general-purpose coding assistance

**Community:** 18.8K stars, 2,034 forks. Academic project with active research development.

---

### 1.5 Gemini CLI (Google)

| Field | Value |
|-------|-------|
| **Repo** | [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) |
| **Stars** | 99,036 |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Created by** | Google |
| **Latest commit** | Mar 25, 2026 |

**What it does:** Google's open-source AI agent that brings Gemini directly into the terminal. A direct competitor to Claude Code, offering agentic coding with file editing, terminal execution, and multimodal understanding powered by Gemini models with massive context windows (1M+ tokens).

**Architecture:**

```
+------------------+
| Terminal (CLI)   |
+--------+---------+
         |
+--------v---------+
| Agent Core       |
| - Plan mode      |
| - Code mode      |
| - Shell access   |
+--------+---------+
         |
    +----+----+
    |         |
+---v---+ +---v---+
| Tools | | Gemini|
| - File| | API   |
| - Exec| | (2.5) |
| - Web | +-------+
+-------+
```

**Key features:**
- Free tier with generous token limits via Google AI Studio
- Plan mode (shipped March 2026) for multi-step reasoning
- 1M+ token context window (Gemini 2.5 Pro)
- Multimodal (images, code, text)
- MCP support for extensibility
- AGENTS.md project configuration
- Shell integration and file editing

**Models supported:** Gemini 2.5 Pro, Gemini 2.5 Flash, and other Gemini family models. Primarily Gemini-only (not model-agnostic).

**Strengths:**
- Massive context window (1M+ tokens)
- Free tier makes it accessible
- Backed by Google with active development
- Second-most-starred coding CLI (99K)
- Multimodal capabilities

**Weaknesses:**
- Gemini-only (no model flexibility)
- Newer than Aider/Claude Code (less battle-tested)
- Google API dependency
- Community perception of Google project longevity

**Community:** 99K stars, 12,607 forks. Google-backed with rapid community adoption.

> **Note:** Gemini CLI is covered in more detail in [13-gemini-cli-architecture.md](13-gemini-cli-architecture.md).

---

## 2. IDE Extensions

### 2.1 Cline

| Field | Value |
|-------|-------|
| **Repo** | [github.com/cline/cline](https://github.com/cline/cline) |
| **Stars** | 59,338 |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Originally** | Claude Dev (by Saoud Rizwan) |
| **Latest commit** | Mar 25, 2026 |

**What it does:** The most popular open-source autonomous coding agent for VS Code. Cline can create/edit files, execute terminal commands, use a browser, and integrate with MCP tools -- all with human approval at every step.

**Architecture:**

```
+---------------------------+
| VS Code Extension Panel   |
| - Chat UI                 |
| - Diff viewer             |
| - Approval interface      |
+-----------+---------------+
            |
+-----------v---------------+
| Plan/Act Pipeline          |
| - Plan: analyze & propose  |
| - Act: execute with approval|
+-----------+---------------+
            |
    +-------+-------+-------+-------+
    |       |       |       |       |
+---v-+ +---v-+ +---v-+ +---v-+ +---v-+
|File | |Term | |Browse| |MCP  | |Sub  |
|Edit | |Exec | |Auto  | |Tools| |Agent|
+-----+ +-----+ +-----+ +-----+ +-----+
```

**Key architectural innovations:**
- **Plan/Act pipeline:** Every task is decomposed into a planning phase and an execution phase. Changes are sorted into snapshots that can be approved or rolled back.
- **Human-in-the-loop:** Every file edit, terminal command, and browser action requires explicit user approval, making it safe for production codebases.
- **Browser automation:** Built-in Puppeteer-based browser control for frontend testing -- can click elements, type into fields, scroll, capture screenshots and console logs.
- **MCP Marketplace:** 100+ pre-built MCP servers for database access, API integrations, browser control, and custom tools.
- **Native subagents (v3.58):** Parallel execution of sub-tasks for complex workflows.

**Models supported:** More providers than any other tool -- OpenRouter, Anthropic, OpenAI, Google Gemini, AWS Bedrock, Azure, GCP Vertex, Cerebras, Groq, and local models via LM Studio or Ollama. Any OpenAI-compatible API.

**Key features:**
- Autonomous file creation/editing with diff view
- Terminal command execution
- Browser automation (click, type, scroll, screenshot)
- MCP tool integration with marketplace (100+ servers)
- Native subagents for parallel execution (v3.58)
- CLI 2.0 with headless CI/CD mode (Feb 2026)
- Context injection via @url, @problems, @file, @folder
- Per-task token and cost tracking
- `.clinerules` files for project-specific configuration
- 5M+ installs across VS Code, Cursor, JetBrains, Zed, Neovim

**Strengths:**
- Most-installed open-source coding extension (5M+)
- Best browser automation of any coding tool
- Richest MCP ecosystem
- Model-agnostic with the widest provider support
- Human-in-the-loop safety by default
- Rapidly shipping features (subagents, CLI, etc.)

**Weaknesses:**
- Can be expensive with token usage (long system prompts)
- Approval fatigue on large tasks (many confirmation dialogs)
- VS Code-dependent for the extension (CLI is newer)
- Context window management with local models requires tuning

**Community:** 59.3K stars, 6,027 forks, 698 open issues. One of the fastest-growing VS Code extensions ever.

---

### 2.2 Continue.dev

| Field | Value |
|-------|-------|
| **Repo** | [github.com/continuedev/continue](https://github.com/continuedev/continue) |
| **Stars** | 32,047 |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Created by** | Continue (YC-backed) |
| **Latest commit** | Mar 25, 2026 |

**What it does:** An open-source AI code assistant for VS Code and JetBrains that emphasizes model flexibility, team configuration, and CI/CD integration. Positions itself as "quality control for your software factory" with source-controlled AI checks enforceable in CI.

**Architecture:**

```
+-------------------+     +-------------------+
| VS Code Extension |     | JetBrains Plugin  |
+--------+----------+     +--------+----------+
         |                         |
         +------------+------------+
                      |
         +------------v------------+
         | Continue Core           |
         | - Chat / Plan / Agent   |
         | - Autocomplete engine   |
         | - Context providers     |
         +------------+------------+
                      |
    +---------+-------+-------+---------+
    |         |               |         |
+---v---+ +---v---+     +----v----+ +---v---+
| LLM   | | MCP   |     | .continue| | CI/CD |
| Router | | Tools |     | /rules/ | | Runner|
+-------+ +-------+     +---------+ +-------+
```

**Key architectural innovations:**
- **Source-controlled AI rules:** `.continue/rules/` directory stores team standards, coding patterns, and AI behaviors. Shared via git, ensuring every team member gets the same AI assistant configuration.
- **CI/CD integration:** Continue CLI can run AI checks in GitHub Actions, Jenkins, GitLab CI, and cron jobs -- making AI-powered code review enforceable.
- **Three interaction modes:** Chat (conversational), Plan (multi-step), Agent (autonomous execution).

**Models supported:** Fully model-agnostic -- any cloud provider (OpenAI, Anthropic, Google, etc.) or local model (Ollama, LM Studio, CodeLlama, Mistral, Llama). BYOK (Bring Your Own Key) model.

**Key features:**
- Chat, Plan, and Agent modes
- Tab autocomplete with any model
- MCP tool support (GitHub, Sentry, Snyk, Linear)
- `.continue/rules/` for team-shared AI configuration
- CI/CD pipeline integration via Continue CLI
- Context providers for codebase awareness
- JetBrains support (not just VS Code)
- Codebase indexing for retrieval

**Strengths:**
- Best IDE breadth (VS Code + full JetBrains family)
- CI/CD integration is unique in the space
- Team-oriented configuration management
- Fully model-agnostic with BYOK
- Apache-2.0 license with no vendor lock-in
- YC-backed with sustainable business model

**Weaknesses:**
- Less autonomous than Cline (more assistant than agent)
- No browser automation
- Autocomplete quality depends heavily on model choice
- Configuration can be complex for beginners
- Extension UX not as polished as Cline/Roo Code

**Community:** 32K stars, 4,296 forks, 528 open issues. Strong enterprise adoption.

---

### 2.3 Roo Code

| Field | Value |
|-------|-------|
| **Repo** | [github.com/RooVetGit/Roo-Code](https://github.com/RooVetGit/Roo-Code) |
| **Stars** | 22,830 |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Originally** | Roo-Cline (fork of Cline) |
| **Latest commit** | Mar 19, 2026 |

**What it does:** A VS Code extension that provides a team of AI agents with specialized modes for different development tasks -- planning, coding, debugging, architecture, and custom workflows. Think of it as Cline with a mode system.

**Architecture:**

```
+---------------------------+
| VS Code Extension Panel   |
+-----------+---------------+
            |
+-----------v---------------+
| Mode Router               |
| - Code (default)          |
| - Architect (planning)    |
| - Ask (read-only Q&A)     |
| - Debug (error tracing)   |
| - Custom (user-defined)   |
+-----------+---------------+
            |
+-----------v---------------+
| Agent Execution Engine    |
| - Tool permissions/mode   |
| - Context management      |
| - Mode switching          |
+-----------+---------------+
            |
    +-------+-------+-------+
    |       |       |       |
+---v-+ +---v-+ +---v-+ +---v-+
|File | |Term | |Browse| |MCP  |
|Edit | |Exec | |Auto  | |Tools|
+-----+ +-----+ +-----+ +-----+
```

**Key architectural innovations:**
- **Mode system:** Five built-in modes (Code, Architect, Ask, Debug, Custom) each with scoped tool permissions. Modes keep models focused and limit context window pollution.
- **Mode Gallery:** Community-published mode configurations for common workflows (backend scaffolding, CI/CD editing, test generation).
- **Smart mode switching:** Modes can detect when a task falls outside their scope and suggest switching to the appropriate mode.

**Models supported:** Model-agnostic -- OpenAI, Anthropic, Google, local models via Ollama, and any other provider. BYOK.

**Key features:**
- 5 built-in modes + custom mode templates
- Mode Gallery for community-shared configurations
- Multi-file editing, terminal execution, browser automation
- MCP tool integration
- Intelligent task coordination across modes
- Model-agnostic architecture
- `.roorules` for project configuration
- v3.50.4 (Feb 2026)

**Strengths:**
- Mode system is genuinely innovative for task separation
- Forked from Cline, so inherits all its capabilities
- Active community with mode marketplace
- Good for teams wanting role-specific AI agents
- Rapid release cadence

**Weaknesses:**
- Smaller community than Cline (the project it forked from)
- Mode switching can add cognitive overhead
- Some features lag behind Cline's latest releases
- Documentation still maturing
- Forked identity can cause confusion with Cline

**Community:** 22.8K stars, 2,934 forks, 743 open issues. Fastest-evolving AI coding extension.

---

### 2.4 Kilo Code

| Field | Value |
|-------|-------|
| **Repo** | [github.com/Kilo-Org/kilocode](https://github.com/Kilo-Org/kilocode) |
| **Stars** | 17,177 |
| **License** | MIT |
| **Language** | TypeScript |
| **Created by** | Kilo AI |
| **Latest commit** | Mar 25, 2026 |

**What it does:** An all-in-one agentic engineering platform for VS Code, JetBrains, and CLI. Claims to be the #1 coding agent on OpenRouter with 1.5M+ users and 25T+ tokens processed.

**Architecture:**

```
+------------------+     +------------------+     +------------------+
| VS Code Extension|     | JetBrains Plugin |     | Kilo CLI         |
+--------+---------+     +--------+---------+     +--------+---------+
         |                        |                         |
         +------------------------+-------------------------+
                                  |
                    +-------------v--------------+
                    | Kilo Engine (shared)       |
                    | - Orchestrator agent       |
                    | - Tool system              |
                    | - MCP registry             |
                    +-------------+--------------+
                                  |
              +-------------------+-------------------+
              |                   |                   |
    +---------v-------+  +-------v--------+  +-------v--------+
    | Agent Modes      |  | Tool System    |  | MCP Marketplace|
    | - Orchestrator   |  | - read_file    |  | - Figma        |
    | - Architect      |  | - apply_diff   |  | - Git          |
    | - Coder          |  | - execute_cmd  |  | - Custom       |
    | - Debugger       |  | - use_mcp_tool |  +----------------+
    | - Ask            |  +----------------+
    +-----------------+
```

**Key architectural innovations:**
- **Shared engine:** One engine powers VS Code extension, JetBrains plugin, and CLI. Same capabilities everywhere.
- **Orchestrator mode:** A meta-agent that plans and delegates to Architect, Coder, and Debugger agents.
- **Parallel agent execution:** Can run multiple agents simultaneously for multi-step tasks.
- **MCP Marketplace:** Curated collection of Skills, MCP Servers, and Modes for the Kilo ecosystem.

**Models supported:** All major providers + local models. Notable partnership with xAI for "Grok Code Fast" with unlimited free access and 262K token context.

**Key features:**
- 5 agent modes (Orchestrator, Architect, Coder, Debugger, Ask)
- Parallel agent execution
- MCP Marketplace with Skills and Modes
- Inline autocomplete
- Browser automation
- Streamable HTTP MCP support (April 2025)
- VS Code + JetBrains + CLI
- 1.5M+ users, 25T+ tokens processed

**Strengths:**
- Multi-platform (VS Code, JetBrains, CLI)
- Orchestrator mode for complex multi-step tasks
- Large user base (1.5M+)
- Active MCP marketplace
- MIT license (most permissive)

**Weaknesses:**
- Newer project, less battle-tested than Cline
- Heavy marketing claims (#1 on OpenRouter) may not reflect all use cases
- Community size smaller than Cline/Roo Code by stars
- Documentation could be more technical

**Community:** 17.2K stars, 2,223 forks. Growing rapidly with dedicated marketplace.

---

### 2.5 Cody (Sourcegraph)

| Field | Value |
|-------|-------|
| **Repo** | [github.com/sourcegraph/cody-public-snapshot](https://github.com/sourcegraph/cody-public-snapshot) |
| **Stars** | 3,794 (public snapshot) |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Created by** | Sourcegraph |
| **Status** | Pivoted to "Amp" (enterprise) |

**What it does:** An AI coding assistant that leverages Sourcegraph's deep code search and intelligence to provide context-aware code assistance. Uniquely strong at understanding large, enterprise-scale codebases due to Sourcegraph's decade of code indexing technology.

**Architecture:**

```
+-------------------+     +-------------------+
| VS Code Extension |     | JetBrains Plugin  |
+--------+----------+     +--------+----------+
         |                         |
         +------------+------------+
                      |
         +------------v------------+
         | Cody Context Engine     |
         | - Sourcegraph Search API|
         | - Symbol index          |
         | - Cross-repo context    |
         +------------+------------+
                      |
              +-------+-------+
              |               |
        +-----v-----+  +-----v-----+
        | LLM Router |  | Code      |
        | (swappable)|  | Intelligence|
        +------------+  +------------+
```

**Key features:**
- Deep codebase context via Sourcegraph's code intelligence
- Autocomplete (single and multi-line)
- Chat with repository-wide context
- Inline edit and refactor
- Swappable LLMs (Claude Sonnet, GPT-4o, Gemini)
- Cross-repository context awareness

**Current status:** Public free/pro plans discontinued in 2025. Cody has been rebranded as **Amp** for enterprise use. The open-source public snapshot is a frozen copy. This is now primarily an enterprise product, not a community open-source tool.

**Community:** 3.8K stars on public snapshot. Enterprise-focused going forward.

---

## 3. Full IDEs / Self-Hosted Platforms

### 3.1 Void

| Field | Value |
|-------|-------|
| **Repo** | [github.com/voideditor/void](https://github.com/voideditor/void) |
| **Stars** | 28,469 |
| **License** | Apache-2.0 |
| **Language** | TypeScript |
| **Created by** | Void (YC-backed) |
| **Latest commit** | Jan 12, 2026 |
| **Status** | **PAUSED** |

**What it does:** An open-source, privacy-focused AI code editor built as a fork of VS Code. Positioned as a free alternative to Cursor with full model flexibility and local execution.

**Architecture:**

```
+----------------------------------+
| VS Code Fork (Electron)         |
| +------------------------------+|
| | Agent Mode | Gather Mode     ||
| | Chat Panel | Inline Editor   ||
| +------------------------------+|
|              |                   |
| +------------v-----------------+|
| | LLM Streaming Layer          ||
| | - Real-time UI updates       ||
| | - Multiple provider support  ||
| +------------------------------+|
| | File Indexing Engine          ||
| +------------------------------+|
+----------------------------------+
```

**Key features:**
- Agent Mode, Gather Mode, and Chat
- AI-powered code completion and inline editing
- Checkpoint and visualize changes
- File indexing for efficient navigation
- Direct LLM connections (no data retention)
- Support for Claude, GPT, Gemini, Ollama

**Current status:** **Development paused.** The team announced they are "exploring novel coding ideas" and while Void will continue running, existing features may stop working without maintenance. Despite 28K+ stars, this project is not actively maintained as of early 2026.

**Community:** 28.5K stars, 2,375 forks. High interest but paused development is a significant risk.

---

### 3.2 Pear AI

| Field | Value |
|-------|-------|
| **Repo** | [github.com/trypear/pearai-app](https://github.com/trypear/pearai-app) |
| **Stars** | 670 |
| **License** | MIT |
| **Language** | TypeScript |
| **Created by** | Pear (YC-backed) |
| **Latest commit** | May 2025 |
| **Status** | Low activity |

**What it does:** An open-source AI code editor (VS Code fork) that bundles multiple AI tools -- Aider for code generation, Supermaven for autocomplete, Continue for assistant features, Mem0 for memory, and Perplexity for search -- into a single editor experience.

**Architecture:**

```
+----------------------------------+
| VS Code Fork (Electron)         |
| +------------------------------+|
| | PearAI Router (model select) ||
| +------------------------------+|
| | Integrated Tools:             ||
| | - Aider (code gen)            ||
| | - Supermaven (autocomplete)   ||
| | - Continue (assistant)        ||
| | - Roo Code/Cline (agent)     ||
| | - Mem0 (memory)              ||
| | - Perplexity (search)        ||
| +------------------------------+|
+----------------------------------+
```

**Key features:**
- Bundles best-of-breed OSS tools into one editor
- PearAI Router for intelligent model selection
- AI Chat, inline prompts, agent mode
- Context-aware with local codebase indexing
- Supported models: GPT-4, Claude, Llama

**Current status:** Low activity. Last commit May 2025. With only 670 stars, this project has not gained significant traction. The "bundle existing tools" approach means it depends on upstream projects that are evolving fast.

**Community:** 670 stars, 190 forks. YC-backed but struggling for adoption.

---

### 3.3 Tabby

| Field | Value |
|-------|-------|
| **Repo** | [github.com/TabbyML/tabby](https://github.com/TabbyML/tabby) |
| **Stars** | 33,050 |
| **License** | Apache-2.0 |
| **Language** | Rust |
| **Created by** | TabbyML |
| **Latest commit** | Mar 2, 2026 |

**What it does:** A self-hosted AI coding assistant, offering an on-premises alternative to GitHub Copilot. Runs on consumer-grade GPUs with no cloud dependency, providing real-time code completion, chat, and repository-level understanding.

**Architecture:**

```
+-------------------+     +-------------------+     +-------------------+
| VS Code Extension |     | JetBrains Plugin  |     | Web UI            |
+--------+----------+     +--------+----------+     +--------+----------+
         |                         |                          |
         +-------------------------+--------------------------+
                                   |
                     +-------------v--------------+
                     | Tabby Server (Rust)        |
                     | - OpenAPI interface         |
                     | - Model serving             |
                     | - Repository indexer         |
                     | - RAG engine                 |
                     +-------------+--------------+
                                   |
                   +---------------+---------------+
                   |               |               |
           +-------v------+ +-----v-----+ +-------v------+
           | Code Models   | | Repository | | Enterprise   |
           | - CodeLlama   | | Index      | | Features     |
           | - StarCoder   | | - RAG      | | - SSO        |
           | - CodeGen     | | - Context  | | - Analytics  |
           | - Custom      | +------------+ | - Teams      |
           +--------------+                 +--------------+
```

**Key architectural innovations:**
- **Self-contained server:** No external DBMS or cloud service needed. Everything runs locally with an OpenAPI interface for easy integration.
- **Rust-based server:** Fast, low-memory, reliable. Runs on consumer GPUs (NVIDIA, AMD).
- **Repository-level RAG:** Indexes your entire repository for context-aware completions and chat. Can index GitLab merge requests for additional context.
- **Enterprise-ready:** Team management, usage analytics, SSO, fine-tuning on private repos.

**Models supported:** Self-hosted coding models -- CodeLlama, StarCoder, CodeGen, DeepSeek Coder, and custom fine-tuned models. Not designed for cloud API models.

**Key features:**
- Real-time code completion (40+ languages)
- Chat interface with repository context
- Repository indexing with RAG
- Fine-tuning on private repositories
- Consumer-grade GPU support
- OpenAPI interface for integration
- Enterprise: SSO, team management, analytics
- VS Code and JetBrains extensions
- Pages feature for persistent, shareable answers

**Strengths:**
- Best self-hosted option (no cloud dependency)
- Rust-based (fast, efficient)
- Enterprise features (SSO, analytics, teams)
- Privacy-first (all data stays on-prem)
- Repository-level context awareness
- Active development with regular releases

**Weaknesses:**
- Requires GPU hardware for good performance
- Smaller model ecosystem than cloud-based tools
- No agent/autonomous capabilities (completion + chat only)
- No MCP or plugin system
- Self-hosting complexity (GPU drivers, model management)

**Community:** 33K stars, 1,692 forks. Strong enterprise and privacy-focused community.

---

## 4. Agent Platforms

### 4.1 OpenHands

| Field | Value |
|-------|-------|
| **Repo** | [github.com/All-Hands-AI/OpenHands](https://github.com/All-Hands-AI/OpenHands) |
| **Stars** | 69,738 |
| **License** | MIT |
| **Language** | Python |
| **Originally** | OpenDevin |
| **Latest commit** | Mar 25, 2026 |

**What it does:** An open platform for AI software developers as generalist agents. OpenHands agents can write code, use the command line, browse the web, and interact with the world in ways similar to a human developer. Published at ICLR 2025.

**Architecture:**

```
+----------------------------------+
| OpenHands Platform               |
|                                  |
| +------------------------------+ |
| | Agent Hub (10+ agents)       | |
| | - CodeAct (generalist)       | |
| | - Web browsing specialist    | |
| | - Code editing specialist    | |
| +-------------+----------------+ |
|               |                  |
| +-------------v----------------+ |
| | Event Stream                 | |
| | - Chronological actions      | |
| | - Observations               | |
| | - User interactions          | |
| +-------------+----------------+ |
|               |                  |
| +-------------v----------------+ |
| | Runtime (Docker Sandbox)     | |
| | - Bash shell                 | |
| | - Web browser                | |
| | - IPython server             | |
| | - File system                | |
| +------------------------------+ |
|                                  |
| +------------------------------+ |
| | SDK (Python library)         | |
| | - Define agents in code      | |
| | - Run locally or cloud       | |
| | - Scale to 1000s of agents   | |
| +------------------------------+ |
+----------------------------------+
```

**Key architectural innovations:**
- **3-layer architecture:** Agent abstraction (pluggable agents), Event stream (action/observation history), Runtime (Docker-sandboxed execution).
- **CodeAct agent:** A strong generalist agent based on the CodeAct architecture that uses code execution as its primary action mechanism, with additions for web browsing and code editing.
- **Composable SDK:** Python library that lets you define agents in code, run locally, or scale to thousands of agents in the cloud.
- **Event stream:** Chronological tracking of all actions and observations, enabling replay, debugging, and audit trails.

**Models supported:** Model-agnostic -- works with any LLM including OpenAI, Anthropic, Google, local models. Designed to be provider-independent.

**Key features:**
- 10+ implemented agents in the agent hub
- Docker-sandboxed runtime with bash, browser, IPython
- Event stream for full audit trail
- Python SDK for custom agent development
- Web UI for interactive use
- Cloud scaling (1000s of agents)
- SWE-bench evaluation built-in
- AMD Lemonade Server integration for local AI

**Strengths:**
- Largest AI agent platform by stars (70K)
- Academic rigor (ICLR 2025, arXiv papers)
- Most comprehensive agent framework
- Docker sandboxing for safety
- SDK enables building custom agents
- Active community (188+ contributors, 2.1K+ contributions)

**Weaknesses:**
- Heavy infrastructure requirements (Docker, Python)
- Steep learning curve for custom agent development
- Not a simple "coding assistant" -- it's a platform
- Overkill for simple code editing tasks
- Resource-intensive (Docker containers per session)

**Community:** 69.7K stars, 8,741 forks. Largest open-source AI agent platform. Published research papers. Very active development.

---

### 4.2 Devon

| Field | Value |
|-------|-------|
| **Repo** | [github.com/entropy-research/Devon](https://github.com/entropy-research/Devon) |
| **Stars** | 3,454 |
| **License** | AGPL-3.0 |
| **Language** | Python |
| **Created by** | Entropy Research |
| **Latest commit** | Jul 2024 |
| **Status** | **STALE** |

**What it does:** An open-source pair programmer with multi-agent architecture. Devon deploys specialized agents for code generation, exploration, configuration writing, testing, and bug fixing. Featured on Hacker News in May 2024.

**Architecture:**

```
+------------------+
| devon-ui (npx)   |
+--------+---------+
         |
+--------v---------+
| devon_agent      |
| (pipx)           |
+--------+---------+
         |
    +----+----+----+
    |    |    |    |
  Code Explore Test Debug
  Agent Agent  Agent Agent
```

**Key features:**
- Multi-file editing
- Codebase exploration
- Test writing and bug fixing
- Configuration writing
- Multi-agent architecture

**Models supported:** Anthropic, OpenAI, Groq APIs.

**Current status:** **Stale.** Last commit July 2024. No activity for 20+ months. The project showed early promise but appears abandoned. The AGPL-3.0 license is also more restrictive than alternatives.

**Community:** 3.5K stars, 279 forks. Initial HN buzz but no sustained development.

---

### 4.3 Sweep AI

| Field | Value |
|-------|-------|
| **Repo** | [github.com/sweepai/sweep](https://github.com/sweepai/sweep) |
| **Stars** | 7,655 |
| **License** | Proprietary (OSS core) |
| **Language** | Python/Jupyter |
| **Created by** | Sweep AI |
| **Latest commit** | Sep 2025 |
| **Status** | Pivoted to JetBrains |

**What it does:** Originally an AI junior developer that automatically resolves GitHub issues by reading your codebase and creating pull requests. Has since pivoted to become a JetBrains IDE plugin focused on autocomplete, inline editing, and agent capabilities.

**Architecture (current JetBrains focus):**

```
+---------------------------+
| JetBrains IDE Plugin      |
| - IntelliJ, PyCharm, etc. |
+-----------+---------------+
            |
+-----------v---------------+
| Sweep Engine               |
| - Project indexer           |
| - Next-edit autocomplete    |
| - Code refactoring agent    |
+-----------+---------------+
            |
+-----------v---------------+
| Sweep's Own LLMs           |
| (no third-party retention) |
+---------------------------+
```

**Key features:**
- Next-edit autocomplete (unique to Sweep)
- Context-aware inline suggestions
- Automated refactoring (function extraction, dead code removal)
- Test generation
- Static analysis feedback
- Uses own LLMs (no code retained by third parties)
- Supports Python, JS/TS, Java, Go, C#, C++, Rust

**Current status:** Active as a JetBrains plugin but the open-source GitHub issue resolver (the original product) has been deprioritized. The GitHub repo is primarily for the legacy product.

**Community:** 7.7K stars, 454 forks. 40K+ JetBrains installs.

---

### 4.4 bolt.diy

| Field | Value |
|-------|-------|
| **Repo** | [github.com/stackblitz-labs/bolt.diy](https://github.com/stackblitz-labs/bolt.diy) |
| **Stars** | 19,204 |
| **License** | MIT |
| **Language** | TypeScript |
| **Created by** | Community (forked from bolt.new) |
| **Latest commit** | Feb 5, 2026 |

**What it does:** An open-source platform for prompting, running, editing, and deploying full-stack web applications using any LLM. Community fork of StackBlitz's bolt.new that adds multi-provider LLM support.

**Architecture:**

```
+----------------------------------+
| Web Interface / Electron App     |
| - Chat-based project creation    |
| - Live preview                   |
| - File editor                    |
+-----------+----------------------+
            |
+-----------v----------------------+
| bolt.diy Engine                  |
| - Vercel AI SDK integration      |
| - WebContainer (in-browser Node) |
| - Diff view & version control    |
+-----------+----------------------+
            |
    +-------+-------+-------+
    |       |       |       |
+---v---+ +---v---+ +---v---+
| 19+   | | Deploy| | MCP   |
| LLM   | | Netlify| | Tools |
| Provs | | Vercel| |       |
+-------+ | GitHub| +-------+
          +-------+
```

**Key architectural innovations:**
- **WebContainer:** Runs a full Node.js environment in the browser via StackBlitz's WebContainer technology. No server needed for previews.
- **Multi-provider LLM support:** The key differentiator from bolt.new -- supports 19+ providers including OpenAI, Anthropic, Ollama, OpenRouter, Gemini, Mistral, DeepSeek, Groq, and more.

**Models supported:** 19+ providers -- OpenAI, Anthropic, Ollama, OpenRouter, Google Gemini, LM Studio, Mistral, xAI, HuggingFace, DeepSeek, Groq, Cohere, Together AI, Perplexity, Amazon Bedrock, and more. Extensible via Vercel AI SDK.

**Key features:**
- Full-stack web app generation from prompts
- In-browser live preview (WebContainer)
- 19+ LLM providers
- Deploy to Netlify, Vercel, or GitHub Pages
- Image attachment for context
- Version history and revert
- Diff view for AI changes
- MCP support
- Docker deployment option
- Electron desktop app
- Download as ZIP

**Strengths:**
- Best tool for full-stack web app generation
- In-browser execution (no Docker/server needed)
- Widest LLM provider support for web app builders
- One-click deployment to major platforms
- Active community fork with rapid features

**Weaknesses:**
- Web-app focused (not general-purpose coding)
- Generated code quality varies by model
- No terminal/CLI access (browser-only)
- WebContainer limitations for non-web projects
- Community-maintained (no corporate backing)

**Community:** 19.2K stars, 10,383 forks. Very active community fork. bolt.new (proprietary) has 16.3K stars separately.

---

## 5. Archived / Inactive

### 5.1 Mentat

| Field | Value |
|-------|-------|
| **Repo** | [github.com/AbanteAI/archive-old-cli-mentat](https://github.com/AbanteAI/archive-old-cli-mentat) |
| **Stars** | 2,559 |
| **License** | Apache-2.0 |
| **Language** | Python |
| **Status** | **ARCHIVED** |

**What it was:** A CLI-based AI coding assistant that coordinated edits across multiple files and locations. Distinguished itself from Copilot by handling multi-file edits and from ChatGPT by automatically having project context.

**Current status:** The original CLI has been archived. AbanteAI pivoted Mentat into an AI-powered GitHub bot (mentat.ai) that writes and reviews code as a SaaS product.

---

### 5.2 CodeGeeX

| Field | Value |
|-------|-------|
| **Repo** | [github.com/THUDM/CodeGeeX4](https://github.com/THUDM/CodeGeeX4) |
| **Stars** | 2,455 (CodeGeeX4) / 7,593 (CodeGeeX2) |
| **License** | Apache-2.0 |
| **Language** | Python |
| **Created by** | Tsinghua University |
| **Status** | Low activity (model weights, not tool) |

**What it is:** A multilingual code generation model (13B parameters) developed by Tsinghua University. Provides code completion, translation, and generation across 20+ programming languages. Available via IDE plugins and self-hosted deployment.

**Key specs:** 128K token context window, 82.3% on HumanEval (CodeGeeX4-ALL-9B). This is more of a model release than a tool -- the IDE plugins wrap the model.

---

## Ecosystem Analysis

### Growth Trajectory (2024 --> 2026)

The open-source AI coding tool ecosystem has exploded:

| Metric | 2024 | 2026 |
|--------|------|------|
| Total stars (top 10 tools) | ~50K | ~550K+ |
| Tools with MCP support | 0 | 8+ |
| Tools with browser automation | 1 | 5+ |
| CLI tools viable for daily use | 2 | 6+ |
| Tools with subagent/parallel exec | 0 | 4+ |

### Key Trends

1. **MCP is becoming table stakes.** Tools without MCP support (Aider, SWE-agent) are feeling the pressure. MCP enables plugin ecosystems that dramatically extend capabilities.

2. **CLI resurgence.** After years of IDE-heavy development, the terminal is back as the center of gravity for AI-assisted coding. OpenCode (130K stars), Gemini CLI (99K), and Aider (42K) prove this.

3. **Mode/Agent systems.** The shift from "one AI assistant" to "a team of specialized agents" is happening across Roo Code, Kilo Code, and OpenHands. Expect every tool to ship modes by end of 2026.

4. **Persistent sessions.** OpenCode's persistent background server is a game-changer. Sessions that survive disconnects are essential for long-running tasks.

5. **CI/CD integration.** Continue.dev's CI/CD runner points to the future -- AI checks enforced in pipelines alongside linting and tests.

6. **Self-hosting demand.** Tabby's 33K stars show strong demand for on-premises solutions, especially in enterprise and regulated industries.

7. **Convergence of interfaces.** Tools are no longer just CLI or just IDE extension. OpenCode, Kilo Code, and Goose all ship CLI + IDE + desktop apps from a single engine.

### The Fork Tree

Understanding the lineage helps explain feature overlap:

```
VS Code (Microsoft)
  |
  +-- Cursor (proprietary)
  +-- Void (fork, paused)
  +-- Pear AI (fork, low activity)

Cline (Claude Dev)
  |
  +-- Roo Code (fork, active)
  +-- Kilo Code (fork lineage, now independent)

bolt.new (StackBlitz)
  |
  +-- bolt.diy (community fork)

OpenDevin
  |
  +-- OpenHands (renamed, thriving)
```

---

## Recommendations by Use Case

### "I want a CLI tool for daily coding"
1. **Aider** -- Most mature, best git integration, widest model support
2. **OpenCode** -- Most features, persistent sessions, largest community
3. **Goose** -- Best MCP integration, Rust-fast, enterprise-backed

### "I want an AI agent in my VS Code"
1. **Cline** -- Most installs, best browser automation, richest MCP ecosystem
2. **Roo Code** -- Best mode system for task separation
3. **Continue.dev** -- Best for teams (shared rules, CI/CD integration)
4. **Kilo Code** -- Best multi-platform (VS Code + JetBrains + CLI)

### "I want to self-host everything on-prem"
1. **Tabby** -- Purpose-built for self-hosting, runs on consumer GPUs
2. **OpenCode + Ollama** -- Full agent with local models
3. **Continue.dev + Ollama** -- IDE assistant with local models

### "I want autonomous agents that solve GitHub issues"
1. **OpenHands** -- Most comprehensive agent platform
2. **SWE-agent** -- Best benchmarked, academic rigor
3. **Sweep AI** -- Original issue-to-PR workflow (now JetBrains-focused)

### "I want to generate full web apps from prompts"
1. **bolt.diy** -- Best multi-provider support, in-browser execution

### "I want the biggest community and ecosystem"
1. **OpenCode** (130K stars)
2. **Gemini CLI** (99K stars)
3. **OpenHands** (70K stars)
4. **Cline** (59K stars)

---

*This document covers the open-source AI coding tool landscape as of March 25, 2026. The ecosystem is evolving rapidly -- star counts and feature sets may change significantly within weeks. All star counts and commit dates were verified via the GitHub API at the time of writing.*
