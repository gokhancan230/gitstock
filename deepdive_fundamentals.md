# Deep-Dive Fundamentals Layer — Analyst-Grade Depth for GCstock

This layer adds equity-research depth to a GCstock report, ported from the GCnewstock deep-dive (tested on ADBE/NFLX/ISRG, 2026-07-20). GCstock's daily AL/SAT/TUT decision sheet stays exactly as is — this is an ADDED fundamental/valuation section, placed AFTER the technical decision blocks and BEFORE the sources footer.

## When to include it

- **Always** for a full single-stock analysis ("X analiz et", "X derinlemesine incele").
- **Skip / collapse** for a quick technical check ("X bugün al mı?", pure day-trade timing) unless the user asks for depth — don't slow a scalp question with a DCF.
- Portfolio scans: include a COMPACT version (valuation verdict + fair-value range + one-line thesis) per holding, not the full 7 blocks.

## Three-way evidence tagging (upgrade from VERİ/YORUM)

The technical part keeps VERİ/YORUM. The deep-dive part uses THREE tags so opinion never masquerades as fact:

- **VERİ** — verified number/fact with a source (filing, FMP endpoint, named article + date)
- **ÇIKARIM** — reasoned inference; say from what data
- **SPEKÜLASYON** — scenario/opinion, clearly flagged

Unverifiable metric → **"Doğrulanamadı"**, never silently filled. Never fabricate a number, ticker, or date. The whole DCF block is ÇIKARIM by construction.

## The 7 deep-dive blocks (same order as GCnewstock)

1. **İş Modeli** — how it actually makes money, revenue segments with % mix (FMP `revenue-product-segmentation` / `revenue-geographic-segments` where available), unit economics, is the model durable or eroding.

2. **Finansal Sağlık** — operating cash flow, free cash flow **trend (multi-year, not one print)**, debt load + maturity/interest coverage. FMP `statements`: `key-metrics-ttm`, `income-statement`, cash-flow. Flag earnings-quality gaps (OCF < net income = receivable/inventory build).

3. **Değerleme — iki bacak, ikisi de zorunlu:**
   - **Çarpanlar vs emsaller**: P/E, EV/Revenue, P/B (+ EV/EBITDA where meaningful) vs 2-4 NAMED peers AND the company's own history. ⚠️ Sanity-check `enterpriseValueTTM` against marketCap first (FMP returned $5.5T EV for NFLX once) — if broken, drop EV multiples and say so.
   - **Kaba DCF / içsel değer**: show assumptions EXPLICITLY (revenue growth path, margin, discount rate ~8-10%, terminal growth ~2-3%) and output a **fair-value RANGE (bear / baz / boğa)** — never one magic number. Then answer: cheap or expensive **relative to its growth**? Whole block = ÇIKARIM.

4. **Makro & Rekabet** — rate sensitivity, regulation, main competitors + share shifts, and name **the single biggest threat** explicitly.

5. **Katalizörler** — obvious (earnings/product dates, VERİ only) AND hidden/underappreciated (index inclusion, forced-seller exhaustion, insider cluster buys, a segment the street isn't modeling). Say WHY each is underappreciated.

6. **Riskler (sıralı)** — regulatory, concentration (customer/segment/geo), competitive, execution, valuation. RANK them by severity; no boilerplate padding.

7. **Yatırım Tezi** — strongest honest **BOĞA** case and strongest honest **AYI** case side by side, then the verdict:
   - **Asimetri**: is risk/reward asymmetric at today's price? Say roughly how much upside vs downside using the DCF range (e.g., "baz $350 vs fiyat $310 → +%13 yukarı / −%X aşağı → POZİTİF asimetri").
   - **İzlenecek metrikler**: the 3-5 numbers that would confirm or break the thesis (e.g., "net yeni ARR · FCF marjı · segment X büyümesi").

## HTML components to reuse (from the GCnewstock report)

Match GCstock's existing color tokens and box styles. Key visual pieces:

- **`fvbar` — Fair-value range bar**: horizontal bar showing bear→base→bull fair-value band with a marker for CURRENT price. Instantly shows cheap/expensive. This is the signature visual — always include it.
- **`bull` / `bear` thesis cards**: two side-by-side cards, green-tinted bull vs red-tinted bear, equal length (bear gets equal effort — a pitch without a real bear case is marketing).
- **Asimetri pill**: POZİTİF / NÖTR / NEGATİF badge with the up-vs-down math beneath.
- **Peer multiple mini-table**: company vs 2-4 named peers vs own-history, P/E / EV/Rev / P/B columns.
- **Revenue-mix bar** (`mix`): stacked segment % breakdown.
- **"İzlenecek metrikler" list**: the watch-metrics as a tagged bullet list.
- Three-way tag chips: VERİ (solid), ÇIKARIM (dashed outline), SPEKÜLASYON (lighter/italic).

## Integration into the 0-100 score

The deep-dive sharpens the existing **"Temel + değerleme" (20 puan)** component — it is no longer a rough guess:
- Fair-value range vs price drives the valuation half (cheap vs its growth = more points).
- FCF trend + debt + earnings quality drive the quality half.
- If fundamentals are plan-gated / unverifiable (e.g., many BIST names), this component is CAPPED low and the report says why — a labeled gap, never an invented number.

## Data fallbacks (same ladder as GCnewstock, verified 2026-07-20)

FMP `statements`/ratios are plan-gated for SOME symbols (worked: NFLX, ADBE, DIS; denied: ISRG, CRM, MDT, SYK). On denial, don't retry — go down the ladder:
1. **stockanalysis.com** — `https://stockanalysis.com/stocks/<TICKER>/statistics/` and `/financials/` via WebFetch (clean multiples + history). Cite it.
2. Yahoo *quote* pages 503 to WebFetch (bot wall) — skip; only Yahoo screener/markets pages work.
3. Still missing → "Doğrulanamadı" and move on.

## Placement in the report (updated order)

... existing GCstock blocks (signal banner → score → NEDEN? → verdict → R/R/olasılık → trend/vol/güven → pahalı-ucuz + satış planı → 1Y chart + indicator cards) ...
**→ THEN the deep-dive section (7 blocks above, opening with the `fvbar` fair-value bar and closing with the bull/bear + asimetri + izlenecek metrikler)**
→ analyst/news/insider panels → skor table → one-line summary → sources.
