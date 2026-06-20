# NexusTrade AI — Multi-Agent Autonomous Trading System

> **Bitget AI Base Camp Hackathon S1** · Track 1: Trading Agent

NexusTrade AI is a multi-agent autonomous trading system that orchestrates five specialized AI agents — Macro Analyst, Technical Analyst, Sentiment Analyst, Risk Manager, and Executor — to perceive market conditions, reach consensus, and execute paper trades with full risk management. Built for the crypto market using live Bitget data.

![NexusTrade AI Dashboard](https://5jz42ca7.mule.page)

**Live Demo:** https://5jz42ca7.mule.page

---

## Core Thesis

Traditional trading bots follow static rules. NexusTrade AI mimics how a professional trading desk actually operates: **specialized analysts each form independent views, debate through a consensus engine, and only execute when risk-adjusted conviction crosses a threshold.**

The core assumption: **multi-agent disagreement is a feature, not a bug.** When the Macro Agent says "risk-on" but the Risk Agent says "exposure too high," the system correctly reduces position size rather than blindly following one signal. This mirrors how real hedge funds operate — alpha comes from the tension between conviction and risk management, not from a single indicator.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    NEXUSTRADE AI — AGENT FLEET                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐                    │
│  │  MACRO   │   │   TECH   │   │SENTIMENT │   Perception Layer  │
│  │  Agent   │   │  Agent   │   │  Agent   │                     │
│  │ DXY/Fed  │   │EMA/RSI/  │   │ F&G/Social│                    │
│  │ Yields   │   │ATR/ICH   │   │ Whale/News│                    │
│  └────┬─────┘   └────┬─────┘   └────┬─────┘                    │
│       │               │               │                          │
│       └───────────────┼───────────────┘                          │
│                       ▼                                          │
│              ┌────────────────┐                                  │
│              │   CONSENSUS    │   Decision Layer                 │
│              │    ENGINE      │   Weighted vote aggregation      │
│              │  (Weighted     │   Confidence scoring 0-100       │
│              │   Voting)      │   Regime detection               │
│              └───────┬────────┘                                  │
│                      │                                           │
│                      ▼                                           │
│              ┌────────────────┐                                  │
│              │     RISK       │   Risk Layer                     │
│              │    MANAGER     │   VaR / CVaR / MaxDD             │
│              │  VaR/Sizing/  │   Kelly Criterion sizing          │
│              │  Correlation   │   Stress testing                 │
│              └───────┬────────┘                                  │
│                      │                                           │
│                      ▼                                           │
│              ┌────────────────┐                                  │
│              │   EXECUTOR     │   Execution Layer                │
│              │    Agent       │   Smart order routing            │
│              │ Smart Routing  │   ATR-scaled SL/TP               │
│              └────────────────┘                                  │
│                                                                  │
├─────────────────────────────────────────────────────────────────┤
│  DATA LAYER: Bitget API · Fear & Greed Index · Price Engine     │
└─────────────────────────────────────────────────────────────────┘
```

### The Five Agents

| Agent | Role | Inputs | Output |
|-------|------|--------|--------|
| **Macro Analyst** | Global macro conditions | DXY, Fed policy, Treasury yields, liquidity | Risk-on / Risk-off bias |
| **Technical Analyst** | Multi-indicator confluence | EMA 20/50, RSI(14), ATR, Market Structure (HH/HL/LH/LL), Ichimoku Cloud | LONG / SHORT / NEUTRAL + confidence |
| **Sentiment Analyst** | Crowd positioning | Fear & Greed Index, social volume, whale flows | Sentiment score + extremes detection |
| **Risk Manager** | Portfolio protection | VaR(95%), CVaR, max drawdown, correlation, exposure | Position sizing + go/no-go |
| **Executor** | Order management | Consensus signal + risk parameters | Smart-routed orders with ATR-scaled SL/TP |

---

## Features

### Signal Engine
- **6-factor confluence scoring** — EMA cross, RSI momentum, ATR volatility, market structure, Ichimoku cloud, multi-timeframe agreement
- **30 USDT pairs** scanned simultaneously
- **ATR-scaled stop losses and take profits** on every signal
- **Risk badges** (Low/Medium/High) per signal
- **Market Regime Detector** — classifies BULL / BEAR / CHOPPY with confidence

### Multi-Agent Consensus
- Each agent independently analyzes all 30 pairs
- Weighted voting produces a consensus score
- Executor only acts when consensus exceeds threshold AND risk manager approves
- Full decision feed showing every agent's reasoning in real-time

### Risk Laboratory
- **Monte Carlo simulation** — 1000 paths, configurable timeframes (7/30/90 days)
- **VaR (95%) and CVaR** calculations
- **Correlation heatmap** across top 8 assets
- **Stress test scenarios** — flash crash, black swan, rally, volatility spike

### Strategy Forge
- Visual strategy builder with configurable parameters
- 5 strategy types: EMA Crossover, RSI Mean Reversion, Breakout + Volume, Ichimoku Cloud, Multi-Factor Confluence
- Backtesting on 200 historical candles
- Full performance analytics: Sharpe ratio, Profit Factor, Max Drawdown, Win Rate

### Paper Trading Lab
- Spot and Futures modes (up to 100x leverage)
- Starting balances: $500 / $1,000 / $5,000 / $10,000
- Liquidation calculator on leveraged trades
- Real-time equity curve with performance metrics
- Complete trade history with CSV export

### AI Chat Assistant (Ask Nexus)
- Context-aware responses grounded in live signal data
- Quick prompts for common queries
- Agent insights panel showing latest reasoning from each agent

### Decision Log
- Every signal scan, agent decision, and paper trade recorded
- Filterable by time range and action type
- Export to CSV or JSON

---

## How It Works

### The Autonomous Loop

```
1. PERCEIVE  →  Agents ingest live market data (prices, indicators, sentiment)
2. ANALYZE   →  Each agent forms independent view with confidence score
3. CONSENSUS →  Weighted voting aggregates views into unified signal
4. RISK      →  Risk Manager validates sizing, VaR, correlation exposure
5. EXECUTE   →  Executor routes order with ATR-scaled SL/TP
6. LOG       →  Full decision trail recorded for audit
7. REPEAT    →  Cycle runs every 60 seconds
```

### Signal Generation (Technical Agent Detail)

The confluence score combines six factors with weighted importance:

| Factor | Weight | Method |
|--------|--------|--------|
| EMA 20/50 Cross | 25% | Golden/death cross detection + slope alignment |
| RSI(14) Momentum | 15% | Oversold/overbought zones + divergence |
| ATR Volatility | 10% | Band width expansion/contraction |
| Market Structure | 20% | HH/HL (bullish) or LH/LL (bearish) pattern detection |
| Ichimoku Cloud | 15% | Price vs cloud position + Tenkan/Kijun cross |
| Multi-TF Agreement | 15% | Signal consistency across 15m, 1H, 4H, 1D |

**Score > 75** = HIGH confidence → full position size  
**Score 50-75** = MEDIUM confidence → half position size  
**Score < 50** = LOW confidence → skip or minimal size

### Risk Management

- **VaR (95%, 1-day):** Maximum expected daily loss at 95% confidence
- **CVaR:** Average loss beyond VaR (tail risk)
- **Kelly Criterion:** Optimal position sizing based on win rate and payoff ratio
- **Correlation adjustment:** Reduces exposure when assets are highly correlated
- **Max drawdown limit:** Hard stop at -15% portfolio decline

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Frontend | Vanilla HTML/CSS/JS (zero dependencies) |
| Data | Bitget Public API (spot prices, 24h stats) |
| Sentiment | Alternative.me Fear & Greed Index |
| Charts | HTML5 Canvas (custom rendering) |
| Hosting | Mule Pages (static deployment) |
| Design | Custom dark terminal aesthetic |

---

## Installation & Running Locally

### Prerequisites
- Any modern web browser (Chrome, Firefox, Safari, Edge)
- No build tools, no npm install, no compilation needed

### Steps

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/nexustrade-ai.git
cd nexustrade-ai

# Option 1: Open directly
open index.html

# Option 2: Serve locally (recommended for API access)
npx serve .
# or
python3 -m http.server 3000

# Open http://localhost:3000 in your browser
```

### No API Keys Required
NexusTrade AI uses Bitget's public API endpoints which require no authentication. The system works out of the box with zero configuration.

---

## Project Structure

```
nexustrade-ai/
├── index.html          # Complete application (single-file, zero dependencies)
├── README.md           # This file
├── logs/
│   ├── paper-trades.csv    # Paper trading log (timestamp, pair, direction, price, qty, balance)
│   └── paper-trades.json   # Same data in JSON format
├── docs/
│   └── PROJECT_DESCRIPTION.md  # Four-part project description for hackathon
└── LICENSE
```

---

## Paper Trading Records

All paper trading activity is logged with full audit trails:

- **Timestamp** — exact time of each trade
- **Trading pair** — e.g., BTC/USDT
- **Direction** — LONG or SHORT
- **Entry/Exit price** — actual execution prices
- **Quantity** — position size in USDT
- **PnL** — profit/loss per trade and cumulative
- **Balance changes** — running portfolio balance

Logs are available in `logs/paper-trades.csv` and `logs/paper-trades.json`.

---

## Live Demo

**https://5jz42ca7.mule.page**

No login required. Fully interactive — scan signals, run backtests, place paper trades, run Monte Carlo simulations, chat with the AI assistant.

---

## Hackathon Submission

- **Track:** Trading Agent (Track 1)
- **Team:** [Your Team Name]
- **Bitget UID:** [Your UID]
- **Demo:** https://5jz42ca7.mule.page
- **Community Post:** [Your tweet link]

---

## License

MIT License — free to use, modify, and distribute.

---

## Acknowledgments

- [Bitget](https://www.bitget.com) — API data and hackathon organization
- [Alibaba Qwen](https://qwen.ai) — Strategic sponsor
- [Foresight Ventures](https://foresightnews.pro) — Media partner
- Built for [Bitget AI Base Camp Hackathon S1](https://bitget.com/zh-CN/activity-hub/hackathon)
