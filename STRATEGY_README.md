# Crypto Multi-Confluence 15-Minute Strategy

## Strategy Overview

A multi-indicator confluence strategy designed for crypto pairs on the **15-minute timeframe**. It combines trend-following (EMA crossover), momentum (RSI + MACD), and volatility (ATR) to generate high-probability entries with dynamic risk management.

---

## Strategy Logic

### Indicators Used

| Indicator | Settings | Purpose |
|-----------|----------|---------|
| EMA 9 / EMA 21 | Fast/Slow crossover | Trend direction & entry trigger |
| RSI 14 | Oversold 30 / Overbought 70 | Momentum filter (avoid extremes) |
| MACD 12/26/9 | Histogram direction | Momentum confirmation |
| ATR 14 | Dynamic multiplier | SL/TP calculation |
| Volume MA 20 | Volume vs average | Volume confirmation filter |

### Entry Rules

#### LONG Entry (all must be true):
1. EMA 9 crosses ABOVE EMA 21
2. RSI is between 30 and 70 (not overbought/oversold)
3. MACD Histogram is POSITIVE (bullish momentum)
4. Volume is above its 20-period moving average
5. No existing position open

#### SHORT Entry (all must be true):
1. EMA 9 crosses BELOW EMA 21
2. RSI is between 30 and 70 (not overbought/oversold)
3. MACD Histogram is NEGATIVE (bearish momentum)
4. Volume is above its 20-period moving average
5. No existing position open

### Exit Rules (SL / TP)

| | Long | Short |
|---|---|---|
| **Stop Loss** | Entry Price - (1.5 x ATR) | Entry Price + (1.5 x ATR) |
| **Take Profit** | Entry Price + (2.5 x ATR) | Entry Price - (2.5 x ATR) |
| **Risk:Reward** | ~1:1.67 | ~1:1.67 |

---

## How to Backtest on TradingView (Step-by-Step)

### 1. Add the Strategy
1. Open [TradingView](https://www.tradingview.com)
2. Open the **Pine Editor** (bottom panel)
3. Delete any existing code
4. Copy & paste the entire contents of `crypto_strategy_15m.pine`
5. Click **"Add to Chart"**

### 2. Configure the Chart
1. Set timeframe to **15 minutes**
2. Open the following pairs (one at a time):
   - `SOLUSDT.P` (Solana Perpetual)
   - `BTCUSDT.P` (Bitcoin Perpetual)
   - `ETHUSDT.P` (Ethereum Perpetual)
   - `DOGEUSDT.P` (Dogecoin Perpetual)

### 3. Set Backtest Range (6 Months)
1. Click the **gear icon** on the strategy in your chart
2. Go to **"Properties"** tab
3. Under **"Date Range"**, check "Use specific dates"
4. Set the range to the last 6 months (e.g., Nov 2025 – May 2026)

### 4. Review Results
Click the **"Strategy Tester"** tab at the bottom to see:
- **Overview**: Net Profit, Win Rate, Profit Factor, Max Drawdown
- **Performance Summary**: Detailed statistics
- **List of Trades**: Every entry/exit with P&L
- **Equity Curve**: Visual profit/loss over time

---

## Expected Backtest Performance (Estimates)

> **Note:** These are estimated ranges based on strategy logic and typical crypto market behavior. Actual results depend on market conditions during the backtest period.

| Metric | Expected Range |
|--------|---------------|
| **Win Rate** | 38% – 52% |
| **Profit Factor** | 1.3 – 2.1 |
| **Risk:Reward** | 1:1.67 |
| **Max Drawdown** | 8% – 18% |
| **Avg Trades/Day** | 2 – 6 per pair |
| **Net Return (6mo)** | 15% – 60%+ (varies by pair) |

### Per-Pair Expectations

| Pair | Volatility | Expected Behavior |
|------|-----------|-------------------|
| **BTCUSDT.P** | Medium | Fewer trades, more reliable signals |
| **ETHUSDT.P** | Medium-High | Good balance of frequency and quality |
| **SOLUSDT.P** | High | More trades, wider ATR stops, higher variance |
| **DOGEUSDT.P** | Very High | Most trades, highest variance, needs wider SL |

---

## Recommended Settings by Pair

| Pair | SL Multiplier | TP Multiplier | Notes |
|------|--------------|--------------|-------|
| BTCUSDT.P | 1.5 | 2.5 | Default works well |
| ETHUSDT.P | 1.5 | 2.5 | Default works well |
| SOLUSDT.P | 1.8 | 3.0 | Slightly wider for volatility |
| DOGEUSDT.P | 2.0 | 3.5 | Wider stops needed for meme coin volatility |

---

## Parameter Tuning Guide

### If Win Rate is Too Low:
- Increase RSI filter range (e.g., 35-65 instead of 30-70)
- Add the Volume Filter if not enabled
- Try enabling the Session Filter to trade active hours only

### If Too Few Trades:
- Remove the Volume Filter
- Widen RSI range back to 30-70
- Consider using EMA 8/18 instead of 9/21

### If Drawdown is Too High:
- Reduce position size (default is 10% of equity)
- Tighten SL multiplier to 1.2x ATR
- Only trade Long in uptrends (disable shorts)

---

## Risk Management Guidelines

1. **Position Size**: Default is 10% of equity per trade. Reduce to 5% for conservative approach.
2. **Max Concurrent Trades**: Strategy only allows 1 position at a time (built-in).
3. **Commission**: 0.06% per trade is factored in (typical for Binance/Bybit futures).
4. **Slippage**: 2 ticks of slippage is included in backtest.

---

## Setting Up Alerts (Live Trading)

1. After adding the strategy to your chart, right-click the strategy name
2. Select **"Add Alert"**
3. Choose condition: `Long Entry Signal` or `Short Entry Signal`
4. Set notification method (app, email, webhook)
5. Set alert to trigger **"Once Per Bar Close"** (important!)

### Alert Messages Include:
- **Long**: "LONG Signal: EMA Cross Up + RSI OK + MACD Positive + Volume Confirmed"
- **Short**: "SHORT Signal: EMA Cross Down + RSI OK + MACD Negative + Volume Confirmed"

---

## Strategy Strengths

- **Multi-confluence**: 4 independent confirmations reduce false signals
- **Dynamic SL/TP**: ATR adapts to current volatility (no fixed pip stops)
- **Volume filter**: Avoids low-liquidity fakeouts
- **Clean R:R**: 1:1.67 means you can be wrong 40% of the time and still profit
- **No repainting**: All signals calculated on bar close

## Strategy Weaknesses

- **Lagging entries**: EMA crossover is inherently lagging (may miss start of moves)
- **Choppy markets**: Sideways/ranging conditions will produce whipsaws
- **Single timeframe**: No higher-TF trend confirmation (can add manually)

---

## Optional Enhancements

If you want to improve this further:
1. Add a **200 EMA** trend filter (only long above 200 EMA, only short below)
2. Add **higher timeframe confirmation** (e.g., 1H trend direction)
3. Add a **trailing stop** instead of fixed TP
4. Add **partial TP** (close 50% at 1.5x ATR, trail the rest)

---

## Files

- `crypto_strategy_15m.pine` — The full Pine Script v5 strategy code
- `STRATEGY_README.md` — This documentation file

---

*Strategy created for educational and backtesting purposes. Always paper trade before risking real capital. Past performance does not guarantee future results.*
