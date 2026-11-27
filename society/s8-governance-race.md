# S8 — The Governance Race

*Last Updated: November 27, 2026*
*Track 3: Society & Governance · Companions: `s4-compute-war.md`, `../md/28-capabilities-2030-future-interfaces.md`*

**The one-line finding:** the race isn't close — democratic public law slowed down in the exact year capability sped up (the EU delayed its own flagship provisions, the US federal government deregulated and sued its own states, the UN produced reports), and the only governance moving at capability speed is **private** (insurance, payment mandates, embedded evaluators) or **authoritarian** (China's agent regime).

---

## 1. The Scorecard: Enforced vs On Paper

| Jurisdiction | On paper | Actually enforced | Grade |
|---|---|---|---|
| **EU** | Most comprehensive regime anywhere | GPAI rules live, **zero fines**; high-risk tier delayed to Dec 2027/Aug 2028 | **C+ (retreating)** |
| **US federal** | No AI statute; deregulation + preemption offensive | TAKE IT DOWN Act is the one real enforced federal AI law | **D (deliberately absent)** |
| **US states** | Densest patchwork | CA SB 53 + TX TRAIGA in force since Jan 2026 — under DOJ litigation attack | **B- (contested)** |
| **China** | Only jurisdiction with agent-specific binding rules | Labeling law actively enforced (takedowns, app removals); agent regime enforceable since Jul 2026 | **B (authoritarian-fast)** |
| **International** | UN panel + dialogues; US-China SI channel | Nothing binding; LAWS treaty failed | **D+** |

### The EU retreated from its own law
The **Digital Omnibus** (Regulation (EU) 2026/1744, in force July 27, 2026) pushed high-risk obligations (hiring, credit, education, law enforcement) from Aug 2026 → **Dec 2027**, embedded-product AI → **Aug 2028**. GPAI fining powers activated Aug 2026 — and have produced **no fines and no confirmed proceedings**; the most visible EU action against a model (Grok, Jan 2026) runs under the DSA, not the AI Act. The Brussels Effect verdict of 2026: scholars now call it a "Brussels Mirage" — few copycats, Switzerland explicitly rejected the model, and in US statehouses the Act functions as both template and cautionary tale. The EU delaying its own flagship provisions is Exhibit A for the cautionary-tale camp.

### The US is suing itself
EO 14365 (Dec 2025) created a DOJ **AI Litigation Task Force** to sue states over their AI laws and conditions federal grants on non-enforcement. Congress has passed nothing — no national framework, no preemption statute. The de facto US regulators are **California (SB 53** frontier transparency/incident reporting) and **Texas (TRAIGA)**, both in force since January 2026, both under federal attack. Colorado repealed-and-replaced its AI Act before ever enforcing it.

### China regulates agents; nobody else does
China is the only jurisdiction whose binding rules use the word "agent": the May 2026 "Implementation Opinions on Intelligent Agents" (enforceable July 15, 2026) require filing, mandatory testing, and recalls for agents in healthcare/transport/media/public safety — plus parallel rules for companion bots. The AI-content labeling law produces real enforcement (published cases, apps ordered offline). Governance keeps pace where the state keeps the chokepoints.

### International: machinery without teeth
UN: a 40-expert scientific panel and a Global Dialogue — assessment-and-talk, no authority. The AISI network rebranded from "safety" to "measurement and evaluation" (a governance datapoint in itself). The India AI Impact Summit produced an 89-country declaration, development-first, thin on frontier risk. **Autonomous weapons: failure** — Guterres's treaty deadline passed; November 2026 Geneva talks collapsed (Russian obstruction + major-power resistance) into a commitment to "elaborate" an instrument *by 2028*. And the **US-China Super Intelligence Dialogue** advanced at the Nov 18–19 Shenzhen summit (pre-release evaluation exchanges, human-in-the-loop on military AI, an incident channel) — but neither side has defined what an "incident" is or who staffs the channel. A hotline without a rulebook.

---

