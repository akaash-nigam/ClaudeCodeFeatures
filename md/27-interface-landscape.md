# The LLM Interface Landscape: Beyond Chat and Terminal (November 2026)

*Last Updated: November 26, 2026*
*Companion to: `26-chat-apps-evolution.md` (the two-interface thesis)*

Doc 26 established that the major labs converged on two surfaces — the terminal coding agent and the general cowork app. This study maps **everything else**: the other interface paradigms that emerged over LLM products, plus deep-dives on two companies attacking the stack from outside the labs — **Factory AI** (the neutral harness layer) and **OpenCode/Anomaly** (the open-source substrate).

---

## Part 1: The Interface Taxonomy — 10 Paradigms

| # | Paradigm | Leaders (Nov 2026) | Status |
|---|----------|--------------------|--------|
| 1 | Agentic browsers | Comet, Dia, Claude in Chrome | Consolidating — extensions beating standalone |
| 2 | IDE-native agents | Cursor, Antigravity, Devin Desktop | Mature, commoditizing |
| 3 | **Async task boards / fleet managers** | GitHub Agent HQ, Codex app, Factory Missions | **Breakout category of 2026** |
| 4 | Messaging-channel agents | OpenClaw, Shortwave, Fyxer | Growing, scrappy |
| 5 | Voice / ambient / wearable | Meta Ray-Ban Display, Sierra, ElevenAgents | Glasses & phone agents up; AI gadgets dead |
| 6 | Canvas / document-centric | tldraw, Figma MCP, Claude Docs/Slides | Growing quietly via MCP |
| 7 | OS-level / desktop agents | Cowork→Claude, ChatGPT Work, Copilot, Siri AI (Gemini) | The new flagship surface |
| 8 | API / agent-to-agent | MCP (~97M downloads), A2A, AgentExchange | MCP won |
| 9 | Spreadsheet / table-native | Claude for Excel, Shortcut AI, Copilot in Excel | Real category, real revenue |
| 10 | **Generative UI** | GPT-6 "Intelligent UI" (Oct 2026) | **Genuinely new paradigm** |

### 1. Agentic Browsers — Consolidating Hard
The category's defining event: **ChatGPT Atlas died in 292 days** (killed Jul 9, 2026, off Aug 9) — folded into ChatGPT Work and the desktop app's built-in browser. **Arc sunsets Dec 22, 2026** as Atlassian ($610M acquisition) goes all-in on AI-first Dia. **Perplexity Comet** is the last major standalone agentic browser, free on all four platforms. Meanwhile the extension model is quietly winning: **Claude in Chrome** reports ~21M Chrome Web Store users, and its side panel has been a full Cowork session since August 2026. Opera Neon's twist: the browser itself acts as an **MCP server** — a tool *for* other agents.

### 2. IDE-Native Agents — Mature, Commoditizing
**Google Antigravity** (Nov 2025; 2.0 in Nov 2026) introduced the "agent manager" surface above the editor. **Cursor** remains the standard. The most interesting mutation: Windsurf became **Devin Desktop** (Jun 2026) under Cognition — an IDE that *hosts* Devin, Codex, Claude Code, OpenCode, and custom agents via ACP. Differentiation moved from autocomplete to agent-orchestration panes.

### 3. Async Task Boards / Agent Fleet Managers — The Breakout Category
The kanban-of-agents: assign a task, inspect the plan, review the PR. **GitHub Agent HQ** ("mission control," public preview Feb 2026) steers Claude, Codex, and Copilot agents in parallel on the same repo. OpenAI's **Codex app** (Feb 2026) was explicitly a "command center" for parallel agents with built-in worktree isolation. **Claude Code on the web**, **Google Jules** (plan → cloud VM → PR), **Devin**, and **Factory Missions** (Part 2) all fit. This is the fastest-growing paradigm of 2026 — the structural answer to the ~2-concurrent-session supervision ceiling documented in doc 26: delegation replaces supervision.

### 4. Messaging-Channel Agents
**OpenClaw** turned one year old in Nov 2026 (now ~395k GitHub stars under the independent OpenClaw Foundation after founder Peter Steinberger joined OpenAI): an agent you drive from WhatsApp/Telegram/Slack/Signal — though it carries 722 security advisories and a Kaspersky "unsafe for general use" label. Email-native agents matured into a real market: **Shortwave** (Gmail rebuilt AI-native), **Fyxer** (drafts every reply in your voice), **Cora**.

### 5. Voice / Ambient / Wearable — Gadgets Died, Glasses and Call Agents Survived
Humane: dead (HP acqui-shutdown). Rabbit: pivoted to software. OpenAI/io device: still unshipped. The survivors: **Meta Ray-Ban Display** (in-lens display + neural wristband) and B2B **phone-call agents** at real scale — Sierra (outcome-priced calls), ElevenLabs "ElevenAgents," Bland, PolyAI, Decagon.

