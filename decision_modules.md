# Decision-Support Modules — 14 Report Add-ons

These modules EXTEND the existing report (design, scoring, data sources unchanged). Add them naturally into the existing layout. Core principles: never fabricate data · unverifiable metrics = "Doğrulanamadı" · every estimate marked YORUM · user decides from ONE page.

## 1) Risk/Getiri Analizi
Auto-compute from entry zone, stop, TP1/TP2:
```
Risk: −%X.X | TP1: +%X.X | TP2: +%X.X
R/R (büyük göster): X.X  + yıldız: <1.2 kötü ★ · 1.2-2 normal ★★★ · 2-3 iyi ★★★★ · 3+ mükemmel ★★★★★
```
Compute R/R from ENTRY ZONE midpoint (not current price) for the planned trade; also state current-price R/R if different.

## 2) Olasılık Analizi (YORUM)
Probability per target, derived from: teknik trend + volatilite + momentum + haber akışı + direnç kuvveti + analist hedefleri.
```
TP1 görülme: %XX · TP2 görülme: %XX · Stop görülme: %XX   [YORUM]
```
Sanity: TP1% > TP2%; probabilities need not sum to 100 (different events).

## 3) Beklenen Holding Süresi (YORUM)
Auto-select from setup type: Scalp 1-3 gün · Swing 5-20 gün · Position 1-3 ay.
(Pullback-to-MA in trend = Swing; 200MA/deep-value entry = Position; breakout momentum = Scalp/Swing.)

## 4) Trend Gücü kutusu
★1-5 from EMA dizilimi + MACD + RSI (+ ADX from FMP if fetched):
★★★★★ Çok Güçlü (full stack + MACD poz + RSI 55-70) · ★★★☆☆ Yatay · ★★☆☆☆ Zayıf · ★ Düşüş

## 5) Volatilite kutusu
```
Beklenen günlük hareket: ±%X.X · Volatilite: Düşük / Normal / Yüksek
```
Use ATR if available; else compute from last 30 days' daily ranges (FMP chart data). Label the method.
Düşük <1% · Normal 1-2% · Yüksek >2% (günlük ortalama mutlak hareket).

## 6) Makro Riskler — "Önümüzdeki 30 Günün Riskleri"
Per stock, from news API + earnings calendar (+ general judgment labeled YORUM):
- US tech örnek: FED toplantısı · Bilanço tarihi · Tarifeler/Çin · AI harcama haberleri · Mega-cap bilanço haftası
- BIST örnek: Petrol · USDTRY · TCMB faiz kararı · Jeopolitik
Confirmed dates get VERİ chip; the rest YORUM.

## 7) Tahmin Güveni (%)
```
Güven = ortalama(Veri Kalitesi, Teknik Uyum, Temel Veri, Haber Yoğunluğu, Analist Uzlaşması)
```
Missing/unverified data AUTOMATICALLY lowers it (e.g., BIST fundamentals missing → Temel Veri ≤40). Show as % + which inputs dragged it down.

## 8) Pozisyon Büyüklüğü kutusu
From stop distance (risk-based): position% = hedef portföy riski / stop mesafesi.
```
Defansif (%0.25 risk): ~%X · Normal (%0.5 risk): ~%X · Agresif (%1 risk): ~%X
```
Cap all at 25% portfolio. Show stop distance used.

## 9) "NEDEN?" kutusu (EN ÖNEMLİ — her raporda zorunlu)
Max 4 bullets explaining the signal, e.g.:
- Neden BEKLE? → zirve bölgesi · F/K tarihsel üstü · R/R zayıf · daha iyi giriş mümkün
- Neden TUT? → trend bozulmadı · EMA20 korunuyor · MACD pozitif · satış sinyali yok
- Neden SAT? → momentum zayıflıyor · direnç bölgesi · R/R bozuluyor

## 10) 30 Günlük Senaryolar (YORUM)
```
Boğa %XX → $XXX · Baz %XX → $XXX · Ayı %XX → $XXX
```
Probabilities from teknik + haber + volatilite. Percentages sum to 100. 30-day horizon (NOT yearly).

## 10b) 3 / 6 / 12 Aylık Fiyat Projeksiyonu (ZORUNLU — her tam analizde)

Beyond the 30-day scenarios, every full report carries a three-horizon projection.

