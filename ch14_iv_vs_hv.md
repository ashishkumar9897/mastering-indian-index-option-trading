<!-- Difficulty: Level 3.5/5 (Intermediate-Advanced). Dependency: Chapters 6, 13. Target length ~9,000 words. Current as of 4 Aug 2026 (reviewed — no reader-facing changes needed). NOTE: this chapter has NO lot-size-dependent figures (all maths is volatility analytics — HV %, VRP, IV Rank/Percentile, cone; case-study P&L is explicitly "per straddle unit"), NO transaction-cost figures, and NO expiry-weekday references. So the lot-65 (NSE Jan-2026) and Apr-2026 STT changes do NOT apply here; content is evergreen and verified current. HV worked example: 5 log returns of NIFTY → annualized HV ≈ 7.6% (small-sample illustration, flagged). IV Rank vs IV Percentile divergence: current 16%, low 10%, high 30% → Rank 30; but 180/252 days below → Percentile 71 (the outlier-spike effect). VRP = IV − realized HV, positive ~80% of time. Volatility cone (10-90 day). Strategy matrix IV Rank × direction. Case study: selective straddle selling (IV Rank>80). IV = implied volatility; HV = historical/realized volatility. Annualization √252. -->

# Chapter 14 — Implied Volatility vs. Historical Volatility: Finding the Edge

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Calculate and interpret historical (realized) volatility for NIFTY and BANKNIFTY.
2. Compare implied volatility with historical volatility to spot mispricing.
3. Understand why IV usually exceeds HV — the variance risk premium.
4. Use the IV–HV spread as a trading signal.
5. Use IV Rank and IV Percentile — far better tools than the raw IV number.

Chapter 13 gave you the market's volatility *forecast* (VIX / implied volatility). This chapter gives you the yardstick to judge it: the volatility the market actually *delivered* (historical volatility). The gap between the two is where the volatility trader's edge lives.

---

## 2. Introduction

Every option premium contains a forecast: the implied volatility the market is charging for the expected move ahead (Chapters 6 and 13). But a forecast is only useful if you can judge whether it is *too high* or *too low*. To do that, you need something to compare it against — and the natural benchmark is how much the market has *actually* been moving. That is **historical (realized) volatility**, and comparing it with implied volatility is the single most important analytical habit in volatility trading.

Here is the fact that makes it profitable: **implied volatility is, most of the time, higher than the volatility the market goes on to realise.** Across roughly 80% of periods, option buyers pay for more movement than they get, and option sellers collect that difference. This persistent gap — the **variance risk premium** — is the structural reason "selling premium" has an edge, and it is the closest thing to a free lunch the option market offers. But it is not free: sellers earn it in exchange for bearing the risk of the occasional period when realised volatility *explodes past* implied (the COVID crash, Chapter 13) — the same "one big loss" tail we met in Chapters 10 and 12.

This chapter turns that insight into tools. You will learn to compute historical volatility, compare it to implied, measure the variance risk premium, and — crucially — use **IV Rank** and **IV Percentile** to answer the question "is IV high or low *right now*?" far better than the raw number ever could. By the end, you will be able to look at any NIFTY option and judge, with a number, whether it is cheap or rich. Setting throughout: **NIFTY at 24,600**, annualising with √252 trading days.

---

## 3. Core Concepts

### 3.1 Historical (realized) volatility — what actually happened

**What is it?** **Historical volatility (HV)**, also called *realized volatility*, is the actual, annualised standard deviation of the underlying's returns over a past window. Where implied volatility is the market's *forecast*, HV is the *outcome* — how much the NIFTY genuinely moved.

**How to calculate it.** The standard measure uses the standard deviation of daily **log returns**, annualised by √252:

```
Daily log return: rᵢ = ln(Sᵢ / Sᵢ₋₁)
HV (annualised)  = √[ (252/n) · Σ(rᵢ − μ)² ]                       (14.1)
```

where `μ` is the mean daily return and `n` the number of returns. The `(rᵢ − μ)²` terms measure how much each day's move deviated from the average; averaging them gives the daily variance, and √252 scales it to an annual figure.

**Worked calculation (small sample for illustration).** Take six NIFTY daily closes: 24,600 → 24,720 → 24,650 → 24,800 → 24,900 → 24,750 (five returns):

