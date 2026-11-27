# AI Capabilities 2028–2030 — and the Interfaces We'll Need

*Last Updated: November 26, 2026*
*Completes the series: doc 26 (chat app evolution) → doc 27 (interface landscape) → doc 28 (where it goes)*

This study does two things: (1) builds an evidence-based forecast of AI capabilities for 2028, 2029, and 2030 from measured trend lines — not hype; (2) derives, year by year, the interfaces those capabilities will force into existence.

---

## Part 1: The Capability Trajectory

### The One Chart That Matters: Task Horizon

METR's task-horizon metric — how long a task (in human-equivalent hours) AI can complete autonomously — is the best single predictor of what interfaces will be needed, because **interface design is a function of how long the agent works between check-ins.**

- **November 2026 state (METR TH2):** frontier is ~27 hours at 50% success on verifiable software tasks. The doubling time has *accelerated* — from ~7 months (2025 paper) to ~4.3 months (Jan 2026) to **~110 days** (Nov 2026).
- **The critical caveat:** the **80%-success horizon is 4–6x shorter** (~5 hours today), and both horizons double together — the reliability gap is *persistent*. Performance is also much worse on "messy" tasks (unclear goals, no feedback loops), and METR's new research-judgment tasks lag well behind.

**Extrapolation (50% horizon):**

| Date | Fast curve (110-day doubling holds) | Slow curve (reverts to 7-month) |
|------|-------------------------------------|--------------------------------|
| Nov 2027 | ~270 h (≈7 work-weeks) | ~90 h (≈2 work-weeks) |
| Nov 2028 | ~2,700 h (≈1.3 person-years) | ~290 h (≈7 work-weeks) |
| Nov 2029 | ~27,000 h (≈13 person-years) | ~940 h (≈6 work-months) |
| Nov 2030 | effectively unbounded | ~3,100 h (≈1.5 person-years) |

At 80% reliability, divide by 4–6. Even the **slow** curve gives you week-long reliable autonomous projects by 2028 and month-long by 2030.

### The Supporting Trend Lines

| Trend | Current state (Nov 2026) | Direction |
|-------|--------------------------|-----------|
| **Real freelance work** (Remote Labor Index) | 2.5% (Oct 2025) → 16.1% (Jul 2026) → **41.3%** (Nov 2026, Fable 5.2 — double the next model) | Doubling every ~3–4 months; must flatten logistically, but majority of bounded digital deliverables by 2028–29 is trend-implied |
| **Cost at fixed capability** | Falling ~10x/year; market price at record-low ~$0.97/M tokens | 2026-frontier intelligence at ~1/100th of today's price by 2028–29 |
| **Compute** (Epoch) | Scaling feasible through 2030: ~2e29 FLOP runs (≈10,000x GPT-4); power is the binding constraint (~6 GW per frontier run) | 200+ models above 1e26 FLOP by 2030; >$1T cumulative infra |
| **Benchmarks** | SWE-bench, ARC-AGI-2, FrontierMath Tier 4, Terminal-Bench 2: saturated. Unsaturated: HLE (~74%), OSWorld 2.0 (~73–82% vs human 72%, but 1.4–2.7x more steps), RLI, research judgment | Every verifiable self-contained benchmark saturates in ~18–24 months; messy/judgment evals don't |
| **Code authorship** | 43–47% of committed code AI-written (75% at Google) | 65–85% by 2028; human role shifts to specification + review |

### Timelines: Who Says What

| Source | Position |
|--------|----------|
| **Lab leaders** (all cluster on 2028) | Amodei: "country of geniuses in a datacenter" ~2028. Altman/Pachocki: automated AI researcher by Mar 2028, superintelligence <10 yrs. Hassabis (Oct 2026): 2–3 years — down from 5–10 in Jan 2026 |
| **Forecaster medians** | Metaculus weak-AGI median: Sep 2030 (drifting earlier); middle-50% begins Mar 2028 |
| **The skeptics** | Epoch's Erdil: full remote-work automation median **2045**. Karpathy: continual learning and the agent stack are "a decade" of work. Sutskever: models generalize like crammers |

### The Honest Synthesis

On **verifiable, self-contained digital work**, every trend line (METR, RLI, cost, compute) points to effectively superhuman, near-free capability by **2028–2029**. The entire forecast disagreement lives in the **transfer gap**: messy contexts, sustained reliability, continual learning, and verification cost. The decisive observable: whether OpenAI's March 2028 "automated AI researcher" target and METR's lagging research-judgment curve converge.

