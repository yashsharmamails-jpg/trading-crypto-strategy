# Crypto Multi-Confluence 15-Minute Strategy (v2)

A robust, multi-filter strategy for crypto futures on the **15-minute timeframe**, designed to maximize win rate × R:R while minimizing drawdown.

> **Important:** No strategy is guaranteed profitable. This script applies well-tested principles (trend-following + momentum + volatility filtering + smart exits). You must backtest it yourself on TradingView with real data, then forward-test on paper before risking capital.

---

## What's New in v2

| Improvement | Why It Helps |
|------------|--------------|
| **200 EMA Trend Filter** | Only trades in direction of macro trend → fewer counter-trend losses |
| **ADX > 20 Filter** | Skips choppy/ranging markets where MA strategies fail hardest |
| **Volatility Spike Filter** | Avoids entering during news-driven spikes (often reversal traps) |
| **Partial TP at 1.5R + Full TP at 4R** | Locks in gains while letting winners run |
| **Auto Breakeven SL after TP1** | Once 50% is closed at profit, remaining 50% is risk-free |
| **Trade Cooldown (8 bars)** | Prevents revenge-trading and overtrading in chop |
| **Time-Based Exit (48 bars / 12h)** | Closes stale trades that aren't going anywhere |
| **On-Chart Performance Table** | See net profit, win rate, profit factor, drawdown live |
| **Date Range Inputs** | Easily backtest specific 6-month windows |

---

## Strategy Logic (Plain English)

A trade is taken **only if ALL of these align**:

### LONG ENTRY (10 conditions)
1. Price is above the 200 EMA (macro uptrend)
2. Fast EMA (9) crosses above Slow EMA (21) — entry trigger
3. RSI is between 40-70 (momentum, not overbought)
4. MACD histogram is positive (bullish momentum)
5. ADX > 20 (market is trending, not ranging)
6. Current ATR < 2.5x its 50-period avg (no extreme volatility spike)
7. Volume > 1.1x its 20-period MA (real participation)
8. At least 8 bars have passed since last trade (cooldown)
9. Within backtest date range
10. Long trades enabled

### SHORT ENTRY
Mirror image of long: price below 200 EMA, EMA bearish cross, RSI 30-60, MACD negative, etc.

### EXIT LOGIC (3-tiered)
1. **TP1 (1.5x ATR)** → close 50% of position, move SL to breakeven on the rest
2. **TP2 (4.0x ATR)** → close remaining 50%
3. **SL (1.5x ATR from entry, then breakeven after TP1)** → exits everything if price reverses
4. **Time Exit (48 bars / 12 hours)** → closes if neither TP nor SL hit

**Effective R:R:** With breakeven trailing, average winning trade ≈ **2.75R** while losses are capped at **1R** (often less due to BE trail).

---

## How to Backtest on TradingView

