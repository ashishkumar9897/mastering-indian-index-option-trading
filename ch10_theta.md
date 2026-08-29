<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapters 8, 9. Target length ~8,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Theta computed from the σ=13% BSM premium curve (premium ≈ 0.4·S·σ·√T = 1279.2·√T): tables use the pure-time-decay derivative (−1279.2/(730·√T)); full BSM adds a small ~₹2/day interest-carry term, noted explicitly. Per-unit Theta values and %-of-premium are lot-independent; only per-lot conversions rescaled to lot 65. No transaction costs → Apr-2026 STT change not applicable. Theta quoted per unit per calendar day; multiply by lot size for rupees. Signs: negative for long, positive for short. IV = implied volatility. -->

# Chapter 10 — Theta: Time Decay and the Option Seller's Edge

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Define Theta and explain why time decay is non-linear.
2. Quantify how much an option loses each day to the passage of time.
3. Understand why Theta is the option seller's primary income source.
4. Weigh the calendar-day versus trading-day debate and how the market actually prices weekends.
5. Master the relationship between Theta and time to expiry — the acceleration curve.
6. Balance Theta income against the Gamma risk you must take to earn it.

In Chapter 9 we met the Gamma–Theta tradeoff and promised that Theta — the *other* side of that coin — would get its own chapter. This is it. **Theta is the clock ticking on every option**, and understanding it separates traders who harvest time from those who are ground down by it.

---

## 2. Introduction

Two traders hold opposite sides of the same NIFTY option through a quiet week. The market barely moves — a few points here and there, closing the week almost exactly where it started. The option *buyer* ends the week down ₹70 a unit. The option *seller* ends it up ₹70 a unit. Nothing happened in the market, yet money changed hands. What paid the seller and drained the buyer?

**Time.** Every day that passes, an option loses a slice of its value — its time value bleeds away toward zero at expiry, whether or not the index moves. That daily bleed is **Theta**, and it is the most reliable force in the option market: the index may go up, down, or nowhere, but time only goes one way. For the buyer, Theta is a headwind that must be overcome by a move large enough and soon enough. For the seller, Theta is a steady income — the reason "selling premium" is a business, not a gamble.

But Theta is not a gift. As Chapter 9 showed, you cannot collect Theta without being short Gamma — without carrying the risk that a single big move undoes weeks of patient income. This chapter builds Theta from the ground up: how fast it decays, why it accelerates into expiry, why at-the-money options bleed fastest, how the market handles weekends, and — crucially — how to weigh the income against the Gamma risk that always rides alongside it. Setting throughout: **NIFTY at 24,600, lot 65, σ = 13%**, with premiums from the same BSM basis as Chapters 6, 8, and 9.

---

## 3. Core Concepts

### 3.1 What Theta is

Theta is the flagship of this chapter.

**What is it?** **Theta (Θ)** is the amount an option's premium falls for each day that passes, holding everything else constant. Formally, `Θ = −∂C/∂t`, expressed per calendar day. If an ATM NIFTY call has a Theta of −₹10.6, then — with the index, volatility, and rates unchanged — its premium will be about ₹10.6 lower tomorrow.

**Why does it exist?** Because an option's time value is a payment for *optionality over remaining time* (Chapter 4), and remaining time shrinks every day. As the window for a favourable move narrows, the value of that window falls. At expiry, time value is exactly zero and only intrinsic value remains. Theta measures the rate of that unavoidable erosion.

**Why should a trader care?** Because Theta is a daily, near-certain transfer of money from option buyers to option sellers. It is the buyer's rent and the seller's income. You cannot hold an option — long or short — without Theta working for or against you every single day, including days the market does nothing.

**Intuitive explanation.** An option is a melting ice cube, and Theta is the rate of melting. The cube (time value) shrinks a little each day and melts fastest at the very end. A buyer owns the cube and watches it disappear; a seller has already sold the water and profits as it evaporates.

**Sign convention (memorise this).** Theta is **negative for long options** (you lose value as time passes) and **positive for short options** (you gain). A trader long a call and short a put has one negative and one positive Theta contribution; the *net* is what matters.