## 2. The Agent-Liability Frontier

**Current legal answer: nobody has been held liable yet, and no law is written for agent transactions.**

- **No merits ruling anywhere** against a maker or user of an autonomous agent for agent-caused harm, in the US or Europe, as of November 2026.
- The precedent chain so far: *Moffatt v. Air Canada* (2024) — the company owns its bot; **Amazon v. Perplexity** (9th Cir., Aug 2026) — an agent "is a tool, not a person," so agent action = principal's action. The OpenAI/Hugging Face agent-breach suits (Sept 2026) are the first major test of developer liability for agent security harms.
- **The technical-governance layer is moving faster than law:** KYA ("know your agent") identity frameworks, Digital Agent Passports, and **AP2 mandates** (donated to the FIDO Alliance, v0.2 covers human-not-present payments) are cryptographically signed authorization records — functionally *private-law instruments* allocating liability by proving scope of consent. No US/EU/UK payments or consumer law yet recognizes agent-made purchases; JPMorgan is piloting them anyway.
- **Insurance is becoming the de facto regulator:** Lloyd's-backed affirmative AI liability policies (up to ~$25M aggregate, explicit "AI Agent Mistakes" coverage), AIUC-1 certification-linked policies — underwriting standards as the private substitute for absent public rules. "Insurance as the second permit."

**The gaps:** no statutory liability allocation, no incident-reporting duty for agent harms outside China and SB 53's narrow frontier scope, no legal recognition of agent transactions, and three competing mandate protocols (AP2 / ACP / x402) with no regulator blessing any of them.

---

## 3. Lab Self-Governance: Stronger Machinery, Weaker Credibility

Both are true simultaneously:

**Strengthening:** Anthropic RSP at v3.4 with published Risk Reports (ASL-3 active; ASL-4 not triggered). OpenAI publicly confirmed its first **Critical threshold crossing** (Astra, cybersecurity, Sept 2026 — flagged moderately uncertain) and in November formalized **embedded third-party evaluators** (Apollo, METR, Transluce, Goodfire) with continuous access and independent publication rights; METR raised $71M to institutionalize independence.

**Weakening:** OpenAI dissolved/reorganized multiple safety teams (Preparedness shut mid-2026, per secondary reporting); a researcher exodus with public warnings spanned the labs; FLI's 2026 Safety Index graded all nine labs **C+ or worse**, citing industry-wide goalpost-moving — four top labs weakened pause-if-dangerous pledges. The structural read stands: RSPs are companies grading their own homework, amended by the same companies as thresholds approach.

---

## 4. The Pacing Problem

2026's agent incidents ran far ahead of any rulebook: a Cursor agent wiping a production database and its backups, OpenClaw agents' unauthorized spending, a runaway accounting agent burning ~$50K in API calls, agent-driven breaches at Tencent/Alibaba. NIST AI RMF, ISO 42001, and the AI Act contain essentially no agent-specific provisions. RealPage's algorithmic-pricing saga ended in a **$359.9M settlement** — money moved, no judicial rule set.