**Method (must be shown in the report):**
1. **Anchor the 12-month leg on consensus EPS** from `forward_looking.md` (`financial-estimates`): `epsLow × düşük çarpan` / `epsAvg × baz çarpan` / `epsHigh × yüksek çarpan`. EPS leg = VERİ (konsensüs), multiple = ÇIKARIM.
2. **Place 3M and 6M between today and the 12M leg** using the catalyst calendar (earnings dates, product/IPO events) — not straight-line interpolation.
3. **±1σ sanity check per horizon**: annualized vol × √(months/12). Flag any scenario outside its band as low probability, and say so in the table.
4. **Show the analyst consensus target** (typically a 12-month target) next to your own 12M base; if they diverge, state the reason (usually the multiple assumption) rather than hiding it.

**Display — PLAIN LANGUAGE TABLE FIRST, chart second.** The forecast card sits in the main decision grid (spanning full width) and uses everyday wording, not scenario jargon:

| Ne zaman | 🟢 İyi giderse | 🟡 Normal giderse | 🔴 Kötü giderse | Ne olursa böyle olur |
|---|---|---|---|---|
| **3 ay sonra**<br>Ekim 2026 | $285 · +%15<br>ihtimal %25 | **$255 · +%3<br>ihtimal %50 ← en olası** | $220 · −%11<br>ihtimal %25 | (olayın adı sade dille) |