**Numerical feel.** The ATM NIFTY 24,600 call with 10 days to expiry has a Theta of about −₹10.6 per unit per day. On a lot (×65) that is −₹689 a day for a buyer, or +₹689 a day for the seller — earned or lost whether or not NIFTY moves.

**Mathematical form (BSM, for a call).**

```
Θ = −[ S · n(d₁) · σ / (2√T) ] − r · K · e^(−rT) · N(d₂)          (10.1)
```

expressed per year; divide by 365 for a per-calendar-day figure. The **first term** is the pure time-value decay (largest at the money, and it grows as √T shrinks); the **second term** is a small interest-carry adjustment.

**Professional interpretation.** Sellers think of Theta as a daily "salary" they collect for underwriting risk — and they know that salary is precisely the premium for being short Gamma (Chapter 9). A desk tracks Position Theta as its daily income run-rate and asks constantly whether the Gamma risk behind it is worth the pay.

**Common mistake.** Buyers who are "right on direction but wrong on timing." They buy an option, the index eventually moves their way — but too slowly, and Theta has already bled the premium to nothing. Being right late is the same as being wrong.

**Practical takeaway.** **Theta is the daily rent on optionality — a headwind for buyers, income for sellers — and it works every day, moving market or not; know your net Theta before you hold any position overnight.**

---

### 3.2 The decay curve — why Theta accelerates

Time value does not bleed away evenly. It drains slowly when expiry is far off and rushes out at the end. The reason is the **square-root-of-time relationship**: an at-the-money option's time value is roughly proportional to √T (Chapter 5). Table 10.1 shows the premium of an ATM NIFTY call from 30 days to expiry, and the daily Theta at each point.

**Table 10.1 — ATM NIFTY call: premium and daily Theta by DTE (σ = 13%; pure time-decay basis)**

| Days to expiry | Premium (₹) | Theta (₹/day) | Theta as % of premium |
| ---: | ---: | ---: | ---: |
| 30 | 367 | −6.1 | 1.7% |
| 20 | 299 | −7.5 | 2.5% |
| 10 | 212 | −10.6 | 5.0% |
| 5 | 150 | −15.0 | 10.0% |
| 3 | 116 | −19.3 | 16.7% |
| 1 | 67 | −33.5 | 50.0% |
| 0 | 0 | — | — |

Two patterns leap out:

* **Theta grows as expiry nears.** The daily decay rises from about ₹6 at 30 days to ₹33.5 at 1 day — because Theta ∝ 1/√T, halving the time multiplies the daily decay by √2.
* **Theta as a *fraction* of the premium accelerates dramatically** — from under 2% a day a month out to **50% a day on the final day.** An ATM option loses half its remaining value on its last day of life.

> **Beginner Alert — the last day is brutal.** The "50% on the final day" figure is not a typo. The Theta shown at 1 DTE (−₹33.5) is the *instantaneous* rate at the start of that day; because decay keeps accelerating through the day, the option actually loses its *entire* remaining ₹67 by expiry. This is why buying options in the last day or two is so dangerous, and why the richest decay a seller can collect sits in the final days — alongside the fiercest Gamma (Chapter 9).

