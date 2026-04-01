# Axion Hedge Fund: Complete Trading & Intelligence Setup

**A personal, AI-native investment operation powered by Claude Code**

*Last Updated: March 25, 2026*

---

## 1. Overview

Axion is a personal hedge fund operation managing three crash-ready portfolios across India (INR), US & Global (USD), and Canada (CAD). It's built entirely on Claude Code as the orchestration layer — with 73+ MCP tools, 4 automated pipelines, 7 broker connections, 8 data APIs, and a suite of custom skills for every aspect of the investment workflow.

**Not a commercial fund.** This is one person's complete investment infrastructure — from morning briefings to crisis analysis to trade execution.

### Key Numbers

| Metric | Value |
|--------|-------|
| Total Portfolio Value | ~$110K USD equivalent (₹78.5L + $43K + C$23K) |
| Broker Accounts | 7 (TD, Questrade, Wealthsimple, IBKR, Zerodha, Dhan, Kraken) |
| Currencies | INR, USD, CAD, BTC |
| Data APIs | 8 (EODHD, Chart-IMG, SnapTrade, Treasury Direct, FRED, DeFiLlama, IBKR, Finnhub) |
| MCP Tools | 73+ across 3 services |
| Claude Code Skills | 10 trading-specific (/premarket, /pipeline, /portfolio-status, /market-pulse, /broker-health, /thesis-check, /war-room, /digest, /deploy, /save-session) |
| Automated Pipelines | 4 (morning-intel, war-daily, weekly-screen, manipulation-monitor) |
| Research Library | 400+ files (AxionResearch, investment-research, crisis research) |
| Deployed Dashboards | 5 (portfolio, stock-tracker, Iran crisis public/private, Meridian) |

---

## 2. Architecture

```
                          ┌──────────────────────────────────┐
                          │        CLAUDE CODE (Opus 4.6)     │
                          │      Orchestration & Intelligence  │
                          │                                    │
                          │  Skills: /premarket /war-room      │
                          │          /thesis-check /digest      │
                          │          /broker-health /pipeline   │
                          │                                    │
                          │  Agents: exposure-calculator        │
                          │          news-gatherer              │
                          │          historical-analogue         │
                          └──────────┬───────────┬─────────────┘
                                     │           │
                    ┌────────────────┘           └────────────────┐
                    ▼                                             ▼
    ┌──────────────────────────┐              ┌──────────────────────────┐
    │     MCP TOOL LAYER       │              │    DATA & RESEARCH       │
    │                          │              │                          │
    │  TradingCLI (28 tools)   │              │  EODHD (prices, news)    │
    │  liquidity-tracker (25)  │              │  Chart-IMG (charts)      │
    │  bond-tracker (14)       │              │  Treasury Direct (bonds) │
    │  india-mcp (6)           │              │  FRED (central banks)    │
    │                          │              │  DeFiLlama (stablecoins) │
    │  Total: 73+ tools        │              │  Finnhub (real-time)     │
    └──────────┬───────────────┘              └──────────────────────────┘
               │
    ┌──────────┴───────────────┐
    │     BROKER LAYER          │
    │                           │
    │  TD Direct (USD) ──────── Screenshot-based (no API)
    │  Questrade (USD) ──────── SnapTrade OAuth
    │  Wealthsimple (CAD) ───── SnapTrade (read-only)
    │  IBKR (CAD/USD) ──────── ib-async (paper mode)
    │  Zerodha (INR) ────────── kiteconnect (SEBI 24hr expiry)
    │  Dhan (INR) ───────────── Static API key (not yet funded)
    │  Kraken (BTC) ─────────── API key+secret
    └───────────────────────────┘
               │
    ┌──────────┴───────────────┐
    │     OUTPUT LAYER          │
    │                           │
    │  Dashboards (5 deployed)  │
    │  Reports (daily/weekly)   │
    │  Digests (CSV time-series)│
    │  Memory (auto-updated)    │
    │  Alerts (threshold-based) │
    └───────────────────────────┘
```

---

## 3. Portfolios

### Portfolio A: India (INR)

