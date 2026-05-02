<h1 align="center">📊 RiskPulse - Trading Analytics Platform</h1>

<p align="center">
  <b>Real-time statistical arbitrage system for cryptocurrency pairs trading with intelligent signal quality assessment and institutional-grade risk management.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/python-3.12-blue" alt="Python">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/docker-ready-brightgreen" alt="Docker">
</p>

<p align="center">
  <img src="docs/images/dashboard-main.png" alt="Main Dashboard" width="800"/>
</p>

<p align="center">
  <a href="#-overview">Overview</a> •
  <a href="#-key-features">Features</a> •
  <a href="#%EF%B8%8F-architecture">Architecture</a> •
  <a href="#-installation">Installation</a> •
  <a href="#-key-learnings">Key Learnings</a>
</p>

---

<h2 align="center">🎯 Overview</h2>

<p align="center">
  <b>Assignment:</b> Build a real-time quantitative trading analytics system demonstrating production-grade infrastructure for statistical arbitrage on cryptocurrency pairs.
</p>

<p align="center">
  <b>My Solution:</b> A complete end-to-end platform that ingests live market data, computes institutional-grade analytics, and visualizes trading opportunities through an intelligent signal quality framework.
</p>

**Core Capabilities Delivered:**

- ✅ **Real-Time Data Pipeline** - Binance WebSocket ingestion with sub-second latency and three-tier storage architecture
- ✅ **Statistical Arbitrage Analytics** - Hedge ratio computation, z-score analysis, and cointegration testing (ADF)
- ✅ **Signal Quality Innovation** - Novel composite scoring system (0-100) that weighs z-score strength, correlation quality, spread stability, cointegration validity, and historical performance
- ✅ **Live Trading Simulation** - Position tracking with institutional metrics including Sharpe ratio, profit factor, and maximum drawdown
- ✅ **Risk Management Framework** - Value at Risk (VaR), Conditional VaR (CVaR), Kelly Criterion position sizing, and portfolio health scoring
- ✅ **Production Architecture** - Containerized deployment with TimescaleDB for time-series optimization, Redis for caching, and async Python for concurrent operations

<p align="center">
  <b>Key Technical Achievement:</b> Implemented a multi-factor validation system that prevents trading on statistically invalid signals—distinguishing between mere correlation (assets moving together) and true cointegration (mean-reverting spread relationship). This distinction is critical for pairs trading profitability.
</p>

---

<h2 align="center">✨ Key Features</h2>

<h3 align="center">🎯 1. Signal Quality Score (My Personal Touch)</h3>

<p align="center">
  Instead of trading on z-score alone, this composite metric intelligently weighs five factors:
</p>

<p align="center">
  <img src="docs/images/component-breakdown.png" alt="Signal Quality Components" width="800"/>
</p>

**Components:**
- **Z-Score Strength (25%)**: Signal magnitude - distance from mean
- **Correlation Quality (25%)**: Pair relationship strength (0.983 = excellent)
- **Spread Stability (20%)**: Coefficient of variation (predictability)
- **Cointegration Test (15%)**: ADF p-value for stationarity validation
- **Historical Performance (15%)**: Win rate + profit factor track record

<p align="center">
  <b>Why This Matters:</b> High correlation (98%+) doesn't guarantee profitable trading. The system correctly identifies when spread is <b>non-stationary</b> (ADF p-value > 0.05), preventing trading during unfavorable conditions.
</p>

---

<h3 align="center">💰 2. Live Trading Simulator</h3>

<p align="center">
  Real-time position tracking with hypothetical execution:
</p>

<p align="center">
  <img src="docs/images/trading-simulator.png" alt="Trading Simulator" width="800"/>
</p>

**Key Features:**
- Entry/Exit Logic: |Z-Score| > 2.0  
- Position Sizing: 10% of capital per trade
- Risk Management: Stop loss (-5%), take profit (+10%)
- Performance Tracking: Sharpe ratio, profit factor, drawdown

<p align="center">
  <b>Honest Results:</b> The system shows both success <b>and</b> failure scenarios, demonstrating real-world challenges when cointegration assumptions fail.
</p>

---

<h3 align="center">⚠️ 3. Risk Dashboard</h3>

<p align="center">
  Institutional-grade risk metrics in sidebar:
</p>

<p align="center">
  <img src="docs/images/price-charts.png" alt="Risk Dashboard" width="800"/>
</p>

**Metrics Provided:**
- **Portfolio Health Score**: Composite risk assessment (0-100)
- **Value at Risk (95%)**: Maximum expected loss at confidence level
- **Current Drawdown**: Distance from peak equity
- **Position Exposure**: % of capital at risk