*(Note on precision: the tables use the pure time-value decay derived from the √T premium curve, which ties exactly to the premiums shown. Full BSM equation (10.1) adds a small, roughly constant interest-carry term of about ₹2 per day, so a broker's Theta may read a rupee or two larger in magnitude.)*

---

### 3.3 Theta by moneyness — the ATM bleeds fastest

Theta is not the same across strikes. Because the decay term in (10.1) is proportional to `n(d₁)` — the normal density, which peaks at the money — **at-the-money options have the highest Theta**, and it falls away toward the wings. Table 10.2 shows Theta across strikes at 10 DTE.

**Table 10.2 — Theta across moneyness (NIFTY 24,600, 10 DTE; illustrative)**

| Strike | Moneyness | Call Theta (₹/day) |
| ---: | --- | ---: |
| 24,000 | Deep ITM | −4.9 |
| 24,400 | ITM | −9.5 |
| **24,600** | **ATM** | **−10.6** |
| 24,800 | OTM | −10.2 |
| 25,200 | Deep OTM | −6.2 |

The ATM strike bleeds fastest in absolute terms; deep ITM and deep OTM options decay more slowly (a deep-ITM option is mostly intrinsic value, which does not decay; a deep-OTM option has little time value left to lose). This is why sellers cluster near the money — that is where the decay income is richest — and it is exactly why the ATM is also where Gamma is highest (Chapter 9). The two peaks coincide because they are the same phenomenon.

---

### 3.4 Weekly versus monthly Theta

India's weekly options are, by construction, high-decay instruments — a fact with big consequences for both buyers and sellers. Compare an ATM weekly (7 DTE) with an ATM monthly (28 DTE):

```
Weekly  (7 DTE):  premium ≈ ₹177, Theta ≈ −₹12.65/day → 7.1% of premium per day
Monthly (28 DTE): premium ≈ ₹354, Theta ≈ −₹6.33/day → 1.8% of premium per day
```

The weekly costs about *half* the monthly to buy, yet decays about **twice as fast per day** — and, as a *fraction of its premium*, about **four times as fast**. For a seller, the weekly offers a far higher daily return on premium; for a buyer, it is a far steeper headwind. This is the mathematical heart of why weekly options dominate Indian volumes and why they are the sellers' preferred hunting ground (and the careless buyer's graveyard).

---

### 3.5 Theta as a percentage of premium — when high Theta is "fair"

A raw Theta number can mislead. A ₹33/day Theta sounds alarming, but on a ₹67 option with one day left it is simply the fair, expected melt of a nearly-expired option. The useful metric is **Theta as a percentage of premium** (Θ ÷ premium), which tells you the decay *rate* relative to what you paid.

* A cheap, near-expiry option has a *high* Theta percentage because almost all of it is about to vanish — that high Theta is "fair," priced in, not a bargain to sell.
* A longer-dated option has a *low* Theta percentage — it decays slowly relative to its price.

The lesson for sellers: do not chase raw Theta. A high Theta percentage means high decay *and* (near expiry, at the money) high Gamma. The decay is compensation for risk, not free money — the higher the Theta percentage, the more Gamma risk sits behind it.

---

### 3.6 Weekend Theta and the calendar-day debate

Theta is quoted *per calendar day*, which raises a practical question: over a weekend, does an option lose three days of Theta (Friday to Monday) even though the market is shut for two of them?

There are two schools. The **calendar-day** view says time value depends on calendar time, so a weekend costs three days of decay. The **trading-day** view says volatility accrues only on trading days (the market cannot move when it is closed), so weekends should decay little. The truth is in between, and — crucially — **the market prices it in.**

In practice, option premiums often "pre-decay" on Friday afternoon: market makers, knowing the weekend is coming, mark down time value ahead of it, so you rarely collect a clean, free three-day decay by simply holding a short position over a weekend. A buyer, conversely, does not usually get to "skip" the weekend's decay.

> **Market Note — Do not count on free weekend Theta.** A common beginner plan is "sell on Friday, collect three days of decay by Monday." It seldom works cleanly, because Friday's prices already discount the weekend. Similarly, holding a long option over a weekend is not a free ride — the decay is spread and partly front-loaded into Friday. Treat weekend decay as *already in the price*, not as an edge to be captured.

---

### 3.7 The 30-day rule

A practical rule of thumb ties the decay curve together: **most of an option's time value erodes in its final 30 days, with the erosion accelerating sharply in the last week.** From Table 10.1, an ATM option worth ₹367 at 30 DTE is worth about ₹177 at 7 DTE — so nearly **half its 30-day value decays in the final 7 days alone.** The first three weeks bleed slowly; the last week is a cliff.

This shapes real behaviour on both sides:

* **Buyers** who need time should buy *longer-dated* options (lower Theta percentage), not cheap weeklies, unless they expect a fast move.
* **Sellers** who want decay income concentrate in the final weeks — but must respect that the same period carries the steepest Gamma (Chapter 9). The richest decay and the sharpest risk live in the same seven days.