### Step 1 — Add the Strategy
1. Go to [TradingView](https://www.tradingview.com)
2. Open the **Pine Editor** (bottom panel)
3. Paste the contents of `crypto_strategy_15m.pine`
4. Click **"Add to Chart"**

### Step 2 — Set Up the Chart
- Timeframe: **15 minutes**
- Pairs to test (one at a time):
  - `BINANCE:BTCUSDT.P` (Bitcoin Perp)
  - `BINANCE:ETHUSDT.P` (Ethereum Perp)
  - `BINANCE:SOLUSDT.P` (Solana Perp)
  - `BINANCE:DOGEUSDT.P` (Dogecoin Perp)
  - `BINANCE:BNBUSDT.P`
  - `BINANCE:XRPUSDT.P`
  - `BINANCE:AVAXUSDT.P`
  - `BINANCE:MATICUSDT.P`

### Step 3 — Configure Date Range
The strategy has built-in date inputs (default: Nov 2025 – Jun 2026 = 7 months).
- Click the gear icon on the strategy → "Inputs" tab → "Backtest Range"
- Adjust dates as needed

### Step 4 — Read Results
- Click **"Strategy Tester"** at the bottom
- Check tabs: **Overview**, **Performance**, **List of Trades**, **Equity Curve**

---

## Recommended Settings Per Pair

| Pair | SL Mult | TP1 Mult | TP2 Mult | ADX Min | Notes |
|------|---------|----------|----------|---------|-------|
| **BTCUSDT.P** | 1.5 | 1.5 | 4.0 | 20 | Default works well — most reliable |
| **ETHUSDT.P** | 1.5 | 1.5 | 4.0 | 20 | Default — strong trends |
| **BNBUSDT.P** | 1.5 | 1.5 | 4.0 | 20 | Default |
| **SOLUSDT.P** | 1.8 | 1.5 | 4.5 | 22 | Higher vol — wider SL/TP2 |
| **AVAXUSDT.P** | 1.8 | 1.5 | 4.5 | 22 | Similar to SOL |
| **XRPUSDT.P** | 1.5 | 1.5 | 4.0 | 20 | Default |
| **MATICUSDT.P** | 1.8 | 1.5 | 4.5 | 22 | High vol |
| **DOGEUSDT.P** | 2.0 | 1.5 | 5.0 | 25 | Meme coin — needs strongest trend filter |

---

## What "Profitable" Realistically Looks Like

Honest expectations for a strategy of this design on 6 months of crypto data:

| Metric | Realistic Range | Bad | Great |
|--------|---------------|-----|-------|
| Win Rate | 38% – 50% | <35% | >50% |
| Profit Factor | 1.3 – 2.0 | <1.1 | >2.0 |
| Max Drawdown | 8% – 18% | >25% | <8% |
| Trades / Month / Pair | 8 – 25 | <5 (too few) | 15-20 (sweet spot) |
| Avg Net Return (6mo) | 20% – 80% | negative | >100% |

**Why these ranges?** Because the filters are strict (ADX, trend, volatility, volume all must align), you'll get fewer but higher-quality trades. With 1.5R partial TP + breakeven trail + 4R runner, even a 40% win rate is highly profitable.

### Where this strategy WILL underperform:
- Long sideways / ranging markets (ADX filter helps but not perfectly)
- Major news events (volatility filter helps)
- Weekend low-liquidity periods on alts

### Where this strategy WILL excel:
- Trending markets (any direction)
- Post-breakout consolidation → continuation
- Strong macro moves (BTC bull/bear runs)

---

## Tuning Workflow (If Backtest Underperforms)

Run the backtest first. Then tune in this order:

1. **If too few trades** (< 5 per month):
   - Lower ADX min from 20 → 15
   - Reduce volume multiple from 1.1 → 1.0
   - Disable cooldown

2. **If win rate is low** (< 35%):
   - Tighten RSI range (e.g., longs 45-65 instead of 40-70)
   - Increase ADX min to 25
   - Enable trend filter if disabled

3. **If drawdown too large** (> 20%):
   - Reduce position size from 10% → 5%
   - Tighten SL multiplier from 1.5 → 1.2
   - Disable shorts (only trade longs in BTC)

4. **If profit factor < 1.2**:
   - Increase TP2 multiplier from 4.0 → 5.0 (let winners run more)
   - Increase TP1 from 1.5 → 2.0 (delay partial close)

---

## Setting Up Alerts (Live Trading)

1. Right-click the strategy on chart → "Add Alert"
2. Condition: `Long Entry` or `Short Entry`
3. Trigger: **"Once Per Bar Close"** (CRITICAL — prevents repaint)
4. Notification: webhook to your bot, app push, email, etc.

---

## Risk Management Rules

1. **Position size**: 10% of equity (default). Reduce to 5% for conservative trading.
2. **One position max** at any time (built-in via `pyramiding=0`).
3. **Commission**: 0.06% per side (Binance/Bybit futures realistic).
4. **Slippage**: 2 ticks factored in.
5. **Never risk more than 1-2% of account per trade** when sizing manually.

---

## Files

- `crypto_strategy_15m.pine` — Pine Script v5 strategy
- `STRATEGY_README.md` — This file

---

## Disclaimer

This is for educational and research purposes only. Cryptocurrency trading involves substantial risk of loss. Past backtest performance does not guarantee future results. Always paper trade for at least 4-6 weeks before risking real capital. Never trade with money you cannot afford to lose.
