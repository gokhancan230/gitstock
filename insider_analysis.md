# Insider Transaction Analysis Framework (SEC Form 4)

## Overview

Insider transaction analysis identifies **high-conviction signals** by analyzing what company leadership is actually doing with their own money - distinct from what they say.

Key insight: **Insiders have information advantage** - their buying/selling patterns often precede price moves.

---

## Transaction Types & Information Value

### INFORMATIVE TRANSACTIONS (High Signal Value)

#### 1. Cluster Buying
**Definition**: 3+ insiders buying within a short window (1-4 weeks)
**Signal Strength**: ⭐⭐⭐⭐⭐ EXTREMELY HIGH
**Meaning**: Multiple people with inside knowledge buying = major bullish signal
**Historical Accuracy**: ~75% lead to outperformance in next 12 months

**Example**:
```
Week of March 1:
- CEO buys 100,000 shares at $45
- CFO buys 50,000 shares at $44
- Board member buys 25,000 shares at $45

Analysis: Convergence of insiders buying near same price = coordinated confidence
```

#### 2. CEO/CFO Open-Market Purchase
**Definition**: C-suite executive voluntarily buying stock on open market (not through stock grants)
**Signal Strength**: ⭐⭐⭐⭐⭐ VERY HIGH
**Meaning**: CEO has conviction to deploy personal capital
**Historical Accuracy**: ~70% lead to outperformance

**Why It Matters**:
- CEO putting their net worth where mouth is = seriousness
- Especially powerful if CEO just finished a prior sale cycle (proving not mechanical)

#### 3. Management Buying Near 52-Week Low
**Definition**: Insider purchases when stock is depressed
**Signal Strength**: ⭐⭐⭐⭐ HIGH
**Meaning**: Conviction that stock is mispriced to downside
**Historical Accuracy**: ~65% success rate

**Important**: Distinguish from panic-driven lows (external shock) vs. permanent business deterioration

### MECHANICAL/ROUTINE TRANSACTIONS (Low Signal Value)

#### 1. 10b5-1 Plan Sales
**Definition**: Pre-programmed, automatic stock sales on a schedule
**Signal Strength**: ⭐ VERY LOW
**Meaning**: Diversification, not opinion on stock
**Historical Note**: 10b5-1 plans were designed to allow selling without insider accusations
**Rule**: Ignore 10b5-1 sales unless part of pattern (accelerated selling, plan changes)

**How to Identify**:
- Form 4 specifically states "10b5-1 Plan"
- Sales occur on regular schedule (e.g., every quarter on first day)
- Amount is fixed/predetermined

#### 2. Option Exercises + Immediate Sale
**Definition**: Exercising vested stock options and immediately selling
**Signal Strength**: ⭐ VERY LOW
**Meaning**: Likely tax withholding, not opinion
**Why**: Employees often must sell to fund exercise cost and taxes
**Rule**: Only count if insider holds acquired shares (not sells same day)

#### 3. Tax Withholding Sales
**Definition**: Required sales to cover tax liability on grants/bonuses
**Signal Strength**: ⭐ VERY LOW
**Meaning**: Mechanical tax management
**Historical Note**: These occur same day as grant vesting

---

## Analysis Framework: 6-Part Insider Research Process

### PART 1: Transaction Summary Table

Create complete table of insider activity past 6-12 months:

```
| Date | Insider | Title | Trans Type | Shares | Price | Value | 10b5-1 | Notes |
|------|---------|-------|-----------|--------|-------|-------|--------|-------|
| 3/15 | John Smith | CEO | Open Buy | 100k | $45 | $4.5M | No | Market order - shows conviction |
| 3/20 | Jane Doe | CFO | Open Buy | 50k | $44 | $2.2M | No | Shows alignment with CEO |
| 4/1 | Bob Jones | Dir | 10b5 Sell | 75k | $52 | $3.9M | Yes | Programmed - ignore |
```

**Key Information to Track**:
- Transaction type (Open Market Buy/Sell, Exercise, Grant, etc.)
- 10b5-1 Plan involvement (Yes/No)
- Timing relative to price (near 52W high/low?)
- Absolute and relative position size

### PART 2: Pattern Classification

Classify the overall insider activity into **one category**:

#### A. Cluster Buying Pattern ⭐⭐⭐⭐⭐
```
Signal: Multiple insiders buying within 1-4 week window
Example: CEO + CFO + 2 board members all buy within one month
Conviction: EXTREME - Highest probability bullish signal
Historical: 70-80% success rate next 12 months
Action: Strong BUY signal
```

#### B. CEO/CFO Open-Market Buy ⭐⭐⭐⭐
```
Signal: C-suite executive voluntarily buying (not mechanical)
Example: CEO exercises options and HOLDS shares instead of selling
Conviction: VERY HIGH
Historical: 65-75% success rate
Action: BUY signal (medium conviction if alone, high if joined by others)
```

#### C. Board/Senior Exec Buying (non-CEO/CFO) ⭐⭐⭐
```
Signal: Director or VP buying open market
Example: Several directors accumulating on weakness
Conviction: MEDIUM-HIGH
Historical: 55-65% success rate
Action: BUY signal but lower conviction than CEO/CFO
```

