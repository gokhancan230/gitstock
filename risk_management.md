# Professional Risk Management Framework

## Core Principle: Risk First, Reward Second

**The Golden Rule**: *Always size positions based on RISK, not reward potential*

Most traders do it backwards:
- ❌ **Wrong**: "I want to make $5,000 on this trade, so I'll buy X shares"
- ✅ **Right**: "I can risk $1,000 on this trade, so I'll buy Y shares"

---

## Method 1: Kelly Criterion Position Sizing

### What is Kelly Criterion?

The Kelly Criterion is a mathematical formula that calculates **optimal position sizing** based on:
- Your win rate (%)
- Your average win size (R)
- Your average loss size (-R)

### The Formula

```
f* = (bp - q) / b

Where:
f* = fraction of capital to risk
b = ratio of win size to loss size (odds)
p = probability of winning (0 to 1)
q = probability of losing (1 - p)
```

### Practical Example

**Your Trading Record**:
- Win rate: 60% (p = 0.60)
- Loss rate: 40% (q = 0.40)
- Average win: $300 per trade
- Average loss: $100 per trade
- Odds ratio (b) = $300 / $100 = 3:1

**Calculation**:
```
f* = (3 × 0.60 - 0.40) / 3
f* = (1.80 - 0.40) / 3
f* = 1.40 / 3
f* = 0.467 = 46.7%

Result: Risk 46.7% of your portfolio per trade
```

### Kelly Criterion Sizing Table

```
Win Rate | 1:1 R/R | 1:2 R/R | 1:3 R/R | 1:4 R/R |
|---------|---------|---------|---------|---------|
| 50% | 0% | 25% | 37.5% | 43.75% |
| 55% | 5% | 32.5% | 45% | 53.75% |
| 60% | 10% | 40% | 52.5% | 60% |
| 65% | 15% | 47.5% | 60% | 66.25% |
| 70% | 20% | 55% | 67.5% | 72.5% |
```

### Half Kelly (Conservative Approach)

**Why Half Kelly?**
- Full Kelly can be psychologically difficult (50% position swings)
- Half Kelly = f* / 2 = More sustainable
- Better for real-world trading with variance

**Example**:
- Full Kelly = 46.7%
- Half Kelly = 23.35% per trade

**Recommendation**: Use 25-50% Kelly depending on experience level

---

## Method 2: Fixed Risk % Model

**Simpler than Kelly, good for beginners**

### The Approach

1. **Decide Max Risk Per Trade**: Typically 0.5% - 2% of portfolio
2. **Calculate Stop Distance**: Stop price - Entry price
3. **Calculate Position Size**: (Max Risk $) / (Stop Distance $)

### Example Calculation

**Your Account**: $100,000
**Risk Per Trade**: 1% = $1,000
**Stock**: AAPL at $150
**Stop Loss**: $145 (5 points down)

**Position Size**:
```
Position Size = $1,000 / $5 per share = 200 shares

Validation:
- Entry: 200 shares × $150 = $30,000 (30% of account)
- Stop Loss: 200 shares × $145 = $29,000
- Max Loss: $1,000 ✓

Risk/Reward on this trade:
- Target: $160 (10 points up)
- Profit at target: 200 × $10 = $2,000
- Risk/Reward: $2,000 / $1,000 = 2:1 ✓
```

### Risk % Guidelines by Experience Level

```
Trader Level | Max Risk/Trade | Typical Account Size |
|-------------|----------------|---------------------|
| Beginner | 0.5% - 1% | < $50K |
| Intermediate | 1% - 1.5% | $50K - $500K |
| Professional | 1.5% - 2% | $500K+ |
| Institutional | 0.5% - 1% | $1M+ (different constraints) |
```

---

## Method 3: Volatility-Adjusted Sizing

**Account for how volatile the stock is**

### Concept

High-volatility stocks need smaller positions (wider stops needed)
Low-volatility stocks can have larger positions (tighter stops possible)

### Calculation

1. **Calculate ATR** (Average True Range) = measure of volatility
2. **Set Stop**: 1.5 - 2 × ATR away from entry
3. **Calculate Position Size**: Same as fixed % method

### Example

**Stock**: TSLA (High Volatility)
```
Current Price: $250
ATR (20-day): $8
Stop distance: 2 × $8 = $16
Account: $100,000
Max Risk: 1% = $1,000

Position Size = $1,000 / $16 = 62.5 shares

Value at entry: 62.5 × $250 = $15,625 (15.6% of account)
```

