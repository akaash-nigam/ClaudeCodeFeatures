# The Evolution of AI Chat Apps: ChatGPT, Claude & Perplexity (2022–2026)

*Last Updated: November 26, 2026*

How the major labs' consumer apps evolved from chatbots into agentic work platforms — and how the industry converged on a **two-interface pattern**: a terminal-based coding agent for developers, and a general "cowork"-style app with machine access for everyone else.

---

## The Core Thesis

By late 2026, the major AI labs have converged on two product surfaces:

| Surface | Audience | Examples | Interaction Model |
|---------|----------|----------|-------------------|
| **A. Terminal/IDE coding agent** | Developers | Claude Code, Codex CLI, Gemini CLI | Long-running agent sessions in terminal, git-native, worktrees, parallel subagents |
| **B. General agentic work app** | All white-collar workers | Claude (post-Cowork merge), ChatGPT Work, Perplexity Computer | Chat front-end + agent harness with file/machine/cloud-VM access, producing finished deliverables |

The surprising part: **surface B is built out of surface A.** The coding-agent harness (long-horizon planning, file manipulation, tool use, verification loops, skills) turned out to be the best general-purpose work engine. Anthropic explicitly positioned Cowork as *"Claude Code for the rest of your work"*; OpenAI's ChatGPT Work *"combines ChatGPT with Codex."*

And both labs have already collapsed the chat/agent split:
- **Anthropic merged Cowork into the Claude chat app on September 16, 2026** ("Cowork and chat are now one Claude")
- **OpenAI merged Chat + Work + Codex into one desktop super app on July 9, 2026**

---

## Part 1: ChatGPT — From Chatbot to Work Platform

### Phase 1: Chatbot (2022–2023)
| Date | Milestone |
|------|-----------|
| Nov 30, 2022 | Launch — free research preview on GPT-3.5; 100M users in ~2 months |
| Feb 2023 | ChatGPT Plus ($20/mo) — the consumer subscription model is born |
| Mar 2023 | Plugins — first third-party tool use (Expedia, Wolfram, browsing, code execution) |
| Jul 2023 | Code Interpreter (sandboxed Python); Custom Instructions |
| Sep–Nov 2023 | Voice + image input; DevDay introduces GPTs (custom chatbots, superseding plugins) |

### Phase 2: Personalized Assistant (2024)
| Date | Milestone |
|------|-----------|
| Jan 2024 | GPT Store + Team plan |
| Feb 2024 | Memory (persistent user facts; expanded to full chat history Apr 2025) |
| May 2024 | GPT-4o + macOS desktop app |
| Oct 3, 2024 | **Canvas** — side-by-side editable workspace; first break from linear chat |
| Oct 31, 2024 | ChatGPT search |
| Dec 2024 | Projects, Sora in ChatGPT, o1 reasoning models |

### Phase 3: Agent (2025)
| Date | Milestone |
|------|-----------|
| Jan 14, 2025 | **Tasks** — scheduled/recurring prompts; first asynchronous behavior |
| Jan 23, 2025 | **Operator** — computer-use agent in its own cloud browser (Pro preview) |
| Feb 2, 2025 | **Deep Research** — long-running cited research reports |
| Jul 17, 2025 | **ChatGPT agent mode** — Operator + Deep Research + terminal merged into the main app |
| Aug 7, 2025 | GPT-5 unified default with auto-routing |
| Sep 25, 2025 | **Pulse** — proactive overnight research briefings (acting unprompted) |
| Oct 6, 2025 | DevDay: **Apps in ChatGPT / Apps SDK** (MCP-based), AgentKit, Codex GA |
| Oct 21, 2025 | **Atlas** — Chromium AI browser for macOS |
| Nov 2025 | GPT-5.1; group chats roll out globally |