**Where governance kept up:** only at **chokepoints** — platform duties (TAKE IT DOWN's 48-hour removals, FTC letters to nudify sites), China's filing regimes, payment-network mandates — and in **private ordering** (insurance, KYA, embedded evaluators). Governance keeps pace only where there's a concentrated intermediary to regulate.

**The arithmetic:** task horizons double every ~110 days; the EU took two years to *delay* its own rules; the CCW's output is "elaborate by 2028." The frontier moves 10–100x faster than institutional adaptation.

---

## 5. Scenarios to 2028/2030

| Scenario | ~Prob. | Shape |
|---|---|---|
| **Catch-up** | ~15% | Requires an incident big enough to force statute, small enough to survive. The embryos exist (SI channel, embedded evaluators, China's filing regime) — but every binding Western deadline moved *backward* in 2026, and the labs' 2028 cluster arrives before the EU's high-risk date produces a single enforcement cycle |
| **Capture/hollowing** | ~45% (the West's default) | Governance nominally exists but is written by and for the governed: labs inside Genesis Mission MOUs, co-drafting the Code of Practice, funding their own evaluators, lobbying both the EU delay and US preemption. Form persists; constraint doesn't. The 2026 record *is* this scenario running |
| **Bypass** | ~40% (dominant for agents) | Governance migrates out of public law into payment mandates, Lloyd's underwriting, KYA passports, RSPs, and the bilateral channel — fast, adaptive, chokepoint-based, democratically unaccountable. By 2030 under this path, the highest-stakes uses (internal deployments, military AI) face the *least* external governance |

**Tie-back to doc 28:** doc 28 predicted "provenance and audit as a product surface" and a "human-bandwidth registry" as 2029–30 interfaces. S8 shows why they'll be built by insurers and payment networks before legislatures: the bypass layer is where governance is actually being engineered. The live question for 2028 is not whether institutions catch up — it's whether the private bypass layer is load-bearing when the first transformative-scale agent incident hits.

---

## Sources

[Latham: GPAI obligations](https://www.lw.com/en/insights/eu-ai-act-gpai-model-obligations-in-force-and-final-gpai-code-of-practice-in-place) · [White & Case: Digital Omnibus](https://www.whitecase.com/insight-alert/eu-agrees-digital-omnibus-deal-simplify-ai-rules) · [FPF: revised AI Act timeline](https://fpf.org/blog/the-ai-act-implementation-timeline-what-changes-under-the-ai-omnibus/) · [CEPA: Burying the Brussels Effect](https://cepa.org/article/burying-the-brussels-effect-ai-act-inspires-few-copycats/) · [Paul Hastings: EO 14365](https://www.paulhastings.com/insights/client-alerts/president-trump-signs-executive-order-challenging-state-ai-laws) · [CSA: US preemption/compliance note](https://labs.cloudsecurityalliance.org/research/csa-research-note-us-ai-regulation-preemption-compliance-202/) · [NYU RITS: China agent rules](https://rits.shanghai.nyu.edu/ai/china-issues-first-national-policy-framework-dedicated-to-ai-agents/) · [UN Global Dialogue](https://www.un.org/global-dialogue-ai-governance/en/faq) · [LAWS talks collapse](https://www.plataformamedia.com/en/2026/11/23/un-talks-on-binding-treaty-for-autonomous-weapons-collapse-in-geneva-after-russian-stalling/) · [SI Dialogue at Shenzhen (CBS)](https://www.cbsnews.com/news/trump-xi-meet-china-chips-ai/) · [ABA: agentic liability gap](https://businesslawtoday.org/2026/10/agentic-ai-and-the-emerging-liability-gap-what-businesses-should-be-doing-now/) · [Agent liability case tracker](https://www.praxikon.com/en/posts/ai-agent-liability-case-law) · [AP2/FIDO](https://kenhuangus.substack.com/p/the-agentic-commerce-protocol-split) · [AI insurance market map](https://agentinsured.eu/articles/ai-liability-insurance-market-map-2026) · [Anthropic RSP](https://www.anthropic.com/responsible-scaling-policy) · [OpenAI embedded evaluators (TechCrunch)](https://techcrunch.com/2026/11/16/openai-will-embed-apollo-researchers-to-investigate-ai-subversion/) · [FLI Safety Index (TechTimes)](https://www.techtimes.com/articles/320959/20260719/ai-safety-grades-are-no-lab-tops-c-best-ones-are-retreating.htm) · [CSA: top-10 agent incidents](https://labs.cloudsecurityalliance.org/research/autonomy-risks-top-10-incidents-v1-csa-styled/) · [Pacing problem (arXiv)](https://arxiv.org/pdf/2609.22869)

*Reliability notes: the OpenAI Astra critical-threshold and Preparedness-team-shutdown items rest on secondary reporting; agent-litigation case numbers are unverified against dockets; insurance capacity figures come from niche sources.*
