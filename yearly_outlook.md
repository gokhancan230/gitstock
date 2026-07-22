# 1-Year Outlook & Scenario Analysis Framework

## Purpose

Provide a **grounded 1-year view** for a holding or named stock — NOT a prediction, but a **reasoned range** built from macro, fundamentals, technicals, and catalysts. Output as a visual HTML report with fan charts / bull-base-bear bands and a catalyst timeline.

Core promise to the user:
- **A reasoned range, not a guess**
- **Fact vs judgment clearly separated**
- **No fabricated numbers or earnings dates** — if data can't be verified, say so
- **Sources cited** for fundamentals and catalysts

---

## Portfolio Mode (Broker Account Holdings)

When the user asks to analyze "my holdings" or "my portfolio":

1. **Get holdings list** — from broker connection (IBKR or other) if an MCP/tool is available, or ask the user to paste their positions (ticker, shares, cost basis optional)
2. **Classify each holding**: Individual stock vs ETF vs other (bond fund, REIT, crypto ETP)
3. **Analyze each** with the appropriate framework (see below)
4. **Rank by attention needed**: Which holdings have the widest risk skew or nearest catalysts?

⚠️ **Broker safety rule**: NEVER execute trades, transfers, or orders. Read-only analysis of positions. If the user asks to "rebalance" or "sell X", provide the analysis and let them execute themselves.

---

## Stock vs ETF: Different Frameworks

### Individual Stocks → Company-Level Analysis
- Revenue/EPS growth trajectory and whether business is improving or deteriorating
- Valuation vs own history and vs sector
- Company-specific catalysts (earnings, launches, FDA dates, litigation)
- Competitive position changes

### ETFs (QQQ, SCHG, SPY, sector funds) → Index-Level Analysis
**Do NOT apply company fundamentals to an ETF.** Instead:

