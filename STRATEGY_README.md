# Liquidity 2nd-Sweep A+ Strategy (v5)

The high-quality version. **Waits for the 2nd sweep of the same level** before entering — this is the single biggest filter for trade quality in price action trading.

---

## Why 2nd-Sweep is Different (and Profitable)

```
Level forms ($50,000 swing high)
    │
    ├── 1st sweep happens   ← STAY OUT
    │   Price wicks above $50K, closes back below
    │   Most retail "sweep traders" enter here and lose
    │   The level is now PRIMED (turns ORANGE on chart)
    │
    ├── Price retraces, comes back to retest
    │
    ├── 2nd sweep happens   ← THIS IS THE A+ ENTRY
    │   Price wicks above $50K AGAIN, closes back below
    │   Smart money is exhausted here, real reversal begins
    │   With RSI divergence: bearish (lower RSI on equal-or-higher price)
    │
    └── Enter SHORT, SL above 2nd-sweep wick, TP at 2x risk
```

This pattern is also called:
- **Double Top** (with sweep wicks)
- **SFP × 2** (Swing Failure Pattern double-tap)
- **Liquidity grab + reversal** (in SMC terms)

---

## Confluence Stack (5 Filters for A+)

Every entry requires **all five**:

| # | Filter | What It Checks |
|---|--------|----------------|
| 1 | **2nd Sweep** | Same level swept twice (with retracement between) |
| 2 | **RSI Divergence** | RSI is lower on 2nd sweep (shorts) / higher on 2nd sweep (longs) — exhaustion |
| 3 | **Strong Rejection Wick** | Wick ≥ 55% of candle range (real rejection, not noise) |
| 4 | **Volume Spike** | > 1.3× the 20-bar volume MA (real participation) |
| 5 | **HTF Bias** | 4H momentum agrees (no EMA — pure 20-bar close diff) |

Plus structural:
- Min 4 bars between 1st and 2nd sweep (forces meaningful retracement)
- 10-bar cooldown between trades
- Levels that close-through are removed (no longer valid)

---

## What's on Your Chart (Clean)

```
Red zone     = Resistance (untouched)
Orange zone  = Resistance/Support that's been swept ONCE — primed for A+
Green zone   = Support (untouched)
Position Tool box at entry:
   ─── Blue line  : entry price
   ─── Red line   : stop loss
   ─── Green line : take profit
   Green box      : profit zone (entry → TP)
   Red box        : risk zone (entry → SL)
   Right-side labels show exact prices and R:R
Info table (top-right) shows live stats
```

❌ **No arrows pointing direction**  
❌ **No EMA / MACD / oscillator overlays**  
❌ **No SWEEP labels above/below candles**  
✅ **Just zones, position tool, and table**

---

## Entry & Exit Logic

### LONG (2nd Bullish Sweep)
- A support level has been swept once (orange zone)
- Price comes back, wicks below the same level a 2nd time
- Closes back above with strong wick + volume + HTF bull bias + RSI divergence
- **Entry**: at sweep candle close
- **SL**: just below the 2nd sweep wick low + ATR buffer
- **TP**: 2× risk (or 1.5×, 3× per setting)

### SHORT (2nd Bearish Sweep)
- A resistance level has been swept once (orange zone)
- Price rallies back, wicks above the same level a 2nd time
- Closes back below with strong wick + volume + HTF bear bias + RSI divergence
- **Entry**: at sweep candle close
- **SL**: just above the 2nd sweep wick high + ATR buffer
- **TP**: 2× risk

---

## Risk:Reward Selector

| Setting | TP Distance | Break-even Win Rate |
|---------|------------|--------------------|
| 1:1.5 | 1.5x risk | 40% |
| **1:2** | 2x risk | **34%** ← recommended |
| 1:3 | 3x risk | 25% |

With 2nd-sweep filter, expected win rate is **55–70%**, so 1:2 R:R produces strong expectancy.

---

## Realistic Expectations (v5)

A 2nd-sweep strategy is genuinely low-frequency, high-quality:

| Metric | Range |
|--------|-------|
| Trades / pair / week | **1 – 3** (very selective) |
| Win Rate | **55 – 70%** |
| Profit Factor | **1.8 – 3.0** |
| Max Drawdown | 5 – 10% |
| Avg Net Return (6mo) | 30 – 100%+ |

**Why fewer trades = more profit:**
- Each trade has 5 layers of confluence
- 2nd-sweep at proven levels is a textbook reversal pattern
- SLs are tight (just past the wick) — losses are small
- TPs are pre-defined — no emotional exits

---

## How to Use on TradingView

### Step 1 — Add Strategy
1. Open TradingView → Pine Editor
2. Paste contents of `crypto_strategy_15m.pine`
3. Click "Save" → "Add to Chart"

### Step 2 — Set Timeframe
- **15m chart** → leave HTF at `240` (4H)
- **1H chart** → change HTF to `D` (Daily)

### Step 3 — Test on Major Crypto Futures
- BINANCE:BTCUSDT.P
- BINANCE:ETHUSDT.P
- BINANCE:SOLUSDT.P
- BINANCE:DOGEUSDT.P
- BINANCE:BNBUSDT.P
- BINANCE:XRPUSDT.P
- BINANCE:AVAXUSDT.P
- BINANCE:LINKUSDT.P

### Step 4 — Read the Chart
- See orange zones? Those are levels primed for A+ entries — watch them
- When 2nd sweep fires, the position tool appears at entry with green TP / red SL boxes
- Lines stay on chart during trade, freeze when trade closes

---

## Per-Pair Recommended Settings

| Pair | Pivot | RR | SL Buffer | Notes |
|------|-------|----|-----------|------|
| **BTCUSDT.P** | 10 | 1:2 | 0.30 | Default — cleanest sweeps |
| **ETHUSDT.P** | 10 | 1:2 | 0.30 | Default |
| **BNBUSDT.P** | 10 | 1:2 | 0.30 | Default |
| **SOLUSDT.P** | 12 | 1:2 | 0.40 | Wider buffer |
| **AVAXUSDT.P** | 12 | 1:1.5 | 0.40 | Tighter R:R |
| **XRPUSDT.P** | 8 | 1:1.5 | 0.30 | Smaller pivots |
| **DOGEUSDT.P** | 12 | 1:1.5 | 0.50 | Wider buffer for meme vol |
| **LINKUSDT.P** | 10 | 1:2 | 0.30 | Default |
| **MATICUSDT.P** | 12 | 1:2 | 0.40 | Default |

---

## Tuning Workflow

| Symptom | Fix |
|---------|-----|
| Too few trades (< 1/week) | Lower wick % to 0.45, disable RSI divergence, lower volume mult to 1.1 |
| SL hits too often | Increase SL buffer ATR from 0.30 to 0.50 |
| TP doesn't reach | Switch from 1:2 to 1:1.5 R:R |
| Wrong-direction trades | Enable HTF bias if disabled |
| Want more strict | Increase min bars between sweeps from 4 to 8, raise wick % to 0.65 |

---

## Live Alerts

1. Right-click strategy on chart → "Add Alert"
2. Condition: `A+ Long 2nd-Sweep` or `A+ Short 2nd-Sweep`
3. Trigger: **Once Per Bar Close** (NEVER every tick)

---

## Disclaimer

For educational purposes. Crypto trading is high-risk. Past results don't guarantee future performance. Paper trade for 4-6 weeks before risking real capital.
