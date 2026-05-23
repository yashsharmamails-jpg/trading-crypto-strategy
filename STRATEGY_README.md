# Crypto Top-Down Multi-Timeframe Strategy (v3)

Professional-grade strategy that performs **top-down analysis** across 3 timeframes before entering a trade. Designed for crypto futures on **15-minute** or **1-hour** charts.

---

## What's New in v3

| Feature | Why It Matters |
|---------|---------------|
| **Daily (1D) Macro Bias** | Only trades aligned with the macro trend |
| **Configurable HTF Trend (1H/4H/1D)** | Confirms intermediate trend before entering |
| **Visual SL/TP/Entry Lines** | Horizontal lines with price labels — see your risk instantly |
| **Selectable R:R (1:1.5 or 1:2)** | Choose your style |
| **Top-Down Analysis Table** | Live dashboard showing all 3 timeframe biases |
| **Works on 15m AND 1h Charts** | Strategy auto-adjusts |

---

## Top-Down Analysis Logic

```
TIER 1: DAILY (1D) — Macro Bias
    Is price above/below 1D EMA 50?
    Only longs in daily uptrend, shorts in downtrend
              |
              v
TIER 2: HTF TREND (1H / 4H / Daily — selectable)
    HTF EMA 50 vs EMA 200 alignment
    Only trades when HTF trend confirms direction
              |
              v
TIER 3: CHART TF (15m or 1h) — Entry Trigger
    EMA 9/21 cross + RSI + MACD + ADX + Volume
    Precise entry timing
              |
              v
        TRADE ENTRY
```

### Recommended HTF Combinations

| Chart TF | Best HTF Setting |
|----------|------------------|
| **15-minute** | 4H (`240`) + Daily bias |
| **1-hour** | Daily (`D`) + 4H bias |

---

## Visual Lines on Chart

When a trade triggers, the strategy automatically draws:

| Line | Color | Purpose |
|------|-------|---------|
| **Entry Line** | Blue dashed | Your entry price (LONG/SHORT label) |
| **Stop Loss** | Red solid | SL price (with $ value label) |
| **Take Profit** | Green solid | TP price (with $ value + R:R label) |

Lines extend right and clear automatically when the trade closes.

---

## Entry Rules (All Must Align)

### LONG Entry
1. Daily: Price above 1D EMA 50 (macro bull)
2. HTF (4H/1D): Close > EMA50 > EMA200 (strong uptrend)
3. Chart TF: EMA 9 crosses above EMA 21
4. Chart TF: RSI between 40-70
5. Chart TF: MACD histogram positive
6. Chart TF: ADX > 20 (trending)
7. Chart TF: Volume > 1.1x its 20-MA
8. Chart TF: ATR not in extreme spike (< 2.5x avg)
9. Cooldown: 8+ bars since last trade

### SHORT Entry
Mirror image: bearish daily, bearish HTF, EMA cross down, RSI 30-60, MACD negative, etc.

---

## Risk:Reward Selector

In strategy settings → "Risk:Reward" group:

| Setting | SL | TP | Break-even Win Rate |
|---------|-----|-----|-------------------|
| **1:1.5** | 1.5 × ATR | 2.25 × ATR | 40% |
| **1:2** | 1.5 × ATR | 3.0 × ATR | 34% |

At 1:2 R:R you only need 34% win rate to break even.

---

## How to Use on TradingView

### Step 1 — Add Strategy
1. Open TradingView → Pine Editor
2. Paste contents of `crypto_strategy_15m.pine`
3. Click "Add to Chart"

### Step 2 — Choose Chart Timeframe
- For 15m signals → set chart to **15m**, leave HTF at **4H (240)**
- For 1h signals → set chart to **1h**, change HTF to **Daily (D)**

### Step 3 — Test on Major Crypto Futures

