---
name: GCstock
description: |
  Professional-grade stock analysis combining 10+ analytical frameworks: technical (multiple timeframes, price patterns, volume, divergences, breakouts), fundamental (earnings quality, hidden assets, valuation), buy-side value detection (business model clarity, forced sellers, mispricing analysis), insider transactions (SEC Form 4 analysis, cluster buying detection, conviction scoring), risk management (Kelly criterion, position sizing), and sector/market context. Generates **actionable BUY/SELL/HOLD (AL/SAT/TUT) recommendations with entry/exit targets, risk assessment, catalyst identification, and visual chart analysis**. Also provides **1-year outlooks with bull/base/bear scenario targets, catalyst timelines, and visual HTML fan-chart reports** — for single stocks or entire portfolios (broker holdings, read-only), with ETFs analyzed at index level. Use whenever the user asks about stock analysis, price targets, portfolio review, "where might this go", insider activity, or trading decisions. Supports US and Turkish stocks. Integrates with TradingView for real-time charts and technical indicators.
compatibility:
  - TradingView MCP (chart analysis, technical indicators, price data, visualization)
  - Massive Market Data MCP (fundamental analysis, historical data, earnings dates)
  - SEC Form 4 filings (insider transaction analysis)
  - Chart Drawing (SVG/visualization for technical setups)
---

# Professional Stock Analysis - Senior Equity Research Level

Institutional-grade stock analysis combining technical, fundamental, buy-side value, and insider transaction analysis frameworks. Designed for professional traders and equity research teams.

> **FIRST STEP — data access:** Read `data_sources.md` before pulling any data. It maps every data need to the verified working tool (including the earnings-calendar workaround for plan-gated endpoints) so you don't waste calls on locked APIs.

> **DECISION MODULES:** Read `decision_modules.md` — 14 mandatory report add-ons (R/R + yıldız, olasılıklar, holding süresi, trend gücü, volatilite, makro riskler, tahmin güveni, pozisyon büyüklüğü, NEDEN? kutusu, 30 günlük senaryolar, skor tablosu, tek cümle özet) with strict VERİ/YORUM separation and placement order.

> **TECHNICALS — indicator engine:** Read `tradingview_indicators.md` before any technical analysis. It defines the verified 5-slot TradingView indicator battery (EMA20, EMA50, Bollinger, RSI, MACD — plan caps at 5 studies), the −10…+10 scoring system that converts readings into AL/SAT/TUT signals, and the confluence-zone method for entry/stop placement. 200MA/ATR/ADX come from FMP, not the chart.

> **DIVIDENDS + REPORT-TIME PRICE STAMP:** Read `dividends.md`. Every full analysis carries a dividend block (ödeme aralığı, son 3 ödeme with ex-dates, yield recomputed against the REPORT-TIME price, raise/cut trend) — or a verified "Temettü ödemiyor". It also defines the mandatory as-of price+time stamp for the whole report.

> **FORWARD-LOOKING DATA:** Read `forward_looking.md` for anything predictive. It maps the verified sources that look AHEAD — analyst forward EPS consensus (epsLow/Avg/High by year + analyst count → anchors the fair-value range in VERİ instead of guesswork), rating-change clusters, short interest / days-to-cover positioning, and consensus-target dispersion → all of which feed the probability module, valuation, and confidence score. Also lists what is plan-gated (options/IV) so you don't waste calls.

> **DEEP-DIVE FUNDAMENTALS:** Read `deepdive_fundamentals.md` for any FULL single-stock analysis. It adds an analyst-grade fundamental/valuation section (7 blocks: iş modeli, finansal sağlık, değerleme with peer multiples + DCF fair-value RANGE, makro & rekabet, katalizörler, sıralı riskler, bull/bear tezi + asimetri + izlenecek metrikler), a three-way VERİ/ÇIKARIM/SPEKÜLASYON evidence tagging, and the `fvbar` fair-value bar. It sharpens the 0-100 score's "Temel + değerleme" component. Skip only for pure quick-timing scalp questions.

## 10 Core Analysis Frameworks

### 1. ✅ Multiple Timeframe Analysis
- **Weekly**: Macro trend direction (most important)
- **Daily**: Swing setup and entry opportunities
- **4H**: Precise entry timing and confirmation
- **1H**: Exact entry/exit and stop placement
- **Principle**: Higher timeframe always takes precedence