Rules for this card:
- Column headers are **İyi / Normal / Kötü giderse** — never "Boğa/Baz/Ayı" as the primary label
- Every cell carries the price, the % change, AND the **gerçekleşme ihtimali**; the most likely one is highlighted with "← en olası"
- The three probabilities per row **sum to 100%** (unlike the touch-probability module, where they don't — say so explicitly wherever both appear)
- Last column explains the driver in one everyday sentence ("30 Temmuz bilançosu iyi gelirse yukarı…"), no indicator names
- Closing caption must state, in plain words: (a) the headline takeaway ("en olası senaryoda 1 yılda ~%10 kazanç, ama dörtte bir ihtimalle %25 kayıp"), (b) where the numbers come from ("43 analistin kâr beklentilerinden hesaplandı — uydurma değil"), (c) an honest caveat when a scenario sits outside the ±1σ band.

The SVG projection fan still appears later as the visual; this table is the answer.

Also surface the 12M base target in the top verdict box so it is visible without scrolling.

⚠️ Label the whole block ÇIKARIM and repeat the framing: **bunlar tahmin değil, gerekçeli aralıklardır.** Probabilities stay judgment unless option-implied data becomes available.

## 10c) BOĞA/AYI TERAZİSİ + Matematiksel Beklenti (ZORUNLU, tezlerin hemen altında)

The bull and bear cards state two arguments; the reader still needs to know **which side wins**. Answer it explicitly:

**1. Score the evidence.** Rate each bull and bear point 1-5 by strength, show them as labelled bars, and render the totals as a single split bar (`🐂 %X` vs `%Y 🐻`). If it comes out near 50/50, say so plainly — a balanced scoreboard IS the justification for a TUT signal.

**2. Split the verdict by horizon — this is usually the real answer.** Evidence rarely favors one side outright; it favors different sides at different times. State it:
- *"Kısa vadede (0-3 ay) AYI haklı: [reasons]. Beklenen 3 aylık getiri sadece +%X — beklemenin maliyeti neredeyse sıfır."*
- *"Uzun vadede (12 ay) BOĞA haklı: [reasons]. Beklenen 12 aylık getiri +%X."*

**3. Three headline numbers, computed from the scenario probabilities:**
- **Yükselme ihtimali** = sum of probabilities of scenarios ending above today's price
- **Düşme ihtimali** = the remainder
- **Matematiksel beklenti** = Σ(senaryo fiyatı × ihtimali) — the probability-weighted average price, shown with its % vs today. This is the single most useful number in the whole report: it folds direction AND magnitude into one figure.

**4. Close with the resolution**, naming why the math can lean one way while the evidence is tied: *"Kanıtlar 50/50 ama matematik boğa tarafında — çünkü kazanma ihtimali (%75) kaybetme ihtimalinden (%25) yüksek VE kazanç büyüklüğü (+%46) kayıp büyüklüğünden (−%25) fazla."*

## 10d) Grafik Okuma Kılavuzu (projeksiyon grafiğinin altında)

A fan chart is meaningless to a non-professional without a key. Under it, add a "📖 Grafiğe nasıl bakılır? — 30 saniyede oku" box explaining, in order: what the left dot is, what each coloured line means (marking the middle one as *"en olası yol — gözünü en çok buna dik"*), what the reference markers are (analyst consensus, 52-week high), **why the cone widens** (*"ne kadar ileriye bakarsan o kadar az emin olabilirsin — uzak tahminlere daha az güven"*), and finally the one-glance takeaway (slope of the middle line, whether the upside area is larger than the downside, and what the near-term narrowness implies).

## 11) Skorlama Tablosu (özet, ★1-5)
Risk/Getiri · Trend · Momentum · Temel · Haber · Volatilite (düşük vol = çok yıldız) · Güven

## 12b) 🎯 SONUÇ — Uygulanabilir Karar Planı (raporun EN SONU, zorunlu)

The report must end with a section the reader can act on without re-reading anything above. Not a summary — **instructions**. Four labelled paths in a bordered card:

**🅰️ HİSSEM YOK — almak istiyorum** (numbered steps)
1. An explicit **AL / ALMA** verdict for today, with the 2-3 reasons in everyday words
2. The exact price to wait for + why that level (confluence) + the probability of reaching it
3. What to do when it arrives: scale in (half first), what confirmation to look for, when to complete
4. The stop price and what % loss it caps
5. The alternative scenario (upside breakout entry) with a smaller size
6. What to do if neither happens ("alma, fırsat maliyeti düşük")
7. Position size in portfolio %, plus what the worst case costs of the TOTAL portfolio

**🅱️ HİSSEM VAR — ne zaman satayım**
- TUT / SAT verdict with the reason
- Pre-event trim guidance if a binary event is near
- Short-term sell ladder (prices + %)
- Long-term sell ladder (prices + %), explicitly marking the fair-value level as "SATMA — orası adil değer"
- The unambiguous ANINDA SAT condition

**⏳ KISA VADE Mİ, UZUN VADE Mİ** — pick one and defend it with 3 reasons, usually built on the expected-return gap between horizons. Add the position-splitting note if the reader wants both.

**🚨 NE OLURSA FİKRİMİ DEĞİŞTİRİRİM** — 3 concrete, checkable invalidation conditions (a price level, a business metric, a cash-flow milestone).

Close with a single bold **"📌 TEK CÜMLEYLE:"** line containing the whole decision, then the disclaimer.

Rule: every number in this section must already appear earlier in the report — the conclusion synthesizes, it never introduces new analysis.

## 12) Rapor Sonu Özeti
One sentence per stock, e.g.: "Trend güçlü ancak değerleme pahalı olduğu için yeni alım yerine geri çekilme beklenmesi daha avantajlı."

## 13) Veri Kuralları (mutlak)
NEVER estimate: F/K, PD/DD, EPS, bilanço, insider, analist verisi → API doğrulamazsa "Doğrulanamadı".
ONLY these may be estimated (ALL marked YORUM): fiyat senaryoları, olasılıklar, hedef ihtimalleri, beklenen süre, volatilite tahmini.

## 14) Tasarım
Same colors, same boxes, same fonts as existing GCstock design. New modules slot in naturally. One-page decision flow preserved; mobile intact; "Karar Özeti" (signal banners) stays FIRST. Feel: professional investment decision-support system, not just TA.

## Placement order in report
1. Karar Özeti (sinyal banner) — mevcut
2. GCstock Puanı — mevcut
3. **NEDEN? kutusu** (#9)
4. Karar Kutusu (verdict) — mevcut
5. **Risk/Getiri + Olasılık + Süre** (#1, #2, #3) tek satırda
6. **Trend Gücü + Volatilite + Tahmin Güveni + Pozisyon** (#4, #5, #7, #8) viz-grid
7. Pahalı/Ucuz + Satış Planı — mevcut
8. 1Y grafik + indikatör kartları — mevcut
9. **30 Günlük Senaryolar** (#10)
10. **Makro Riskler** (#6)
11. Analist + Haber panelleri — mevcut
12. **Skorlama Tablosu** (#11) + **Tek cümle özet** (#12)