---

<h3 align="center">📈 4. Real-Time Analytics</h3>

<p align="center">
  Complete statistical arbitrage toolkit:
</p>

<p align="center">
  <img src="docs/images/spread-analysis.png" alt="Spread Analysis" width="400"/>
  <img src="docs/images/correlation.png" alt="Correlation" width="400"/>
</p>

**Features:**
- Spread & Z-Score charts with threshold visualization
- Rolling correlation analysis (60-period window)
- Price comparison with volume overlay
- Analytics summary table (all statistical metrics)

---

<h2 align="center">🏗️ Architecture</h2>

<p align="center">
  <img src="docs/images/architecture.png" alt="System Architecture" width="800"/>
</p>

<h3 align="center">Layer-by-Layer:</h3>

**1. Data Ingestion**
- Binance WebSocket API (BTC-USDT, ETH-USDT)
- ~100-500 ticks/second
- Data validation + tick buffering (500 ticks in-memory)

**2. Three-Tier Storage**
- **In-Memory Buffer**: Sub-millisecond latency for hot path
- **Redis Cache**: 5-60s TTL for analytics state
- **TimescaleDB**: Historical time-series queries (hypertables)

**3. Analytics Engine** (Runs every 5 seconds)
- Hedge ratio via OLS regression
- Z-score computation (rolling 60-bar window)
- ADF test for cointegration
- Signal Quality Score synthesis
- Risk metrics calculation

**4. Presentation Layer**
- Streamlit dashboard with Plotly charts
- Auto-refresh every 5 seconds
- Configurable parameters (sidebar)

<p align="center">
  <b>Tech Stack:</b> Python 3.12, Streamlit, TimescaleDB, Redis, Docker Compose, Pandas/NumPy, Plotly
</p>

---


<h2 align="center">🚀 Installation</h2>

### Prerequisites

| Requirement | Version |
|---|---|
| Python | 3.12+ |
| Docker & Docker Compose | Latest |
| Git | Any |


---

<h2 align="center">📊 Demo</h2>

<h3 align="center">Analytics Summary</h3>

<p align="center">
  <img src="docs/images/analytics-summary.png" alt="Analytics Summary" width="800"/>
</p>

**Key Statistics:**
- Hedge Ratio (β): 29.7250 (R² = 1.000)
- Current Z-Score: -2.63 (TRADING SIGNAL)
- Correlation: 0.983 (very high)
- ADF P-Value: 0.7908 (non-stationary ❌)
- Stationary: No (critical issue!)

**💾 Data Export:**
Click Download Price Data (CSV)" button in the Summary tab to export historical prices with timezone-aware timestamps for offline analysis and backtesting.

---

<h2 align="center">🎓 Key Learnings</h2>

<h3 align="center">The Cointegration Revelation</h3>

**The Problem:**

Initial strategy had:
- ✅ 98.3% correlation (excellent!)
- ✅ R² = 1.000 (perfect fit!)
- ❌ ADF p-value = 0.79 > 0.05 (non-stationary!)
- ❌ Result: Massive losses 💀

<p align="center">
  <b>The Insight:</b>
</p>

<p align="center">
  <b><i>High correlation ≠ mean reversion</i></b>
</p>

<p align="center">
  Two assets can move together (correlation) while their spread trends indefinitely (no cointegration). For pairs trading, you need <b>both</b>.
</p>

**The Solution:**

Through parameter optimization:
1. **Adjusted lookback period** (30 minutes for stable hedge ratio)
2. **Raised z-score threshold** (2.5 for extreme deviations only)
3. **Result:** Better signal quality and controlled risk

<p align="center">
  <b>Outcome:</b> This demonstrates why statistical rigor (cointegration testing) is essential in quantitative trading.
</p>

<p align="center">
  See full post-mortem: <a href="docs/LEARNINGS.md">LEARNINGS.md</a>
</p>

---

<h2 align="center">📈 Results</h2>

<p align="center">
  The system honestly reports both successes and challenges, demonstrating real-world trading complexity and the importance of proper statistical validation.
</p>

---

### One-command setup 

```bash
# 1. Clone the repository
git clone https://github.com/aryadoshii/RiskPulse-Trading-Analytics-Platform.git
cd RiskPulse-Trading-Analytics-Platform

# 2. Run setup (starts Docker services + installs dependencies)
chmod +x scripts/setup.sh
./scripts/setup.sh

# 3. Start everything with a single command
chmod +x scripts/run.sh
./scripts/run.sh
```

The dashboard opens automatically at **http://localhost:8501**


---