### 2. ✅ Price Pattern Recognition
- Head & Shoulders (reversal, 70% accuracy)
- Double Bottom/Top (reversal, strong signal)
- Triangle Breakouts (breakout pattern)
- Wedge Patterns (continuation/reversal)
- Engulfing Candles (reversal candles)
- Breakaway Gap Patterns (trend continuation)

### 3. ✅ Volume Confirmation Analysis
- High volume on breakout = Strength (likely to hold)
- Low volume on breakout = Weakness (likely to fail)
- Volume surge = Breakout confirmation
- Declining volume on rally = Warning sign
- Volume analysis at key levels = Critical validation

### 4. ✅ Earnings Calendar Integration
- Earnings dates and impact probability
- Earnings surprises history (beats/misses %)
- Pre-earnings consolidation patterns
- Post-earnings technical setup (gap direction?)
- Earnings volatility expectations (wide stop placement)
- Guidance revisions analysis

### 5. ✅ Sector Analysis & Comparative Performance
- Stock vs. Sector Index momentum
- Relative strength ranking (top/middle/bottom)
- Sector rotation (which sectors leading/lagging?)
- Industry-specific headwinds/tailwinds
- Peer comparison (valuation vs. peers)
- Sector sentiment (bullish/bearish consensus)

### 6. ✅ Liquidity & Spread Analysis
- Bid-Ask Spread (tighter = easier entry/exit)
- Average Daily Volume (ADV - sufficient for position size?)
- Market Depth (can you exit at market price?)
- Trading Hours (US vs. Turkish market considerations)
- Slippage Risk (esp. for larger positions)

### 7. ✅ Divergence Analysis
- **Price-RSI Divergence**: Price makes new high but RSI doesn't = Weakness
- **Price-MACD Divergence**: Price rallies but MACD doesn't = Reversal warning
- **Price-Volume Divergence**: Price up but volume down = Fake breakout
- **Higher Timeframe Divergence**: Daily up but Weekly RSI failing = Caution

### 8. ✅ Risk Management Framework
- **Kelly Criterion Position Sizing**: f* = (bp - q) / b where sizing matches edge
- **Fixed % Risk Model**: Risk only X% of portfolio per trade
- **Max Loss per Trade**: Typically 0.5-2% of portfolio
- **Risk/Reward Ratio**: Minimum 1:2, prefer 1:3+
- **Position Scaling**: Build positions into support, scale into resistance
- **Stop Loss Placement**: Based on price structure, not arbitrary %

### 9. ✅ Breakout Confirmation Mechanics
- **Volume confirmation**: Breakout must be on high volume
- **Timeframe confirmation**: Daily breakout confirmed by 4H/1H
- **Momentum confirmation**: RSI/MACD aligned with direction
- **False breakout identification**: 2-3 day false breakout common (wait for retest)
- **Breakout pullback entry**: Enter on pullback INTO breakout (lower risk entry)

### 10. ✅ Supply & Demand Level Analysis
- **Support levels**: Where price bounced 3+ times historically
- **Resistance levels**: Where price rejected 3+ times historically
- **Support strength**: More tests = stronger support
- **Order flow clustering**: Volume profile analysis (where buyers/sellers cluster)
- **Breakout implications**: Support break = major selling; Resistance break = major buying

### BONUS: Insider Transaction Analysis (SEC Form 4)
- Cluster buying (3+ insiders buying = high conviction)
- C-suite open-market purchases (CEO/CFO buys = confidence)
- Forced seller identification (10b5-1 plan sales = mechanical)
- Conviction scoring (ownership %, holding period, history)
- Historical pattern comparison (did insiders buy at lows?)
- Timing analysis (buys near 52W lows vs. highs?)

### BONUS: 1-Year Outlook & Scenario Analysis (Portfolio Mode)
**Read `yearly_outlook.md` when the user asks for a yearly view, portfolio review, price targets, or "where might this go".**
- Portfolio scan: analyze broker holdings (IBKR etc., read-only) or a named stock
- **Stocks vs ETFs handled differently**: ETFs (QQQ, SCHG) analyzed at INDEX level — index valuation, earnings growth, concentration, rate sensitivity — never company fundamentals
- Bull / Base / Bear scenarios with reasoned 1-year targets (EPS × multiple, work shown)
- Historical volatility sanity check (targets outside ±1.5σ get flagged)
- Catalyst timeline: earnings dates, launches, macro events — verified dates only, never fabricated
- **Visual HTML report**: fan chart / scenario bands per holding + catalyst timeline
- Fact vs judgment clearly separated; sources cited for fundamentals and catalysts