| Tier 1 (Most Liquid) | Tier 2 (High Volume) | Tier 3 (Volatile Alts) |
|---------------------|----------------------|------------------------|
| BINANCE:BTCUSDT.P | BINANCE:BNBUSDT.P | BINANCE:SOLUSDT.P |
| BINANCE:ETHUSDT.P | BINANCE:XRPUSDT.P | BINANCE:DOGEUSDT.P |
| | BINANCE:ADAUSDT.P | BINANCE:AVAXUSDT.P |
| | BINANCE:LINKUSDT.P | BINANCE:MATICUSDT.P |

### Step 4 — Configure
- **R:R**: Pick `1:2` (recommended) or `1:1.5`
- **HTF**: `240` for 15m chart, `D` for 1h chart
- **Backtest Range**: Last 6-12 months

### Step 5 — Read the Top-Down Table

```
TOP-DOWN ANALYSIS    BTCUSDT.P
-----------------------------
Daily Bias           BULL
4H Trend             BULL
HTF RSI              58.3
15m Signal           WAIT LONG
ADX                  22.1 ok
R:R Ratio            1:2
Net Profit           +1245.32
Win % / Trades       44.2% / 86
```

---

## Per-Pair Recommended Settings

| Pair | Chart TF | HTF | SL Mult | R:R | Notes |
|------|----------|-----|---------|-----|-------|
| **BTCUSDT.P** | 15m | 4H | 1.5 | 1:2 | Most reliable |
| **ETHUSDT.P** | 15m | 4H | 1.5 | 1:2 | Strong trends |
| **BNBUSDT.P** | 15m | 4H | 1.5 | 1:2 | Default |
| **SOLUSDT.P** | 15m | 4H | 1.8 | 1:2 | Wider SL |
| **AVAXUSDT.P** | 15m | 4H | 1.8 | 1:1.5 | Tighter R:R |
| **XRPUSDT.P** | 15m | 4H | 1.5 | 1:1.5 | More chop |
| **MATICUSDT.P** | 15m | 4H | 1.8 | 1:2 | Default |
| **DOGEUSDT.P** | 15m | 4H | 2.0 | 1:1.5 | Wider SL, smaller TP |
| **LINKUSDT.P** | 15m | 4H | 1.5 | 1:2 | Default |
| **ADAUSDT.P** | 15m | 4H | 1.5 | 1:1.5 | Tighter R:R |

For 1h chart, change HTF to `D` (Daily); same SL multipliers.

---

## Realistic Performance Expectations

| Metric | Expected Range | Considered Good |
|--------|---------------|-----------------|
| Win Rate | 40-55% | >45% |
| Profit Factor | 1.4-2.2 | >1.5 |
| Max Drawdown | 6-15% | <10% |
| Trades / Pair / Month | 5-15 | 8-12 (sweet spot) |
| Avg Net Return (6mo) | 25-90% | varies by pair |

The 3-tier filter (Daily + HTF + Chart TF) is intentionally strict. Quality over quantity.

---

## Setting Up Live Alerts

1. Right-click strategy on chart → "Add Alert"
2. Condition: `Long Entry` or `Short Entry`
3. Trigger: **Once Per Bar Close** (NEVER "every tick" — causes repaint)

---

## Tuning Workflow

| Symptom | Fix |
|---------|-----|
| Too few trades (<3/month) | Lower ADX min to 15, disable Daily bias |
| Win rate <35% | Tighten RSI ranges (longs 45-65, shorts 35-55) |
| Big drawdown | Reduce position size to 5%, disable shorts |
| Low profit factor | Switch from 1:1.5 to 1:2 R:R |
| Whipsaw losses | Increase HTF to Daily, increase ADX min to 25 |

---

## Files

- `crypto_strategy_15m.pine` — Pine Script v5
- `STRATEGY_README.md` — This documentation

---

## Disclaimer

For educational purposes only. Crypto trading is high-risk. Past results don't guarantee future performance. Paper trade for 4-6 weeks before risking real capital.