**Bottlenecks ranked:** (1) power — binding through ~2028 (US shortfall estimates 35–57 GW); (2) chips/memory — binding 2027–28; (3) **verification cost — the quiet constraint on economic impact** (generation scaled ~10x, human review bandwidth didn't); (4) continual learning — the candidate hard wall; (5) data — *not* binding through 2030.

---

## Part 2: What We Already Know About High-Autonomy Interfaces

The research base (full sources at end) converges on five findings:

1. **Span of control saturates fast.** Humans supervise ~2 coding agents comfortably (Jellyfish telemetry, doc 26); ~4 overwhelms experienced engineers (ParallelPilot). There is **no established staffing science** for agents-per-human by risk class — a glaring gap.
2. **The verification asymmetry is the binding constraint.** Generation accelerated ~10x; review bandwidth stayed flat (one dataset: +98% merged PRs, median review time +441%). Adding reviewers doesn't help — it's cognitive bandwidth. ~48% of orgs name validating AI output at scale as their biggest gap (Qodo 2026).
3. **The answer to verification is changing the artifact, not reading faster.** Anthropic generated ~180M lines of machine-checked formal proof with almost no human reviewers; "spec as the quality gate" research; AI-checking-AI monitors. Pattern: **humans verify the spec; machines verify the work.**
4. **Oversight signals are decaying exactly when needed.** Chain-of-thought monitoring is "the most effective oversight tool for current systems" (OpenAI) — and CoT monitorability is *decreasing* in GPT-6-class models. Uncertainty gets "laundered" as it passes between agents.
5. **The in → on → over-the-loop migration is the consensus shape.** In-the-loop (approve each action) → on-the-loop (act by default, monitored interrupt) → over-the-loop (humans set policy, audit outcomes). Aviation's lesson: trust must be earned in stages against demonstrated reliability, or you get complacency-then-oscillation.

The labs' directions, in one line each: **Anthropic** — autonomy made legible (plans, permissions, classifiers, proofs; 800+ internal agents; a C compiler built across ~2,000 Claude sessions). **OpenAI** — ChatGPT as OS, agents as employees (Frontier), model-rendered UI, screenless io device (~2027). **Google** — the OS itself becomes agentic (Astra → Gemini, Android cross-app agency). **Meta** — the interface is your face (glasses + neural band + Muse). **Microsoft** — the research toolkit (Magentic-UI: co-planning, action guards, answer verification).

---

## Part 3: The Derivation — Interfaces We'll Need, Year by Year

The logic: each doubling of the autonomy horizon changes *what the human is doing*, and therefore what the interface must be. A chat box is an interface to a 5-minute task. A kanban board is an interface to a 5-hour task. Neither is an interface to a 5-week task.

### 2028 — The Portfolio Era
*Capability basis: week-to-month projects at ~80% reliability; majority of bounded freelance deliverables automatable; 2026-frontier intelligence ~100x cheaper; code mostly AI-written.*

The human stops being a reviewer of work and becomes a **manager of a portfolio of workstreams**. Required interfaces:

1. **The exception console** (evolves from today's fleet dashboards). Not a kanban of tasks you watch — a quiet surface that interrupts only on *material* exceptions, with the exception carrying: what changed, what the agent already tried, the decision needed, and the blast radius. The design inversion: today's notification economy maximizes interruptions; this must formalize **when machines may claim human attention** as a budgeted, first-class resource.
2. **Spec-as-contract interfaces.** If humans can't read a month of agent output, the spec becomes the quality gate. Interfaces for *negotiating* specifications before work starts: the agent interrogates the goal, surfaces ambiguities and edge cases, and produces a machine-checkable acceptance contract the human signs. (Early forms exist: plan mode, co-planning in Magentic-UI. What's missing: the contract as a durable, enforceable artifact.)
3. **The verification stack as UI.** Three tiers visible in one view: machine-checked (proofs, tests, type systems — green/red), AI-audited (adversarial verifier agents with *diverse lenses*, since uncertainty launders across hops), and human-sampled (statistical spot-checks with confidence intervals — "we verified 4% of the work; estimated defect rate 0.3±0.2%"). Humans read the audit summary, not the work.
4. **Trust ledgers / staged autonomy.** Aviation's lesson operationalized: per-agent, per-domain reliability records that *earn* autonomy expansions ("this agent has 200 clean deploys in this repo; auto-approve tier 2 actions?"). Today's binary permission modes become graduated, evidence-based autonomy contracts.

### 2029 — The Organization Era
*Capability basis: multi-month autonomous projects; AI meaningfully accelerating AI research; agent-to-agent delegation normal; most routine digital work delegable.*

Single agents become **agent organizations** — and the human's unit of management shifts from workstreams to *organizational design*. Required interfaces:

5. **The org chart as interface.** You design and edit structures: which agent roles exist, reporting lines (which agents review which), escalation policies, budgets per role. Middle-manager agents supervise worker agents and surface only what crosses thresholds. The human's screen looks less like Slack and more like an **organizational design canvas with live telemetry**. (Precursors: Factory Missions, Claude workflows, OpenAI Frontier's "operating system for AI coworkers.")
6. **Policy-and-constitution editors.** At over-the-loop scale, you govern by policy, not approval. Interfaces for writing, testing, and versioning the rulebook: natural-language policies compiled to enforceable guards ("never spend >$500 without human sign-off; never touch production data outside region; always brief legal on contract language"), with **policy simulation** — replay last month's 10,000 agent decisions against the new rule before deploying it.
7. **Economic interfaces.** Agents transacting with agents (mandate protocols — AP2, ACP, x402 — already exist) need human-side surfaces: budget allocation per workstream, spend telemetry, mandate signing ("this agent may spend up to X on Y class of things until Z"), and dispute/rollback. The expense report inverts: you don't approve expenses after; you design spending authority before.
8. **Provenance and audit as a product surface.** When regulators, courts, or customers ask "why did your agents do that?", the answer must be a navigable, plain-language why-chain — goal → plan → delegation → action → evidence — exportable and tamper-evident. Compliance becomes a UI problem.