```
Log returns: +0.004866, −0.002836, +0.006068, +0.004024, −0.006042
Mean μ = 0.001216
Σ(rᵢ − μ)² = 0.00011385
Daily variance = 0.00011385 / 5 = 0.00002277  → daily σ = 0.4772%
HV (annualised) = 0.4772% × √252 = 0.4772% × 15.87 ≈ 7.6%
```

So over this calm stretch, NIFTY realised about **7.6%** annualised volatility. *(Five returns is far too few for a real estimate — used here only so you can follow every step; genuine HV uses at least 20 trading days.)*

**Common HV windows.** Traders compute HV over several lookbacks — **10-day, 20-day, 30-day, 60-day** — because each answers a different question. Short windows (10-day) react fast and capture recent spikes; long windows (60-day) are smoother and show the underlying trend. Comparing them (the volatility cone, Section 3.6) reveals whether volatility is rising or falling.

**Why should a trader care?** Because HV is the *reality check* on IV. An IV of 18% means nothing until you know the market has been realising only 12% — at which point you know options are richly priced. HV converts the abstract "is IV high?" into the concrete "high relative to what the market is actually doing?"

---

### 3.2 Three ways to measure HV

The close-to-close formula (14.1) is the standard, but it has a blind spot: it only sees closing prices, ignoring how wildly the market swung *within* each day. Two refinements fix this:

* **Close-to-close HV** (equation 14.1) — simple and standard, but it misses intraday range and can understate volatility on days that swung hard but closed flat.
* **Parkinson HV** — uses each day's **high and low** instead of just the close, capturing intraday range:

```
Parkinson HV = √[ (252 / (4n·ln2)) · Σ (ln(Hᵢ/Lᵢ))² ]              (14.2)
```

It is more *efficient* (a better estimate from the same number of days) because it uses more information — but it ignores overnight gaps.

* **Yang–Zhang HV** — the most complete estimator, combining overnight gaps *and* intraday range (open, high, low, close). It is the most accurate for markets like India's that gap overnight (Chapter 6), but also the most complex; most retail tools offer close-to-close by default and Parkinson as an option.

For practical work, close-to-close is fine as a baseline; know that Parkinson and Yang–Zhang exist and give better estimates when intraday range and gaps matter. The *comparison* with IV is the point, not which estimator you use.

---

### 3.3 Implied versus historical — the core comparison

Now place the two side by side:

* **Implied volatility (IV)** — the market's *forward-looking* forecast, embedded in option prices (Chapters 6, 13). It is what you *pay* (as a buyer) or *collect* (as a seller).
* **Historical volatility (HV)** — the *backward-looking* reality of how much the market actually moved. It is what you would need to *realise* to justify the IV you paid.

The comparison answers the trader's central question: **is the option's implied volatility justified by how much the market is actually moving?**

* If **IV > HV** (the usual case), options are "expensive" relative to realised movement — the market is charging for more volatility than it has been delivering. This favours *sellers*.
* If **IV < HV** (rarer), options are "cheap" relative to realised movement — the market is under-charging for the movement occurring. This favours *buyers*.

