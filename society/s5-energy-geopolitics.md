# S5 — Energy Geopolitics of the AI Buildout

*Last Updated: November 27, 2026*
*Track 2: Geopolitics · Companions: `s4-compute-war.md`, `s2-token-economy.md`*

**The one-line finding:** energy succeeds chips as the binding constraint, but it's a *locational* chokepoint, not an exportable one — a gigawatt of firm power can't be shipped or smuggled — so the 2026–2028 crunch manifests as **price and politics, not blackouts**, and leverage accrues to whoever controls siting and long-dated PPAs.

---

## 1. The Scorecard: Energy-for-AI (Nov 2026)

| Dimension | US | China | Gulf | Rest |
|---|---|---|---|---|
| Generation headroom | Weak (headroom turns negative ~2027E) | **Dominant** (~2x US, spare capacity) | Strong per capita | Mixed — even Norway rationing |
| Speed to energize | Medium (bridge-gas hacks) | **Fast** (state-directed) | Fast on paper, slipping in practice | Slow (EU) / improving (Japan nuclear) |
| Firm clean pipeline | Medium (restarts '27, SMRs 2030s) | **Strong** (36 reactors under construction) | Weak | Japan/Korea strong; EU = France only |
| Chips to fill the watts | **Dominant** | Weak (~10% fill estimate) | Strong but revocable (US licenses) | US-dependent |
| Political durability | **Weak — the ratepayer revolt is live** | Strong | Strong | Weak-medium |
| **Net** | **Leads compute despite the energy handicap** | Energy superpower, compute-constrained | Leveraged satellite of US compute | Niche hosts |

The S4 asymmetry, quantified from the energy side: **the US has chips and needs power; China has power and needs chips** — and an estimate holds all Huawei chips produced since 2025 could fill only ~a tenth of China's datacenter capacity.

---

## 2. The US Buildout Reality

**The hard physical constraint is gas turbines.** GE Vernova's backlog hit 116 GW (a turbine ordered today delivers in **2031**; reservations sold out through 2030); Siemens is sold out through FY2028. New firm gas ordered now arrives *after* the crunch window.

**Nuclear is 2027+, SMRs are 2030s.** Palisades slipped to end-2026; Three Mile Island/Crane (835 MW for Microsoft) targets 2027, reportedly ahead of schedule, with a $1B federal loan. Oklo reached first criticality on a test reactor (Aug 2026) but HALEU fuel arrives 2029; TerraPower/Meta's 6.6 GW nuclear commitments run 2032–2035. **SMRs are irrelevant to this crunch.**

**What's actually bridging the gap:**
1. **Behind-the-meter gas and fuel cells** — now specified as *primary* power for first tranches; Bloom Energy scaling to 4 GW/yr of fuel cells (90-day delivery vs 4-year turbines); SemiAnalysis projects >50% of new US datacenter power is behind-the-meter from 2028
2. **Solar+storage in ERCOT** (41.9 GW solar + 21.5 GW storage live) — fastest adds despite federal hostility
3. **Curtailable interconnection** — FERC's June 2026 show-cause orders forced every RTO to reform large-load rules; MISO/ISO-NE/NYISO propose non-firm service ("capacity with interruptions"); rules land 2027
4. **Co-location at existing plants** (Amazon's 1.2 GW at Comanche Peak nuclear)

**The queues are fantasy, the energization is real:** ERCOT's large-load queue exploded 63 → 474 GW (vs a ~90 GW system peak) but only ~4.3 GW actually draws power; Dominion Virginia has ~70 GW queued against a 24.7 GW all-time peak; of 16 GW announced for 2026 delivery, only ~5 GW was under construction mid-year.

**The ratepayer revolt is now the defining US political constraint.** PJM capacity auctions cleared at records three straight years, hit the negotiated cap, and **failed to procure enough capacity two auctions running** — the first system-wide reliability shortfalls in PJM history, with datacenters driving ~93% of load growth. Electricity prices (+21% NJ, +13% VA) handed Democrats landslide wins in Nov 2025 on "make datacenters pay their fair share" platforms; NJ created a separate datacenter rate class (Jul 2026); utilities filed a record $31B in rate hikes; and the **November 2026 midterm "blue wave" was widely read as an energy-cost rebuke**.

**Trump policy cuts both ways:** fast-track permitting, the Crane loan, FERC pressure, a voluntary "Ratepayer Protection Pledge" — but also a federal freeze on renewables *including solar*, a cancelled 6.2 GW solar project, a terminated $4.9B transmission loan, and $1.22B paid to cancel offshore wind. Critics (including Nvidia's own sustainability chief) note this blocks the fastest-to-build generation during the crunch.

---

## 3. China: Energy Solved, Chips Not

~10,500 TWh generation (>2x US); ~$940B energy investment in 2026 (largest globally); State Grid spending $574B over 2026–30 (+40%); **36 reactors under construction (~half the world total)**; solar additions of 180–240 GW in 2026 — more than the rest of the world combined, and that's a *slowdown*. The East-Data-West-Computing program has >80% of intelligent compute inside 8 national hubs at ~40% below eastern power costs. No ratepayer backlash, no interconnection queue, no turbine shortage. **China has eliminated energy as a variable; its constraint is accelerators** (S4).

## 4. The Gulf: Hosts, Not Powers

Stargate UAE's first 200 MW targeted Q4 2026 but slipping amid re-planning (the 5 GW campus needs more power than the UAE itself had forecast); Saudi Humain broke ground on 100 MW sites with xAI's first non-US datacenter (500+ MW) and a $5B AWS AI Zone. The Nov 2025 Blackwell authorizations formalized the bargain — chips for investment, conditioned on **phasing out Huawei equipment**; the UAE got license-free access in Jul 2026, a tier above Saudi. Verdict: petrostates are becoming *hosts of American compute* rather than independent AI powers — likely well under 1 GW combined energized by end-2026 — which is precisely Washington's design.

## 5. The Rest

- **Europe — structurally constrained:** datacenters eat 23% of Ireland's electricity (Dublin moratorium to 2028); ~700 GW stuck in queues across 8 member states; Irish industrial power costs 2.3x France's. Hosts sovereign/inference niches, not frontier training.
- **Japan/Korea — the nuclear re-openers:** Kashiwazaki-Kariwa back online (Apr 2026); TEPCO's ¥10.2T grid+nuclear program explicitly targets AI datacenters.
- **Hydro states discover pricing power:** Alberta got >25 GW of applications (double its peak supply) and went "bring your own power"; Hydro-Québec is asking to *double* datacenter rates; **Norway froze all new datacenter grid reservations (Nov 9, 2026)** after 26 GW of applications exceeded national peak demand. Even power-rich jurisdictions now ration.

---

## 6. Energy as Leverage

Goldman calls power "probably the forever bottleneck" (~$7.6T capital need 2026–31). But the strategic texture differs from chips: **compute goes to the electrons**, so the leverage instruments are siting rights, interconnection positions, and long-dated firm PPAs — Microsoft–Crane (835 MW/20yr), Amazon–Comanche Peak, Meta's 6.6 GW nuclear book (~9.8 GW of AI-nuclear deals mapped). These are the new strategic reserves, comparable to chip allocations on the balance sheet.

**Climate is the quiet casualty:** Microsoft+Amazon+Google emitted 119 Mt CO₂e in FY2026 (+~20% YoY — a third of France); net-zero pledges retained on paper, drifting out of reach; the realistic US path through 2030 is gas-heavy. Political risk now cuts both ways — emissions on the left, rates everywhere.

---

## 7. The Crunch Window & 2028/2030 Projections

**What breaks (confirmed):** PJM missed its reliability requirement twice; US grid headroom turns negative ~2027; turbines arrive 2030–31; restarts add <2 GW before 2028. The failure mode is **delayed energization, bidding wars for powered land, and rate pass-through** — already happening.

**What resolves it:** the pincer of supply arriving late (turbine wave + Crane + FERC reforms converge 2028–30) and **demand marking itself down** — SemiAnalysis's November 2026 revision cut its 2030 AI accelerator power forecast **122.8 → 80.7 GW (-34%)** and 2028 capex -28%. The most bullish quantitative shop just blinked. 2027 is the maximum-stress year.

| Source | 2030 projection | Confidence |
|---|---|---|
| IEA | ~945 TWh global datacenter demand (~3% of global electricity) | High (anchor base case) |
| EPRI | US datacenters 9–17% of US electricity (380–790 TWh) | High (honest wide band) |
| Epoch | Largest single training run 4–16 GW (6 GW central); >100 GW global AI capacity | Medium — conditional on scaling persisting |
| SemiAnalysis (revised) | ~80.7 GW global AI accelerator power | The bearish correction |

**Tie-back to doc 28:** doc 28's capability forecast listed power as binding constraint #1 through 2028 — this study confirms it but sharpens the mechanism: the constraint expresses as *politics* (ratepayer revolts, rate classes, siting fights) before physics, which means the capability curve's US leg depends partly on winning elections, not just building turbines. And the SemiAnalysis markdown is the first quantitative crack in the "scaling continues through 2030" assumption worth watching.

---

## Sources

[GE Vernova backlog (Utility Dive)](https://www.utilitydive.com/news/ge-vernova-gas-turbine-backlog-climbs-to-116-gw/826039/) · [Siemens backlog](https://www.utilitydive.com/news/siemens-gas-turbine-backlog-nears-70-gw-as-company-expands-manufacturing/827390/) · [Crane ahead of schedule (WNN)](https://www.world-nuclear-news.org/articles/us-reactor-restart-project-ahead-of-schedule) · [SemiAnalysis: solving the power problem](https://newsletter.semianalysis.com/p/how-ai-labs-are-solving-the-power) · [FERC large-load orders (Willkie)](https://www.willkie.com/publications/2026/06/ferc-directs-grid-operators-to-reform-procedures-for-large-loads-connecting-to-the-bulk-transmission) · [ERCOT queue (Compute Law)](https://computelaw.blog/power/ercot-large-load-interconnection-texas/) · [EPRI 2030 update](https://www.epri.com/about/media-resources/press-release/trb5wwt7oemdbkaamxrccqkq2ktteae8) · [PJM shortfall (mgrid)](https://mgrid.org/2026/02/27/pjm-2026-2027-capacity-prices-reach-329-mw-day-as-data-centers-drive-first-ever-system-wide-reliability-shortfall/) · [Electricity-price elections (CNBC)](https://www.cnbc.com/2025/11/12/electricity-prices-data-center-ai-new-jersey-virginia-midterm-election.html) · [2026 midterms (CNBC)](https://www.cnbc.com/2026/11/07/midterm-election-blue-wave-trump-renewable-energy.html) · [$31B rate hikes (Fortune)](https://dc.fortune.com/2026/01/29/record-utility-rate-hike-requests-31-billion-public-outcries) · [China grid spend (Asia Financial)](https://www.asiafinancial.com/china-to-spend-574-billion-on-power-grids-amid-renewables-push) · [China nuclear (WNA)](https://world-nuclear.org/information-library/country-profiles/countries-a-f/china-nuclear-power) · [East-West computing (TechNode)](https://technode.com/2026/11/11/china-accelerates-data-center-expansion-as-the-west-faces-mounting-opposition/) · [Stargate UAE (Epoch)](https://epoch.ai/data/ai-data-centers/directory/openai-stargate-uae) · [Gulf chip authorizations (MEI)](https://mei.edu/policymemo/us-authorizes-chips-for-the-uae-saudi-arabia-2/) · [Ireland/EU constraints (Euronews)](https://www.euronews.com/next/2026/05/05/europe-is-hungry-for-ai-data-centres-but-its-energy-grid-cannot-feed-them) · [Norway freeze (TFTC)](https://www.tftc.io/norway-ai-data-center-grid-freeze-26000-mw-statnett) · [Goldman forever bottleneck (Axios)](https://www.axios.com/2026/10/20/goldman-ai-energy-infrastructure-bottleneck) · [SemiAnalysis forecast cut (Longbridge)](https://longbridge.com/en/news/305662589) · [IEA Energy & AI](https://www.iea.org/reports/energy-and-ai/executive-summary) · [Hyperscaler emissions (Heatmap)](https://heatmap.news/daily/google-amazon-microsoft-2026-data)