### 6. Canvas / Document-Centric — Agent-Writable Surfaces
The twist isn't apps adding chatbots — it's surfaces becoming **agent-writable via MCP**. Figma opened its canvas (Mar 2026): Claude Code/Cursor/Codex write directly into live Figma files using the team's design system. tldraw made the infinite canvas an agent surface ("Make Real," tldraw computer). Claude gained Docs, Slides, Dashboards, and Motion as native outputs (Sep–Oct 2026).

### 7. OS-Level / Desktop Agents — The Platform War
The flagship new surface of 2026 (covered in depth in doc 26): Cowork→Claude, ChatGPT Work, and Microsoft's "Copilot as the new OS for work." The platform-shaking move: **Apple pays Google ~$1B/year for a custom Gemini as Siri's brain** (deal Jan 2026; Siri AI beta Sep 2026, 6 languages by Nov 13) — and Apple is reportedly making third-party agents native on macOS.

### 8. API / Agent-to-Agent — MCP Won
MCP: ~97M downloads, used by 16 of 22 surveyed AI companies, now the de facto interface layer. A2A hit v1.0 (Mar 2026) and moved under the AAIF foundation alongside MCP, but has only ~150 production deployments — and Anthropic, OpenAI, and xAI don't use it. The 2026 subplot is agentic-commerce protocol sprawl (ACP, AP2, UCP, x402).

### 9. Spreadsheet / Table-Native Agents
**Claude for Excel** (GA May 2026, alongside Word/PowerPoint; Claude Sheets beta Nov 10). **Shortcut AI** ($125/mo) beat Claude for Excel in Ankura's independent CFO benchmark by routing across Anthropic + OpenAI models — the harness-beats-model story in miniature.

### 10. Generative UI — The Genuinely New Thing
**GPT-6 "Intelligent UI"** (rolling out from Oct 7, 2026): the model composes bespoke interactive responses — charts, forms, calculators, adjustable trip maps — per query, via native streamable components. The interface is no longer fixed; the model renders it on demand. Claude's Easel charting mod (Nov 2026) is the same direction. An active research field ("just-in-time interfaces").

### Also tried — and died
**Proactive ambient feeds**: ChatGPT Pulse (nightly research → morning briefing cards) was retired after 9 months (Jun 17, 2026). The lesson quoted at its funeral: *"a feed without an action attached becomes homework."*

---

## Part 2: Factory AI — Betting on the Harness Layer

The strongest independent challenge to lab-owned coding agents. Founded 2023 (Matan Grinberg, Eno Reyes — met at a LangChain hackathon); the thesis is the **"agent-native SDLC"**: agents as first-class workers across the whole lifecycle, not an IDE autocomplete.

### The Trajectory
| Date | Milestone |
|------|-----------|
| Nov 2023 | $5M seed (Sequoia, Lux) — launch with six specialist "Droids" (Code, Review, Test, Knowledge, Project, Document) |
| Jun 2024 | $15M Series A (Sequoia), ~$120M valuation |
| May 2025 | **Droid CLI** — the direct Claude Code competitor; model-agnostic, 60+ models, BYOK |
| Sep 2025 | **#1 on Terminal-Bench** (58.75% with Opus 4.1); $50M Series B (NEA), ~$300M valuation |
| Apr 2026 | $150M Series C (Khosla) at **$1.5B**; EY deployment ("31x faster feature delivery" — vendor claim) |
| **Sep 15, 2026** | **$200M at $5B valuation** (Blackstone, Khosla, Sequoia) — 3.3x in five months, >$400M total raised |
| Oct–Nov 2026 | Three acquisitions in a month: **Mentlio** (model routing/context compression, ~30% cost cut), **Typedef** (enterprise data-context layer), **HumanLayer** (multiplayer agent IDE) |
| Oct 31, 2026 | **Droid 1.0** — model-independent harness with programmatic "Script Mode" tool calling (36 requests/3.1M tokens collapsed to 2 requests/~61K tokens in their example) |

### The Interface Story: "Bring Agents to Where Work Happens"
Factory runs the **same Droid** across: terminal (CLI), web app, IDE (VS Code/Cursor/Windsurf/JetBrains/Zed), **Slack and Teams**, **Linear and Jira** (assign a ticket to a Droid → get back a PR), GitHub/GitLab/CI, mobile, and persistent cloud **Environments**. **Missions** is their fleet layer: decompose a project into subtasks, assign each to a parallel Droid on remote compute, with human checkpoints — a more packaged orchestration story than either lab's.