1. **What does it track?** (Nasdaq-100, S&P 500 Growth, sector index)
2. **Concentration risk**: Top-10 holdings weight (e.g., QQQ top-10 ≈ 45-50% — it's a mega-cap tech bet, not "diversified")
3. **Index valuation**: Forward P/E of the index vs its 5/10-year average
4. **Index earnings growth**: Consensus aggregate EPS growth for the index
5. **Macro/rate sensitivity**: Growth-heavy indexes are long-duration assets — rate cuts help, rate spikes hurt
6. **Flows & regime**: Is the style (growth/value/small-cap) in or out of favor?
7. **Catalysts** = macro events: Fed meetings, CPI prints, mega-cap earnings weeks (since top holdings dominate), rebalances

---

## Per-Holding Analysis Structure

### 1. Technicals (Where is it NOW?)
- Price vs 52-week range: "trading at X% of its 52W range"
- Trend: above/below 50-day and 200-day MA; golden/death cross status
- Momentum: RSI, recent relative strength vs SPY
- Key support/resistance for the year ahead

### 2. Fundamentals (Is the business improving?)
- Revenue and EPS growth: trailing + forward consensus
- Valuation: P/E, EV/EBITDA, PEG vs own 5-year history and sector
- Margin trajectory: expanding or compressing?
- Balance sheet: debt, buybacks, dividend safety
- **Verdict**: Improving / Stable / Deteriorating — with evidence
- **Cite sources**: earnings reports, consensus data source, filing dates

### 3. Macro Backdrop (What helps or hurts it?)
- Rate sensitivity: long-duration growth vs rate-insensitive value
- Sector cycle: where is the sector in its cycle?
- Demand environment: consumer strength, enterprise spend, credit conditions
- Currency/geopolitics if relevant (esp. Turkish stocks: TRY, CBRT policy, inflation)

### 4. Upcoming Catalysts (Next 12 Months)
List with dates where verifiable:
- Earnings dates (next 4 quarters — use confirmed dates; label estimates as "expected ~")
- Product launches / events (only if announced — cite source)
- Regulatory decisions, litigation, index inclusion
- Macro events that matter for THIS holding
- ⚠️ **Never fabricate a date.** If unknown: "next earnings expected early [Month] (unconfirmed)"

### 5. Bull / Base / Bear Scenarios

Build each scenario with explicit reasoning:

```
BULL CASE (target: $XXX, +X%)
├─ What has to go right: [2-3 specific things]
├─ Multiple assumption: [e.g., re-rates to 28x forward EPS]
├─ Earnings assumption: [e.g., EPS grows 15% to $X]
└─ Probability feel: [Low/Medium — judgment, not math]

BASE CASE (target: $XXX, +X%)
├─ Most likely path: [consensus-ish assumptions]
├─ Multiple: [stays near current/historical average]
└─ Earnings: [consensus estimate, cited]

BEAR CASE (target: $XXX, -X%)
├─ What goes wrong: [2-3 specific risks]
├─ Multiple compression: [e.g., de-rates to 18x]
└─ Earnings: [miss scenario]
```

**Target construction method** (show your work):
`Target = Scenario EPS × Scenario Multiple` (stocks)
`Target = Index earnings growth ± multiple re-rating` (ETFs)

### 6. Volatility Sanity Check

Ground the range in historical volatility:
- Get annualized volatility (from ATR, historical σ, or implied vol if available)
- 1-year ±1σ range ≈ current price × (1 ± annualized vol)
- **If your bull/bear targets fall outside ±1.5σ, flag it**: "Bull case implies a move larger than ~85% of historical 1-year outcomes — treat as low probability"
- Present: "Historically, a 1-year move for this stock has been within ±X% about two-thirds of the time"

---

## HTML Visual Report

Generate a self-contained HTML report (inline CSS/JS, no external dependencies) with:

### Per-Holding Card
1. **Fan chart / scenario bands**: Current price on the left, three diverging bands (bull/base/bear) extending 12 months right. Shade the ±1σ historical volatility range behind the bands as sanity-check context. SVG is fine.
2. **Catalyst timeline**: Horizontal 12-month timeline below the chart with markers for each catalyst (earnings = ●, product/events = ▲, macro = ■). Confirmed dates solid, estimated dates hollow/dashed.
3. **Key stats strip**: Current price, 52W range position, trend status, forward P/E, next earnings date
4. **Scenario table**: Bull/Base/Bear with targets, % moves, and one-line reasoning each

### Report-Level
- Summary table of all holdings: ticker, current price, base-case target, range width, nearest catalyst
- **Fact vs Judgment legend**: Facts (prices, dates, reported financials — cited) styled differently from judgments (targets, probabilities, scenario reasoning — clearly labeled "analyst judgment")
- Sources footer: where fundamentals and catalyst dates came from
- Theme-aware (light/dark) if published as an Artifact

### Chart Style Guide
- Bull band: green tint; Base: neutral/blue; Bear: red tint
- Bands widen over time (uncertainty grows)
- Mark today's date and price clearly
- Never draw a single-line "prediction" — always ranges

---

## Data Sourcing Rules

| Data | Source | If unavailable |
|------|--------|----------------|
| Current price | TradingView quote_get / market data API | Say "as of [date]" with last known |
| 52W range, MAs | TradingView OHLCV / studies | Compute from OHLCV |
| Fundamentals | Market data API (statements, ratios) | State "unverified — user should confirm" |
| Consensus estimates | Analyst data API | Use reported TTM + clearly-labeled judgment |
| Earnings dates | Earnings calendar API | "expected ~[month], unconfirmed" |
| Historical volatility | Computed from OHLCV | Use ATR-based approximation, label it |
| Holdings | Broker MCP (read-only) or user-provided list | Ask user to paste positions |

**The cardinal rule**: A wrong number presented confidently is worse than an honest "couldn't verify." Label every unverified figure.

---

## Integration with AL/SAT/TUT

The 1-year outlook complements (not replaces) the trade-level AL/SAT/TUT:

- **AL/SAT/TUT** = tactical: entry zones, stops, targets for the next days-weeks
- **1-Year Outlook** = strategic: is this worth holding through volatility?

When both are requested, present the yearly scenario view first (strategic context), then the tactical plan. Note when they conflict — e.g., "tactically overbought (wait for pullback to buy) but strategically attractive (base case +18%)."
