# Forward-Looking Data Layer — Predicting Future Movement

Sources tested live 2026-07-21 on AMZN. This layer feeds the report's **probability module, valuation anchors, and catalyst timeline** — the parts that look ahead rather than describe the past.

## ✅ WORKING — use these

### 1. Analyst Forward Estimates (BIGGEST WIN) — FMP `analyst` / `financial-estimates`
```
endpoint: financial-estimates, symbol: <SYM>, period: "annual", limit: 4
```
Returns per fiscal year: **revenueLow/Avg/High, ebitdaAvg, netIncomeAvg, epsLow/epsAvg/epsHigh, numAnalystsEps**.

**This replaces guessed DCF inputs with a real consensus distribution.** Verified AMZN:

| Yıl | EPS düşük | EPS ort. | EPS yüksek | Analist |
|-----|----------:|---------:|-----------:|--------:|
| 2027 | 8.46 | **10.10** | 11.31 | 43 |
| 2028 | 9.92 | 13.09 | 15.44 | 26 |
| 2029 | 14.78 | 15.59 | 16.31 | 24 |
| 2030 | 18.46 | 19.48 | 20.38 | 14 |

**How to use:** build the fair-value RANGE from `epsLow × düşük çarpan` / `epsAvg × baz çarpan` / `epsHigh × yüksek çarpan`. The EPS leg becomes VERİ (consensus), only the multiple leg stays ÇIKARIM. Also report `numAnalystsEps` — a 43-analyst consensus is far more reliable than a 14-analyst one, and thin coverage should cut the confidence score.

⚠️ Watch for a **consensus-vs-price contradiction**: if the implied forward P/E on next-year consensus is much lower than the trailing P/E, the market is discounting the estimates — say so explicitly rather than treating consensus as truth.

### 2. Analyst Rating Changes — FMP `analyst` / `grades`
```
endpoint: grades, symbol: <SYM>, limit: 12
```
⚠️ **Output is huge (~200KB, 1400+ records) and gets saved to a file.** Parse it with python (`json.load`, slice the first 10-15), never dump it into context.

Fields: `date, gradingCompany, previousGrade, newGrade, action` (upgrade / downgrade / maintain / initialise).

**Signal value:** `maintain` rows are noise. What matters is **upgrade/downgrade clusters** and *initiations*. A run of pure "maintain" (AMZN's last 14 = all maintain) means **no analyst is changing their mind** → the street is in wait-and-see mode, usually ahead of a binary event. That itself is a report-worthy observation.

### 3. Short Interest — Massive `/stocks/v1/short-interest`
```
params: {"ticker": "<SYM>", "limit": 4, "sort": "settlement_date.desc"}
```
Returns `settlement_date, short_interest, avg_daily_volume, days_to_cover` on a two-week cadence.

**How to read (verified AMZN):** 100.3M short on 2026-06-30, days-to-cover 1.23.
- **Short % of float** = short_interest / shares outstanding. AMZN ≈ 0.93% → negligible bearish positioning, **no squeeze fuel**.
- **days_to_cover**: <2 easy exit · 3-5 crowded · >7 squeeze potential
- **Trend across the 4 prints matters more than the level** — rising short interest into a rising price = disagreement building.

### 4. Consensus Price Targets — FMP `analyst` / `price-target-consensus`
`targetHigh / targetLow / targetConsensus / targetMedian`. Report the **width** of the band, not just the consensus: AMZN $175–$335 around $309 consensus = the street cannot agree on the capex thesis → drives the "analist uzlaşması" input of the confidence score DOWN.

### 5. Earnings Calendar (already in data_sources.md)
Date-range `earnings-calendar` + filter → next earnings date, EPS and revenue estimates. The single most reliable forward catalyst.

## ❌ PLAN-GATED — do not burn calls

| Source | Status |
|--------|--------|
| Massive options chain `/v3/snapshot/options/{ticker}` (IV, delta, open interest) | **403 NOT_AUTHORIZED** — tested 2026-07-21 |
| Massive `/benzinga/v1/earnings`, `/benzinga/v2/news` | plan-gated |
| FMP `insiderTrades` | plan-gated → use Massive form-4 instead (see data_sources.md) |
| FMP `calendar` `earnings-company` (symbol-based) | plan-gated → use date-range workaround |

> **If options data ever becomes available**, it is the single biggest upgrade to this skill: option **delta ≈ market-implied probability of finishing beyond a strike**, which would convert the probability module from ÇIKARIM to market-derived VERİ, and IV would replace the historical-volatility estimate. Worth re-testing after any plan change.

## How this layer changes the report

| Report module | Before | After |
|---------------|--------|-------|
| Fair-value range | EPS guessed by analyst (me) | **Consensus epsLow/Avg/High × multiple** — EPS leg is now VERİ |
| Olasılık analizi | pure ÇIKARIM | still ÇIKARIM, but anchored to short interest + estimate dispersion + consensus width |
| Tahmin güveni | judgment | `numAnalystsEps` and target-band width feed it numerically |
| Katalizör listesi | earnings only | + rating-change clusters, + short-interest build-up |
| Yeni kutu: **Konumlanma** | — | Short % of float, days-to-cover, trend across 4 prints |

**Honesty rule stays:** consensus estimates are other people's forecasts, not facts about the future. Tag them **VERİ (konsensüs)** — verified as *what analysts currently project* — and keep the multiple assumption and any scenario weighting as ÇIKARIM.