---

### 3.8 The seller's edge — and the buyer's bleed

Theta is why *selling* options is a coherent business. **Theta-positive strategies** — selling naked options, credit spreads, iron condors, strangles — collect time decay every day, profiting when the market moves less than the premium implied. They win often and small: a steady drip of Theta income on quiet days.

The mirror image is the **buyer's bleed**. An option buyer pays Theta every day and needs a move large enough, and soon enough, to overcome it. This is the origin of the most painful beginner experience — *"I was right on direction but still lost money"* — because the move came, but after Theta had already drained the premium (Chapter 4's lottery-ticket trap, now quantified). Being right on direction is necessary but not sufficient; a buyer must also be right on *timing and magnitude*, because Theta is charging rent the whole time.

But — and this is the drumbeat of Part III — the seller's steady income is not free. It is precisely the premium for being **short Gamma**. Every day the seller collects Theta, they are underwriting the risk of a move that could wipe out weeks of income in an afternoon (the expiry-day trap of Chapter 9). Theta and Gamma are inseparable.

---

### 3.9 Balancing Theta against Gamma — the sweet spot

Since high Theta always comes with high Gamma, the seller's real question is: *where on the curve is the reward worth the risk?*

* **Far from expiry (30+ DTE):** Theta is low (₹6/day, 1.7% of premium) and Gamma is low. Safe, but slow income.
* **Very near expiry (1–2 DTE):** Theta is enormous (₹33/day, 50% of premium) but Gamma is explosive (Chapter 9) — a single move can be catastrophic and un-hedgeable.
* **The middle (roughly 5–15 DTE):** Theta is meaningful (₹10–15/day, 5–10% of premium) while Gamma, though rising, is still manageable and hedgeable.

Many premium sellers therefore favour this middle window — enough decay to be worth collecting, before the final-days Gamma bomb — and *close or roll* positions before the last day or two rather than holding into the explosion. This is a judgment, not a fixed rule, but the principle is universal: **the "sweet spot" for selling is where Theta per day is high but Gamma risk is still controllable.**

> **Professional Insight — Theta is paid, not earned.** A professional never describes Theta as "free money" or "guaranteed income." They describe it as being *paid to take Gamma risk* — an insurance premium collected for underwriting moves. Framed that way, the discipline follows automatically: size the position for the move you are insuring against, not for the calm you expect. The sellers who survive are the ones who treat every rupee of Theta as a liability they have underwritten, not an asset they have banked.

---

## 4. Examples (Real-World)

**Example 1 — The quiet-week transfer.** A range-bound week moves NIFTY a handful of points net. The ATM straddle buyer loses the week's Theta; the straddle seller collects it. No trend, no drama — just time doing its one-directional work, exactly as in the introduction.

**Example 2 — Right, but too late.** A trader buys a 5-DTE ATM call, correctly expecting a rally. NIFTY does rally — but on the *sixth* day, after the option has expired. The direction was perfect; the timing killed it. Theta does not wait for your thesis to play out.

**Example 3 — The seller's good month and bad day.** A strangle seller collects small Theta gains on 24 of 30 days. On the one volatile day, short Gamma hands back a chunk of the month's income. The month is still net positive — but the "one bad day" defines the strategy's true risk profile, as the case study shows.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65, σ = 13%; figures per unit unless a lot value is given.

### Numerical Example 1 — Reading the daily Theta table

From Table 10.1, an ATM call at 5 DTE has Theta −₹15.0/day (10% of its ₹150 premium). On a lot, the buyer loses 15 × 65 = **₹975 per day** to time; the seller collects the same. Over five calendar days to expiry, if the index sat perfectly still, the buyer would lose essentially the whole ₹150 (₹9,750 on the lot) and the seller would keep it — the decay accelerating each day.

### Numerical Example 2 — Weekly versus monthly decay

```
Weekly  (7 DTE):  Theta ≈ −₹12.65/day on a ₹177 premium → 7.1%/day
Monthly (28 DTE): Theta ≈ −₹6.33/day on a ₹354 premium → 1.8%/day
```