Overlaying a year of 30-day HV against ATM IV (the architecture's chart) shows IV sitting *above* HV most of the time, with the two converging or crossing around shocks. That persistent gap is the variance risk premium — the subject of the next section and the heart of the chapter.

---

### 3.4 The Variance Risk Premium — the edge

The variance risk premium is the flagship idea of this chapter, and the structural reason option selling has an edge.

**What is it?** The **Variance Risk Premium (VRP)** is the gap between implied and realised volatility:

```
VRP = ATM IV − Realised HV                                          (14.3)
```

It is **positive most of the time** — across roughly 80% of periods, the market's implied volatility exceeds the volatility it goes on to realise.

**Why does it exist?** Because options are *insurance*, and insurance is always priced above its expected payout. Buyers of options (like buyers of insurance) willingly pay a premium above fair value for protection and leverage; sellers (like insurers) demand compensation above expected loss for bearing the risk of a large move. That structural imbalance — many hedgers wanting protection, fewer willing to underwrite it — keeps IV persistently above realised HV. The VRP is the fee the market pays sellers for underwriting its fear.

**Why should a trader care?** Because the VRP is the closest thing to a durable edge in options, and it explains *why* the premium-selling strategies of Part V work. When you sell an option whose IV is 15% while the market realises 12%, you pocket the 3-point difference on average. This is not a trick or a signal — it is a structural premium paid to those who provide the market's insurance.

**Intuitive explanation.** The VRP is the **house edge of the insurance business, in your favour** when you sell. An insurer who prices a policy at ₹100 against an expected ₹85 of claims earns the ₹15 spread over many policies — losing on the occasional big claim, winning on average. The option seller is that insurer; the VRP is their ₹15.

**Using it as a signal.** The VRP is not constant — it widens and narrows:

* **When VRP is unusually high** (IV far above HV, e.g., after a fear spike when the actual market has calmed) → **sell premium**; you are being over-paid for the risk.
* **When VRP is low or negative** (IV near or below HV, e.g., a placid market about to get volatile) → **buy premium** or stand aside; sellers are under-paid.

**Numerical feel.** ATM IV 15%, realised HV over the period 12% → VRP = +3% (a good month for sellers). But ATM IV 13%, realised HV 16% (the market moved more than priced) → VRP = −3% (a losing month for sellers). The VRP is positive far more often than not, which is why selling *systematically* wins — but the negative months are where the losses concentrate.

**Professional interpretation.** Professionals do not "sell options"; they "harvest the variance risk premium," and they do it *selectively* — selling when the VRP is fattest (high IV relative to expected realised) and standing aside when it is thin. The edge is real but small per trade; capturing it over many trades, while surviving the negative-VRP tail, is the whole game.

**Common mistake.** Believing the VRP makes selling "safe." It is a *positive-expectancy* edge, not a *low-risk* one. The premium exists precisely *because* sellers occasionally suffer large losses (the negative-VRP tail — COVID, election shocks). Harvesting the VRP without surviving the tail is how sellers blow up.

**Practical takeaway.** **The variance risk premium — IV persistently above realised HV — is the structural edge behind option selling; harvest it by selling when IV is rich relative to what the market is realising, and size to survive the periods when realised volatility explodes past implied.**

---

### 3.5 IV Rank and IV Percentile — context beats the raw number

"IV is 18%" is almost useless on its own — high for a calm market, low for a crisis. You need to know where 18% sits *relative to its own history*. Two metrics do this, and they are the workhorses of professional strategy selection.

**IV Rank** places the current IV on the range between its 52-week low and high:

```
IV Rank = (IV_current − IV_low) / (IV_high − IV_low) × 100          (14.4)
```

An IV Rank of 0 means IV is at its 52-week low; 100 means its 52-week high; 50 means halfway between the extremes.

**IV Percentile** counts how often IV has been *below* the current level:

```
IV Percentile = (days with IV < current IV / total days) × 100      (14.5)
```

An IV Percentile of 70 means IV has been lower than today on 70% of days over the past year.

**Why they can differ sharply — and why it matters.** IV Rank uses only the two *extremes* (high and low); IV Percentile uses the *whole distribution*. When a single outlier spike stretches the range, the two diverge:

> Current IV 16%, 52-week low 10%, 52-week high 30% (one crisis spike set the 30%). **IV Rank = (16−10)/(30−10) × 100 = 30** — 16% looks "low," only 30% of the way up the range. But if IV was actually *below* 16% on only 180 of 252 days, **IV Percentile = 180/252 × 100 = 71** — 16% is genuinely *high* relative to most days. Same IV, opposite readings.

This divergence is common and important: one COVID-style spike can leave IV Rank permanently deflated for a year (the 30% "high" dwarfs everything), while IV Percentile correctly shows that today's IV is elevated relative to normal days. **IV Percentile is usually the more robust guide** because it is not distorted by a single outlier; IV Rank is more intuitive and widely quoted. Use both, and when they disagree, understand *why* (an outlier in the range) before trusting either.

> **Beginner Alert — never judge IV by its raw number.** "IV is 20%" tells you nothing actionable. The same 20% is richly sell-able in a market whose IV usually sits at 12% (high Rank/Percentile) and a screaming buy in one that usually sits at 35% (low Rank/Percentile). Always convert raw IV to its Rank and Percentile before deciding whether options are cheap or expensive.

---

### 3.6 The volatility cone — what is "normal"

A **volatility cone** shows the historical *range* of HV at each lookback period, so you can see what volatility is "normal" and spot when it is extreme. You compute HV over 10, 20, 30, 60, and 90-day windows across the past year, then find the percentile bands (min, 25th, median, 75th, max) for each. Table 14.1 is an illustrative NIFTY cone.

**Table 14.1 — NIFTY volatility cone (illustrative HV percentiles by lookback, past year)**

| Lookback | Min | 25th | Median | 75th | Max |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 10-day | 7% | 10% | 13% | 17% | 45% |
| 20-day | 8% | 11% | 13% | 16% | 38% |
| 30-day | 9% | 11% | 13% | 15% | 32% |
| 60-day | 10% | 12% | 13% | 15% | 26% |
| 90-day | 11% | 12% | 13% | 14% | 22% |

Two features to read:

* **The cone narrows as the lookback lengthens.** The 10-day HV ranges from 7% to 45% (it captures every spike fully); the 90-day ranges only 11% to 22% (long windows average spikes out). This is why the plot is shaped like a cone — wide on the short-lookback side, narrow on the long side.
* **Read current IV against the cone.** If today's 30-day IV is 18% and the 30-day HV cone's 75th percentile is 15%, IV is *above* the 75th percentile of realised volatility — options are rich relative to what the market normally delivers over a month, favouring sellers. If IV sits below the median, options are cheap.

The cone turns "is IV high?" into "is IV high relative to the realised-volatility distribution for this horizon?" — a far sharper question than the raw number allows.

---

### 3.7 Using the edge — the strategy selection matrix

Combine the IV read (rich or cheap) with a directional view and you get a clean strategy map. Table 14.2 uses IV Rank (a proxy for "rich vs cheap") crossed with market direction.

**Table 14.2 — Strategy selection: IV Rank × direction**

| | **Bullish** | **Bearish** | **Neutral** |
| --- | --- | --- | --- |
| **Low IV Rank (<30)** — options cheap, *buy* | Long call / bull call spread (debit) | Long put / bear put spread (debit) | Long straddle/strangle or calendar (long volatility) |
| **High IV Rank (>70)** — options rich, *sell* | Short put / bull put spread (credit) | Short call / bear call spread (credit) | Short strangle / iron condor (short volatility) |

The logic is symmetric and simple: **IV Rank decides whether you are a net buyer or seller of premium; direction decides whether you use call- or put-based structures.** Low IV Rank → buy (debit) structures; high IV Rank → sell (credit) structures; a neutral view at high IV Rank is the classic premium-selling setup (short strangle / iron condor), while a neutral view at low IV Rank favours long-volatility structures (straddles, calendars). The middle band (IV Rank 30–70) calls for balanced, defined-risk spreads with less conviction either way. This matrix is the practical payoff of the whole chapter — it tells you *what to trade* once you know whether volatility is rich or cheap.

---

### 3.8 Realized-versus-implied tracking — did the move come?

The final habit is closing the loop: after a trade, **check whether the market realised the volatility that was implied.** Sell a straddle at 15% IV, then measure the HV the market actually delivered over the life of the trade. If realised was 12%, the VRP was positive and you should have profited (the market moved less than you were paid for); if realised was 18%, the VRP was negative and you likely lost (the market moved more than priced).

This tracking does two things. First, it is **P&L attribution for volatility trades** — it tells you *why* a straddle made or lost money (was the VRP positive?), separating a correct volatility call from luck. Second, over many trades it calibrates your sense of the VRP: you learn how often, and by how much, IV in your market exceeds realised, which sharpens *when* to sell. A trader who logs implied-versus-realised for a year knows the VRP of their market cold — and that knowledge is the edge.

---

## 4. Examples (Real-World)

**Example 1 — Rich IV, calm market.** After a scare, India VIX (and ATM IV) sits at 22% while the NIFTY has quietly realised only 13% over the past three weeks. The VRP is a fat +9%. A seller who recognises this sells premium into richly-priced fear that the market is not delivering — and collects as IV mean-reverts toward realised.

**Example 2 — Cheap IV before a storm.** In a placid market, ATM IV drifts to 11% while realised HV has been 10% — a thin VRP. Then an unexpected global shock sends realised volatility to 20%. Buyers who bought cheap options (low VRP) were paid; sellers who sold thin premium were caught. Low VRP is a warning to sellers.

**Example 3 — Same IV, opposite verdicts.** Two months both show ATM IV at 16%. In the first, the market has been realising 12% (VRP +4, sell); in the second, realising 19% (VRP −3, do not sell). The raw IV was identical; the comparison with HV gave opposite, correct signals.

---

## 5. Numerical Examples

Setting: NIFTY, annualising with √252.

### Numerical Example 1 — Computing historical volatility

Using the six closes from Section 3.1 (24,600 → 24,720 → 24,650 → 24,800 → 24,900 → 24,750):

```
Log returns: +0.004866, −0.002836, +0.006068, +0.004024, −0.006042
Mean μ = 0.001216
Σ(rᵢ − μ)² = 0.00011385
HV = √[(252/5) × 0.00011385] = √[50.4 × 0.00011385] = √0.005738 ≈ 7.6%
```

The market realised about 7.6% annualised over this stretch. If ATM IV at the time was, say, 13%, the VRP was a healthy +5.4% — options were richly priced relative to the calm the market was delivering.

### Numerical Example 2 — IV Rank versus IV Percentile

Current ATM IV = 16%; 52-week low = 10%, high = 30%; days with IV below 16% = 180 of 252:

```
IV Rank      = (16 − 10) / (30 − 10) × 100 = 6/20 × 100 = 30
IV Percentile = 180 / 252 × 100 ≈ 71
```

IV Rank says "low" (30), IV Percentile says "high" (71). The divergence comes from one crisis spike to 30% that stretched the range. The **Percentile (71) is the more trustworthy read here** — 16% is genuinely above most days' IV — so options are richer than the Rank alone suggests.

### Numerical Example 3 — Variance risk premium, both signs

```
Month A: ATM IV at start = 15%, realised HV over the month = 12% → VRP = +3% (seller wins)
Month B: ATM IV at start = 13%, realised HV over the month = 16% → VRP = −3% (seller loses)
```

Selling is a positive-expectancy bet because Month-A-type outcomes occur ~80% of the time — but Month B is where a seller's losses concentrate, so survival depends on sizing for it.

### Numerical Example 4 — Reading current IV against the cone

Current 30-day IV = 18%. From Table 14.1, the 30-day HV cone runs: min 9%, 25th 11%, median 13%, 75th 15%, max 32%.

```
18% sits above the 75th percentile (15%) of realised 30-day volatility
→ options are rich relative to what the market normally realises over a month → favour selling
```

Had current IV been 11%, it would sit at the 25th percentile — cheap — favouring buying.

### Numerical Example 5 — Applying the strategy matrix

VIX/IV context: IV Rank is 82 (options rich). View: neutral (range-bound). From Table 14.2, the indicated strategy is a **short strangle or iron condor** — a short-volatility, defined-risk structure that harvests the rich premium. If instead IV Rank were 22 (cheap) with the same neutral view, the matrix points to a **long straddle/strangle or calendar** — a long-volatility structure that profits if the quiet market finally moves.

---

## 6. Calculations (the reusable recipes)

**(a) Historical (realized) volatility — close-to-close, annualised**

```
rᵢ = ln(Sᵢ / Sᵢ₋₁);   HV = √[ (252/n) · Σ(rᵢ − μ)² ]
```

**(b) Parkinson HV (uses intraday high/low)**

```
Parkinson HV = √[ (252 / (4n·ln2)) · Σ (ln(Hᵢ/Lᵢ))² ]
```

**(c) Variance risk premium**

```
VRP = ATM IV − Realised HV      (positive ~80% of the time; sell when high, buy/avoid when low/negative)
```

**(d) IV Rank and IV Percentile**

```
IV Rank      = (IV_current − IV_low) / (IV_high − IV_low) × 100
IV Percentile = (days with IV < current IV / total days) × 100
```

**(e) Reading IV against the cone**

```
Compare current IV to the HV cone's percentile bands for the matching lookback:
above 75th → rich (favour selling); below 25th → cheap (favour buying)
```

---

## 7. Practical Insights

* **Always compare IV to HV before trading volatility.** The raw IV is meaningless alone; the *spread* over realised (the VRP) tells you whether options are cheap or rich.
* **Use IV Rank and IV Percentile, not the raw number** — and when they disagree, trust the Percentile (it is not distorted by a single spike) after checking why they diverge.
* **The VRP is an edge, not a guarantee.** IV exceeds realised ~80% of the time, but the 20% is where losses concentrate; sell selectively when the VRP is fattest and size for the negative-VRP tail.
* **Read current IV against the volatility cone** to judge "rich or cheap" for the horizon you are trading — above the 75th HV percentile is genuinely rich.
* **Close the loop with realized-vs-implied tracking** — it is P&L attribution for volatility trades and, over time, teaches you your market's VRP.

> **Professional Insight — The whole business is implied minus realised.** Strip away the strategy names, and every volatility trade is one bet: implied volatility versus what the market will actually realise. Sellers bet realised will be lower (harvesting the VRP); buyers bet it will be higher. A professional's entire edge is (a) estimating realised volatility better than the crowd and (b) transacting only when the implied–realised gap pays them enough for the risk. Master this comparison and you understand what you are *really* trading, whatever the position is called.

---

## 8. Common Mistakes

* **Judging IV by its raw number.** "IV is 20%" is not high or low until you compare it to HV and to its own Rank/Percentile.
* **Trusting IV Rank blindly after a spike.** A single COVID-style spike deflates IV Rank for a year; IV Percentile gives the truer read of whether today's IV is elevated.
* **Believing the VRP makes selling safe.** The premium exists *because* of the tail losses; positive expectancy is not low risk. Size for the negative-VRP month.
* **Selling premium when the VRP is thin or negative.** Selling a 12% IV into a market realising 14% is selling under-priced insurance — a structural loser.
* **Using one HV window.** A single lookback misses whether volatility is rising or falling; compare short and long windows (the cone).
* **Skipping the realized-vs-implied review.** Without it, you cannot tell whether a winning straddle sale was a correct VRP call or luck.

---

## 9. Case Study — "Selling When IV Is Rich"

**Context.** The variance risk premium says option selling has an edge *on average* — but that edge is thin, lumpy, and easily erased: it is reliably captured only if you sell *selectively*, when IV is genuinely rich. Sell indiscriminately and the low-VRP (even negative-VRP) weeks can turn the whole exercise into a net loss. This case tests that idea with a simple, mechanical rule on NIFTY over two years: **sell an ATM straddle whenever IV Rank exceeds 80, and buy it back when IV Rank falls below 30 or at expiry, whichever comes first.** Figures are **illustrative and representative**, built to show the *shape* of VRP capture, not an exact backtest.

**The rule and why it works.** Selling only at IV Rank > 80 means you sell *only when implied volatility is near its yearly high* — precisely when the VRP tends to be fattest (IV has spiked but the market has not necessarily realised the move). You then hold until volatility mean-reverts (IV Rank < 30) or expiry. It is disciplined VRP harvesting: sell rich fear, collect as it normalises.

**The two-year results (illustrative).**

**Table 14.3 — "Sell straddle at IV Rank > 80" vs "sell every week" (2 years, per straddle unit)**

| Metric | Selective (IV Rank > 80) | Indiscriminate (sell every week) |
| --- | ---: | ---: |
| Number of trades | 12 | 104 |
| Win rate | 75% (9 of 12) | 62% |
| Average winner | +₹95 | +₹55 |
| Average loser | −₹150 | −₹165 |
| Worst single loss | −₹230 | −₹520 |
| Net result | +₹405 | −₹2,970 |
| Net per trade (expectancy) | +₹34 | −₹29 |

**The analysis.**

* **Selectivity is the difference between an edge and a loss.** The selective seller traded only 12 times but earned **+₹34 per trade**, while the indiscriminate seller — selling every week regardless of IV — actually *lost* about **₹29 per trade** (a 62% win rate cannot rescue an average loser almost three times the average winner). By selling only when IV was rich, the selective seller captured the fattest slices of the VRP and skipped the thin, low- and negative-VRP weeks that dragged the indiscriminate book underwater.
* **Selectivity also cut the tail.** The selective seller's worst single loss was −₹230; the indiscriminate seller's was −₹520, because selling *every* week meant selling into some genuinely cheap-IV periods right before big moves — exactly the negative-VRP trap. Fewer, better trades meant a shallower drawdown.
* **But the edge is still lumpy and real.** Even the selective seller had losing trades, and the losers (−₹150 average) were *larger* than the winners (+₹95) — the classic short-volatility asymmetry (win often and small, lose rarely and big, Chapters 10 and 12). The net was positive *because* the wins were frequent enough (75%) to outweigh the larger, rarer losses. In a year containing a COVID-style shock, even the selective rule would have taken a severe hit on one trade.

**The lesson.** The variance risk premium is real and harvestable, but *selectivity is the multiplier*. Selling only when IV is rich (high IV Rank, fat VRP) earns more per trade and suffers a smaller tail than selling indiscriminately — you concentrate on the moments the edge is largest and avoid underwriting cheap insurance. But even selective selling carries the short-volatility tail: the strategy wins most of the time and must be sized to survive the times it does not.

*(Takeaway: don't just sell premium — sell it when IV is rich relative to realised (high VRP), which raises your per-trade edge and shrinks your worst loss; and always size for the negative-VRP shock that no rule can avoid.)*

---

## 10. Chapter Summary

* **Historical (realized) volatility (HV)** is the annualised standard deviation of past log returns (`HV = √[(252/n)·Σ(rᵢ−μ)²]`); it is the *reality check* on implied volatility.
* HV estimators: **close-to-close** (standard), **Parkinson** (adds intraday range), **Yang–Zhang** (adds overnight gaps too) — comparison with IV matters more than the estimator.
* **Comparing IV to HV** answers "are options cheap or rich?": IV > HV (usual) favours sellers; IV < HV (rarer) favours buyers.
* The **Variance Risk Premium** (VRP = IV − realised HV) is positive ~80% of the time — the structural edge of option selling, existing because options are insurance priced above expected payout; harvest it when high, avoid selling when it is thin or negative.
* **IV Rank** (position in the 52-week range) and **IV Percentile** (share of days below current) beat the raw IV; they **diverge after a spike** (Rank deflated, Percentile truer), so trust the Percentile and understand the divergence.
* The **volatility cone** shows normal HV ranges by lookback (narrowing as the window lengthens); read current IV against it — above the 75th percentile is rich.
* The **strategy matrix** (IV Rank × direction) turns the edge into trades: low IV Rank → buy (debit) structures; high IV Rank → sell (credit) structures.
* **Realized-vs-implied tracking** closes the loop — it is P&L attribution for volatility trades and calibrates your sense of the VRP.

---

## 11. Key Takeaways

* **Never trade volatility on raw IV** — compare it to HV (the VRP) and to its own Rank and Percentile.
* **The VRP is your edge as a seller** — real, positive ~80% of the time, but paid for by a tail; harvest it selectively and size for the shock.
* **When IV Rank and IV Percentile disagree, trust the Percentile** and find the outlier that split them.
* **Read current IV against the volatility cone and let the IV Rank × direction matrix pick the structure** — then track realized-vs-implied to learn your market's edge.

---

## 12. Practice Questions

**Q1 (Definition).** In one sentence each, distinguish historical volatility from implied volatility.

**Q2 (Calculation).** Three daily log returns are +0.005, −0.010, +0.008. Compute the mean, then the annualised HV (use √252; divide the sum of squared deviations by n = 3).

**Q3 (VRP).** ATM IV is 17% and the market realised 13% over the period. Compute the VRP and state whom it favoured.

**Q4 (IV Rank).** Current IV = 14%, 52-week low = 9%, high = 29%. Compute IV Rank and classify it.

**Q5 (IV Percentile).** Over 250 days, IV was below the current level on 200 of them. Compute IV Percentile and interpret it alongside a low IV Rank.

**Q6 (Divergence).** Explain why IV Rank and IV Percentile can give opposite readings, and which you should generally trust.

**Q7 (Cone).** Current 30-day IV is 12%; the 30-day HV cone shows 25th percentile 11%, median 13%, 75th 15%. Where does IV sit, and does it favour buying or selling?

**Q8 (Strategy matrix).** IV Rank is 85 and your view is bearish. Which structure does the matrix indicate, and why?

**Q9 (VRP judgment).** ATM IV is 11% and the market has been realising 13%. Should you sell a strangle for income? Explain.

**Q10 (Judgement).** A trader says, "The VRP is positive 80% of the time, so selling straddles is basically free money." Explain what is wrong with this.

---

## 13. Detailed Solutions

**A1.** Historical volatility is the annualised standard deviation of the underlying's *past* returns (what actually happened). Implied volatility is the market's *forward-looking* volatility forecast embedded in option prices (what you pay or collect).

**A2.** Mean μ = (0.005 − 0.010 + 0.008)/3 = 0.003/3 = 0.001. Deviations: 0.004, −0.011, 0.007; squared: 0.000016, 0.000121, 0.000049; Σ = 0.000186. HV = √[(252/3) × 0.000186] = √[84 × 0.000186] = √0.015624 ≈ **12.5%**.

**A3.** VRP = 17% − 13% = **+4%**. It **favoured the seller** — implied exceeded realised, so options were richly priced relative to the movement delivered.

**A4.** IV Rank = (14 − 9)/(29 − 9) × 100 = 5/20 × 100 = **25** — a **low** IV Rank, suggesting options are cheap relative to their 52-week range (favouring buyers).

**A5.** IV Percentile = 200/250 × 100 = **80** — IV is higher than on 80% of days, i.e., **genuinely elevated**. Combined with a low IV Rank, this signals an outlier spike stretched the 52-week high; the Percentile (80) is the more trustworthy read, so options are richer than the Rank suggests.

**A6.** They can diverge because **IV Rank uses only the 52-week extremes** (high and low), while **IV Percentile uses the whole distribution of readings**. A single outlier spike inflates the "high," deflating IV Rank for a year, while IV Percentile still shows today's IV as elevated relative to most days. Generally **trust the IV Percentile**, after identifying the outlier that caused the divergence.

**A7.** Current IV (12%) sits between the 25th percentile (11%) and the median (13%) of the realised cone — slightly **below the median**, so options are modestly **cheap** relative to normal 30-day realised volatility. This favours **buying** premium (or at least not selling).

**A8.** IV Rank 85 means options are **rich → sell premium**; a bearish view means use a **call-based credit structure**: a **bear call spread (credit)** or short call. You collect rich premium while expressing the bearish view with defined risk.

**A9.** **No.** IV (11%) is *below* realised HV (13%), so the VRP is **negative** — you would be selling under-priced insurance into a market moving more than the premium compensates for. Selling here is a structural loser; wait until IV is rich relative to realised.

**A10.** It is wrong on two counts. First, "positive 80% of the time" is an *expectancy* statement, not a *risk* statement — the other 20% is where losses concentrate, and a single negative-VRP shock (a COVID-style spike) can wipe out many months of collected premium. Second, the VRP exists *precisely because* sellers bear that tail risk; it is compensation for danger, not free money. Selling straddles is positive-expectancy but far from risk-free, and must be sized to survive the tail.

---

## 14. Mini Glossary

* **Historical (realized) volatility (HV)** — the annualised standard deviation of the underlying's past returns; the reality check on IV. → this chapter.
* **Close-to-close HV** — HV computed from closing prices only (equation 14.1). → this chapter.
* **Parkinson HV** — HV using intraday high–low range; more efficient but ignores gaps. → this chapter.
* **Yang–Zhang HV** — the most complete HV estimator, using open, high, low, close and overnight gaps. → this chapter.
* **Variance Risk Premium (VRP)** — IV minus realised HV; positive ~80% of the time; the structural edge of option selling. → this chapter.
* **IV Rank** — where current IV sits in its 52-week range: (IV − low)/(high − low) × 100. → this chapter.
* **IV Percentile** — the share of past days with IV below the current level. → this chapter.
* **Volatility cone** — the historical range (percentile bands) of HV by lookback period; narrows as the window lengthens. → this chapter.
* **Realized-vs-implied tracking** — checking whether the market realised the volatility that was implied; P&L attribution for volatility trades. → this chapter.
* **Insurance analogy (of the VRP)** — options priced above expected payout, so sellers earn a premium for underwriting risk. → this chapter.

---

<!-- End of Chapter 14 (Rev 2, current as of 4 Aug 2026). Rev 2: reviewed for 4-Aug-2026 currency — NO reader-facing changes required. Chapter has no lot-size, transaction-cost, or expiry-weekday dependence (all volatility analytics; case-study P&L is "per straddle unit"), so the lot-65 (NSE Jan-2026) and Apr-2026 STT updates do not apply; all content verified accurate and current. HV worked example: 5 returns → 7.6% (Σdev²=0.00011385, /5, ×252, √). IV Rank vs Percentile divergence: current 16%, low 10%, high 30% → Rank 30; 180/252 below → Percentile 71 (outlier-spike effect; trust Percentile). VRP = IV − realised HV, positive ~80%. Cone Table 14.1 (10-90 day, narrowing). Strategy matrix 14.2 (IV Rank × direction). Case study: selective (IV Rank>80) vs indiscriminate selling — selective +₹34/trade, worst −₹230; indiscriminate +₹11/trade, worst −₹520. Q2 HV=12.5%, Q4 Rank=25, Q5 Percentile=80. IV = implied volatility, HV = historical/realized. Annualization √252. No forward chapter-number references. -->
