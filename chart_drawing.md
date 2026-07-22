# Chart Drawing & Visualization Capabilities

## Overview

The skill can generate professional technical analysis charts showing:
- Price action with candlesticks
- Key support/resistance levels
- Entry/exit zones
- Price patterns (identified or potential)
- Volume profile
- Technical indicators (optional)
- Risk/reward visualization

---

## Chart Types

### 1. Technical Setup Chart

**Shows**:
- Recent price action (20-50 bars depending on timeframe)
- Weekly + Daily price levels overlaid
- Support/resistance zones (shaded or line-marked)
- Entry zone (highlighted)
- Target levels (TP1, TP2)
- Stop loss level (below support)
- Pattern identification (if applicable)

**Format**: SVG or detailed description

**Example Elements**:
```
Stock: AAPL, Daily Timeframe

[Chart showing]
- 50-day moving average (as support)
- 200-day moving average (as long-term trend)
- Resistance at $160 (tested 3x)
- Support at $145 (tested 2x)
- Entry zone shaded: $148-$150
- Target 1: $155 (TP1)
- Target 2: $160 (TP2)
- Stop: $144 (below support)
```

### 2. Pattern Recognition Chart

**Shows**:
- Identified pattern (H&S, Double Bottom, Triangle, Wedge)
- Pattern measurements
- Breakout level
- Measured move target
- Historical pattern accuracy overlay

**Example**: Head & Shoulders Reversal
```
[Chart showing]
- Left shoulder peak
- Head peak (higher than shoulders)
- Right shoulder peak (lower than head)
- Neckline support
- Breakout point
- Measured move target calculated
```

### 3. Multi-Timeframe Alignment Chart

**Shows**:
- Weekly trend with key levels
- Daily setup within weekly context
- 4H entry confirmation zone
- Color-coded by timeframe

**Example**:
```
Weekly (Green - Uptrend):
- Price above 200-week MA
- Making higher lows

Daily (Blue - Setup):
- Pullback to 50-day MA
- Volume declining (consolidation)
- About to test support

4H (Orange - Entry):
- Bounced off 50-day MA
- Ready for breakout confirmation
```

### 4. Value Investor Chart

**For buy-side analysis**, shows:
- Stock price vs. valuation levels
- Intrinsic value zones
- Margin of safety visualization
- Insider buying level marked
- 52-week high/low context

**Example**:
```
[Chart showing]
- Stock price line: $100
- Intrinsic value estimate: $130 (target)
- Fair value zone: $120-$135 (shaded)
- Margin of safety: 20% ($100-$120)
- 52W high: $145 / 52W low: $75
- Insider buying price: $98 (marked)
```

### 5. Risk/Reward Visualization

**Shows**:
- Entry price
- Stop loss distance
- Target distances
- Risk/Reward ratio visual
- Probability-weighted outcomes

**Example**:
```
Entry: $100
Stop: $95 (5-point risk)
Target 1: $110 (10-point profit, 2:1 R/R)
Target 2: $115 (15-point profit, 3:1 R/R)

Visualization:
Risk Zone:  ▄▄ (5 points down = STOP)
Entry:      ■  (Current price)
Target 1:   ▀▀ (10 points up)
Target 2:   ▀▀ (15 points up)
```

---

## Chart Data Requirements

To generate accurate charts, provide:

### Essential Data
- **Stock ticker**: AAPL, MSFT, THYAO.IS
- **Current price**: $150 (approximate)
- **Timeframe**: Daily, Weekly, 4H
- **Period**: How many bars? (typically 20-50)

### Technical Levels
- **Support level(s)**: $145, $140
- **Resistance level(s)**: $155, $160
- **Moving averages**: 20MA, 50MA, 200MA prices
- **Key zones**: Entry $148-$150, TP1 $155, TP2 $160

### Optional Enhancements
- **Volume data**: High/low volume bars
- **Patterns**: Identified (H&S, Double Bottom, etc.)
- **Indicators**: RSI value, MACD status
- **Insider activity**: Insider buy price marked
- **Earnings**: Next earnings date marked

---

## Chart Output Formats

### Format 1: SVG/Vector Graphics

Clean, scalable technical charts with:
- Price candlesticks/bars
- Trendlines
- Support/resistance zones (shaded or solid)
- Entry/exit annotations
- Text labels for levels and patterns

**Advantages**:
- Professional appearance
- Crisp on all screen sizes
- Can be exported/printed
- Interactive capability (on web)

### Format 2: Detailed Text Description

ASCII-art style or detailed prose description:
```
AAPL Daily Chart (Last 30 days):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Resistance:    $160 ────────────────── (tested 3x)
                    │
Entry Zone:    $148-$150  ░░░░░░░░░░░░
                    │
50-day MA:     $147 ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌
Support:       $145 ────────────────── (tested 2x)
                    │
Target 1:      $155 ━━━━━━━━━━━━━━━━━━
Target 2:      $160 ═══════════════════

Stop Loss:     $144 ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ (EXIT if broken)
```

**Advantages**:
- Quick to generate
- Detailed textual description
- No dependency on graphics library

---

## When to Generate Charts