| Ticker | Sector | Allocation | Entry Trigger |
|--------|--------|-----------|---------------|
| GOLDBEES | Gold | 15% | Nifty <23500 or INR >93 |
| HAL | Defense | 12% | India defense budget news |
| BEL | Defense | 10% | Same |
| TCS | IT Services | 10% | Rupee weakness play |
| INFY | IT Services | 8% | Same |
| ONGC | Energy | 10% | Oil >$90 |
| COALINDIA | Energy | 8% | Stagflation hedge |
| Cash | — | 27% | Deploy on triggers |

- **Total:** ₹78.5L (~$93K USD at current rates)
- **Broker:** Zerodha (₹2L cash + ₹30L incoming from MF redemption), Dhan (planned ₹5L for algo)
- **Thesis:** India defense spending + stagflation hedge + rupee depreciation

### Portfolio B: US & Global (USD)

| Ticker | Sector | Allocation | Conviction |
|--------|--------|-----------|-----------|
| NTR | Fertilizer | 10% | HIGH |
| EQNR | Energy (Norway) | 15% | HIGH |
| GDX | Gold Miners | 10% | HIGH |
| KTOS | Defense (Drones) | 5% | MEDIUM |
| AVAV | Defense (Drones) | 5% | HIGH |
| TSM | Semiconductors | 5% | MEDIUM |
| CCJ | Uranium | 8% | HIGH |
| Cash | — | 20% | — |

- **Total:** ~$43,000
- **Brokers:** TD RRSP (primary), Questrade FHSA (secondary), IBKR TFSA (international)
- **Thesis:** Energy supercycle + defense spending surge + de-dollarization gold bid

### Portfolio C: Canada (CAD)

| Ticker | Sector | Allocation |
|--------|--------|-----------|
| XEG.TO | Energy ETF | 30% |
| SU.TO | Suncor (Oil Sands) | 20% |
| CVE.TO | Cenovus (Oil Sands) | 20% |
| XGD.TO | Gold Miners ETF | 15% |
| CCO.TO | Cameco (Uranium) | 15% |

- **Total:** ~C$23,000
- **Broker:** Wealthsimple (3 accounts: FHSA, RRSP, TFSA)
- **Thesis:** Canadian energy + gold exposure in CAD

### Deployment Triggers

| Trigger | Condition | Action |
|---------|-----------|--------|
| VIX Spike | VIX > 35 | Deploy Tranche 1 (30% of each portfolio) |
| Nifty Crash | Nifty < 23,500 | Deploy India portfolio |
| SPY Crash | SPY -3% intraday | Deploy US portfolio |
| TSX Energy Crash | TSX Energy -5% | Deploy Canada portfolio |
| Oil Spike | Oil > $110 | Trim energy, add gold |

**Rule: NEVER deploy all at once.** Tranched: T1 → T2 → T3 with specific triggers per tranche.

---

## 4. Data Infrastructure

### Active APIs

| API | Type | Cost | Key Data | Rate Limits |
|-----|------|------|----------|-------------|
| **EODHD** | Market data | $99/mo | EOD prices, intraday, fundamentals, news, macro, 70+ exchanges | 5 concurrent |
| **Chart-IMG** | Charts | Paid | TradingView-quality PNG charts with RSI/MACD/BB overlays | 2 concurrent |
| **SnapTrade** | Broker bridge | Free | Questrade + Wealthsimple position sync | — |
| **Treasury Direct** | US debt | Free | Live public debt ($39T+), auction data, debt-to-the-penny | — |
| **FRED** | Central banks | Free (demo) | Fed, ECB, BOJ, PBOC balance sheets for liquidity tracking | — |
| **DeFiLlama** | Crypto | Free | Stablecoin supply (USDT + USDC) for liquidity model | — |
| **IBKR** | Broker | Free | Paper trading, real-time data (pending live approval) | — |
| **Finnhub** | Real-time | Free | Stock-tracker frontend, 60 req/min | 60/min |

### MCP Tool Inventory (73+ Tools)

| Service | Tools | Key Capabilities |
|---------|-------|-----------------|
| **TradingCLI** | 28 | Quotes, charts, portfolio, execution, screening, analysis across all brokers |
| **TradingCLI India** | 6 | Zerodha/Dhan specific: holdings, orders, positions, funds |
| **Liquidity Tracker** | 25 | Global liquidity index, central bank data, stablecoins, correlations, cycle analysis |
| **Bond Tracker** | 14 | Bond search, yield curves, credit spreads, auction data, live Treasury debt |

---

## 5. Automated Pipelines