---

## Analysis Workflow

```
STEP 1: TIMEFRAME HIERARCHY ✅
├─ Weekly: Establish macro trend direction
├─ Daily: Identify swing setup
├─ 4H: Confirm entry point
└─ 1H: Precise entry/exit

STEP 2: PRICE STRUCTURE ANALYSIS ✅
├─ Pattern Recognition: What pattern is this?
├─ Supply/Demand: Key S/R levels?
├─ Volume: Breakout confirmed by volume?
└─ Divergences: Any momentum divergences?

STEP 3: INSIDER TRANSACTION ANALYSIS ✅
├─ SEC Form 4 Review: Last 6-12 months
├─ Pattern Classification: Cluster buy? CEO buy? Routine selling?
├─ Timing Analysis: Near 52W lows? Before/after earnings?
├─ Conviction Scoring: Insider ownership % + history
├─ Red Flags: Divergence between words and actions?
└─ Forced Sellers: Who has to sell regardless of value?

STEP 4: VALUATION & SECTOR CONTEXT ✅
├─ Buy-Side Analysis: Is this mispriced?
├─ Earnings Calendar: Events coming up?
├─ Sector Position: Leading/lagging peers?
├─ Fundamental Quality: Earnings quality + sustainability
└─ Liquidity: Can we actually trade this size?

STEP 5: RISK MANAGEMENT FRAMEWORK ✅
├─ Position Size: Kelly Criterion or Fixed %?
├─ Max Loss: How much will we risk?
├─ Stop Loss: Where based on structure?
├─ Risk/Reward: Minimum 1:2?
└─ Breakout Confirmation: Real breakout or false?

STEP 6: FINAL ACTIONABLE RECOMMENDATION ✅
├─ Signal: BUY / SELL / HOLD + Conviction Level
├─ AL: When? Entry Zone + Confirmation
├─ SAT: When? Target prices + Exit signals
├─ TUT: When? Time horizon + Watch levels
├─ Chart: Visual technical setup (if requested)
└─ Risk Profile: Position sizing for YOUR account

STEP 7 (OPTIONAL): 1-YEAR OUTLOOK ✅ (see yearly_outlook.md)
├─ Bull / Base / Bear scenario targets (reasoning shown)
├─ Catalyst timeline: next 12 months, verified dates only
├─ Volatility sanity check: range vs historical ±1σ
├─ ETF? → Index-level analysis (never company fundamentals)
└─ HTML visual report: fan chart + catalyst markers
```

---

## Key Principles

1. **Timeframe Hierarchy**: Weekly > Daily > 4H > 1H (Always respect higher timeframe)
2. **Pattern + Volume**: Entry is only valid if price pattern AND volume align
3. **Insider = Conviction**: Cluster buys are rare and valuable signals
4. **Forced Sellers**: Identify who has to sell = opportunity to buy
5. **Margin of Safety**: Only buy if valuation gives you edge
6. **Risk First**: Position sizing on risk, not reward potential
7. **Multiple Confirmation**: Need 3+ indicators aligned for high conviction
8. **Divergence Warning**: Price making new high but momentum doesn't = Reversal coming

---

## How to Use This Skill

### Basic Analysis

When you need stock analysis, provide:
1. **Stock ticker**: AAPL, MSFT, THYAO.IS, etc.
2. **Timeframe** (optional): Daily, Weekly (defaults to Daily)
3. **Analysis type**: Full professional analysis
4. **Your goals**: Quick trade, long-term investment, value hunt

### With Insider Analysis

For insider transaction analysis, provide:
1. **Company name** (for context)
2. **Stock ticker**
3. **Time period** for Form 4 review (e.g., "last 6 months")
4. (Optional) **Specific insiders** to focus on

### With Chart Output

For visual technical setup, request:
- "Include chart" or "Draw technical setup"
- Stock will be analyzed AND visualized with key levels, patterns, entry/exit

### 1-Year Outlook / Portfolio Review

For a yearly scenario view, request:
- "1 yıllık görünüm", "portföyümü analiz et", "where might X go this year"
- Provide holdings list (or connect broker read-only) — or name a single stock
- Output: Bull/Base/Bear targets with reasoning, catalyst timeline, volatility-checked range, visual HTML report with fan charts
- ETFs analyzed at index level (valuation, concentration, rates), stocks at company level