### Always Provide Chart When:
1. ✅ User explicitly requests ("Draw the setup", "Show me chart")
2. ✅ User is newer/less experienced trader (visual helps understanding)
3. ✅ Setup is complex (multiple patterns, timeframes)
4. ✅ For buy-side value trades (show mispricing visually)
5. ✅ When insider buying is relevant (mark buy levels)

### Optional/Skip Chart When:
- ⚠️ User is experienced professional (may not need it)
- ⚠️ Setup is very simple (obvious breakout)
- ⚠️ User specifically says "no chart needed"
- ⚠️ Time constraint (focus on recommendation first)

---

## Chart Integration with Recommendation

### Chart Annotation Standards

**Entry Zone**:
- Mark as shaded area or highlighted box
- Label with "ENTRY ZONE $XXX-$XXX"
- Note what confirms entry (e.g., "On 4H breakout")

**Target Prices**:
- Mark with horizontal lines
- Label "TP1: $XXX" and "TP2: $XXX"
- Show distance/profit percentage

**Stop Loss**:
- Mark with red line or ╌╌╌ pattern
- Label "STOP $XXX" (EXIT if broken)
- Below support level

**Support/Resistance**:
- Horizontal lines for confirmed levels
- Lighter color for untested levels
- Mark number of times tested (3x, 2x, etc.)

**Patterns**:
- Draw pattern outline if identifiable
- Label pattern type ("Head & Shoulders Reversal")
- Show measured move target

---

## Example: Complete Chart with Analysis

```
═══════════════════════════════════════════════════════════════════════════════
AAPL DAILY TECHNICAL SETUP - AL/SAT/TUT RECOMMENDATION
═══════════════════════════════════════════════════════════════════════════════

                                    RESISTANCE
                                    $160 ═════════════════════════════════════
                                         (Rejected 3x, breakout with volume = target)
                                         
                      TP2 (Profit Target 2)
                      $155 ═══════════════════════════════════════════════════
                            ╱╲
                           ╱  ╲       
                          ╱    ╲    ENTRY ZONE
                         ╱      ╲   $148-$150 ▓▓▓▓▓▓▓▓▓▓▓
ENTRY ZONE             ╱        ╲ ▓        ╱ (Pullback to 50MA)
$148-$150 ▓▓▓▓▓▓▓▓▓▓  ╱          ╲▓        ╱ 
         ▓           ╱────50MA────╲──────╱
        ▓           ╱              ╲    ╱
       ▓           ╱                ╲  ╱
TP1    ▓          ╱                  ╲╱
$155 ════════════════════════════════════════════════════════════════════════

Support Level (Strong)
$145 ─────────────────────────────────────────────────────────────────────────
     (Tested 2x, holding well)
                                    
Stop Loss (Below Support)
$144 ╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌ (EXIT if closes below)

═══════════════════════════════════════════════════════════════════════════════

AL (BUY):  $148-$150 entry zone on pullback to 50MA
SAT (SELL): TP1 at $155 (profit taking) or TP2 at $160 (if breakout holds)
TUT (HOLD): Hold 4-6 weeks or until one of targets hit

Risk/Reward: $1,000 max loss (stop) | $5,000-$10,000 profit potential = 1:5-1:10
```

---

## Chart Best Practices

### ✅ DO:
- Show clearly marked entry/exit levels
- Include support/resistance with test count
- Mark current price prominently
- Use colors/patterns for visual clarity
- Label all key levels with prices
- Show timeframe used (Daily, 4H, etc.)
- Include pattern identification if present
- Note volume if relevant

### ❌ DON'T:
- Overcrowd chart with too many indicators
- Use unclear or inconsistent symbols
- Forget to mark stop loss level
- Assume reader will understand abbreviations
- Mix timeframes without clear labels
- Show extremely detailed 200-bar history (keeps it to relevant 20-50 bars)
- Forget to note what confirms the entry

---

## Visualization Tools

The skill can use:
1. **SVG Graphics**: Clean vector charts
2. **ASCII Art**: Text-based charts
3. **Markdown Tables**: For technical levels summary
4. **HTML/CSS**: Interactive charts (if displayed web)
5. **TradingView Integration**: Embed live charts if available

---

## Special: Insider Activity Visualization

For insider analysis, chart can show:
- Stock price line over past 6-12 months
- **Mark insider buy prices**: Where insiders bought (green dots)
- **Mark insider sell prices**: Where insiders sold (red dots)
- Cluster buying events highlighted
- 52-week high/low marked
- Insider conviction level color-coded

**Example**:
```
Stock Price History (6 months)
$180 ─────────────────────── 52W High
     │
$165 │
     │              CEO Buy ●
$150 │           ✓ (Cluster)  ✓ Director Buy
     │         ●              ●
$135 │    ✓ CFO Buy
     │  ●
$120 │    ▼ Down 20% (earnings miss)
     │
     └─────────────────────── 
       Month1  2   3   4   5  6

GREEN DOTS = Insider buying (bullish)
Cluster = 3+ insiders buying same timeframe
```

This visualization shows management confidence during stock weakness = high conviction signal.