### 2030 — The Governance Era
*Capability basis (fast curve): horizon effectively unbounded on verifiable work; (slow curve): person-year projects. Either way: humans cannot review even the summaries of the summaries.*

The human role completes its migration: **operator → manager → director**. You govern a productive system you cannot inspect directly — the relationship a board has to a company, or a government to an economy. Required interfaces:

9. **Goal-and-boundary consoles.** The primary human act is setting objectives, constraints, and values-weights — then watching *outcome* metrics, not activity. The interface resembles an instrument panel for intent: what we're optimizing, what we'll never trade away, how the system's drift is trending against both.
10. **Independent AI auditors with adversarial standing.** At this scale, AI-checking-AI stops being a feature and becomes a *separation of powers*: auditor agents with different models, different incentives, and protected channels to the human — because CoT monitorability decay means you can't trust the worker's own account. The interface surfaces *disagreement between estates* as the primary alarm.
11. **Generative UI as the default — governed.** The model renders the right interface per decision (GPT-6 Intelligent UI generalized): a one-minute disposable console for approving a pricing change; a bespoke simulator for a strategy fork. The open problem research already flags: who audits an interface that existed for one minute? Expect **certified UI generators** — interface-rendering constrained by attested component libraries, the way the trust stack works for code.
12. **The human-bandwidth protocol.** The scarcest resource in the economy becomes calibrated human judgment. Interfaces must price it: every escalation to a human carries a cost, every delegation has an owner, and "which decisions still *require* a human" becomes an explicit, auditable, periodically re-litigated registry — the constitutional layer of the whole stack.

### The Stack, Assembled

```
2030  GOVERNANCE   goal/boundary consoles · independent AI auditors ·
                   certified generative UI · human-bandwidth registry
2029  ORGANIZATION org-design canvas · policy editors + simulation ·
                   economic mandates · provenance/audit surfaces
2028  PORTFOLIO    exception consoles · spec-as-contract ·
                   verification stacks · trust ledgers
2026  FLEET        task boards (Agent HQ, Missions) · cowork apps ·
                   ~2-session supervision ceiling          ← we are here
2024  COPILOT      chat · autocomplete · artifacts
```

Each layer doesn't replace the one below — it *absorbs* it. The chat box survives at every layer as the escalation surface of last resort; what changes is how rarely it's needed.

### What This Implies for Builders (2027 Window)

Mapped against the white-space analysis in the companion research series:

- **The staffing-science gap is open.** Nobody has the "agents-per-human by risk class" data product. Whoever instruments real fleets and publishes the actuarial tables becomes the authority (the Jellyfish telemetry was a glimpse).
- **Trust ledgers are unbuilt.** Permission systems are binary everywhere; evidence-based graduated autonomy is a clear 2027–28 product.
- **Policy simulation doesn't exist yet** — "replay history against the proposed rule" is standard in fraud/fintech and absent in agent platforms.
- **The verification stack is the picks-and-shovels play.** Formal-verification-as-a-service, adversarial audit agents, and sampled-QA dashboards all ride the one trend line (verification asymmetry) that *every* credible source agrees on — it's the bet that pays out on both the fast and slow curves.
- **Exception design is the new notification design.** The firms that formalize machine-initiated interruption (budgets, batching, blast-radius framing) will define the UX standard the way mobile push defined 2010s attention.