### Output

The skill will:
- ✅ Analyze using all 10+ frameworks
- ✅ Provide institutional-quality research
- ✅ Give **clear AL/SAT/TUT timing** (When to Buy/Sell/Hold)
- ✅ Insider transaction analysis with conviction scoring
- ✅ Draw technical charts if requested
- ✅ Position sizing for your account

---

## Output Format (Professional Research Report)

### ⚡ RULE: Auto-save every report to the archive folder

Every HTML report MUST also be saved (copied) to:
```
/Users/gokhancan/Desktop/Claude Skill/GCstockA/GCstock-[TICKERS]-[YYYY-MM-DD].html
```
- Example: `GCstock-AAPL-2026-07-20.html`, multi-stock: `GCstock-AAPL-THYAO-2026-07-20.html`
- Do this automatically on every report — no need to ask
- Same-day re-analysis of the same ticker OVERWRITES that day's file (latest wins); a new day gets a new file
- The file must be self-contained (charts embedded as base64) so it opens offline
- **The file MUST start with `<meta charset="utf-8">` as its very first line** — without it, browsers opening the local file render Turkish characters as mojibake (Ã¼, Ä± garbage). The Artifact publish adds its own wrapper, but the LOCAL copy needs the charset declaration itself.
- Create the folder with `mkdir -p` if missing

### ⚡ REPORT IDENTITY: This is a DAILY decision report, not a yearly outlook

The default GCstock report answers TODAY's two questions:
1. **Yeni alım için: pahalı mı, ucuz mu?** — explicit PAHALI/MAKUL/UCUZ verdict (P/E vs own history, FCF yield, distance to analyst consensus, 52W position) + the price zone where it WOULD become cheap
2. **Eldeki hisse ne zaman satılır?** — a sell LADDER (kademe 1 %40 / kademe 2 %40 / kalan %20 trailing) + an unambiguous ANINDA SAT condition (daily close below X)

The 1-year element in the report is ONLY the price chart (TradingView screenshot with the indicator battery) — NOT fan charts, NOT 12-month scenario tables, NOT catalyst timelines. Those belong to the separate optional yearly-outlook module (`yearly_outlook.md`) and appear only when the user explicitly asks for a yearly view.

### ⚡ RULE #0: Signal Banner is the VERY FIRST thing in every report

Before score, before everything — a big, unmissable banner per stock:

```
┌────────┬────────────────────┬─────────────────────────┬──────────────────────────┐
│  AL    │ 🚪 İLK KEZ ALACAKSAN│ ⚡ HİSSEN VARSA—KISA VADE│ 🎯 HİSSEN VARSA—UZUN VADE│
│ (veya  │ Giriş: $XXX – $XXX  │ Satış: $XXX – $XXX      │ Satış: $XXX – $XXX       │
│TUT/SAT)│ + teyit koşulu      │ teknik dirençler·haftalar│ değerleme tavanı·6-12 ay │
└────────┴────────────────────┴─────────────────────────┴──────────────────────────┘
```

- **Signal word**: AL (green) / TUT (amber) / SAT (red) — one word, huge, colored
- **İlk kez alacaklar için**: entry price RANGE (confluence zone), not a single price, plus the confirmation to wait for
- **Holders get TWO separate sell ranges — never one blended number:**
  - **KISA VADE (haftalar)** — driven by *price*: technical resistance levels, BB upper, prior highs. Ladder TP1→TP2 + an unambiguous ANINDA SAT (daily close below X).
  - **UZUN VADE (6-12 ay)** — driven by *value*: where the stock becomes expensive vs the consensus-anchored fair-value range (typically between the base and bull legs, cross-checked against the analyst consensus target). Explicitly mark the fair-value BASE as "SATMA — burası adil, prim değil".
  - **Uzun vade exit is thesis-driven, not price-driven.** Name 3 concrete, checkable conditions that break the thesis (a growth rate falling below X for two consecutive quarters, a cash-flow metric failing to turn by a stated year, a cost ratio staying above a threshold). If one triggers, the position is cut regardless of price.
  - Add the position-splitting note: managing one holding on two horizons requires splitting it up front (e.g. 60% long-term core + 40% trading tranche), otherwise short-term sells silently close the long-term thesis.