**Stock**: KO (Low Volatility)
```
Current Price: $60
ATR (20-day): $0.75
Stop distance: 2 × $0.75 = $1.50
Account: $100,000
Max Risk: 1% = $1,000

Position Size = $1,000 / $1.50 = 666.6 shares

Value at entry: 666.6 × $60 = $40,000 (40% of account)
```

**Insight**: Volatile stock = smaller position %; Stable stock = larger position %

---

## Stop Loss Placement Rules

### Rule 1: Use Price Structure (Most Important)

**Stop BELOW support** (for longs):
```
Price has bounced off $100 support 3x
Entry at $105
Stop: Just below $100 (e.g., $99.50)

Why: If $100 breaks, setup is invalidated
```

**Stop ABOVE resistance** (for shorts):
```
Price has rejected $200 resistance 2x
Entry short at $195
Stop: Just above $200 (e.g., $200.50)

Why: If $200 breaks, short thesis broken
```

### Rule 2: Use Technical Levels

- Support/Resistance levels
- Moving average (20, 50, 200-day)
- Pattern breakdown levels
- Pivot points

### Rule 3: Avoid Arbitrary % Stops

**❌ Bad**: "I'll stop out if it goes down 5%"
- Ignores price structure
- Often stops in noise/volatility

**✅ Good**: "I'll stop out if it closes below the 50-day MA"
- Based on technical structure
- More likely to be a real breakdow

### Rule 4: Time-Based Stops

**When to use time stops:**
- Setup isn't working but hasn't been invalidated
- After X days with no movement, exit (opportunity cost)
- Before major events (earnings, Fed announcement)

**Example**:
```
Entry on breakout - give it 5 days to work
If no progress in 5 days, exit with small loss
Don't hold waiting for eventual "squeeze"
```

---

## Risk/Reward Ratio Requirements

### Minimum Standards

```
Scenario | Min R/R | Ideal R/R | Win Rate Needed |
|---------|----------|-----------|-----------------|
| Technical only | 1:1.5 | 1:2.5 | 50% |
| Fundamental + Tech | 1:1.5 | 1:2 | 55% |
| Multi-confirmation | 1:1 | 1:2 | 60% |
| Insider buying | 1:1.5 | 1:3 | 45% |
```

### The Breakeven Calculation

```
Win Rate = Losses / (Wins + Losses) to breakeven

Example: If R/R = 1:2 (risk 1 to make 2)

Breakeven Win Rate = 1 / (1 + 2) = 1/3 = 33.3%

Meaning: Even with 33% win rate, you break even
```

**Implication**: Higher R/R means you can be wrong MORE OFTEN and still profit

---

## Position Scaling Strategy

### Pyramid In (Build into Support)

**When price pulls back into support zone:**
```
Entry 1: At resistance, size 50% = 100 shares
Pullback: Price falls to support
Entry 2: At support, add 50% = 50 shares more
Entry 3: (Optional) If strong support holds, add final 50% = 50 shares

Total position: 200 shares
Average entry: Lower than if bought all at once
Stop: Below support (below all entries)
```

**Why This Works**:
- Lower average entry price
- Confidence building as support holds
- Larger position only after confirmation

### Scale Out (Take Partial Profits)

**At Resistance Levels**:
```
Entry: 200 shares at $100
Stop: $95 (below support)

Position 1: Sell 50 shares (100) at $110 = $5,500 profit
Position 2: Move stop to $105 (at entry) for remaining 100
Position 3: Sell 50 more at $115 = $1,000 profit
Position 4: Let 50 run with trailing stop

Result: Locked in $6,500, let some run for bigger winner
```

**Benefits**:
- De-risks the trade (lock in early wins)
- Let winners run
- Reduce average cost if averaging down
- Clear exit plan = less emotional

---

## The 2% Rule (Professional Standard)

### What Is It?

Never risk more than 2% of total portfolio on a single trade

### Calculation

```
Portfolio: $500,000
2% Risk = $10,000 per trade
Stop Distance = $2/share
Position Size = $10,000 / $2 = 5,000 shares

Risk Summary:
- If stopped out: Lose $10,000 (2% of portfolio)
- If target hit (at 1:2 R/R): Win $20,000 (4% profit)
```