#### D. Routine Selling (10b5-1 Plans) ⭐
```
Signal: Programmed stock sales on schedule
Example: CEO's quarterly 10b5-1 sales hitting schedule
Conviction: NO SIGNAL - Mechanical
Historical: Meaningless for short-term direction
Action: IGNORE - Normal wealth diversification
```

#### E. Accelerated Selling Pattern ⭐⭐ (Potential Concern)
```
Signal: Increased selling pace or volume above historical norm
Example: CEO sold 10k/quarter historically, now selling 50k/quarter
Conviction: MEDIUM-NEGATIVE
Historical: 40-50% precede underperformance
Action: CAUTION - May indicate concerns about near-term outlook
```

#### F. Mixed/Neutral ⭐
```
Signal: No clear pattern - some buying, some selling
Example: CEO buying while CFO selling via 10b5-1 plan
Conviction: NO CLEAR SIGNAL
Action: WAIT - Look for pattern to clarify
```

---

### PART 3: Context & Timing Analysis

#### Question 1: Were purchases made at opportune times?

**Bullish Timing**:
- Purchases near 52-week low (bought when scared)
- Purchases after significant selloff (-20%+ on bad news)
- Purchases ahead of major announcements (pre-announcement buying)

**Neutral Timing**:
- Regular purchases during normal market conditions
- Scheduled purchases via equity compensation plans

**Bearish Timing**:
- Sales near 52-week highs (selling into strength)
- Sales ahead of earnings (possible concern)
- Sales accelerating before announced guidance miss

#### Question 2: Did insiders change or cancel 10b5-1 plans?

**EXTREMELY IMPORTANT**: Plan changes are more informative than the actual sales

```
Bullish Signal:
- Insider CANCELS a 10b5-1 plan = believes stock will rise (doesn't want to sell)
- Insider REDUCES 10b5-1 sales amount = building conviction

Bearish Signal:
- Insider INITIATES a new 10b5-1 plan = plans to sell regularly (concern)
- Insider ACCELERATES 10b5-1 sales = needs to exit
```

#### Question 3: Is there divergence between what management says and what they do?

**Example Red Flags**:
```
Management says: "We're excited about the opportunity, we're all in!"
Reality: Management selling heavily into stock strength
Assessment: MAJOR RED FLAG - Words and actions diverge

Management says: "Guidance under pressure, uncertain times"
Reality: CEO and CFO both buying on open market
Assessment: BULLISH - Actions show confidence despite cautious rhetoric
```

#### Question 4: What's the magnitude of ownership?

Calculate each insider's **Remaining Ownership** as % of personal wealth:

```
CEO owns: 1 million shares
Stock price: $100
CEO's personal net worth: Estimated $200M

Ownership calculation: ($100M / $200M) = 50% of net worth in company stock

Implication: CEO has massive skin in game - actions are credible
```

**Conviction Scoring**:
- If insider has > 50% net worth in stock: EXTREME conviction signals
- If insider has 20-50% net worth in stock: HIGH conviction signals
- If insider has < 5% net worth in stock: LOWER conviction (diversified, less skin in game)

---

### PART 4: Insider Conviction Score (1-5 Scale)

Rate each active insider:

```
Score | Meaning | Criteria |
|-----|---------|----------|
| 5 | Maximum Conviction | CEO buying >1% float, >50% personal net worth in stock, holding from past vests |
| 4 | High Conviction | C-suite buying >0.5% float, 30-50% net worth in stock, consistent holding pattern |
| 3 | Medium Conviction | Director buying, 10-30% net worth in stock, history of both buying and selling |
| 2 | Low Conviction | Mechanical sales/purchases, <5% net worth in stock, routine diversification |
| 1 | No Conviction | Required sales (tax withholding), fractional ownership, no pattern |
```

**Example Scoring**:

```
CEO John Smith:
- Bought 100k shares in open market = +1
- Was CFO 5 years, rarely sold during strong periods = +1
- Net worth ~$250M, now owns $100M in stock (40%) = +1
- Recent open market buy, not via 10b5-1 = +1
- Organized other directors to buy (implicit coordination?) = +1
TOTAL CONVICTION SCORE: 5/5 = Maximum

CFO Jane Doe:
- Selling via regular 10b5-1 plan = -1
- Plan was initiated 18 months ago (ongoing) = -1
- Also just bought 30k shares on open market = +1
- Net worth $50M, owns $5M in stock (10%) = 0
- Younger exec, pattern still developing = 0
TOTAL CONVICTION SCORE: 2/5 = Low (mechanical selling dominating)
```

---

### PART 5: Historical Pattern Comparison

**Key Questions**:

1. **Did insiders buy at the lows?**
```
Example: Stock fell from $100 to $40 on earnings miss
- Did insiders buy at $40-$50 range? (YES = smart money)
- Or did they wait until stock recovered to $60? (NO = not smart money)

Implication: If insiders have history of buying at actual lows = credible signals
```

