# S4 — The US–China Compute War

*Last Updated: November 27, 2026*
*Track 2: Geopolitics · Companions: `s2-token-economy.md`, `../md/28-capabilities-2030-future-interfaces.md`*

**The one-line finding:** the US is decisively winning the compute war (72–78% of world AI compute; Huawei at <4% of Nvidia's output), drawing the model war (a stubborn ~6-month frontier gap; China owns open weights and Global South diffusion), and losing the energy war — and 2026's signature development was *mutual decoupling by choice*: Washington re-tightened after its 2025 liberalization flopped, and Beijing banned the very chips it once demanded.

---

## 1. The Power Map (who controls each layer, Nov 2026)

| Layer | US | China | Allied | Verdict |
|---|---|---|---|---|
| **Chip design** | Nvidia/AMD/Google/Amazon ~90%+ of frontier accelerators | Huawei, Cambricon 1–2 gens behind | ARM | **US dominant** |
| **Leading-edge fab** | <5% (TSMC Arizona still <5% of leading edge) | SMIC 5nm-class at ~20% yield, DUV-only | **Taiwan >90%**, Korea, Japan (Rapidus 2027) | **Allied, Taiwan-concentrated** |
| **Litho/equipment** | Applied/Lam/KLA | Domestic EUV ~2030s | **ASML 100% of EUV** | **Allied chokepoint holds** |
| **Memory (HBM)** | Micron ~20–25% | CXMT entering HBM3E at 20–30% yield — **China's #1 bottleneck** | SK Hynix + Samsung ~75% | **Allied dominant** |
| **Energy** | 44 GW shortfall, 2,300 GW stuck in interconnect queues | **2x US generation, ~30% cheaper power, ~400 GW spare** | — | **China's one clear win** |
| **Models** | Every frontier-defining model since 2023; ~6-month closed-model lead | **Owns the open-weight frontier**; Qwen >50% of global open downloads | Mistral (on US chips) | **US leads frontier; China leads diffusion** |
| **Compute stock** | ~72–75% of world AI compute; 56 GW DC capacity | ~10% of compute; 24 GW capacity, **chip-gated** (~29% unracked) | Gulf/EU/Japan buying in | **US dominant, widening** |

The two powers' constraints are mirror images: **the US has chips but needs power; China has power but needs chips.**

---

## 2. Export Controls: Reversal → Re-tightening

The 2025–26 arc:

- **Aug 2025**: H20 licensed to China under an unprecedented ~15% revenue share — then only ~$60M of revenue ever materialized.
- **Sept–Nov 2025**: Beijing flipped the game — barred major Chinese firms from buying Nvidia, mandated domestic chips in state datacenters, drafted an ≥80% domestic-content rule.
- **Jan 2026**: H200 case-by-case licensing with a 25% export fee — **near-zero uptake**; China approves imports only "under exceptional circumstances."
- **Nov 2025–now**: Blackwell-class (B30A) blocked; no Blackwell part approved for China.
- **Nov 16–19, 2026**: the newest front — Commerce closed the **cloud-rental loophole** (licenses required for overseas datacenters serving China-HQ'd firms >12M TPP); Nvidia barred neocloud sales tied to Chinese renters days later.
- **Enforcement got real in 2026**: $300M smuggling arrest (California), $2.5B Super Micro-linked scheme charged, a dedicated DOJ AI-crime unit — though analysts call known cases "the tip of the iceberg."
- **The truce layer**: Entity List frozen >1 year; Affiliates Rule suspended to **Jan 10, 2027** as part of the trade truce; the GAIN AI Act died in conference.

**Did controls work?** At the compute layer, yes — the gap is *widening* (US share of new compute: 60% in 2022–24 → 78% in H1 2026). At the capability layer, only partially: the model gap held at ~6 months because Chinese labs convert scarce FLOPs with extreme efficiency. Controls also triggered an irreversible domestication drive — bifurcation is now structural.

---

## 3. China's Domestic Stack

- **Huawei**: ~600k Ascend 910C in 2026; but Epoch's November analysis is definitive — **<4% of Nvidia's compute output in 2026**, falling to ~1% through 2028 if restricted to domestic HBM; Huawei's optimistic 2030 output ≈ Nvidia's 2026. **A persistent ~4-year hardware lag.**
- **SMIC**: 7nm at ~70k wafers/month; 5nm-class via DUV multi-patterning at **~20% yields** (vs TSMC 80%+). Domestic EUV: early-to-mid 2030s.
- **CXMT (the variable that matters most)**: HBM3E mass production starting ~Q4 2026 at 20–30% yields. Every Chinese 2027–28 chip plan hinges on this ramp.
- **Market result**: domestic chips ~90% of China's AI accelerator market by end-2026; Nvidia squeezed to single digits in China — and **zero China in Nvidia's guidance**.
- **Models**: DeepSeek R2 never shipped; V4 (Apr 2026, 1.6T params) did. Kimi K3 (2.8T) is the largest open-weight model ever. **GLM-5 (745B, MIT license) was trained entirely on Huawei Ascend** — the single most important proof that domestic silicon can train competitive (if not frontier) models. Zhipu and MiniMax IPO'd in Hong Kong. PLA procurement now explicitly specifies DeepSeek; civilian-release-to-military-procurement lag is measured in weeks.

---

## 4. Taiwan

Concentration is *increasing* in absolute terms: N2 ramps overwhelmingly in Taiwan (120–130k wafers/month by end-2026); Arizona reaches 3nm volume only ~Q3 2027. The 2026 US Threat Assessment says China does not intend invasion by 2027 — the live scenario is **blockade/quarantine**, renewed by November 2026 PLA drills. Cost modeling: blockade = 30–40% of global chip supply cut for 6–12 months (~$1T); war = ~$10T (~10% of world GDP). Diversification (Kumamoto, Dresden, Rapidus, Samsung Taylor) is real but changes nothing before 2028.

## 5. Sovereign AI: Builders vs Buyers

Pattern: **everyone except Japan (fabs) and Korea (memory) is buying access to the US stack**, and Washington uses export licenses to convert sovereign-AI money into alignment — UAE moved to Country Group A:5 (G42/Core42 named, expires Apr 2027); Saudi's Humain authorized for ~35k GB300-class chips; India's IndiaAI at ~38k+ GPUs with sovereign small models; the EU's Gigafactories call (€10B, 7 sites) closed Nov 12 with selection in 2027 — while Mistral trains on 13,800 Nvidia GB300s: **"sovereignty stops at the chip."**

## 6. The Strategic Frame

2026's weird duality: **a race in silicon alongside a truce in trade.** The Trump–Xi summitry produced a $30B tariff cut, the Affiliates Rule suspension, and — remarkably — a **"US–China Super Intelligence Dialogue" plus an SI incident hotline** (Sept 2026; follow-through shaky). Chips were explicitly off the table. Lab positioning: Anthropic is the hawk (Amodei: race "decided by ~2028"; lobbying up 5.9x); OpenAI plays compute geopolitics (Stargate ~$400B+, "OpenAI for Countries"); Nvidia lobbies for access. Aschenbrenner's Situational Awareness frame took damage — the arms-race-by-2027 predictions missed and his fund lost ~65% in Q3's AI rout — but his competitive-dynamics predictions (espionage, smuggling, military procurement) largely landed.

---

## 7. Scenarios to 2028/2030

| Scenario | ~Prob. | Shape |
|---|---|---|
| **Controls hold** (base) | ~50% | US keeps a 5–10x compute lead and ~6-month model lead through 2030; China completes a parallel domestic stack and owns Global South diffusion via open weights. Risk inside this branch: the US power wall throttles the US curve; Chinese open weights erode US standard-setting even as the US "wins" compute |
| **Controls fail** | ~25% | Mechanisms: smuggling outruns enforcement; CXMT yields surprise; a trade-deal administration trades Blackwell access for rare earths (precedent exists: H20 → H200 → Affiliates suspensions); or capability-per-FLOP keeps improving until the compute moat stops mattering. Gap → 0–3 months by 2028 |
| **Détente** | ~25% | SI Dialogue deepens into managed competition — verified chip sales, safety coordination. Beijing's problem: it now *rejects* US chips strategically; realistic version is narrow chips-for-rare-earths deals inside structural rivalry |
| **Wildcard: Taiwan blockade** | — | Converts the compute war into a ~$10T global crisis and moots every other variable |

**Watch, in order:** CXMT's HBM yield curve (late Q4 2026) → the US power buildout → the Affiliates Rule decision (Jan 10, 2027) → Taiwan.

**Tie-back to doc 28:** doc 28's capability forecast assumed compute scaling continues through 2030 — this study says that assumption holds *for the US*, is chip-gated for China, and has one catastrophic tail risk (Taiwan) that no capability curve survives. And the ~6-month model gap means the *interface* and *deployment* layers (docs 26–27), not raw capability, are where national advantage compounds.

---

## Sources

[Epoch: Huawei's roadmap to 2031](https://epoch.ai/publications/huaweis-roadmap-to-2031) · [Epoch: US vs China ECI](https://epoch.ai/data-insights/us-vs-china-eci) · [Epoch chip imports explorer](https://epoch.ai/latest/introducing-the-ai-chip-imports-explorer) · [BIS H200 licensing (IAPS)](https://www.iaps.ai/research/bis-licensing-policy-for-h200s) · [Cloud-loophole rule (CNBC)](https://www.cnbc.com/2026/11/26/neoclouds-nvidia-china-ai.html) · [Affiliates Rule suspension (Clifford Chance)](https://www.cliffordchance.com/content/dam/cliffordchance/briefings/2026/11/BIS%20Suspends%20Affiliates%20Rule.pdf) · [SMIC yields (Tom's Hardware)](https://www.tomshardware.com/tech-industry/semiconductors/china-can-make-advanced-chips-without-euv-but-the-bill-keeps-growing-duv-multiple-patterning-means-bigger-dies-lower-yields-and-longer-manufacturing-times) · [CXMT HBM (Reuters/WTAQ)](https://wtaq.com/2026/10/27/exclusive-chinas-cxmt-to-start-advanced-ai-memory-production-despite-poor-yields-sources-say/) · [Qwen >50% downloads (SCMP)](https://www.scmp.com/tech/big-tech/article/3349552/alibabas-qwen-family-captures-over-50-global-open-source-downloads-report-finds) · [China DC buildout (SemiAnalysis via vlsi.kr)](https://www.vlsi.kr/en/china-ai-datacenter-24gw-compute-gap-en/) · [China energy edge (Bloomberg)](https://www.bloomberg.com/graphics/2026-china-ai-energy-future/) · [SI Dialogue (Axios)](https://www.axios.com/2026/09/26/us-china-ai-si-deal) · [Amodei export advocacy (SCMP)](https://www.scmp.com/tech/big-tech/article/3362105/anthropic-ceo-amodei-urges-washington-tighten-china-chip-export-bans) · [PLA + DeepSeek (CSET)](https://cset.georgetown.edu/wp-content/uploads/CSET-Chinas-Military-AI-Wish-List.pdf) · [Taiwan cost modeling (Insurance Journal)](https://www.insurancejournal.com/news/international/2026/02/12/857770.htm) · [TSMC Arizona reality](https://asiatechmacro.substack.com/p/tsmc-arizonas-165b-bet-and-why-5) · [Nvidia Q3 FY27](https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Announces-Financial-Results-for-Third-Quarter-Fiscal-2027/) · [Smuggling enforcement (NBC)](https://www.nbcnews.com/tech/tech-news/doj-urged-investigate-nvidia-china-chip-smuggling-rcna609879)