### Pipeline 1: Morning Intel
- **Schedule:** 5:30 AM PT / 8:30 AM ET, weekdays
- **Duration:** ~2 minutes
- **What:** Portfolio snapshot → macro dashboard → overnight news → threshold alerts
- **Thresholds:** VIX >35, DXY >110, Oil >$110, INR >93, Nifty <23,500
- **Output:** `reports/daily/morning-intel-YYYYMMDD.md`

### Pipeline 2: Weekly Screen
- **Schedule:** Sunday 5 PM PT / 8 PM ET
- **What:** Value screen (P/E, FCF) → momentum screen (RSI, crosses) → insider scan → country rotation
- **Output:** `reports/weekly/weekly-screen-YYYYMMDD.md`

### Pipeline 3: War Daily
- **Schedule:** 9 AM, 1 PM, 6 PM PT (3x daily, weekdays)
- **What:** Oil complex → stress indicators → geopolitical OSINT → position impact
- **Output:** `reports/daily/war-daily-YYYYMMDD-HHMM.md`

### Pipeline 4: Manipulation Monitor
- **Schedule:** Saturday weekly
- **What:** CFTC COT → COMEX volume analysis → physical premiums → bank participation
- **Output:** `reports/weekly/manipulation-YYYYMMDD.md`

### Cost: ~$0.24/day for Grok queries + EODHD subscription

---

## 6. Claude Code Skills for Trading

| Skill | What It Does | Agents |
|-------|-------------|--------|
| `/premarket` | Full pre-market pipeline: batch ticker analysis, charts, macro, report | — |
| `/pipeline` | Self-healing ticker analysis with checkpointing, 3 parallel workers, rate-limit recovery | — |
| `/portfolio-status` | Quick position check across all 7 brokers, P&L, alerts | — |
| `/market-pulse` | Real-time market news + X/Twitter sentiment + key levels | — |
| `/broker-health` | Check all 7 broker tokens, rate limits, balances before trading | — |
| `/thesis-check` | Compare actual positions vs CURRENT-THESIS.md, flag drift/violations | exposure-calculator |
| `/war-room` | Crisis analysis: 3 parallel agents (news + exposure + historical) in <3 min | news-gatherer, exposure-calculator, historical-analogue |
| `/digest` | Process newsletters (Ed Steer, FFTT, Bear Traps) → structured data + PDF + CSV time-series | — |
| `/save-session` | Preserve trading session context for next conversation | — |
| `/research` | Structured research gathering with WebSearch/WebFetch | — |

---

## 7. Deployed Dashboards

| Dashboard | URL | What |
|-----------|-----|------|
| **Axion Portfolio** | github.io/portfolio/ (PIN: 2806) | 3 portfolios + currencies + bonds |
| **Stock Tracker** | github.io/stock-tracker/ | 11 investor trackers (Buffett, Dalio, etc.) |
| **Iran Crisis (Public)** | github.io/portfolio/us-iran-crisis-research/ (PIN: 2805) | Public research dashboard |
| **Iran Crisis (Private)** | github.io/portfolio/us-iran-crisis-research/private/ (PIN: 2806) | P&L, execution, reports |
| **Meridian AI Capital** | github.io/meridian-ai-capital/ | Quant platform dashboard |
| **Liquidity Tracker** | localhost:3001 | Global Liquidity Index (local) |
| **Bond Tracker** | localhost:3000 | Bond market (local) |

---

## 8. Research Library

| Collection | Files | What |
|-----------|-------|------|
| **AxionResearch** | 177 files | Full research library |
| **India Q1 2026** | 45 articles | India-focused deep research |
| **Investment Research** | Multi-folder | India/Canada/US/Portfolio/VedicAstrology |
| **US-Iran-Feb28** | 22 reports | Iran crisis analysis + trading guide |
| **33rd Parallel** | 59 files | Vedic/statistical/esoteric research |
| **Avaantage** | 488 reports | Completed diligence reports |
| **Commodities Thesis** | research/ | Metals, oil, stagflation, sector winners |
| **Design Docs** | 36 files | AI-native hedge fund blueprint |

---

## 9. Digests Intelligence Archive