2. **Have previous cluster buys worked out?**
```
Look at: Every time 3+ insiders bought together in past 5 years
- What was average return 3 months later?
- What was average return 12 months later?

Example Historical Data:
- Cluster buy April 2015: Stock up 35% in 12 months = GOOD PREDICTOR
- Cluster buy September 2018: Stock down 5% in 12 months = MISSED
- Cluster buy March 2020: Stock up 120% in 12 months = EXCELLENT

Pattern: If historically 2 out of 3 cluster buys work = 67% accuracy
```

3. **Is management "smart money" or poor timers?**
```
Track all insider sales for past 5 years:
- Average stock price when insiders sold: $85
- Stock price today: $120
- Did insiders sell too early? (They were right to sell, wrong on timing)

Track all insider purchases for past 5 years:
- Average stock price when insiders bought: $60
- Stock price today: $120
- Did insiders buy at good prices? (YES = smart money)

Conclusion: Track whether insiders sell near highs and buy near lows
```

---

### PART 6: Red Flags & Research Questions

**RED FLAG #1**: CEO/CFO Accelerated Selling
```
Pattern: Suddenly increasing sale volume compared to historical norm
Question: Why the urgency? What do they know about near-term?
Action: Dig into earnings guidance, customer losses, competitive threats
```

**RED FLAG #2**: Divergence Between CEO and Board
```
Pattern: CEO buying while Board members selling
Question: Is there disagreement about strategy/valuation?
Action: Check for governance issues, recent board changes, dissent
```

**RED FLAG #3**: Selling into Strength
```
Pattern: Insiders sold heavily when stock near 52W high
Question: Do they believe price is stretched?
Action: Check valuation metrics, competitor moves, industry trends
```

**RED FLAG #4**: Plan Changes/Cancellations
```
Pattern: Insider suddenly cancels 10b5-1 plan or initiates new plan
Question: What triggered the change in strategy?
Action: Check news/announcements around the date of plan change
```

**RED FLAG #5**: Forced Seller Identification
```
Pattern: Multiple insider sales BUT all via 10b5-1 plans
Question: Are these forced diversification or strategic selling?
Action: Check if 10b5-1 plans were initiated recently or longstanding
```

---

## Real-World Example: Apple (AAPL) Analysis

### Scenario:
Stock down 15% on iPhone slowdown concerns. SEC Form 4's show:

**Recent Activity**:
- Tim Cook (CEO): Bought 100k shares on open market at $160 (2 weeks ago)
- Luca Maestri (CFO): Bought 50k shares at $159 (same week as Cook)
- 2 board members: Each bought 25k shares at $158-$161 (within one week)
- No 10b5-1 sales from any executive (existing plans are paused)

### Analysis:

**Pattern Classification**: CLUSTER BUYING ⭐⭐⭐⭐⭐

**Conviction Scores**:
- Tim Cook: 5/5 (CEO, large purchase, buying lows, coordinated with others)
- Luca Maestri: 4/5 (CFO, significant purchase, aligned with CEO)
- Board Members: 3/5 (Directors, smaller amounts, but same timing)

**Historical Comparison**:
- Cook has bought 5 times in past 10 years
- 4 out of 5 purchases preceded positive 12-month returns (+45%, +32%, +28%, +18%)
- 1 missed (bought at $130, stock fell to $110 then recovered)
- Accuracy: 80%

**Timing Analysis**:
- All purchases made near 52W low range ($155-$165 when normal range is $140-$220)
- No sales planned (10b5-1 plans paused)
- Purchases happened RIGHT AFTER negative iPhone news

**Divergence Check**:
- Cook's earnings call comments: "iPhone is core but we see Services opportunity"
- Cook's actions: Buying significant amounts = Believes short-term pessimism overdone

### Conclusion:
```
INSIDER ACTIVITY ASSESSMENT: STRONGLY BULLISH ⭐⭐⭐⭐⭐

Multiple senior executives coordinated buying near 52W lows after
negative news. Historical track record shows Cook's purchases precede
positive returns. No offsetting insider selling. Clear divergence
between temporary market pessimism and management confidence.

Research Questions:
1. Why was the iPhone slowdown more severe than prior cycles?
2. What is Services TAM and growth rate?
3. How much of margin compression is temporary vs. permanent?
4. Competitive threat from Android growing?
```

---

## Summary: When Insider Activity Really Matters

**STRONGEST SIGNALS** (Most predictive):
1. Cluster buying (3+ insiders, 1-4 week window) = 75% accuracy
2. CEO buying near 52W lows = 70% accuracy
3. 10b5-1 plan cancellation = 65% accuracy (insider wants to hold, not forced sell)

**MEDIUM SIGNALS**:
4. Director buying on open market = 55% accuracy
5. Coordinated C-suite buying (any price) = 60% accuracy

**WEAK SIGNALS** (Often ignored):
6. Regular 10b5-1 sales = No signal
7. Option exercise + sale = No signal
8. Single insider buying = Limited signal (unless CEO at extreme low)

**NEGATIVE SIGNALS** (Warning):
9. CEO accelerated selling ahead of decline = 50-60% precede underperformance
10. Insider selling near 52W highs = Possible overvaluation