### Phase 4: Work Platform / Super App (2026)
| Date | Milestone |
|------|-----------|
| Jan–Feb 2026 | ChatGPT Go (~$8/mo) global; ads on Free/Go tiers |
| Feb 2, 2026 | **Codex app** (macOS; Windows Mar 4) — "command center" for multiple parallel coding agents with built-in worktree isolation |
| Mar 2026 | **Super-app consolidation announced**: ChatGPT + Codex + Atlas → one desktop app |
| Apr 22, 2026 | **Workspace agents** — Codex-powered continuously-running shared team agents; metered consumption pricing; custom GPTs deprecated (Aug 26) |
| May 21, 2026 | Codex **Goal Mode** GA — persistent plan-execute-replan loops running 14+ hours unattended |
| Jun 17, 2026 | Pulse sunset — folded into expanded scheduled tasks |
| **Jul 9, 2026** | **ChatGPT Work + unified desktop app** — Chat / Work / Codex in one app with built-in browser; Work delegates long multi-step white-collar tasks against connected apps and local files, returning finished docs/sheets/decks. Press framed it as the direct answer to Claude Cowork |
| Aug 2026 | **Atlas shut down** (~10 months after launch) — replaced by the desktop app's built-in browser |
| Sep–Nov 2026 | GPT-6 "Astra" (1M context, Sep 3); GPT-6 Instant with Intelligent UI widgets (Oct 7); GPT-6.2 (Nov 17) |

**OpenAI's pattern: launch-fast-then-fold-in.** Plugins → GPTs → GPT Store → workspace agents. Operator → agent mode → ChatGPT Work. Pulse → scheduled tasks. Atlas → built-in browser. Standalone Codex app → Codex pane. The sprawl of 2024–25 experiments collapsed into one desktop app with three modes: **Chat** (converse), **Work** (delegate outcomes), **Codex** (delegate code).

---

## Part 2: Claude — From claude.ai to One Unified Claude

### The Climb (2023–2025)
| Date | Milestone |
|------|-----------|
| Jul 11, 2023 | claude.ai launches with Claude 2 (US/UK beta, 100K context) |
| May–Jul 2024 | iOS app; **Artifacts** (Jun 20, with Claude 3.5 Sonnet); Projects; Android app |
| Oct 2024 | Computer use (API beta); Analysis tool; **Claude Desktop** (Oct 31) |
| Nov 25, 2024 | **MCP open-sourced** — Claude Desktop is the first MCP host |
| May 1, 2025 | **Integrations** — remote MCP connectors (Jira, Zapier, Asana, Linear…) + upgraded Research |
| Aug 25, 2025 | **Claude in Chrome** pilot (browser-acting extension; all paid plans by Dec) |
| Sep–Oct 2025 | **Memory** rollout (Team → Enterprise → Max/Pro); incognito chats |
| Oct 16, 2025 | **Agent Skills** across claude.ai, Claude Code, and API — the shared capability layer (open standard Dec 2025) |
| Oct 20, 2025 | **Claude Code on the web** — async sandboxed coding agents on Anthropic infra, GitHub-connected |

### Cowork: "Claude Code for the Rest of Your Work" (2026)
| Date | Milestone |
|------|-----------|
| **Jan 12, 2026** | **Claude Cowork launches** (research preview, Claude Desktop macOS, Max; Pro Jan 16) — grant a folder, Claude reads/edits/creates/organizes files, runs long multi-step tasks in parallel with check-ins |
| Jan 26, 2026 | Interactive Claude apps / MCP Apps — Slack, Asana, Figma, Canva render UIs inside chat |
| Apr 9, 2026 | Cowork **GA on macOS + Windows** (Linux beta later) |
| Jul 7, 2026 | Cowork expands to **web and mobile** (beta, Max) — usage data shows ~90% of sessions are non-coding |
| **Sep 16, 2026** | **THE MERGE: "Cowork and chat are now one Claude."** Cowork tab removed; one input box; Claude routes between quick answers and agentic background tasks. Claude Docs and Slides launch (beta) |
| Oct 6, 2026 | New Cowork-style tasks run **cloud-only** on Pro/Max (local-only execution removed) |
| Oct 8, 2026 | Dashboards + Motion launch; Docs/Slides/Design exit beta on all plans |
| Oct 23 – Nov 16, 2026 | Unified experience GA for Enterprise (Oct 23), Team (Nov 12); **on-by-default for Enterprise Nov 16** (Team Dec 1) |
| Nov 23, 2026 | **1.2M-session usage study**: >90% non-coding; 33% business ops; 16% decks/docs; coding only 8.7% — Cowork handles "the work around work" |