The weekly decays about **2× faster per day** and about **4× faster as a fraction of premium**. A seller earns a far higher daily return on the weekly — but takes on proportionately more Gamma risk to do so.

### Numerical Example 3 — Position Theta of a portfolio

Long 2 lots of a NIFTY call (Θ = −₹5.2/unit) and short 1 lot of a NIFTY put (position Θ = +₹4.8/unit, positive because you are short). Theta is quoted *per unit*; multiply by lot size:

```
Call legs:  2 × (−5.2) × 65 = −₹676/day
Put leg:    1 × (+4.8) × 65 = +₹312/day
Position Theta = −676 + 312 = −₹364/day
```

The portfolio is **net long options**, losing ₹364 a day to time. To become Theta-positive (a net collector of decay), you would need to shift the balance toward the short leg.

### Numerical Example 4 — Theta as a percentage of premium

The same ₹33.5/day Theta means very different things depending on the premium:

```
At 1 DTE:  Θ/premium = 33.5 / 67  = 50%/day   (fair — nearly expired)
At 10 DTE: Θ/premium = 10.6 / 212 = 5%/day    (moderate)
At 30 DTE: Θ/premium = 6.1 / 367  = 1.7%/day  (slow)
```

The raw Theta rises toward expiry, but the *percentage* rises far faster — the metric that tells a seller how much decay they are collecting relative to the premium (and how much Gamma sits behind it).

### Numerical Example 5 — The 30-day rule quantified

An ATM option worth ₹367 at 30 DTE is worth ≈ ₹177 at 7 DTE:

```
Decay over the final 7 days ≈ ₹177  (the entire remaining premium)
As a share of the 30-day premium ≈ 177 / 367 ≈ 48%
```

Nearly half of the option's 30-day value melts in its last week — the acceleration cliff that defines both the seller's opportunity and the buyer's danger.

---

## 6. Calculations (the reusable recipes)

**(a) Theta from BSM (per year; ÷365 for per calendar day)**

```
Θ_call = −[ S · n(d₁) · σ / (2√T) ] − r · K · e^(−rT) · N(d₂)
```

**(b) Approximate ATM decay (pure time value, from premium ≈ 0.4·S·σ·√T)**

```
Θ_ATM/day ≈ − (0.4 · S · σ) / (730 · √T)     (accelerates as T → 0)
```

**(c) Theta as a percentage of premium (efficiency metric)**

```
Theta % = Θ ÷ Premium
```

**(d) Position Theta (per day; use POSITION signs)**

```
Position Theta = Σ (Θᵢ × Qᵢ × Lot size)     (Θ negative for long, positive for short)
```

**(e) Weekly-vs-monthly rule of thumb**

```
Since time value ∝ √T, the monthly's premium ≈ 2× the weekly's, but it decays over ~4× the days
→ the weekly decays ≈ 2× faster per day and ≈ 4× faster as a % of premium
```

---

## 7. Practical Insights

* **Know your net Theta before holding overnight.** Every position has a daily time P&L that runs whether or not the market moves; a buyer should know the headwind, a seller the income.
* **Theta accelerates — the last week is a cliff.** Nearly half of a 30-day option's value decays in its final seven days, and half of *that* on the last day. Buyers should avoid short-dated options on slow theses; sellers find their richest decay here, alongside the sharpest Gamma.
* **Use Theta-as-%-of-premium, not raw Theta.** It tells you the decay rate relative to price and warns you how much Gamma risk you are being paid for.
* **Do not bank on free weekend decay.** The market pre-prices weekends into Friday; there is no clean three-day gift.
* **Sell in the sweet spot, not the danger zone.** The middle of the curve (roughly 5–15 DTE) offers meaningful Theta with manageable Gamma; the final days offer the most decay and the most catastrophic risk.

---

## 8. Common Mistakes

