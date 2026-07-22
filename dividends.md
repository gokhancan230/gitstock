# Dividend Module — Temettü Bölümü (ZORUNLU her tam analizde)

Verified live 2026-07-21 (KO returns data, AMZN correctly returns none).

## Data source

```
FMP `calendar` endpoint: dividends-company, symbol: <SYM>, limit: 5
```

Returns per payment: `date` (ex-date), `recordDate`, `paymentDate`, `declarationDate`, `dividend`, `adjDividend`, `yield`, `frequency`.

Verified KO output: frequency `Quarterly`, last three $0.53 (Eyl'26) / $0.53 (Haz'26) / $0.53 (Mar'26), prior two $0.51 → **a raise from $0.51 to $0.53 in early 2026 is visible in the series.** Always pull 5 so the raise/cut is detectable, but display the last 3.

## Handling a non-payer

`{"status":"not_found"}` on this endpoint means no dividend records. **Cross-check before declaring it:** if `key-metrics-ttm` also carries no dividend yield, write **"Temettü ödemiyor"** (a fact). If the two disagree, or the symbol is thinly covered (many BIST names), write **"Doğrulanamadı"** instead — never assume absence of data equals absence of a dividend.

Verified: AMZN returns not_found AND has no dividend yield in key-metrics → "Temettü ödemiyor" is safe to state.

## PLACEMENT: a strip directly under the report header

The dividend block is **not** buried mid-report — it sits immediately below the header (above the signal banner), as a 4-cell strip with a big VAR / YOK badge:

```
┌──────┬──────────────┬─────────────────────┬──────────────────┬───────────────┐
│ VAR  │ Ödeme sıklığı│ Son 3 ödeme         │ Sonraki ödeme    │ Temettü verimi│
│(yeşil│ Çeyreklik    │ $0.53 (15 Eyl) ·    │ 1 Eki 2026       │ %2.5          │
│ /gri)│              │ $0.53 (15 Haz) ·    │ ($0.53, ex:15Eyl)│ rapor anı fiy.│
│      │              │ $0.53 (13 Mar)      │                  │               │
└──────┴──────────────┴─────────────────────┴──────────────────┴───────────────┘
```

Badge: **VAR** (green) / **YOK** (grey). Four cells, always in this order: sıklık · son 3 ödeme (ex-tarihleriyle) · sonraki ödeme · verim.

**Sonraki ödeme:** the same `dividends-company` call returns FUTURE-dated records — a record whose `paymentDate` is after today IS the next payment. Report `paymentDate` as the headline date with the ex-date and amount beneath (the ex-date is what matters for eligibility: you must own the share before it). If no future record exists, write "açıklanmadı" and, when the cadence is regular, add the expected window as ÇIKARIM (e.g. "~Kasım, geçmiş ritme göre").

Below the strip, one caption line: the VERİ tag, the cross-check note, and the one-sentence analytical reading.

## What each field must contain

- **Ödeme sıklığı**: Çeyreklik / 6 Aylık / Yıllık / Aylık — from the `frequency` field
- **Son 3 ödeme**: amount + ex-date each, newest first
- **Sonraki ödeme**: payment date + amount + ex-date, or "açıklanmadı"
- **Temettü verimi**: recomputed against the report-time price (see below)
- **Trend** (in the caption): artırdı / sabit / kesti — detected from the 5 records pulled

**Critical:** compute the yield against the **report-time price**, not the API's own `yield` field — that field is computed at the ex-date price and drifts. Show the formula: `(yıllıklandırılmış temettü / rapor anındaki fiyat) × 100`.

**Frequency → annualization:** Quarterly ×4 · Semi-Annual ×2 · Annual ×1 · Monthly ×12. State which multiplier was used.

## Analytical reading (not just the numbers)

- **Raise streak** = management confidence + FCF comfort. A raise while FCF is tight is a stronger signal than a raise from a cash pile.
- **Cut or suspension** = a red flag that usually precedes or confirms fundamental deterioration — surface it prominently, it outranks most technical signals.
- **Non-payer**: say WHY it fits the story. A company reinvesting 100% (heavy capex, negative FCF) is a *coherent* non-payer; a mature cash-rich company that pays nothing is a capital-allocation question.
- **Yield vs the stock's own history**: an unusually high yield is often the market pricing in a cut, not a gift.
- Tie the payout to the FCF finding from `deepdive_fundamentals.md` — a dividend not covered by free cash flow is being funded by debt or asset sales.

## Report-time price stamp (applies to the WHOLE report)

Every report must make the **as-of moment** unmistakable, because every level in it (entry, stop, targets, yield, R/R) is anchored to that price:

```
Fiyat: $XXX.XX  ·  Rapor anı: DD Ay YYYY, HH:MM  ·  [Piyasa açık / kapalı]
```

Put it in the header AND next to the price in the stats strip. Use the quote's own `timestamp` field (unix → local time) rather than the wall clock, so the stamp reflects when the data was actually captured. If the market was open, note that intraday levels move.