The deepest point from the whole series: **the interface has always encoded who does the work.** The chat box encoded "AI assists human." The task board encoded "human assigns AI." The interfaces of 2028–2030 encode "human governs AI organizations" — and the labs' product history (docs 26–27) shows they already know it, which is why both built their general-work apps out of their most autonomous component, the coding agent harness.

---

## Sources

**Capability trends:** [METR TH2 analysis](https://blog.pebblous.ai/report/metr-time-horizon-eval-cost-2026-11/en/) · [METR horizons accelerating (Unite)](https://www.unite.ai/metr-finds-ai-time-horizons-doubling-as-research-judgment-lags/) · [Epoch: Can scaling continue through 2030?](https://epoch.ai/publications/can-ai-scaling-continue-through-2030) · [Epoch AI 2030 report](https://epoch.ai/files/AI_2030.pdf) · [Epoch GATE](https://epoch.ai/blog/announcing-gate) · [Remote Labor Index (Scale/CAIS)](https://scale.com/blog/rli) · [GDPval (OpenAI)](https://openai.com/index/gdpval/) · [Token price index](https://report-ai.org/indexes/ai-economics/llm-token-price-index/) · [OSWorld 2.0](https://github.com/xlang-ai/OSWorld-V2) · [Multi-decade timelines case (Epoch)](https://epoch.ai/gradient-updates/the-case-for-multi-decade-ai-timelines) · [Karpathy on Dwarkesh](https://www.dwarkesh.com/p/andrej-karpathy) · [Amodei on Dwarkesh](https://www.dwarkesh.com/p/dario-amodei-2) · [Hassabis timeline (The Decoder)](https://the-decoder.com/deepmind-founder-hassabis-shortens-agi-timeline-from-five-to-two-to-three-years/)

**Oversight & verification research:** [ParallelPilot](https://arxiv.org/pdf/2609.33113) · [Overseeing Agents Without Constant Oversight](https://arxiv.org/pdf/2602.16844) · [Faster AI, Uneven Frontier](https://arxiv.org/pdf/2607.12125) · [DeepMind AGI safety approach](https://arxiv.org/pdf/2504.01849) · [Debate + weak-to-strong](https://arxiv.org/abs/2501.13124) · [CoT monitorability (OpenAI)](https://openai.com/index/evaluating-chain-of-thought-monitorability/) · [Confidence laundering](https://arxiv.org/pdf/2606.20662) · [Qodo State of AI Code Quality 2026](https://www.qodo.ai/state-of-ai-code-quality-report/) · [The End of Code Review](https://arxiv.org/pdf/2606.13175) · [Claude formal proofs at scale (The Decoder)](https://the-decoder.com/anthropics-claude-now-writes-code-and-proves-it-safe-automatically/) · [Evidence tracing survey](https://arxiv.org/pdf/2606.04990) · [Aviation lessons](https://tamsnow.substack.com/p/six-lessons-from-aviation-that-every)

**Interface concepts:** [NN/g: AI paradigm](https://www.nngroup.com/articles/ai-paradigm/) · [NN/g: Generative UI](https://www.nngroup.com/articles/generative-ui/) · [Interface of Theseus (JIT interfaces)](https://arxiv.org/pdf/2609.06770) · [GPT-6 Intelligent UI](https://openai.com/index/gpt-6-for-everyone/) · [Magentic-UI (Microsoft)](https://www.microsoft.com/en-us/research/blog/magentic-ui-an-experimental-human-centered-web-agent/) · [OpenAI Frontier](https://www.reworked.co/digital-workplace/openai-expands-enterprise-push-with-frontier-ai-agent-platform/) · [Anthropic Managed Agents](https://www.anthropic.com/engineering/managed-agents) · [Agent commerce protocol map](https://dev.to/brudy_dev24/agentic-commerce-protocols-in-november-2026-a-verified-map-of-acp-ap2-ucp-x402-mcp-a2a-and-45nn) · [a16z: the agentic interface](https://podscripts.co/podcasts/a16z-podcast/big-ideas-2026-the-agentic-interface)

*Method note: compiled from three parallel research passes (~50 web searches). Trend-implied projections are arithmetic extrapolations and inherit the assumption that measured curves persist; lab timelines carry commercial incentive; the 2028-vs-2045 disagreement between lab leaders and Epoch is the honest error bar on everything in Part 3.*