* **"Right on direction, wrong on timing."** Buying options and being correct too late — Theta drains the premium before the move arrives.
* **Buying cheap weeklies for a slow view.** The steepest decay in the market fights you daily; a longer-dated option is often the right tool for a patient thesis.
* **Chasing raw Theta near expiry as "free income."** High Theta percentage means high Gamma; the decay is payment for risk, not a bargain.
* **Assuming a free weekend of decay.** Friday's prices already discount it; the "sell Friday, collect Monday" plan rarely delivers.
* **Ignoring the sign and units of Theta.** Long is negative, short is positive, and Theta is per *unit* — forgetting the lot multiplier understates your daily P&L 65-fold.
* **Holding short options into the final-day Gamma explosion to squeeze the last Theta.** The richest decay sits exactly where a single move can wipe out the month.

---

## 9. Case Study — "The Theta Harvester"

**Context.** A trader runs a systematic **short strangle** on NIFTY for one 30-day cycle to harvest Theta: with the index near 24,600, they sell a 30-DTE **25,200 call** and **24,000 put** (both roughly 0.15-Delta OTM), collecting a total credit of about **₹180 per unit** (₹11,700 on a lot of 65). The position is near Delta-neutral, strongly Theta-positive, and — as always — short Gamma. Figures are illustrative but representative.

**The month, week by week (per unit).**

**Table 10.3 — Theta Harvester: 30-day P&L path (illustrative)**

| Period | What happened | P&L this period | Cumulative |
| --- | --- | ---: | ---: |
| Days 1–12 | Range-bound; steady Theta collected | +₹95 | +₹95 |
| Day 13 | Sharp 400-point NIFTY drop; short Gamma + IV spike | −₹130 | −₹35 |
| Day 13 (action) | Roll the tested 24,000 put down to 23,600; cut size | — | −₹35 |
| Days 14–30 | Market stabilises; Theta resumes on the adjusted position | +₹125 | **+₹90** |

**Final result:** +₹90 per unit, or **₹5,850 on the lot** — a positive month, but the trader kept only *half* of the ₹180 credit they set out to collect.

**The analysis.** Three lessons sit inside this record.

* **Theta income is real but lumpy.** For 12 quiet days the strategy did exactly what it promised — a steady drip of decay income, +₹95. This is the seller's edge: winning often and small when the market moves less than the premium implied.
* **The one bad day defines the risk.** Day 13's 400-point drop cost ₹130 — more than the first 12 days had earned — because the position was **short Gamma** (the loss accelerated as NIFTY fell and the put's Delta ran) and **short Vega** (the IV spike inflated the premiums the trader owed). One volatile session nearly erased a fortnight of patience. This is the steamroller behind the coins.
* **The adjustment saved the month.** By rolling the tested put down and cutting size on Day 13, the trader capped further damage and let Theta resume on a safer position. Without that risk management, a continued fall could have turned the ₹130 loss into a multiple of the month's target. The edge is in the Theta; the *survival* is in the adjustment and the sizing.

**The lesson.** A Theta harvester is paid to be short Gamma. The strategy makes money most days and gives some back on the bad ones; over time it is profitable *only* if the good-day income exceeds the bad-day losses — which depends entirely on sizing small enough to survive the bad day and adjusting before it becomes fatal. Theta is the income; Gamma is the bill; risk management is what keeps the two in balance.

*(Takeaway: selling premium harvests Theta steadily, but the profit is decided by the one or two big-move days a month — size and adjust for those, not for the quiet days.)*

---

## 10. Chapter Summary