```
~/Axion/AxionHedgeFund/digests/
├── daily-reports/
│   ├── precious-metals/        # Ed Steer, GATA, KWN
│   ├── macro-thematic/         # Zero Hedge, macro
│   ├── political-risk/         # Geopolitical
│   ├── broker-statements/      # Position snapshots
│   └── analyst-reports/        # Stock/sector
├── weekly-reports/
│   ├── fftt/                   # Luke Gromen (macro/liquidity)
│   ├── bear-traps/             # Larry McDonald (political risk)
│   ├── cot/                    # CFTC COT analysis
│   └── macro-summary/          # Weekly summaries
├── data-snapshots/             # 7 CSV time-series files
│   ├── prices.csv              # PM prices, DXY, 10Y
│   ├── slv-shorts.csv          # SLV/GLD short positions
│   ├── comex-inventory.csv     # COMEX flows
│   ├── shanghai.csv            # Shanghai premium + inventory
│   ├── treasury.csv            # Auction results
│   ├── macro-indicators.csv    # FFTT: liquidity, credit, fiscal
│   └── risk-indicators.csv     # Bear Traps: risk, credit, VIX
└── thesis-flags/               # Daily thesis relevance alerts
```

### Newsletter Sources

| Source | Frequency | Focus |
|--------|-----------|-------|
| Ed Steer's Gold & Silver Digest | Daily | PM prices, COMEX, SLV shorts, Shanghai |
| FFTT (Luke Gromen) | Weekly | Macro/liquidity, fiscal dominance |
| Bear Traps (Larry McDonald) | Weekly | Political risk, credit stress |
| GATA Dispatch | Daily | Gold manipulation, central banks |
| Zero Hedge | Ad-hoc | Bonds, Fed, macro |

---

## 10. Investment Thesis (Summary)

### Core Thesis: Fiscal Dominance + Commodity Supercycle

The US (and global) fiscal trajectory is unsustainable. Debt-to-GDP ratios require either:
1. **Inflation** (debase the debt away) → Long gold, commodities, real assets
2. **Financial repression** (cap yields below inflation) → Long gold, short bonds
3. **Default/restructuring** (unlikely for USD) → Long hard assets

Meanwhile:
- **Energy underinvestment** since 2014 → supply deficit → oil supercycle
- **Defense spending surge** → NATO 3%, India 3%+ → defense stocks
- **De-dollarization** → BRICS gold settlement → central bank gold buying
- **Silver manipulation** → SLV short squeeze potential → physical silver

### Thesis Monitoring

| Signal | Source | Threshold |
|--------|--------|-----------|
| VIX | EODHD / TradingCLI | >35 = deploy trigger |
| DXY | EODHD / Chart-IMG | <98 = dollar breaking down |
| 10Y Yield | Treasury Direct | >4.5% = Fed intervention needed |
| Oil (Brent) | EODHD | >$100 = energy supercycle confirmed |
| Gold/Silver Ratio | Ed Steer digest | <60 = silver outperforming |
| SLV Short Position | Short reports via /digest | Watch for squeeze setup |
| Shanghai Premium | Ed Steer digest | >8% = physical demand strong |
| COMEX Inventory | Ed Steer digest | Declining = supply tightness |
| 2Y Auction Quality | /digest Treasury data | Tail >1.5bps = fiscal stress |

---

## 11. Master Thesis Document

The full investment thesis with position-level detail is at:

**`~/Axion/AxionHedgeFund/CURRENT-THESIS.md`** (42KB)

This is the single source of truth. `/thesis-check` compares actual positions against it. `/war-room` references it for exposure analysis. `/digest` flags data relevant to it.

---

## 12. Manipulation Rules

Documented in memory (`market-manipulation-rules.md`):

1. **Trump Tweet Whipsaws:** Initial market move reverses within 24-48 hours. Don't chase the initial spike.
2. **Government Oil Suppression:** SPR releases, OPEC pressure. Short-term bearish, long-term bullish (depletes reserves).
3. **Gold/Silver Price Suppression:** COMEX paper shorting during low liquidity (6 PM Globex). Physical demand remains strong.
4. **Treasury Market Intervention:** Fed/PPT buying to cap yields. Unsustainable long-term.
5. **DXY Propping:** Dollar index being artificially supported. Crashes happen suddenly when support fails.

These rules are referenced by `/war-room` before generating recommendations.

---

## 13. Daily Workflow

### Morning (8:30 AM ET)
1. `/broker-health` — verify all tokens active
2. `/premarket` — or `morning-intel` pipeline if cron active
3. `/digest` — process Ed Steer overnight email
4. Review thesis flags from digest