- Multi-stock reports: stack one banner per stock at the very top as a quick-decision summary

### ⚡ RULE: GCstock Puanı (0-100) comes right after the banner

Before even the verdict box, show the composite score with its transparent breakdown:

| Component | Max | Source |
|-----------|----:|--------|
| Teknik motor | 25 | Indicator engine score (−10…+10 → 0-25, see tradingview_indicators.md) |
| Temel + değerleme | 20 | Quality (ROIC, earnings quality) AND valuation (P/E vs history); unverifiable fundamentals cap this at ~8 |
| Giriş kalitesi (R/R) | 15 | Distance to stop vs distance to first resistance from CURRENT price — poor R/R at current price scores low even in strong trends |
| Momentum/Sektör | 10 | Relative strength, 52W position, sector leadership |
| Katalizör | 10 | Confirmed near-term catalysts; imminent binary events (earnings <2wk) cut this |
| Insider | 10 | Cluster buys 9-10 · CEO buy 7-8 · neutral/routine 5 · heavy discretionary selling 1-3 · no data 3 |
| Haber duyarlılığı | 10 | News sentiment engine (see news_sentiment.md): 5 + NET/2. Positive and negative ALWAYS shown separately in the report |

Tiers: **80+** GÜÇLÜ (AL bölgesi) · **65-79** İYİ (pullback'te AL / TUT) · **50-64** NÖTR (izle) · **35-49** ZAYIF (azalt) · **<35** SAT bölgesi.

The score measures **opportunity quality NOW** (trend + value + entry), not just company quality — a great company at a bad entry scores mid-range.

### ⚡ RULE: Write for a NON-PROFESSIONAL reader — plain Turkish, jargon always explained

The user is an individual investor, not a fund analyst. Numbers can be precise; the language must not be. Three mandatory elements:

**1. Score-component explanations.** Directly under the 0-100 breakdown, one plain sentence per component saying what it measures and what a high score means — e.g. *"Giriş kalitesi — Bugünkü fiyattan alsam, kazanabileceğim kaybedebileceğime değer mi? Düşük puan = şirket iyi olsa bile fiyat şu an uygun değil."* Close with the framing line: the score measures **today's opportunity quality, not company quality**.

**2. The NEDEN? box in everyday language.** Lead each bullet with a bold plain-language claim, then the numbers as support — not the reverse. Translate every mechanism:
- ❌ *"Fiyat 200G MA üstünde, MACD sıfır çizgisi üzerinde yukarı kesişim yaptı (histogram +1.14)"*
- ✅ *"Grafik hâlâ iyi durumda — fiyat uzun vadeli ortalamasının ($234) üstünde, yani genel yön hâlâ yukarı. Momentum göstergesi de yeni yukarı döndü."*
- ❌ *"R/R 0.5"* → ✅ *"riskin, kazancından iki kat büyük"*
- ❌ *"binary olay"* → ✅ *"tek günde sert oynayabilir — böyle bir belirsizlikten hemen önce tüm paranı yatırmak kumar olur"*

**3. Every metric gets a "Ne demek? → Gelecek fiyat için:" pair.** A number alone teaches nothing. Under each metric row (F/K, EV/EBITDA, FCF verimi, 52H konumu, short interest, konsensüs EPS, not değişiklikleri…), attach two short lines:
- **Ne demek:** the metric translated into everyday terms — *"F/K 29.3x = şirketin bir yıllık kârının 29 katını ödüyorsun; bu parayı geri çıkarması 29 yıl sürer."*
- **→ Gelecek fiyat için:** the consequence for the price, which is the only reason the reader cares — *"Rakipleri 19-25 kattan işlem görüyor. AMZN'in daha pahalı olması piyasanın daha hızlı büyüme beklediği anlamına gelir; beklenti tutmazsa fiyat bu farkı kapatmak için düşer."*

Style the pair as an indented note with an accent left-border so it reads as commentary, not data. Never leave a raw multiple, ratio or positioning figure standing without this pair.

**4. A glossary card near the end** ("📖 Küçük Sözlük") defining every term that appears in the report in one line each: destek, direnç, stop, R/R, kademeli satış, hareketli ortalama, RSI, MACD, F/K, FCF, capex, insider, 10b5-1, konsensüs, volatilite, short interest.

Keep the analytical rigor identical — only the wording gets simpler. Never dumb down a risk to make it sound smaller.

### ⚡ RULE: Verdict Box comes SECOND — right after the score

Every analysis (text or HTML) MUST open with this summary box before any detail. The reader gets the decision in 5 seconds; the reasoning follows below.

```
╔═══════════════════════════════════════════════════════╗
║  [TICKER] — [Şirket]           Fiyat: $/₺XXX          ║
╠═══════════════════════════════════════════════════════╣
║  SİNYAL:        AL / SAT / TUT   (Güven: Y/O/D)       ║
║  1Y HEDEF:      $/₺XXX  (baz senaryo, +X%)            ║
║                 Boğa $/₺XXX │ Ayı $/₺XXX              ║
║  STOP LOSS:     $/₺XXX  (−X% | gerekçe: seviye)       ║
║  YENİ GİRİŞ:    $/₺XXX–XXX bölgesi + teyit koşulu     ║
║                 (şu an girilir mi: EVET/BEKLE)        ║
╚═══════════════════════════════════════════════════════╝
```

Rules for the box:
- **SİNYAL**: one word + conviction. If holder vs new-entry advice differs, show both ("TUT — yeni giriş: BEKLE").
- **1Y HEDEF**: base-case target with bull/bear range beneath (from scenario analysis; label as YORUM).
- **STOP LOSS**: exact price + why that level (support/EMA/confluence, not arbitrary %).
- **YENİ GİRİŞ**: the confluence-zone entry price(s), the confirmation to wait for, and an explicit "girilir mi şimdi" answer.

The analysis follows this structured format:

### Technical & Price Structure
- Multi-timeframe setup (Weekly > Daily > 4H > 1H hierarchy)
- Price patterns and volume confirmation
- Supply/demand levels and breakout mechanics
- Support/resistance identification

### Insider Transaction Analysis
- Transaction summary table (dates, names, types, amounts, 10b5-1 status)
- Pattern classification (Cluster buying? CEO buy? Routine?)
- Timing analysis (52W lows? Before earnings? Plan changes?)
- Conviction scoring (1-5 scale per insider)
- Red flags and research questions
- Smart money assessment

### Valuation & Fundamentals
- Buy-side value analysis and mispricing detection
- Fundamental valuation and sector context
- Earnings quality and hidden assets
- Earnings calendar impact assessment

### Risk Management
- Liquidity and trading logistics
- Position sizing (Kelly Criterion + Fixed %)
- Stop loss placement (based on price structure)
- Risk/Reward ratio analysis

### 🎯 FINAL ACTIONABLE RECOMMENDATION

```
═══════════════════════════════════════════════════════
AL (BUY) SIGNAL: [Yes/No/Conditional]
Cuando: Entry Zone $XXX - $XXX
Confirmación: What to wait for before entering
Targets: TP1 $XXX | TP2 $XXX
Potencial: +X% profit
Riesgo: $XXX max loss
═══════════════════════════════════════════════════════
SAT (SELL) SIGNAL: [Profit taking levels]
Cuando: Exit at $XXX (TP1) or $XXX (TP2)
Señal: [What signals exit - price, time, event?]
Stop Loss: $XXX (below support)
R/R Ratio: 1:X (risk/reward)
═══════════════════════════════════════════════════════
TUT (HOLD) SIGNAL: [Time frame to hold]
Duración: X days/weeks holding period
Watch Levels: Monitor $XXX and $XXX
Invalidation: Exit if price closes below $XXX
═══════════════════════════════════════════════════════
```

### Visual Chart (Optional)
- Technical setup visualization
- Key support/resistance levels marked
- Entry/exit/stop zones highlighted
- Pattern identification visual
- Volume profile if relevant

### Catalysts & Risk Assessment
- Near-term catalysts (earnings, events, insider activity)
- Main risks (technical, fundamental, macro)
- Invalidation scenarios

---

## Research Notes

- **Turkish vs US Markets**: Account for different trading hours, disclosure standards, liquidity profiles
- **Earnings Dates**: Mark earnings on calendar; adjust stops before announcements
- **Sector Context**: Sector momentum can make or break individual stock moves
- **Insider Timing**: C-suite buying near 52W lows = high conviction; near highs = warning
- **Never Fight the Weekly**: Daily pullbacks in weekly uptrends = best entries
- **Volume is Final Arbiter**: Price can lie; volume tells truth (high volume = real move)
