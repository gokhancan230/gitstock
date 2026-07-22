# GCstock Data Sources — Verified Tool Map

Tested and verified on 2026-07-20. Use this map to pull data; fallbacks listed in order.

## Price & Technicals

| Data | Primary Tool | Fallback |
|------|-------------|----------|
| Live quote, 52W range, 50/200MA | FMP `quote` (endpoint: quote) | TradingView `quote_get` |
| RSI/SMA/EMA/ADX | FMP `technicalIndicators` ⚠️ returns FULL history (~160KB) — grep/slice the saved file for latest values only | TradingView `data_get_study_values` (needs indicator visible on chart) |
| Daily price history | FMP `chart` endpoint `historical-price-eod-light` with `from_date`/`to_date` (keep range ≤ 3-6 months to limit size) | TradingView `data_get_ohlcv` with `summary: true` |
| Intraday (1H/4H) | FMP `chart` endpoints `intraday-1-hour`, `intraday-4-hour` | TradingView (switch timeframe) |
| Visual chart | TradingView `capture_screenshot` (region: "chart", wait_for_render: true) — requires TradingView Desktop running; check `tv_health_check` first, `tv_launch` if down | ASCII chart from price data |

## Earnings Calendar ⚠️ IMPORTANT WORKAROUND

- ❌ FMP `calendar` endpoint `earnings-company` (symbol-based) → **plan-gated, DO NOT USE**
- ❌ Massive `/benzinga/v1/earnings` → **plan-gated, DO NOT USE**
- ✅ **FMP `calendar` endpoint `earnings-calendar` with `from_date`/`to_date` range → WORKS.**
  Pull the date range (e.g., today + 4 weeks, limit 200), then filter the result for your symbol.
  Returns: date, epsEstimated, revenueEstimated, lastUpdated.
  Example verified result: AAPL 2026-07-30, EPS est $1.88, revenue est $108.8B.

## Fundamentals

| Data | Tool |
|------|------|
| P/E (via earnings yield), FCF yield, EV/EBITDA, ROIC, ROE, income quality, net debt | FMP `statements` endpoint `key-metrics-ttm` |
| Income statement, growth | FMP `statements` endpoints `income-statement`, `financial-statement-growth` |
| Ratios vs peers | Massive `/stocks/financials/v1/ratios` (ticker param) |

## Insider Transactions (SEC Form 4) — ✅ PRIMARY: Massive `/stocks/filings/vX/form-4`

> **FIXED 2026-07-21.** FMP `insiderTrades` went fully plan-gated (all symbols). **Massive Market Data has its own Form 4 endpoint and it is STRICTLY BETTER — use it as the primary source. Do not call FMP insiderTrades at all.**
> Regression-verified: UUUU CEO buy returned identical to FMP's prior data (Bhappu 74,000 @ $13.08 = $967,920; Hansen 4,000 @ $12.695 = $50,780).

```
call_api path: /stocks/filings/vX/form-4
params: {"tickers": "<SYMBOL>", "limit": 15, "sort": "filing_date.desc"}
cluster-buy scan: add "transaction_code": "P"   ← open-market PURCHASES only, the highest-value signal
```

**Why it beats FMP** — fields the old source didn't give:

| Field | Use in the insider framework |
|-------|------------------------------|
| `aff_10b5_one` (True/False) | **Direct mechanical-vs-discretionary flag.** True = 10b5-1 plan sale → routine, ignore. False on a P-purchase = genuine conviction buy. No more guessing. |
| `transaction_code` | P=open-market buy ⭐ · S=sale · M=option/RSU exercise · A=grant · G=gift |
| `footnotes` | Contains the literal plan text incl. **plan adoption date** ("10b5-1 plan adopted on 11/10/2025") → enables plan-change/cancellation detection, the skill's most informative signal |
| `shares_owned_following_transaction` | Remaining ownership → conviction scoring |
| `officer_title`, `is_director`, `is_officer`, `is_ten_percent_owner` | Role weighting (CEO/CFO buys score highest) |
| `transaction_value` | Pre-computed $ size |
| `direct_or_indirect` + `nature_of_ownership` | Filters out spouse/trust/401k noise |

**Historical pattern comparison now possible:** query `transaction_code: "P"` with a high limit and you get years of purchases — check whether insiders bought at prior lows and what the stock did next. (UUUU proof: cluster of buys at $4.08–4.25 in Feb–Mar 2025, stock later hit $27.90.)

**Parsing note:** output is CSV; `record_type` distinguishes `transaction` rows from `holding` rows — score only `transaction` rows. Price `0.0` on an M/A code = grant/vesting, not a trade.
- Key fields: transactionType (P-Purchase = open-market buy ⭐; S-Sale; M-Exempt = RSU vesting; F-InKind = tax withholding; G-Gift), price (0 = grant/vesting, not a trade), securitiesOwned (remaining), typeOfOwner
- Classification shortcuts: price=0 + M-Exempt/F-InKind → mechanical, ignore. S-Sale right after vesting dates → routine. P-Purchase → informative, investigate. 3+ distinct insiders with P-Purchase in ≤4 weeks → CLUSTER BUY.
- `insider-trade-statistics` endpoint gives buy/sell counts per quarter — quick pattern check.

## Turkish Stocks (BIST)

- TradingView: use `BIST:THYAO` format for charts
- FMP: `THYAO.IS` format; coverage thinner than US — label gaps honestly

## Rules

1. Never fabricate a number or date. Plan-gated/missing data → say "doğrulanamadı" and label estimates.
2. Cross-check price between FMP and TradingView when both available (verified match on test: $325.33 vs $325.73 intraday drift — acceptable).
3. Large tool outputs (technicalIndicators) get saved to a file — grep/slice it, don't re-call.
4. TradingView down? → `tv_launch`, wait, `tv_health_check`. Still down? Proceed with FMP + note chart unavailable.