### Why 2% Rule?

1. **Psychological**: Can handle 50 losses in a row ($500K → $25K) before account wiped
2. **Mathematical**: Even with 40% win rate, account still grows
3. **Sustainable**: Allows trading for years without catastrophic loss

### Exception: Insider Buying Cluster

When 3+ insiders buying cluster (very rare, high conviction):
- Can risk up to 3-4% on that specific trade
- Higher odds justify higher risk

---

## Risk Management Checklist

Before every trade, verify:

- [ ] **Position Size Calculated**: Based on risk %, not reward potential
- [ ] **Stop Loss Placed**: Below/above technical level (not arbitrary %)
- [ ] **Risk/Reward Confirmed**: Minimum 1:1.5 (or acceptable for setup)
- [ ] **Total Risk**: Not exceeding 2% of portfolio
- [ ] **Portfolio Heat**: Total open risk < 6% (multiple positions)
- [ ] **Exit Plan**: Know exactly when to exit profit / loss
- [ ] **Timeframe**: Holding period realistic for chosen timeframe?
- [ ] **Scenario Planning**: What invalidates this setup?
- [ ] **Earnings Risk**: Adjusting stop before earnings? Or exiting?
- [ ] **Liquidity Check**: Can I exit at target price without slippage?

---

## Common Risk Management Mistakes

### ❌ Mistake 1: Revenge Trading After Loss
**Problem**: Lost $1,000, immediately enter larger trade to "make it back"
**Result**: Usually leads to bigger loss
**Fix**: Stick to position sizing rules; take break after 2-3 losses

### ❌ Mistake 2: Moving Stop Loss Further
**Problem**: "Stop's too tight, I'll move it lower"
**Result**: Large loss when it finally hits
**Fix**: If stop is wrong, exit and re-enter with correct stop

### ❌ Mistake 3: No Exit Plan
**Problem**: "I'll decide when to exit after I'm profitable"
**Result**: Give back profits waiting for bigger move
**Fix**: Set profit targets BEFORE entering trade

### ❌ Mistake 4: Ignoring Correlation Risk
**Problem**: 5 positions in same sector (all move together)
**Result**: Worse than individual 5% losses = 20%+ decline in correlated move
**Fix**: Limit sector exposure to <20% total portfolio

### ❌ Mistake 5: Over-Leveraging
**Problem**: Using margin to buy twice the size
**Result**: 50% drawdown becomes account wipeout
**Fix**: Trade without margin until consistent; master 1:1 sizing first

---

## Risk Management by Market Environment

### Bull Market (Uptrend)
- Larger positions OK (momentum in your favor)
- Tighter stops justified (more frequent pullbacks)
- Scale into winners
- Risk: 1-2% per trade

### Bear Market (Downtrend)
- Smaller positions (momentum against you)
- Wider stops needed (deeper pullbacks)
- Scale into losers cautiously
- Risk: 0.5-1% per trade

### Range/Consolidation
- Medium positions (no directional edge)
- Tight stops at support/resistance
- Range trading = higher frequency, smaller wins/losses
- Risk: 0.5% per trade (high volume of trades)

---

## Real-World Position Sizing Example

### Scenario: Professional Trader

**Account Size**: $500,000
**Daily Risk Limit**: 2% = $10,000
**Target Win Rate**: 60%

**Today's Opportunities**:

**Trade 1**: AAPL
```
Entry: $150, Stop: $147 (3-point risk), Target: $156 (6-point profit)
R/R: 1:2 ✓
Position Size: $10,000 / 3 = 3,333 shares
Value at entry: $500K (oops, can't afford this!)
Recalculate: Risk $5,000 on this one (safer)
Position Size: $5,000 / 3 = 1,667 shares
```

**Trade 2**: TSLA
```
Entry: $250, Stop: $240 (10-point risk), Target: $275 (25-point profit)
R/R: 1:2.5 ✓
Position Size: $5,000 / 10 = 500 shares
Value at entry: $125,000 (25% of account) ✓
```

**Summary**:
- Total risk today: $10,000 (2% limit)
- AAPL: $5K at risk
- TSLA: $5K at risk
- If both stop out: Lose $10K (acceptable)
- If both hit targets: Win $20K (4% profit)
- Heat level: 2% (comfortable for day trader)