* **Theta (Θ)** is the daily loss of premium from the passage of time (`Θ = −∂C/∂t`, per calendar day); **negative for long options, positive for short.**
* Time decay is **non-linear** — time value ∝ √T — so Theta **accelerates into expiry**: from ~₹6/day (1.7% of premium) at 30 DTE to ~₹33/day (50% of premium) at 1 DTE for an ATM NIFTY call.
* **ATM options have the highest Theta** (the decay term ∝ n(d₁), peaking at the money); deep ITM/OTM decay more slowly — and the ATM Theta peak coincides with the ATM Gamma peak.
* **Weekly options decay ~2× faster per day and ~4× faster as a % of premium** than monthlies — high-decay by design.
* **Theta as a % of premium** is the useful metric; high values mean fast decay *and* high Gamma — the decay is payment for risk, not free money.
* **Weekend decay is pre-priced** into Friday — there is no clean free three-day gift; the calendar-vs-trading-day answer is "the market has already handled it."
* **The 30-day rule:** ~half of a 30-day option's value decays in its final week — a cliff that helps sellers and punishes buyers.
* **Theta is the seller's income and the buyer's bleed**, but it is inseparable from **short Gamma**; the "sweet spot" for selling (≈5–15 DTE) balances meaningful decay against manageable Gamma.

---

## 11. Key Takeaways

* **Know your net Theta every day** — it is the one P&L that runs whether the market moves or not.
* **Respect the acceleration** — the final week, and especially the final day, decay fastest; buy longer-dated for slow theses, and sell in the sweet spot rather than into the expiry Gamma bomb.
* **Judge decay by Theta-as-%-of-premium,** and remember that a high value is compensation for Gamma risk, not free income.
* **A premium seller is paid to be short Gamma** — the month's profit is decided by the big-move days, so size and adjust to survive them.

---

## 12. Practice Questions

**Q1 (Definition).** Define Theta in one sentence, and give its sign for long and for short options.

**Q2 (Non-linearity).** From Table 10.1, compare the daily Theta at 30 DTE with that at 1 DTE, and explain why they differ.

**Q3 (Multiple choice).** Theta is highest (in absolute terms) for options that are:
(a) deep in the money; (b) at the money; (c) deep out of the money; (d) already expired.

**Q4 (Percentage metric).** An ATM option at 1 DTE has premium ₹67 and Theta −₹33.5. Compute Theta as a percentage of premium and interpret it.

**Q5 (Weekly vs monthly).** Why does a weekly ATM option decay faster than a monthly, both per day and as a percentage of premium?

**Q6 (Position Theta).** You are long 3 lots of a call (Θ = −₹6/unit) and short 2 lots of a put (position Θ = +₹5/unit), lot 65. Compute your Position Theta and state whether you gain or lose to time each day.

**Q7 (Timing).** A trader is bullish and buys a 3-DTE ATM call. NIFTY is flat for two days, then rallies strongly on day four. Explain, using Theta, why the trade may still lose.

**Q8 (30-day rule).** Roughly what fraction of a 30-day ATM option's value decays in its final week, and what does this imply for a buyer versus a seller?

**Q9 (Weekend).** A trader plans to sell an option on Friday to "collect three days of decay by Monday." Why is this often a poor plan?

**Q10 (Tradeoff/judgement).** A seller wants maximum Theta, so they sell ATM options with 1 day to expiry. Using the Gamma–Theta tradeoff, explain the danger and suggest a better approach.

---

## 13. Detailed Solutions

**A1.** Theta is the amount an option's premium falls for each day that passes, all else equal. It is **negative for long options** (the holder loses value) and **positive for short options** (the seller gains).

**A2.** At 30 DTE, Theta ≈ −₹6.1/day; at 1 DTE, ≈ −₹33.5/day — over five times larger. They differ because time value ∝ √T, so Theta ∝ 1/√T: as time runs out, the same day represents a larger fraction of the remaining life, and decay accelerates.

**A3.** **(b) at the money.** The decay term is proportional to n(d₁), which peaks at the money; deep ITM options are mostly non-decaying intrinsic value, and deep OTM options have little time value left to lose.

**A4.** Theta % = 33.5 ÷ 67 = **50% per day**. It means the option loses about half its remaining value in a day — "fair" for a nearly-expired option (the decay is fully priced in), and a warning that Gamma risk is at its most extreme.

**A5.** Because time value ∝ √T: the monthly's premium is only about twice the weekly's (√28 ≈ 2√7), yet it decays over about four times as many days. So the weekly decays about **twice as fast per day** and, relative to its smaller premium, about **four times as fast as a percentage**.