### The Strategic Position
- **Neutrality is the wedge.** Enterprises hedge model risk and route per-task (cheap model for lint, frontier for architecture). Droid 1.0's sharpest claim: the *same* Opus 5.5 scores **65.2% on Terminal-Bench 4 inside Factory's harness — 7.6 points above Claude Code** — and beats Codex by 3.5 points on GPT-6.1. (Vendor-run benchmarks; treat accordingly.)
- **Co-opetition, not war.** Both labs let enterprise spend commitments flow to Factory via the OpenAI B2B marketplace (launch partner) and the Claude Marketplace — the labs treat Factory as a token-distribution channel even while competing at the app layer.
- **Enterprise wins**: Nvidia, Adobe, EY, Palo Alto Networks, Adyen, Blackstone, RBC, T-Mobile.
- **The risk**: ~$60M last-reported ARR against a $5B valuation (~80x); labs subsidize their own agents' tokens and ship day-one support for their newest models.

---

## Part 3: OpenCode — The Open-Source Substrate

The open-source harness war has a decisive winner: **OpenCode** (Anomaly, formerly SST) — **~228k GitHub stars, 1,000+ contributors, ~13–22M monthly developers claimed, ~$56–58M ARR run rate** — versus Charm's Crush at ~28k stars.

### Timeline
| Date | Milestone |
|------|-----------|
| Early 2025 | Kujtim Hoxha's original Go `opencode`; acrimonious split with SST over the name |
| Jun 19, 2025 | sst/opencode public launch — provider-agnostic from day one |
| Jul 30, 2025 | The Go lineage relaunches as **Charm Crush** |
| Oct–Dec 2025 | 1.0; 1M+ downloads; desktop app |
| Jan 2026 | Rebrand to **Anomaly** (anomalyco/opencode); 10M+ downloads; **OpenCode Black** subscriptions ($20–200/mo, batches that kept selling out) |
| **Sep 11, 2026** | **OpenCode 2.0** — one background service per machine (TUI, web, desktop all connect to it); background subagents; JS "Code Mode" batching MCP calls; **but LSP support silently dropped** (config accepted, inert) — ironic, since LSP was the original differentiator, and Claude Code added official LSP plugins the same quarter |
| Oct 31, 2026 | Zen renamed **OpenCode Models** — pay-as-you-go model catalog (4.6% + $0.31 top-up fee) |
| Nov 2026 | Mobile: Android on Google Play, iOS in TestFlight; v2.4.0 adds a built-in desktop browser; v2.4.2 current (Nov 26) |

*(A widely circulated "$420M Series B" claim is unverified and likely a conflation with a same-named healthcare company — Anomaly runs on ~10 employees and gateway revenue.)*

### The Business Model Mirror
OpenCode won by copying the labs' economics: the MIT-licensed agent is a **free loss-leader for a model gateway** (Go $10 / Go Plus $40 / Teams, plus pay-as-you-go Models) that takes margin on inference. It competes with Claude Code on **provider freedom at half the price point**, not on the harness.

### The Open-Source Ecosystem Answer to "Cowork"
Not a product — a **composition**: **OpenClaw** (the always-on general agent, 395k stars) delegates coding to OpenCode/Claude Code/Codex via its coding-agent skill (Telegram message → OpenCode in a git worktree → PR). Third parties build the cowork layer *on* OpenCode: **OpenWork** (YC S26, "open-source Claude Cowork, powered by opencode"), Eigent.

### The 2026 Graveyard and Survivors
Open source is also where projects go to die: **Google retired Gemini CLI** (104k stars) in June 2026 for the closed-source Antigravity CLI — the landmark open-to-closed reversal; Roo Code archived itself; Aider's last commit was May 2026; Goose went to the Linux Foundation. Survivors have either a revenue engine (OpenCode, Cline) or a foundation (Goose, OpenClaw).

---

## Part 4: Synthesis — The Full Stack as of November 2026

Combining this with doc 26's two-interface thesis, the industry structure looks like:

```
┌─────────────────────────────────────────────────────────────┐
│  GENERATIVE UI (model renders the interface per query)       │  ← newest layer
├─────────────────────────────────────────────────────────────┤
│  SUPERVISORY LAYER: fleet managers / task boards              │
│  (Agent HQ, Codex app, Factory Missions, Claude workflows)    │
├─────────────────────────────────────────────────────────────┤
│  TWO FLAGSHIP SURFACES (per lab):                             │
│    A. Terminal coding agent      B. General work agent        │
│    (Claude Code, Codex CLI)      (Claude, ChatGPT Work)       │
├─────────────────────────────────────────────────────────────┤
│  EMBEDDED AGENTS in existing surfaces:                        │
│  browser (extensions) · IDE · Excel/Sheets · email ·          │
│  Slack/ticketing (Factory) · OS (Siri-Gemini, Copilot)        │
├─────────────────────────────────────────────────────────────┤
│  NEUTRAL HARNESS LAYER: Factory ($5B) — same agent, every     │
│  surface, any model                                           │
├─────────────────────────────────────────────────────────────┤
│  OPEN-SOURCE SUBSTRATE: OpenCode (+OpenClaw, OpenWork         │
│  composing the open cowork stack)                             │
├─────────────────────────────────────────────────────────────┤
│  PROTOCOL LAYER: MCP (won, ~97M downloads) · A2A (niche) ·    │
│  commerce protocols (ACP/AP2/UCP/x402 — unresolved)           │
└─────────────────────────────────────────────────────────────┘
```

