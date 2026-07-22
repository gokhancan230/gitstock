# TradingView Indicator Playbook — AL/SAT/TUT Engine

Verified live on 2026-07-20 (BIST:THYAO test). This is the standard indicator battery GCstock sets up on TradingView and how each reading feeds the AL/SAT/TUT decision.

## ⚠️ Hard Constraints (learned from live testing)

1. **Indicator limit: ~5 studies per chart** on this TradingView plan. The 6th+ add fails silently (`success: false, new_study_count: 0`) AND may trigger an upgrade popup that covers the chart. If a popup appears, send `ui_keyboard` Escape to close it.
2. **Add indicators ONE AT A TIME** — parallel `chart_manage_indicator` calls race and fail. Sequential calls only.
3. **Full names required**: "Relative Strength Index" not RSI, "Moving Average Exponential" not EMA, "Bollinger Bands" not BB.
4. **Screenshot after symbol change**: wait_for_render can still capture a stale frame right after `chart_set_symbol` — if header/symbol mismatch, retake once.
5. Indicators persist on the chart between calls — check `chart_get_state` first; don't re-add what's already there.
6. **Timeframe desync (lived it on NVDA test)**: the chart can silently drop to 1-minute (popup/Escape side-effect). Symptom: BB bands ~$1 wide, EMA20≈EMA50≈price, tiny MACD. **SANITY CHECK every reading**: if BB width < 2% of price on a daily chart, values are junk. Fix: `chart_set_timeframe("D")`, re-read. The VISUAL pane may stay stuck on 1m even when the data layer is correct (chart_get_state says 1D, header shows 1m) — in that case cross-verify values against FMP and, if a chart image is needed, DRAW THE 1-YEAR CHART AS SVG from FMP `historical-price-eod-light` data instead of screenshotting.

## The 5-Slot Battery (use exactly this)

| Slot | Indicator (full name) | Inputs | Role |
|------|----------------------|--------|------|
| 1 | Moving Average Exponential | `{"length": 20}` | Short-term trend / dynamic support |
| 2 | Moving Average Exponential | `{"length": 50}` | Swing trend / key pullback zone |
| 3 | Bollinger Bands | default (20, 2σ) | Volatility envelope, extremes, squeeze |
| 4 | Relative Strength Index | default (14) | Momentum, overbought/oversold, divergence |
| 5 | MACD | default (12,26,9) | Trend momentum, crossovers, histogram |

**What's NOT on the chart (fetch from FMP instead):**
- 200-day MA → FMP `quote` returns `priceAvg200` (and `priceAvg50`) for free
- ATR (stop placement) → FMP `technicalIndicators` `standard-deviation`, or approximate from recent bar ranges via `data_get_ohlcv`
- ADX (trend strength) → FMP `technicalIndicators` `average-directional-index`

## Setup Sequence

```
1. tv_health_check                     → down? tv_launch, wait, re-check
2. chart_set_symbol("BIST:THYAO")      → or NASDAQ:AAPL etc.
3. chart_get_state                     → what studies already exist?
4. chart_manage_indicator × N          → ONLY missing ones, ONE AT A TIME
5. data_get_study_values               → all readings in one call (~500 bytes)
6. capture_screenshot (wait_for_render) → visual; retake if stale header
```

## Reading → Signal Map

Score each dimension −2…+2, then sum (range −10…+10):

### 1. Trend Structure (EMA 20/50 + FMP 200MA)
| Reading | Score |
|---------|-------|
| Price > EMA20 > EMA50 > 200MA | +2 (full bull stack) |
| Price > EMA50, but below EMA20 | +1 (uptrend, short-term cooling — pullback zone) |
| Price between EMA50 and 200MA, EMAs flat | 0 (no trend) |
| Price < EMA50 but > 200MA | −1 (correction) |
| Price < EMA20 < EMA50 < 200MA | −2 (full bear stack) |

### 2. Momentum (RSI 14)
| Reading | Score |
|---------|-------|
| RSI 55–70, rising | +2 |
| RSI 45–55 (neutral) | 0 |
| RSI > 75 | −1 (overbought — chase risk; not a short signal alone) |
| RSI 35–45, falling | −1 |
| RSI < 30 in an uptrend | +1 (oversold bounce setup) · in a downtrend −2 |
| **Divergence**: price new high, RSI lower high | −2 override |

### 3. MACD (12,26,9)
| Reading | Score |
|---------|-------|
| MACD > 0 AND MACD > Signal, histogram growing | +2 |
| MACD > 0 but MACD < Signal (bearish cross above zero) | −1 (momentum fading in uptrend) |
| MACD < 0 AND MACD < Signal | −2 |
| MACD < 0 but MACD > Signal (bullish cross below zero) | +1 (early turn) |

### 4. Bollinger Bands (20, 2σ)
| Reading | Score |
|---------|-------|
| Price rides upper band with expanding bands | +2 (strong trend, not "overbought") |
| Price at mid-band (basis) in uptrend | +1 (healthy reset) |
| Price at lower band + EMA50 confluence | +1 (high-quality entry zone) — flag as AL bölgesi |
| Band squeeze (narrowest in ~3 months) | 0 but FLAG: breakout imminent, direction unknown |
| Price closes below lower band on high volume | −2 (breakdown) |

### 5. Volume (from data_get_ohlcv or FMP)
| Reading | Score |
|---------|-------|
| Up-moves on above-avg volume, pullbacks on low volume | +2 |
| Volume flat/mixed | 0 |
| Rally on shrinking volume | −1 (suspect move) |
| Breakdown on heavy volume | −2 |

## Total Score → Signal

| Sum | Signal | Conviction |
|-----|--------|-----------|
| +6 … +10 | **AL** | High |
| +3 … +5 | **AL** (pullback'te) / **TUT** (pozisyondaysan) | Medium |
| −2 … +2 | **TUT / BEKLE** — entry only at marked confluence zones | Low |
| −5 … −3 | **SAT/AZALT** | Medium |
| −10 … −6 | **SAT** | High |

## Confluence Zones (where AL orders live)

The highest-probability entries are where 2+ indicator levels stack within ~1-2%:
- EMA50 + BB lower band → classic uptrend pullback buy
- EMA20 + BB basis → shallow pullback in strong trend
- 200MA + prior horizontal support → major-correction buy
- Always: entry at confluence, stop 1 ATR (or ~2-3%) below the LOWER edge of the confluence, targets at BB upper band → prior high → measured move.

## Worked Example (THYAO, 2026-07-20, live values)

```
Price ₺328 | EMA20 ₺329.58 | EMA50 ₺320.70 | BB 318.08 / 332.08 / 346.07
RSI 50.71 | MACD 4.33 vs Signal 6.30, Histogram −1.98

Trend: price > EMA50 but < EMA20 → +1 (uptrend, cooling)
RSI 50.7 neutral → 0
MACD positive but bearish cross → −1
BB: at mid-band, lower band ₺318 ≈ EMA50 ₺320.7 → CONFLUENCE ZONE ₺318-321 flagged → +1
Volume: mixed → 0

TOTAL: +1 → TUT/BEKLE
AL bölgesi: ₺318-321 (BB alt + EMA50 çakışması) + dönüş teyidi
SAT: ₺346 (BB üst) → ₺355 (52H zirve)
STOP: ₺310 (confluence altı, ~%2.5)
```

This scoring is mechanical input — final AL/SAT/TUT still weighs fundamentals, insider flow, earnings proximity, and higher-timeframe trend per SKILL.md.