**A6.** Position Theta = (3 × −6 × 65) + (2 × +5 × 65) = −1,170 + 650 = **−₹520/day**. The portfolio is net long options and **loses ₹520 a day** to time.

**A7.** A 3-DTE ATM option has very high Theta (roughly ₹19/day and rising, ~17%+ of premium per day). Over the two flat days, decay drains a large part of the premium. By the time the rally arrives on day four, the option may have already expired (3 DTE) or lost so much value that the move cannot recover the Theta already paid. Being right on direction but late on timing loses, because Theta charged rent the whole time.

**A8.** Roughly **half** (≈48%) of a 30-day ATM option's value decays in its final week (₹367 → ~₹177). For a **buyer**, this is a steep, accelerating headwind — avoid short-dated options for slow theses. For a **seller**, it is the richest decay income — but it coincides with the steepest Gamma, so it must be sized and managed carefully.

**A9.** Because the market **pre-prices the weekend** into Friday afternoon: premiums are marked down ahead of the non-trading days, so you rarely collect a clean, free three-day decay by holding a short position over the weekend. The expected weekend decay is already in the Friday price, not an edge to be captured.

**A10.** At 1 DTE the ATM option has the highest Theta (~50% of premium) but also the highest, most explosive **Gamma** (Chapter 9), so a single move can be catastrophic and impossible to hedge in time — the rich Theta is precisely payment for that risk. A better approach is to sell in the **sweet spot (≈5–15 DTE)**, where Theta is still meaningful (5–10% of premium) but Gamma is manageable, and to close or roll before the final-day Gamma explosion.

---

## 14. Mini Glossary

* **Theta (Θ)** — the daily loss in an option's premium from the passage of time; negative for long, positive for short. → this chapter.
* **Time decay** — the erosion of time value as expiry approaches; non-linear and accelerating. → this chapter.
* **Square-root-of-time relationship** — time value ∝ √T, so Theta ∝ 1/√T and accelerates near expiry. → this chapter.
* **Theta as % of premium** — Θ ÷ premium; the decay rate relative to price, and a proxy for the Gamma risk behind it. → this chapter.
* **Theta-positive strategy** — a position that collects net time decay (selling options, credit spreads, iron condors, strangles). → this chapter.
* **Position Theta** — Σ(Θ × quantity × lot size); the portfolio's daily time P&L. → this chapter.
* **Weekend Theta** — the decay attributed to non-trading days, in practice pre-priced into Friday. → this chapter.
* **Calendar-day vs trading-day debate** — whether decay follows calendar time or only trading time; resolved in practice by the market pricing it in. → this chapter.
* **The 30-day rule** — most of an option's value decays in its final 30 days, ~half of that in the last week. → this chapter.
* **Buyer's bleed** — the daily Theta cost that makes "right on direction, wrong on timing" a losing trade. → this chapter.
* **Sweet spot (for selling)** — the DTE window (≈5–15 days) where Theta is high but Gamma is still manageable. → this chapter.

---

<!-- End of Chapter 10 (Rev 2, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026 revision) — per-lot conversions rescaled: numerical-feel −₹689/day; NE1 15×65=₹975/day, ₹9,750/lot; NE3 Position Theta −₹364/day; Theta Harvester credit ₹11,700/lot, final ₹5,850/lot; Q6/A6 −₹520/day. Per-unit Theta values (−6.1@30d, −10.6@10d, −15.0@5d, −33.5@1d), Theta% (1.7%→50%), weekly/monthly ratios, and premiums are all lot-independent — unchanged. Theta tables from σ=13% BSM premium curve (premium≈1279.2·√T). Weekly(7d) −12.65/day(7.1%) vs monthly(28d) −6.33/day(1.8%): 2× per day, 4× per %. 30-day rule: ~48% decays in final week. Full BSM interest-carry term (~₹2/day) noted as omitted from tables. Theta Harvester case: strangle credit ₹180, final +₹90/unit after a −₹130 bad day + adjustment. No transaction costs → Apr-2026 STT change not applicable. Gamma–Theta tradeoff carried from Ch9. IV = implied volatility. No forward chapter-number references. -->