### The Architecture Story
Claude Code (Feb 2025 preview → GA May 2025) was an internal power tool that became a ~$500M+ ARR product. Anthropic's insight: the Claude Code **harness** — agent loop + file access + tools + skills + long-running execution — generalizes far beyond code. Cowork was that harness in a consumer GUI (reportedly built in ~1.5 weeks with Claude writing essentially all the code). Through 2026 the layers converged:

- **Skills** (Oct 2025) → shared capability layer across chat / Code / API
- **MCP + connectors** → shared integration layer
- **Cloud sandboxes** (Claude Code web, then Cowork cloud sessions) → shared execution layer
- **Sep 2026 merge** → chat becomes the universal front-end; the Code-derived harness is the universal back-end

Post-merge, Anthropic has exactly **two surfaces: Claude (chat) and Claude Code** — the cleanest expression of the two-interface pattern.

---

## Part 3: Perplexity — Search → Browser → Digital Worker

A different path to the same destination: Perplexity owns no frontier model, so its bet was **owning the container** (the browser, then the orchestration layer).

| Date | Milestone |
|------|-----------|
| Dec 7, 2022 | Answer engine launches — cited answers vs "ten blue links" |
| 2023 | Pro ($20/mo), Copilot guided search, Collections |
| 2024 | Enterprise Pro (Apr); **Pages** (May); Pro Search multi-step reasoning (Jul); Finance/Shopping verticals + **Buy with Pro** one-click checkout (Oct–Nov); Spaces; $9B valuation (Dec) |
| Feb 2025 | **Deep Research**; in-house Sonar models |
| May 2025 | **Labs** — generates reports, spreadsheets, dashboards, small web apps |
| **Jul 9, 2025** | **Comet browser** launches — Chromium + Comet Assistant sidebar agent (reads pages, fills forms, books, triages email/calendar) |
| Aug 2025 | $34.5B unsolicited bid for Google Chrome; Comet Plus publisher revenue share (80%) |
| Sep–Dec 2025 | Email Assistant (Max); Comet free worldwide (Oct); Amazon lawsuit over the shopping agent (Nov); Comet for Android; PayPal Instant Buy; NYT lawsuit (Dec) |
| **Feb 25, 2026** | **Perplexity Computer** — general-purpose agent platform orchestrating 19+ interchangeable models, isolated compute environment (file system, browser, tools) per task; pitched as a "general-purpose digital worker" |
| Mar 2026 | Comet Enterprise; Comet iOS; agent mode free on all four platforms; Samsung Galaxy S26/Bixby integration |
| Aug 2026 | 9th Circuit vacates the Amazon injunction (users, not Perplexity, access Amazon's systems) |
| Oct–Nov 2026 | Reported internal coding agent "**Teammate**" (unreleased, rumor stage); public **Perplexity CLI** gives third-party coding agents web search; ~$30B Nvidia-linked round in progress; $750M+ annualized revenue; 100M+ monthly users claimed |

**Perplexity's divergence:** after OpenAI retired Atlas (Aug 2026), Comet became the last major standalone free agentic browser on all platforms. Its "cowork" analog is **Computer** — a background digital-worker platform orchestrating other labs' models. No public coding agent (only the rumored internal Teammate). Its real differentiator is **distribution**: telco bundles (Airtel), OEM pre-installs (Samsung), payment rails (PayPal), and opportunistic bids (Chrome, TikTok).

---

## Part 4: The Two-Interface Pattern — Where It Stands (Nov 2026)

| | **Anthropic** | **OpenAI** | **Perplexity** |
|---|---|---|---|
| **Coding surface (A)** | Claude Code (terminal, IDE, web, mobile) | Codex (CLI, IDE, cloud, app → pane in super app) | None public ("Teammate" internal rumor; CLI is search-for-agents) |
| **General work surface (B)** | Claude — chat + Cowork merged Sep 2026 | ChatGPT Work (in unified desktop app, Jul 2026) | Perplexity Computer (Feb 2026) + Comet browser |
| **B is built on A's harness?** | Yes — explicitly ("Claude Code for the rest of your work") | Yes — "combines ChatGPT with Codex" | Partially — orchestrates third-party models |
| **Browser strategy** | Extension only (Claude in Chrome) | Atlas launched Oct 2025 → killed Aug 2026 → built-in browser | Browser-first (Comet) — the surviving standalone agentic browser |
| **Surfaces after consolidation** | 2 (Claude, Claude Code) | 1 app, 3 modes (Chat/Work/Codex) + CLI/IDE | 2 (Comet, Computer) |
| **Execution environment** | Anthropic cloud VMs (cloud-only since Oct 2026) + local for Code | Cloud + local files/apps with permission | Isolated compute environment per task |

### Why the Split Exists (and Where It's Heading)

**The terminal exhausts developers.** The evidence behind "developers can't manage more than ~2 sessions":

- **Jellyfish Research, "Measuring AI Agent Concurrency"** (Claude Code telemetry, 30-day window): **~84% of users peaked at 1–2 concurrent sessions**; ~11.4% at 3; only ~4.7% at 4+. The authors expected far more concurrency. This is the closest thing to the "2-session limit" source — revealed behavior, not a lab-proven hard cap.
- **ParallelPilot** (arXiv 2609.33113): formative study of 14 developers; treats >2 parallel sessions as advanced, expertise-gated usage; proposes the PILOT framework (Planning, Isolating, Logging, Observing, Triaging).
- **Workplace shadowing study** (arXiv 2610.33588): ~33% of developers' observed time went to prompting/checking agents — supervision overhead is what caps concurrency.
- **Delegation survey** (arXiv 2611.10058, n=203): users report lower workload *and* rate 5+ of 10 supervision activities "very/extremely mentally demanding" — **supervision, not generation, is the bottleneck**.
- **METR (Jul 2025 RCT)**: experienced OSS devs were 19% *slower* with AI assistance — the cognitive cost of evaluating agent output (single-session, but the same mechanism).

**The labs' response is structural, not numerical.** Rather than asking humans to babysit more sessions, 2026 products make agents longer-running and less supervision-hungry: Codex Goal Mode (14-hour unattended runs), workspace agents (continuously-running, shared across a team), Claude's cloud-only Cowork sessions with check-ins, Claude Code workflows (deterministic orchestration of hundreds of subagents under one session), and scheduled/cloud tasks on both platforms. The ceiling isn't being raised — it's being **routed around** by moving from *concurrent supervision* to *asynchronous delegation*.

### The Convergent Arc

```
2022-23   Chat          (answers)
2023-24   Assistant     (tools, memory, personalization)
2024-25   Workspace     (Canvas / Artifacts / Pages — artifacts, not answers)
2025      Agent         (Operator, agent mode, computer use, Deep Research)
2025-26   Delegation    (Cowork, ChatGPT Work, Computer — outcomes, not artifacts)
2026 →    Consolidation (one chat front-end routing to an agent back-end;
                         coding agent kept as the only separate surface)
```

The unit of value shifted **answers → artifacts → outcomes**, and pricing followed: flat subscriptions → ads on the consumer funnel (ChatGPT, Feb 2026) → **metered consumption pricing for agent runtime** (workspace agents) — pricing agent labor like labor.

---

## Key Takeaways

1. **The two-interface thesis is confirmed — and already consolidated.** Both major labs ran (terminal coding agent) + (general cowork app), then merged the cowork app into chat during 2026. The developer terminal remains the only separate surface, because git/terminal/IDE workflows genuinely differ.
2. **The coding harness won as the universal work engine.** Both labs built their white-collar agent out of their coding agent — not out of their chat app. Chat is distribution; the harness is the product.
3. **The ~2-session ceiling is real as observed behavior** (Jellyfish: 84% peak at 1–2), driven by supervision cost, and the industry's answer is asynchronous delegation (goal modes, cloud tasks, check-ins), not better multitasking UIs.
4. **Perplexity proves there's a third path** — no frontier model, browser-first, distribution-heavy — but it converged on the same endpoint: an isolated compute environment doing work for you (Computer).
5. **Anthropic's usage data validates the market**: >90% of Cowork sessions are non-coding. The agentic app for "the work around work" is a bigger surface than coding ever was.

---

## Sources

**Anthropic/Claude:** [Cowork is now Claude (official)](https://claude.com/blog/cowork-is-now-claude) · [Unified experience admin docs](https://support.claude.com/en/articles/17444462) · [Cowork usage study](https://claude.com/resources/articles/how-people-are-using-claude-cowork) · [Cowork launch (VentureBeat)](https://venturebeat.com/technology/anthropic-launches-cowork-a-claude-desktop-agent-that-works-in-your-files-no) · [TechCrunch on Cowork web/mobile](https://techcrunch.com/2026/07/07/the-coding-agent-wars-are-spilling-into-the-rest-of-the-office-claude-cowork/)

**OpenAI/ChatGPT:** [ChatGPT Work launch (Reuters)](https://money.usnews.com/investing/news/articles/2026-07-09/openai-launches-chatgpt-work) · [Workspace agents (OpenAI)](https://openai.com/index/introducing-workspace-agents-in-chatgpt/) · [Codex app (OpenAI)](https://openai.com/index/introducing-the-codex-app/) · [Super-app merge (The Decoder)](https://the-decoder.com/openai-plans-to-merge-chatgpt-codex-and-atlas-browser-into-a-single-desktop-superapp/) · [Atlas retirement (Yahoo)](https://tech.yahoo.com/ai/chatgpt/articles/openai-retire-chatgpt-atlas-browser-211627117.html)

**Perplexity:** [Perplexity Computer](https://www.buildfastwithai.com/blogs/what-is-perplexity-computer) · [Comet launch (TechRepublic)](https://www.techrepublic.com/article/news-perplexity-ai-browser-comet/) · [Comet Plus (Axios)](https://www.axios.com/2025/08/26/perplexity-comet-plus-subscription) · [Teammate report (Analytics Insight)](https://www.analyticsinsight.net/news/ai-coding-war-heats-up-as-perplexity-takes-on-anthropics-claude-code)

**Concurrency research:** [Jellyfish: Measuring AI Agent Concurrency](https://jellyfishresearch.substack.com/p/measuring-ai-agent-concurrency) · [ParallelPilot (arXiv 2609.33113)](https://arxiv.org/abs/2609.33113) · [Developers as Managers of AI Agents (arXiv 2610.33588)](https://arxiv.org/pdf/2610.33588) · [From Delegation to Action Approval (arXiv 2611.10058)](https://arxiv.org/abs/2611.10058) · [METR transcript analysis](https://metr.org/notes/2026-02-17-exploratory-transcript-analysis-for-estimating-time-savings-from-coding-agents/)

*Note: 2026 items rest on multi-source web research; load-bearing dates (the Sep 16 Cowork merge, Jul 9 ChatGPT Work, Feb 25 Perplexity Computer) are corroborated by first-party announcements. Single-source details (e.g., Perplexity "Teammate", exact December rollout dates) are flagged in-line as reported/rumored.*