### Intraday (if event occurs)
5. `/war-room "event description"` — crisis analysis
6. `/market-pulse` — quick sentiment check
7. `/portfolio-status` — check exposure

### End of Day
8. `/save-session` — preserve context for tomorrow

### Weekly (Sunday)
9. `/thesis-check` — compare positions vs thesis
10. `/digest` — process FFTT + Bear Traps weekly reports
11. Review weekly-screen output

---

## 14. Technology Stack

| Layer | Technology |
|-------|-----------|
| **Orchestration** | Claude Code (Opus 4.6, 1M context) |
| **CLI Tool** | TradingCLI (Python, 21K+ lines, uv package manager) |
| **Data Services** | Next.js dashboards + FastAPI backends + MCP servers |
| **Broker Connectivity** | SnapTrade (Questrade/WS), ib-async (IBKR), kiteconnect (Zerodha) |
| **Charts** | Chart-IMG API → TradingView-quality PNGs |
| **Deployment** | GitHub Pages (dashboards), Cloud Run (chart-api) |
| **Document Generation** | pandoc + pdflatex |
| **Data Storage** | JSONL checkpoints, CSV time-series, markdown reports |
| **Memory** | Claude Code auto-memory (market-data-latest.md) |

---

## 15. What's Unique About This Setup

1. **AI-native from day one** — Claude Code isn't bolted on, it IS the operating system
2. **MCP as the bridge** — 73+ tools let Claude directly query brokers, data sources, and services
3. **Skills as workflows** — each trading task is a reusable, tested skill with error recovery
4. **Parallel agents for speed** — /war-room runs 3 agents simultaneously for <3 min crisis analysis
5. **Digest pipeline** — newsletters automatically become structured data + CSV time-series
6. **Thesis enforcement** — /thesis-check automatically detects position drift
7. **Multi-currency** — operates across INR, USD, CAD simultaneously
8. **Research depth** — 400+ files of structured research accessible to Claude via file system
9. **Crash-ready portfolios** — pre-built, pre-sized, waiting for trigger conditions
10. **Manipulation awareness** — rules for known market manipulation patterns baked into analysis

---

## 16. Port Map & Local Services

| Port | Service | Status |
|------|---------|--------|
| 3000 | Bond Tracker frontend | Start manually |
| 3001 | Liquidity Tracker frontend | Start manually |
| 8001 | Liquidity Tracker API | Start manually |
| 8002 | Bond Tracker API | Start manually |
| 4001 | IBKR Gateway | Paper mode |

### Starting Everything

```bash
# Backend APIs
cd ~/Axion/AxionHedgeFund/services/liquidity-tracker/backend && source venv/bin/activate && python main.py &  # :8001
cd ~/Axion/AxionHedgeFund/services/bond-tracker/api && source venv/bin/activate && python main.py &           # :8002

# Frontends
cd ~/Axion/AxionHedgeFund/services/liquidity-tracker/frontend && npm run dev &  # :3001
cd ~/Axion/AxionHedgeFund/services/bond-tracker && npm run dev &                # :3000
```

---

## 17. Key File Locations

| Document | Path |
|----------|------|
| Master Thesis | `CURRENT-THESIS.md` |
| Data Sources | `DATA-SOURCES.md` |
| Pipeline Architecture | `DAILY-PIPELINES.md` |
| Automation Guide | `AUTOMATION.md` |
| India Thesis | `india/EQUITIES-INDIA-INR.md` |
| US Thesis | `us/EQUITIES-US-USD.md` |
| Canada Thesis | `canada/EQUITIES-CANADA-CAD.md` |
| Global Thesis | `global/EQUITIES-GLOBAL.md` |
| Commodities Thesis | `research/COMMODITIES-THESIS.md` |
| Stagflation Scenarios | `research/STAGFLATION-SCENARIOS.md` |
| Digests Archive | `digests/` |
| AI Hedge Fund Blueprint | `docs/ai-native-hedge-fund-design/` (36 files) |
| TradingCLI Config | `TradingCLI/config/settings.toml` |

---

*This document is part of the ClaudeCodeFeatures library at `~/Desktop/ClaudeCodeFeatures/`.*
*For the AI coding tools comparison, see documents 13-19 in the same directory.*