**Five conclusions:**

1. **Destination apps lost; embedded agents won.** Atlas, Humane, Rabbit, Pulse, standalone browsers — all dead. Agents embedded in Chrome, Excel, Gmail, GitHub, Slack, and the OS won. The exception that proves it: the two flagship surfaces (coding terminal + work app), which are destinations because the *work itself* lives there.
2. **The supervisory layer is the new UI frontier.** Fleet managers are how the industry routes around the ~2-session supervision ceiling — the interface shifts from conversation to delegation-and-review.
3. **The harness is the contested middle.** Factory's $5B bet and OpenCode's 228k stars both say the agent loop is worth owning independently of the model; the labs' counter is managed infrastructure (cloud sandboxes, fleet dashboards, enterprise identity) that's hard to clone.
4. **MCP is the quiet winner** — it turned every canvas, browser, and spreadsheet into an agent-writable surface, enabling the embedded-agent pattern that beat destination apps.
5. **Generative UI points at the endgame**: if the model renders the interface per query, the remaining human surface is a dispatch console plus whatever UI the task needs, generated just-in-time.

---

## Sources

**Interface survey:** [Atlas retirement (OpenAI help)](https://help.openai.com/en/articles/20001371) · [Arc sunset (TechCrunch)](https://techcrunch.com/2026/10/22/arc-browser-sunsets-december-22-as-the-browser-company-doubles-down-on-dia/) · [GitHub Agent HQ](https://github.blog/news-insights/company-news/welcome-home-agents/) · [GPT-6 Intelligent UI (TechRepublic)](https://www.techrepublic.com/article/news-gpt-6-intelligent-ui-charts-forms/) · [A2A status (Credal)](https://credal.ai/blog/what-happened-to-a2a-protocol) · [tldraw](https://tldraw.dev/use-cases/ai-enabled-canvas) · [Shortcut vs Claude for Excel benchmark](https://shortcut.ai/cases/shortcut-vs-claude-for-excel-ankura-office-of-the-cfo-benchmark) · [Pulse shutdown](https://prowlo.com/blog/chatgpt-pulse-shut-down)

**Factory AI:** [TechCrunch seed](https://techcrunch.com/2023/11/02/factory-wants-to-use-ai-to-automate-the-software-dev-lifecycle) · [Series B + Terminal-Bench](https://factory.ai/news/terminal-bench) · [$200M at $5B (Dealroom)](https://dealroom.co/news/151015-factory-raises-200m-at-5b-valuation-to-build-autonomous-coding-agents/) · [Droid 1.0 (MarkTechPost)](https://www.marktechpost.com/2026/10/31/factory-droid-1-0-frontier-harness/) · [Missions](https://factory.ai/product/missions) · [HumanLayer acquisition](https://runtimewire.com/article/factory-acquires-humanlayer-multiplayer-coding-agents)

**OpenCode:** [Press kit](https://opencode.ai/press) · [Founding story (TechFundingNews)](https://techfundingnews.com/opencode-the-background-story-on-the-most-popular-open-source-coding-agent-in-the-world/) · [YC Root Access interview](https://www.ycrootaccess.com/p/how-opencode-became-the-worlds-most) · [OpenCode 2.0 analysis](https://capitalandcompute.net/blog/opencode-2-0-what-changed/) · [Gemini CLI retirement (The Register)](https://www.theregister.com/ai-ml/2026/05/20/bye-bye-gemini-cli-google-nudges-devs-toward-antigravity/5243605) · [OpenWork (YC)](https://www.ycombinator.com/companies/openwork) · [OpenClaw (Wikipedia)](https://en.wikipedia.org/wiki/OpenClaw)

*Reliability notes: Factory's Droid 1.0 head-to-head numbers are vendor-run; OpenCode's "$420M raise" is unverified and likely false; Meta Charm and some rollout minutiae come from low-authority aggregators; user counts (Claude-in-Chrome 21M, OpenCode 22M) are platform/vendor figures.*
