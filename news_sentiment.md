# News Sentiment Engine — Positive/Negative Split Scoring

Verified live 2026-07-20 (AAPL test: 15 articles → 7 pos / 2 neg / 6 neutral).

## Data Source (verified working)

**Massive Market Data** — `call_api` with:
```
path: /v2/reference/news
params: {"ticker": "<SYMBOL>", "limit": 15, "order": "desc", "sort": "published_utc"}
```

- Returns per-article `insights` array with **per-ticker sentiment (positive/negative/neutral) AND sentiment_reasoning** — no manual sentiment guessing needed
- ⚠️ Output is large (~50KB for 15 articles) → gets saved to a file. Parse with python (csv + ast.literal_eval on `insights` column), filter insights to the target ticker only
- Coverage: US stocks strong; BIST coverage thin — if empty for Turkish stocks, label "haber verisi bulunamadı"
- Benzinga real-time news (`/benzinga/v2/news`) is plan-gated — don't use

## Scoring: Positive and Negative Scored SEPARATELY

The user sees BOTH sides — a stock can be 8/10 positive AND 6/10 negative simultaneously (contested narrative = volatility warning).

### Step 1: Relevance weight per article

| Article type | Weight |
|--------------|-------:|
| Direct company news (deal, product, earnings, guidance, litigation) | ×2 |
| Sector/indirect (analysis mentioning company meaningfully) | ×1 |
| Passive mention (ETF holding list, index composition, unrelated topic) | ×0.5 — or exclude |
| Neutral sentiment articles | not scored (report count only) |

### Step 2: Compute both scores

```
POZİTİF SKOR = min(10, weighted sum of positive articles)
NEGATİF SKOR = min(10, weighted sum of negative articles)
NET = POZİTİF − NEGATİF   (range −10…+10)
```

### Step 3: Interpretation

| Pattern | Read |
|---------|------|
| Poz yüksek, Neg düşük (8/2) | Tailwind — narrative supports the trend |
| Poz düşük, Neg yüksek (2/8) | Headwind — check if technicals confirm breakdown |
| BOTH high (7/7) | Contested story → elevated volatility, tighten stops |
| Both low (2/1) | No narrative — technicals dominate |
| Many neutral/passive only | Stock is "wallpaper" in others' stories — no signal |

### Step 4: Feed into GCstock Puanı (0-100)

News contributes the **Haber Duyarlılığı /10** component:
```
Haber puanı = 5 + NET/2   (clamped 0-10)
```
Örnek: Poz 8, Neg 3 → NET +5 → Haber 7.5 ≈ 7/10

## Report Display Rule

Always show the split — never just a net number:

```
📰 HABER DUYARLILIĞI (son X gün, Y haber)
├─ 🟢 POZİTİF: 8/10  (7 haber — en önemlisi: Intel çip anlaşması)
├─ 🔴 NEGATİF: 3/10  (2 haber — değerleme endişesi, kâr realizasyonu)
├─ ⚪ NÖTR: 6 haber (pasif değinme — puanlanmadı)
└─ NET: +5 → Anlatı trendi DESTEKLİYOR
```

Each side lists its top 2-4 headlines with date + one-line reasoning (from the API's sentiment_reasoning — cite, don't invent). In HTML reports: two-column panel, green/red headers, per-article rows.

## Cross-checks (judgment layer)

1. **News vs price action**: 7 positive articles but stock falling = distribution into good news (warning). Negative news but stock rising = strong hands absorbing (bullish).
2. **News vs insider**: positive news + insider selling = management selling into the hype (red flag).
3. **Freshness**: weight last 48h headlines over week-old ones when signals conflict.
4. **Single-source risk**: if all articles are one publisher, note it (narrative may be one desk's view).
