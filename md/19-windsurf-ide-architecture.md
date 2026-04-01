# Windsurf IDE Architecture

> Comprehensive architecture document covering Windsurf's history, features, context engine, model support, acquisition saga, and current state under Cognition AI ownership.

**Last Updated:** March 25, 2026

---

## Table of Contents

1. [Overview](#1-overview)
2. [Architecture](#2-architecture)
3. [Core Features](#3-core-features)
4. [Context Engine](#4-context-engine)
5. [Model Support](#5-model-support)
6. [Rules and Instructions System](#6-rules-and-instructions-system)
7. [MCP Support](#7-mcp-support)
8. [Terminal Integration](#8-terminal-integration)
9. [Multi-File Editing](#9-multi-file-editing)
10. [Unique Features](#10-unique-features)
11. [Extensions](#11-extensions)
12. [Pricing](#12-pricing)
13. [Strengths](#13-strengths)
14. [Limitations](#14-limitations)
15. [The Acquisition Saga](#15-the-acquisition-saga)
16. [Version History](#16-version-history)

---

## 1. Overview

### What Is Windsurf?

Windsurf is an AI-native code editor that deeply integrates agentic AI into every part of the coding workflow. It is a standalone desktop application built on top of VS Code's architecture, with its own AI infrastructure and a flagship agent called **Cascade**. It bills itself as "the first agentic IDE" -- one where the boundary between developer typing and AI typing is intentionally blurred.

### History

**2021 -- Exafunction Founded.** Varun Mohan (CEO) and Douglas Chen (co-founder) started Exafunction in June 2021. Both were MIT classmates who had reconnected. Mohan came from Nuro (autonomous vehicle deep learning infrastructure); Chen from Meta (Oculus Quest VR tools). The original mission was optimizing GPU utilization at scale.

**2022 -- Pivot to Codeium.** The team pivoted from GPU management to AI-powered developer tools, rebranding as Codeium. The first beta product launched in October 2022 as an IDE extension offering AI autocomplete, targeting enterprise development teams working with large, complex codebases.

**2023-2024 -- Rapid Growth.** Codeium achieved significant enterprise traction with hundreds of enterprise customers. The product expanded from a simple autocomplete extension to a full coding assistant with chat, search, and context awareness. Codeium raised $150M+ in venture funding from Kleiner Perkins, Greenoaks, and others.

**November 2024 -- Windsurf IDE Launches.** Codeium released the Windsurf Editor, its own standalone IDE (a VS Code fork), introducing Cascade as the core AI agent. The company rebranded from Codeium to Windsurf.

**May 2025 -- OpenAI $3B Acquisition Agreed.** OpenAI reached a definitive agreement to acquire Windsurf for $3 billion, its largest acquisition ever.

**June 2025 -- Anthropic Conflict.** Anthropic revoked Windsurf's direct API access to Claude models with less than a week's notice, citing the pending OpenAI acquisition.

**July 2025 -- Deal Collapse and Three-Way Split.** The OpenAI deal collapsed (see Section 15). Google executed a $2.4B licensing/talent deal. Cognition AI acquired Windsurf's remaining assets, IP, product, brand, and ~210 employees within 72 hours.

**2025-2026 -- Under Cognition.** Windsurf continues operating under Cognition's ownership, integrating Devin autonomous agent capabilities. SWE-1.5 model launched. Claude access restored. As of early 2026, Windsurf ranks among the top AI dev tools with hundreds of thousands of daily active users and $82M ARR at time of acquisition.

### Current State (March 2026)

Windsurf is owned by **Cognition AI** (makers of Devin). The product continues active development with Wave 14 as the latest major release. The editor supports multiple frontier models (GPT-5.x, Claude Sonnet 4.6, Gemini 3.x) alongside Cognition's proprietary SWE-1.5 model. The integration of Devin's autonomous engineering capabilities into the IDE is underway.

---

## 2. Architecture

### VS Code Fork Foundation

Like Cursor, Windsurf is built on a fork of VS Code (the open-source VS Code base). This gives it:

- Familiar UI, keybindings, and settings model
- Language server protocol (LSP) support for all major languages
- Integrated terminal, Git, and debugging
- Theme and partial extension compatibility

### How Windsurf Differs from Cursor Architecturally

| Aspect | Windsurf | Cursor |
|--------|----------|--------|
| **AI Philosophy** | "Agentic" -- AI participates proactively | "Augmented" -- AI assists on demand |
| **Core Agent** | Cascade (dual-agent: planner + executor) | Composer (single-agent loop) |
| **Context Model** | M-Query RAG with 768-dim embeddings | Codebase indexing + @ mentions |
| **Tab Completion** | Supercomplete (diffs, jumps, imports) | Tab (multi-line, cursor prediction) |
| **Memory** | Auto-generated + user-defined Memories | No persistent memory system |
| **Proprietary Models** | SWE-1 family (SWE-1, SWE-1.5) | Cursor-small (lightweight) |
| **Workflows** | Markdown-defined multi-step workflows | No equivalent |
| **Ownership** | Cognition AI (Devin) | Independent ($9B valuation) |

### System Architecture Layers

```
+--------------------------------------------------+
|              Windsurf Editor (VS Code Fork)       |
|  +--------------------------------------------+  |
|  |  UI Layer: Editor, Terminal, Sidebar, Diff  |  |
|  +--------------------------------------------+  |
|  |  Cascade Agent Layer                        |  |
|  |  +--------+  +----------+  +------------+  |  |
|  |  | Planner|  | Executor |  | Tool Caller|  |  |
|  |  +--------+  +----------+  +------------+  |  |
|  +--------------------------------------------+  |
|  |  Context Engine                             |  |
|  |  +----------+  +---------+  +----------+   |  |
|  |  | Indexer   |  | M-Query |  | Memories |   |  |
|  |  |(768-dim)  |  | (RAG)   |  | (Local)  |   |  |
|  |  +----------+  +---------+  +----------+   |  |
|  +--------------------------------------------+  |
|  |  Model Router                               |  |
|  |  GPT-5.x | Claude 4.x | Gemini 3.x | SWE-1|  |
|  +--------------------------------------------+  |
|  |  MCP Layer  |  Rules Engine  |  Workflows   |  |
|  +--------------------------------------------+  |
+--------------------------------------------------+
```

---

## 3. Core Features

### 3.1 Cascade -- The AI Agent

Cascade is Windsurf's flagship agentic AI assistant. It is not a chatbot bolted onto an IDE -- it is an integrated agent that reads your codebase, plans multi-step operations, executes file edits, runs terminal commands, and iterates on its own output.

#### Dual-Agent Architecture

Cascade employs a two-agent system:

1. **Planning Agent** -- A specialized agent that continuously refines the long-term plan in the background. It maintains a structured todo list, tracks progress, and adjusts strategy as the task evolves.
2. **Execution Agent** -- The selected model (e.g., Claude Sonnet 4.6, GPT-5.2-Codex) focuses on taking short-term actions based on the planner's roadmap.

This separation means Cascade handles multi-step tasks more coherently than single-model approaches. It rarely loses the thread of what it was doing, even across 10-15 sequential operations.

#### Cascade Modes

| Mode | Description | Key Use |
|------|-------------|---------|
| **Code** | Creates and modifies files, runs commands, iterates on output | Building features, refactoring, debugging |
| **Chat** | Optimized for questions; proposes code you can accept/insert | Learning, exploration, code review |
| **Plan** | Creates detailed implementation plans before code generation | Architecture design, complex features |

#### Key Capabilities

- **Tool Calling**: Cascade invokes tools (file read/write, terminal commands, web search, MCP servers) as part of its workflow
- **Checkpoints**: Named snapshots of project state within a conversation, with one-click revert
- **Real-Time Awareness**: Tracks edits, terminal commands, clipboard contents, conversation history, and file navigation to infer intent
- **Linter Integration**: Reads linter output to self-correct generated code
- **Voice Input**: Speak instructions to Cascade (added in Wave 11)
- **Turbo Mode**: Auto-executes terminal commands without per-command approval

#### Reasoning Effort Levels

Cascade offers four reasoning effort tiers: **Low**, **Medium**, **High**, and **xHigh**. Most tasks run well on Medium. xHigh is reserved for complex architectural reasoning.

### 3.2 Flows

"Flows" is the conceptual model for Cascade's multi-step reasoning chains. When given a complex task, Cascade:

1. Breaks it into discrete steps
2. Shows the plan before executing
3. Executes each step sequentially
4. Maintains context across all steps
5. Allows user intervention at any point

Flows are distinct from Workflows (see below) -- Flows describe Cascade's internal reasoning process, while Workflows are user-defined automation scripts.

### 3.3 Windsurf Tab (Autocomplete + Supercomplete)

Windsurf Tab is a unified completion experience that combines four capabilities:

- **Autocomplete**: Traditional inline code completion at cursor position
- **Supercomplete**: The more powerful mode that suggests both deletions and additions as small diff windows around your cursor. If you start renaming a variable, Supercomplete may proactively suggest renaming it across the entire file
- **Tab to Jump**: Anticipates your next cursor position and shows a jump label; pressing Tab navigates there
- **Tab to Import**: Auto-suggests import statements when you reference unimported symbols

Windsurf Tab is powered by a custom in-house model trained from scratch, optimized for speed and flow awareness. Context sources include: open files, recent code changes, terminal activity, Cascade chat history, prior editor actions, and clipboard contents (opt-in).

### 3.4 Chat (Sidebar)

The sidebar chat is Cascade in Chat mode. It can:

- Answer questions about your codebase using indexed context
- Explain code, suggest approaches, review diffs
- Propose code that can be accepted and inserted inline
- Reference past conversations using @mentions
- Search the web for documentation and solutions

### 3.5 Command (Inline Editing)

Invoked via `Cmd+I` (Mac) or `Ctrl+I` (Windows/Linux):

- **In editor**: Generates or edits code inline with natural language prompts
- **With selection**: Edits the highlighted code region
- **Without selection**: Generates code at cursor position
- **In terminal**: Generates CLI commands from natural language descriptions
- **No premium credits required** for Command usage
- Supports accept/reject/follow-up actions via code lens or keyboard shortcuts

### 3.6 Workflows

Workflows are reusable, structured automation scripts stored as markdown files in `.windsurf/workflows/`:

```markdown
# deploy-service
## Description
Deploy a service to production with validation.

## Steps
1. Run all tests and verify they pass
2. Build the Docker image with production configuration
3. Push to container registry
4. Deploy to Cloud Run
5. Run smoke tests against the deployed URL
6. Report deployment status
```

Key characteristics:
- Invoked via slash commands: `/deploy-service`
- Each step has specific instructions for Cascade
- Steps execute sequentially
- Can be shared across teams via version control
- Support for inputs, expectations, and output format

Example workflow lifecycle:
- `/0-task` -- Initialize and set up tracking
- `/1-discovery` -- Analyze current code state
- `/2-design` -- Propose design options
- `/3-implement` -- Incremental implementation
- `/4-clean` -- Refactoring and cleanup

---

## 4. Context Engine

### How Windsurf Understands Your Code

Windsurf's context engine is a multi-layered system that builds deep understanding of your codebase, actions, and intent.

### Codebase Indexing

When you open a project, Windsurf immediately begins indexing the **entire local codebase** -- not just open files:

- Each file and function is converted to **768-dimensional vector embeddings** that capture semantic meaning
- Indexing runs in the background and updates incrementally as files change
- For Teams/Enterprise users, remote repositories can also be indexed

### M-Query Retrieval

Windsurf uses a proprietary retrieval method called **M-Query** that improves precision over basic cosine similarity:

- LLM-enhanced retrieval-augmented generation (RAG) on your codebase
- Reduces hallucination rate compared to naive RAG approaches
- Produces higher quality suggestions by retrieving more relevant code snippets

### Context Assembly Pipeline

When you interact with Cascade, the system runs through this assembly pipeline:

```
1. Load Rules (global + workspace + AGENTS.md)
2. Retrieve relevant Memories from previous sessions
3. Read open files and recent file activity
4. Run M-Query codebase retrieval for relevant snippets
5. Read recent actions (edits, terminal commands, clipboard)
6. Assemble final prompt with all sources merged and weighted
```

### Real-Time Action Tracking

Cascade monitors:
- File edits and which files you view
- Terminal commands and their output
- Clipboard contents (opt-in)
- Conversation history
- Cursor position and navigation patterns

This allows Cascade to infer intent without requiring repeated context. Typing "continue" picks up exactly where the last interaction left off.

---

## 5. Model Support

### Frontier Models (as of March 2026)

| Provider | Models Available |
|----------|----------------|
| **OpenAI** | GPT-5.4, GPT-5.2-Codex (4 reasoning tiers), GPT-5.1-Codex Max |
| **Anthropic** | Claude Opus 4.5, Claude Sonnet 4.6, Claude Sonnet 3.7 |
| **Google** | Gemini 3.1 Pro, Gemini 3 Flash, Gemini 3 Pro |
| **Cognition** | SWE-1.5, SWE-1, SWE-1-lite, SWE-1-mini |

### SWE Model Family (Proprietary)

Windsurf/Cognition's in-house models built specifically for software engineering tasks:

**SWE-1** (May 2025):
- Three variants: SWE-1 (full), SWE-1-lite, SWE-1-mini
- Focused on tool-call reasoning
- Performance comparable to Claude 3.5 Sonnet, more cost-efficient
- Trained on Windsurf's proprietary data from millions of coding sessions

**SWE-1.5** (December 2025):
- Frontier-size model with hundreds of billions of parameters
- Achieves **near-SOTA on SWE-Bench Pro** (Scale AI's benchmark)
- Speed: up to **950 tokens/second** -- 6x faster than Haiku 4.5, 13x faster than Sonnet 4.5
- Made free for all users for 3 months at launch
- Excels specifically at agentic coding workflows

### Benchmarks Used

Windsurf evaluates models with two proprietary benchmarks:
1. **Conversational SWE Task Benchmark**: Tests addressing user queries mid-session with a half-finished task
2. **End-to-End SWE Task Benchmark**: Tests solving problems from scratch to completion

### Anthropic Access Saga

- **June 2025**: Anthropic revoked Windsurf's direct API access to Claude models (Claude 3.5 Sonnet, 3.7 Sonnet, and Claude 4 series) due to the pending OpenAI acquisition
- **June-July 2025**: Users could only access Claude via BYOK (Bring Your Own Key)
- **Post-Cognition acquisition**: Access restored. Cognition CEO Jeff Wang stated: "We're friends with Anthropic again"
- **Current**: Claude Sonnet 4.6 and Opus 4.5 available with first-party support

---

## 6. Rules and Instructions System

Windsurf offers three mechanisms for configuring AI behavior:

### 6.1 Windsurf Rules

Rules are persistent prompts automatically included in Cascade's context. They guide coding style, conventions, and behavior.

**File Locations:**
- **Global rules**: `global_rules.md` -- apply across all workspaces
- **Workspace rules**: `.windsurf/rules/` directory -- project-specific
- **Legacy**: `.windsurfrules` file in project root

**Format:**
```markdown
---
trigger: always
---

# Project Rules

- Use TypeScript strict mode
- All API endpoints must have error handling
- Use Zod for input validation
- Follow the repository's existing naming conventions
- Run `pnpm test` after making changes
```

**Activation Modes:**
- `always` -- Always included in context
- `glob` -- Activated when Cascade reads/edits files matching a pattern
- `description` -- Activated based on natural language description match

**Limits:**
- Individual rule files: **6,000 characters** max (truncated beyond)
- Total combined rules (global + workspace): **12,000 characters** max
- If limit exceeded: global rules take priority, then workspace rules, excess truncated

### 6.2 AGENTS.md

An industry-standard file (supported by 25+ tools including Codex, Copilot, Cursor, Windsurf) for project configuration:

- **Root `AGENTS.md`**: Treated as always-on rule, included in every Cascade prompt
- **Subdirectory `AGENTS.md`**: Auto-scoped to that directory (`<dir>/**`), applied only when Cascade operates on files in that subtree
- Hierarchical: `frontend/AGENTS.md`, `backend/AGENTS.md`, `docs/AGENTS.md` each apply to their domain

### 6.3 Memories

Persistent context across conversations (see Section 4):
- **Auto-generated**: Cascade stores useful context it discovers (architectural patterns, naming conventions, dependency relationships)
- **User-created**: Manual memory entries for project-specific knowledge
- **Storage**: `~/.codeium/windsurf/memories/` (local, not committed to repo)
- **Scope**: Per-workspace; not shared across workspaces
- **Cost**: Creating/using auto-generated memories does NOT consume credits

### Comparison with Other Tools

| Feature | Windsurf | Cursor | Claude Code |
|---------|----------|--------|-------------|
| Project rules file | `.windsurf/rules/` | `.cursorrules` / `.cursor/rules/` | `CLAUDE.md` |
| Global rules | `global_rules.md` | Global cursor rules | `~/.claude/CLAUDE.md` |
| AGENTS.md support | Yes | Yes | Yes |
| Auto-memory | Yes (Memories) | No | Yes (auto-memory) |
| Workflows | Yes (.windsurf/workflows/) | No | Yes (Skills/commands) |
| Character limits | 6K per file, 12K total | Similar limits | No hard limit |

---

## 7. MCP Support

### Overview

Cascade natively integrates with MCP (Model Context Protocol), the Anthropic-created standard for LLM-to-tool communication. Windsurf was among the first AI IDEs to adopt MCP (added in Wave 3, early 2025).

### Technical Details

- **Transport types supported**: stdio, Streamable HTTP, SSE
- **OAuth support**: Available for all transport types
- **Tool limit**: Maximum **100 total tools** accessible to Cascade at any time
- **Per-tool toggle**: Individual tools can be enabled/disabled from settings

### Configuration

MCP servers can be added via:
1. **MCP Marketplace**: Accessible from the Cascade panel (top-right icon)
2. **Settings**: Windsurf Settings > Cascade > MCP Servers
3. **Configuration files**: Manual JSON configuration

### Practical Use

MCP enables Cascade to interact with external services: databases, APIs, deployment platforms, documentation systems, and custom internal tools. This extends Cascade's capabilities beyond file editing and terminal commands.

---

## 8. Terminal Integration

### AI-Powered Terminal

Windsurf's terminal integration goes beyond a standard embedded terminal:

**Cascade Command Execution:**
- Cascade can run terminal commands directly (installs, builds, tests, servers)
- Commands appear in the conversation with their output
- Turbo Mode: auto-execute without per-command approval

**Dedicated Agent Shell:**
- Windsurf provides a dedicated zsh shell specifically configured for reliability
- Separate from the user's default shell to avoid configuration conflicts
- Ensures consistent behavior across different development environments

**Natural Language CLI:**
- `Cmd+I` / `Ctrl+I` in terminal opens inline chat
- Describe what you want in natural language; Windsurf generates the proper CLI syntax
- Example: "find all TypeScript files modified in the last week" generates the appropriate `find` command

**Auto-Execution Control:**
- Four distinct auto-execution levels
- **Allow list**: Commands that auto-execute without approval
- **Deny list**: Commands that always require confirmation
- Configurable per-workspace

**Context Flow:**
- Terminal output feeds back into Cascade's context
- If a command fails, Cascade can read the error and suggest fixes
- Tab completion is aware of recent terminal activity

---

## 9. Multi-File Editing

### How Cascade Handles Cross-File Changes

Cascade's multi-file editing is central to the "agentic IDE" value proposition:

1. **Full Codebase Understanding**: Windsurf indexes the entire project. When you ask Cascade to add authentication to an Express app, it already knows the route structure, middleware stack, and database models.

2. **Planning Phase**: The planning agent creates a structured plan for cross-file changes. For a feature like "add user authentication," this might include: create auth middleware, update route files, add user model, update environment config, write tests.

3. **Sequential Execution**: Changes are applied file by file, with each change appearing as an **inline diff** you can review.

4. **Review Options**: Accept individual changes, modify them, ask Cascade to take a different approach, or revert to a checkpoint.

5. **Self-Verification**: Cascade can run tests and read linter output after making changes, iterating if something breaks.

6. **Rename Propagation**: Operations like rename-and-update-all-imports that would take manual find-and-replace are handled coherently across the entire codebase.

### Parallel Multi-Agent Sessions (Wave 13+)

- Run multiple Cascade agents simultaneously
- Each agent operates in its own **Git worktree** (separate branch, separate directory, shared history)
- Side-by-side Cascade panes for comparing approaches
- Enables parallelizing independent tasks on the same repository

---

## 10. Unique Features

### 10.1 Arena Mode (Wave 14)

Blind A/B testing of AI models directly in the IDE:
- Two models generate responses simultaneously to the same request
- Outputs labeled "Side A" and "Side B" with hidden identities
- Developer picks the preferred output; that model's changes are applied
- **Battle Groups**: Choose specific models or let Windsurf randomly select (e.g., "fast models" vs. "smart models")
- Personal and global leaderboards track which models perform best
- Helps developers discover which models work best for their specific codebase and tasks

### 10.2 Megaplan / Plan Mode

An interactive planning mode (reimagined in Wave 14):
- Switches Cascade into planning mode instead of coding mode
- Cascade asks clarifying questions before producing implementation plans
- Maintains a living document of the plan that evolves with discussion
- Plans can then be handed off to Code mode for execution
- Invoked via chat type toggle or by typing "megaplan"

### 10.3 Memories System

The most distinctive feature vs. other AI IDEs:
- Cascade autonomously generates and stores "memories" about your codebase between conversations
- Architectural patterns, naming conventions, configuration quirks, dependency relationships
- No credit cost for memory creation or retrieval
- Over time, Cascade becomes more attuned to your specific project

### 10.4 DeepWiki Integration (Wave 12)

AI-generated documentation accessible on hover:
- Rich explanations of any function, class, or variable
- Available via hover or keyboard shortcut
- Powered by Devin's codebase understanding capabilities

### 10.5 Proactive Suggestions

Supercomplete anticipates your next move:
- If you rename a variable, it may suggest renaming across the file
- If you write a function signature, it predicts the implementation
- Feels less like autocomplete and more like a proactive pair programmer

### 10.6 SWE-grep (Cognition)

A specialized search model from Cognition that enhances Cascade's ability to find relevant code across large codebases, more precise than standard text search.

---

## 11. Extensions

### VS Code Compatibility

Windsurf inherits VS Code's extension architecture, but with important caveats:

**Microsoft Marketplace Restriction:**
Microsoft prohibits non-Microsoft products from accessing the VS Code Marketplace directly. This means Windsurf cannot pull extensions from `marketplace.visualstudio.com` out of the box.

**Workarounds:**
- Extensions published to **Open VSX** (the open-source alternative registry) are available natively
- Manual `.vsix` installation works for most VS Code extensions
- Some configuration changes can enable broader marketplace access
- Many popular extensions are available on Open VSX

**Windsurf Plugin for Other Editors:**
Windsurf/Codeium also ships extensions for:
- **VS Code** (as a plugin, not the standalone editor)
- **JetBrains** (IntelliJ, WebStorm, PyCharm, Rider, GoLand, CLion)
- **Visual Studio**
- **Eclipse**
- **Vim/Neovim**

**Limitation:**
The extension ecosystem is smaller than Cursor's community, and the Microsoft Marketplace restriction remains one of the biggest friction points for VS Code fork users.

---

## 12. Pricing

### Current Plans (March 2026)

| Plan | Price | Key Inclusions |
|------|-------|----------------|
| **Free** | $0 | ~25 credits/month, unlimited basic completions, ~5 Cascade sessions/day |
| **Pro** | $15-20/mo | 500 credits, all frontier models, Supercomplete |
| **Max** | ~$200/mo | Significantly larger daily/weekly quotas, comparable to Cursor Ultra |
| **Teams** | $30-40/user/mo | 500 credits/user, admin controls, team rules sharing |
| **Enterprise** | $60/user/mo | 2x Teams quotas, ZDR (Zero Data Retention), RBAC, SSO + SCIM, priority support |

**Note:** Pricing is in transition as of March 2026. Official docs still show older pricing ($15 Pro, $30 Teams) while newer blog posts indicate quota-based pricing ($20 Pro, $40 Teams, $200 Max). The shift is from credit-based to quota-based billing.

### Pricing Context vs. Competitors

| Tool | Entry Price | Pro/Standard | Heavy Usage |
|------|-------------|-------------|-------------|
| Windsurf | Free | $15-20/mo | $200/mo (Max) |
| Cursor | Free (limited) | $20/mo | $200/mo (Ultra) |
| Claude Code | Free (limited) | $20/mo (via Claude Pro) | $200/mo (Max 20x) |
| GitHub Copilot | Free (limited) | $10/mo | $39/mo (Business) |

Windsurf's free tier is more generous than Cursor's or Claude Code's, making it attractive for budget-conscious developers and students.

---

## 13. Strengths

### Why Choose Windsurf

1. **Best Free Tier** -- More generous free credits and Cascade sessions than competitors. SWE-1.5 was offered free for 3 months.

2. **Cascade's Dual-Agent Architecture** -- The planner/executor split maintains coherence on long tasks better than single-model approaches.

3. **Memories System** -- Persistent, auto-generated context across sessions is genuinely unique. No other AI IDE learns and remembers your project this way.

4. **Proactive AI** -- Supercomplete's anticipatory suggestions feel collaborative rather than reactive.

5. **Workflows** -- Reusable, version-controlled automation scripts for repetitive multi-step tasks. No equivalent in Cursor.

6. **Arena Mode** -- Unique ability to blind-test models against each other in your actual workflow.

7. **Devin Integration** -- Cognition ownership brings autonomous agent capabilities (Devin) directly into an IDE, a combination no competitor offers.

8. **SWE-1.5 Speed** -- 950 tokens/second with near-SOTA coding performance is a compelling speed/quality tradeoff.

9. **Enterprise Features** -- Zero Data Retention, on-premises deployment, remote repository indexing, SSO/SCIM.

10. **Multi-Editor Support** -- Windsurf plugin works across VS Code, JetBrains, Visual Studio, Vim/Neovim -- not locked to one editor.

---

## 14. Limitations

### Where Windsurf Falls Short

1. **Context Window Size** -- Effective context around ~100K tokens. Significantly smaller than Claude Code's 1M token context window.

2. **Speed vs. Accuracy Tradeoff** -- Cascade sometimes makes assumptions without asking. Less thorough than Claude Code for complex architectural decisions.

3. **Extension Ecosystem** -- Microsoft Marketplace restrictions and smaller community mean fewer readily available extensions than VS Code or Cursor.

4. **Benchmark Performance** -- In some independent tests, Windsurf ranked behind Cursor and Claude Code in both backend and frontend coding scores.

5. **Ownership Uncertainty** -- Three ownership changes in 3 months (independent -> OpenAI deal -> Google talent grab -> Cognition acquisition) created instability. Key founders (Mohan, Chen) left for Google.

6. **Model Access Volatility** -- The Anthropic access revocation demonstrated that model availability can change rapidly. While resolved, it exposed a risk.

7. **Gemini Default Push** -- Windsurf has been promoting Gemini models as defaults, which some users find less capable than Claude for coding tasks.

8. **Rules Character Limit** -- 6K per file and 12K total for rules is restrictive for complex projects. Claude Code's CLAUDE.md has no hard limit.

9. **Not a Terminal-Native Tool** -- For developers who prefer CLI-first workflows, Windsurf is still a GUI IDE. Claude Code's terminal-native approach offers more flexibility for scripting, CI/CD integration, and headless operation.

10. **Smaller Community** -- Cursor has 1M+ users; Windsurf's user base, while growing rapidly, is smaller, meaning fewer community resources, shared rules, and third-party integrations.

---

## 15. The Acquisition Saga

The Windsurf acquisition story is one of the most dramatic in recent AI history, involving three tech giants competing over a single startup within 72 hours.

### Phase 1: OpenAI's $3B Bid (April-July 2025)

- **April 16, 2025**: Reports surface that OpenAI is in talks to acquire Windsurf for ~$3 billion
- **May 6, 2025**: Definitive agreement announced. OpenAI's largest acquisition ever
- **Exclusivity period**: OpenAI had exclusivity through July 11, 2025
- **The Microsoft Problem**: CEO Varun Mohan didn't want Microsoft involved in the deal. When OpenAI asked if they could keep Windsurf's technology private from Microsoft, Microsoft refused. This was the core deal-breaker.

### Phase 2: Anthropic Cuts Access (June 2025)

- **June 3, 2025**: Anthropic revokes Windsurf's direct API access to all Claude models with less than a week's notice
- Rationale: Anthropic did not want to subsidize a competitor (OpenAI) through API access
- Impact: Windsurf users forced to use BYOK for Claude models
- Public fallout: Windsurf publicly complained, calling Anthropic's move anti-competitive

### Phase 3: Three-Way Split (July 11-14, 2025)

**Friday, July 11, 2025 -- OpenAI exclusivity expires:**
- Google swoops in with a $2.4 billion "reverse acquihire" and licensing deal
- Google hires CEO Varun Mohan, co-founder Douglas Chen, and ~40 senior R&D staff
- Google gets a non-exclusive license to selected Windsurf technology
- Windsurf continues as an independent entity (Google does not acquire the company)

**Friday evening, July 11 -- Cognition calls:**
- Cognition AI (makers of Devin) contacts Windsurf about acquiring remaining assets
- Negotiations begin after 5 PM on Friday

**Monday, July 14, 2025 -- Cognition acquisition announced:**
- Cognition signs a definitive agreement to acquire Windsurf within 72 hours
- Deal valued at approximately $250 million
- Includes: Windsurf's IP, product, trademark, brand, and ~210 remaining employees
- Does NOT include: The ~40 staff who went to Google, or the founders

### Current Ownership Structure

- **Cognition AI** owns Windsurf (product, brand, IP, business)
- **Google** employs the founders and key R&D staff; holds a non-exclusive technology license
- **OpenAI** received nothing from the deal
- **Anthropic** restored API access after the Cognition acquisition ("We're friends with Anthropic again")

### Impact on Product

- Windsurf continues active development under Cognition
- Devin capabilities being integrated into the IDE
- SWE-1.5 and SWE-grep models became available in Windsurf
- Enterprise customers (350+) retained
- ARR was $82M at time of acquisition, with enterprise ARR doubling quarter-over-quarter

---

## 16. Version History

### Wave Releases (Major Milestones)

| Wave | Date | Key Features |
|------|------|--------------|
| **Launch** | Nov 2024 | Windsurf Editor released. Cascade agent introduced. |
| **Wave 1** | Dec 2024 | Multimodal image input. AI-assisted website building from screenshots. |
| **Wave 2** | Jan 2025 | Web search. Automatic memory system. Enterprise support. Issue tagging. |
| **Wave 3** | Feb 2025 | MCP (Model Context Protocol) support. Drag-and-drop image input. Tab to Jump. |
| **Wave 4** | Mar 2025 | Interactive preview (click components to send context to Cascade). Claude 3.7 Sonnet. |
| **Wave 5** | Apr 2025 | Major Windsurf Tab overhaul -- latency, quality, reliability improvements. Supercomplete refined. |
| **SWE-1** | May 2025 | SWE-1 model family launched (SWE-1, SWE-1-lite, SWE-1-mini). |
| **Wave 6-10** | May-Oct 2025 | Incremental improvements, model updates, performance optimization. |
| **Wave 11** | Oct 2025 | Voice command support. Named checkpoints. Past conversation references. |
| **Wave 12** | Nov 2025 | Devin integration begins. DeepWiki (hover documentation). Cognition models integrated. |
| **Wave 13** | Dec 2025 | Parallel multi-agent sessions. Git worktrees. SWE-1.5 (free for 3 months). Dedicated agent terminal shell. |
| **Wave 14** | Jan 30, 2026 | Arena Mode (blind model comparison). Plan Mode / Megaplan reimagined. GPT-5.4 support. |

### Recent Model Additions (2026)

| Date | Model |
|------|-------|
| Mar 5, 2026 | GPT-5.4 |
| Feb 19, 2026 | Gemini 3.1 Pro |
| Feb 17, 2026 | Claude Sonnet 4.6 |
| Jan 12, 2026 | GPT-5.2-Codex, Agent Skills |
| Jan 9, 2026 | Plan Mode update with Skills support |
| Dec 27, 2025 | Gemini 3 Flash, SWE-1.5 |

---

## Summary

Windsurf occupies a unique position in the AI coding tool landscape in early 2026. It is the only major AI IDE owned by an autonomous agent company (Cognition/Devin), giving it a path toward tighter human-agent collaboration that neither Cursor nor Claude Code can easily replicate. Its Cascade dual-agent architecture, Memories system, Workflows, and Arena Mode are genuinely differentiated features.

The turbulent ownership history -- from independent startup to OpenAI target to Google talent acquisition to Cognition product -- has created both risks (leadership loss, model access volatility) and opportunities (Devin integration, SWE model family, renewed Anthropic partnership). With $82M ARR, 350+ enterprise customers, and a generous free tier driving adoption, Windsurf remains a serious contender in the rapidly evolving AI IDE market.

For developers choosing between tools:
- **Windsurf** excels at iterative, collaborative building with proactive AI, especially for teams wanting structured workflows and persistent memory
- **Cursor** excels at polished IDE augmentation with the largest user community
- **Claude Code** excels at complex architectural work requiring massive context, terminal-native workflows, and deep reasoning

---

## Sources

- [Windsurf Official Site](https://windsurf.com/)
- [Windsurf Documentation](https://docs.windsurf.com/)
- [Windsurf Changelog](https://windsurf.com/changelog)
- [Cascade Documentation](https://docs.windsurf.com/windsurf/cascade/cascade)
- [Context Awareness Overview](https://docs.windsurf.com/context-awareness/overview)
- [AI Models Documentation](https://docs.windsurf.com/windsurf/models)
- [Plans and Usage](https://docs.windsurf.com/windsurf/accounts/usage)
- [AGENTS.md Documentation](https://docs.windsurf.com/windsurf/cascade/agents-md)
- [Cascade MCP Integration](https://docs.windsurf.com/windsurf/cascade/mcp)
- [Terminal Documentation](https://docs.windsurf.com/windsurf/terminal)
- [Cascade Memories](https://docs.windsurf.com/windsurf/cascade/memories)
- [Workflows Documentation](https://docs.windsurf.com/windsurf/cascade/workflows)
- [Windsurf Tab Documentation](https://docs.windsurf.com/tab/overview)
- [Command Documentation](https://docs.windsurf.com/command/windsurf-overview)
- [OpenAI Acquires Windsurf for $3 Billion -- Bloomberg](https://www.bloomberg.com/news/articles/2025-05-06/openai-reaches-agreement-to-buy-startup-windsurf-for-3-billion)
- [OpenAI's $3B Windsurf Deal Collapses -- Fortune](https://fortune.com/2025/07/11/the-exclusivity-on-openais-3-billion-acquisition-for-coding-startup-windsfurf-has-expired/)
- [Windsurf CEO Goes to Google -- TechCrunch](https://techcrunch.com/2025/07/11/windsurfs-ceo-goes-to-google-openais-acquisition-falls-apart/)
- [Cognition Acquires Windsurf -- TechCrunch](https://techcrunch.com/2025/07/14/cognition-maker-of-the-ai-coding-agent-devin-acquires-windsurf/)
- [Cognition's Windsurf Blog Post](https://cognition.ai/blog/windsurf)
- [Google, Cognition Carve Up Windsurf -- DeepLearning.AI](https://www.deeplearning.ai/the-batch/google-cognition-carve-up-windsurf-after-openais-failed-3b-acquisition-bid/)
- [Windsurf Drama: 72-Hour Split](https://elephas.app/blog/windsurf-ai-3-billion-collapse-72-hours)
- [Anthropic Limits Windsurf Claude Access -- TechCrunch](https://techcrunch.com/2025/06/03/windsurf-says-anthropic-is-limiting-its-direct-access-to-claude-ai-models/)
- [Cognition + Windsurf: "Friends with Anthropic Again" -- VentureBeat](https://venturebeat.com/programming-development/remaining-windsurf-team-and-tech-acquired-by-cognition-makers-of-devin-were-friends-with-anthropic-again)
- [Windsurf SWE-1 Launch -- InfoQ](https://www.infoq.com/news/2025/05/windsurf-swe-models/)
- [SWE-1.5 Blog Post -- Cognition](https://cognition.ai/blog/swe-1-5)
- [Wave 14: Arena Mode -- Windsurf Blog](https://windsurf.com/blog/windsurf-wave-14)
- [Windsurf Business Breakdown -- Contrary Research](https://research.contrary.com/company/windsurf)
- [Building Windsurf -- Lenny's Newsletter](https://www.lennysnewsletter.com/p/the-untold-story-of-windsurf-varun-mohan)
- [Cursor vs Windsurf vs Claude Code 2026 -- DEV Community](https://dev.to/pockit_tools/cursor-vs-windsurf-vs-claude-code-in-2026-the-honest-comparison-after-using-all-three-3gof)
- [AI Coding Agents 2026 Comparison -- Lushbinary](https://lushbinary.com/blog/ai-coding-agents-comparison-cursor-windsurf-claude-copilot-kiro-2026/)
- [Windsurf Pricing 2026 -- Verdent Guides](https://www.verdent.ai/guides/windsurf-pricing-2026)
- [Windsurf Rules Guide -- Playbooks](https://playbooks.com/windsurf-rules)
