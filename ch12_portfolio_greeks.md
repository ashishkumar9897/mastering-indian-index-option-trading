<!-- Difficulty: Level 3.5/5 (Intermediate-Advanced). Dependency: Chapters 8, 9, 10, 11. Target length ~9,000 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision); one futures lot = 65 Deltas. Capstone of Part III. Per-unit Greeks drawn consistently from Ch8-11 (10 DTE, S=24,600, σ=13%) — lot-independent, unchanged. 5-position portfolio RE-SUMMED at lot 65: +Δ29.9, −Γ0.046, +Θ₹643.5/day, −ν₹1,001.6/vol pt (was +34.5/−0.053/+742.5/−1,155.8 at lot 75). All attribution, scenario-matrix, and hedge figures propagated. Case study §9 and Q5/Q6 use standalone round illustrative Greeks (not lot-derived) — valid at lot 65, unchanged. No transaction costs → Apr-2026 STT change not applicable. P&L attribution uses ΔP≈Δ·ΔS+½·Γ·(ΔS)²+Θ·Δt+ν·Δσ with POSITION Greeks. Higher-order Greeks (Charm/Vanna/Volga) at practical-interpretation level only. IV = implied volatility; "vol point" = 1 percentage point of IV. -->

# Chapter 12 — Putting the Greeks Together: Portfolio Greeks and Dynamic Management

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Calculate and interpret portfolio-level (position) Greeks across many positions.
2. Understand how the Greeks interact — the Gamma–Theta seesaw and the Vega–Theta link.
3. Make adjustment decisions based on how your Greek exposures change.
4. Read the higher-order Greeks — Charm, Vanna, and Volga — at a practical level.
5. Use Greeks to compare the risk profiles of different strategies and attribute your P&L.

This is the capstone of Part III. You have met the five Greeks one at a time; now you assemble them into a single dashboard that tells you, at a glance, exactly what your whole book will do in any market.

---

## 2. Introduction

A trader runs what looks like a fortress: a NIFTY short strangle, delta-hedged to exactly zero with futures, throwing off a comfortable positive Theta every day. "Delta-neutral and Theta-positive," they tell a friend. "I make money if the market goes up, down, or nowhere — as long as it doesn't move too much."

Then, on a single session, NIFTY drops 400 points and India VIX jumps 6 points. By the close the "fortress" has lost ₹12,800 — despite starting the day perfectly Delta-neutral. How does a market-neutral, income-generating position lose that much in a day?

Because **Delta-neutral is not risk-neutral.** The trader had zeroed out *one* of five Greeks and left the other four live. The move triggered a Gamma loss (Delta ran against the short position); the VIX spike triggered a Vega loss (short volatility revalued); Theta's small daily gain barely dented either. The portfolio was hedged against the one risk the trader was watching and exposed to the two that actually arrived.

This chapter is the antidote to that blindness. Individually, the Greeks are instruments; together, they are a **cockpit** — a single, aggregate read of every way your book can make or lose money. You will learn to roll five positions into one set of portfolio Greeks, read the resulting "sign profile" like a fingerprint, attribute yesterday's P&L to each Greek, run scenario matrices for the moves you fear, and decide *which* Greek to hedge *first* when the market shifts. Setting throughout: **NIFTY at 24,600, lot 65**, with per-unit Greeks carried forward from Chapters 8–11.

---

## 3. Core Concepts

### 3.1 Portfolio Greeks — the aggregate dashboard

This is the flagship idea of the chapter.

**What is it?** **Portfolio (position) Greeks** are the sum of every leg's Greek, signed for long/short and scaled by quantity and lot size. A book of ten positions collapses into just five numbers — one net Delta, Gamma, Theta, Vega, and Rho — that describe how the *entire* book behaves:

```
Portfolio Greek = Σ (Greek_i × Quantity_i × Lot size)          (Q negative for short legs)
```

**Why does it exist?** Because you do not trade one option; you trade a *book*, and the legs interact. A long call here and a short call there may offset in Delta but stack in Vega. Only by aggregating can you see your *net* exposure to each risk — which is the only exposure that actually determines your P&L.

**Why should a trader care?** Because your real risk lives at the portfolio level, not the position level. Two positions that each look fine can combine into a dangerous whole (say, doubling your short Gamma) or a harmless one (offsetting Deltas). Managing options *is* managing portfolio Greeks; everything else is bookkeeping.

**Intuitive explanation.** Think of the five portfolio Greeks as the **five gauges on an aircraft cockpit**: heading (Delta), how fast the heading changes (Gamma), fuel burn per hour (Theta), sensitivity to turbulence (Vega), and altitude drift (Rho). A pilot does not stare at one gauge; they scan all five and know instantly whether the plane is stable or about to stall. Your portfolio Greeks are that scan.

**Numerical feel.** A five-leg NIFTY book (worked fully in Numerical Example 1) might net to Delta +29.9, Gamma −0.046, Theta +₹643.5/day, Vega −₹1,001.6/vol point. That single line tells you everything: mildly bullish, short Gamma, earning time, short volatility — before you have looked at a single individual leg.

**Professional interpretation.** A trading desk manages a book of hundreds of options purely through its aggregate Greeks. Traders rarely discuss individual options; they say "we're long 200 Deltas and short 3 lakh of Vega" and act on *that*. The portfolio Greek line is the language of professional risk.

**Common mistake.** Judging risk position-by-position. A trader who is comfortable with each leg separately can be unknowingly carrying a huge net short-Gamma or short-Vega exposure once the legs are summed.

**Practical takeaway.** **Roll your whole book into five portfolio Greeks and read that line before anything else — it is the only complete statement of how you will make or lose money.**

---

### 3.2 Reading the sign profile

Once you have the five numbers, their *signs* tell a story at a glance. Each Greek's sign says what helps and what hurts:

| Greek | Positive means you profit when… | Negative means you profit when… |
| --- | --- | --- |
| **Delta (Δ)** | the index rises | the index falls |
| **Gamma (Γ)** | the index makes a big move (either way) | the index stays calm |
| **Theta (Θ)** | time passes | — (you pay time) |
| **Vega (ν)** | implied volatility rises | implied volatility falls |

So a portfolio reading **+Δ, −Γ, +Θ, −ν** — the profile of our worked book — is a fingerprint that reads: *mildly bullish (+Δ); wants calm, hurt by big moves (−Γ); earns money as time passes (+Θ); wants volatility to fall, hurt by a VIX spike (−ν).* That is the classic **premium-seller profile with a bullish tilt** — the signature of most income strategies.

Learn to read these fingerprints instantly. **+Δ, +Γ, −Θ, +ν** is an option *buyer* (directional, wants movement, pays time, wants IV up). **≈0 Δ, −Γ, +Θ, −ν** is a pure short-volatility seller. The sign profile *is* the strategy, stated in the only terms that matter for P&L.

---

### 3.3 The fundamental seller's identity

There is a deep relationship among three of the Greeks that explains why "selling premium" is one coherent bet rather than three separate ones:

```
Short Gamma  ≈  Long Theta  ≈  Short Vega          (for an option seller)
```

When you sell options, all three arrive *together and inseparably*: you are short Gamma (big moves hurt), long Theta (you collect decay), and short Vega (IV spikes hurt). They are three faces of the same coin — the coin being "I have sold optionality." You cannot collect the Theta without accepting the short Gamma and short Vega; Chapter 9 established the Gamma–Theta link, Chapter 11 the Vega risk, and here they unite.

The mirror identity holds for buyers: **Long Gamma ≈ Short Theta ≈ Long Vega.** Buying optionality means you benefit from movement (long Gamma) and from rising IV (long Vega), and you pay for both through time decay (short Theta).

This identity is why the seller's two disaster scenarios — a big move (short Gamma) and a volatility spike (short Vega) — so often strike *together*: volatility spikes precisely when the market moves violently. The trinity that pays you calmly on quiet days turns on you all at once on the bad one.

> **Beginner Alert — "Selling premium" is one bet, not three.** It is tempting to think a short strangle makes money three ways (from Theta, from calm, from falling IV). It really makes money *one* way — by the market moving and its IV changing *less than the premium implied*. The positive Theta, the short Gamma, and the short Vega are all the same underlying bet viewed from three angles; when that bet is wrong, all three lose at once.

---

### 3.4 P&L attribution — the master equation

At the end of any period, you can decompose exactly *why* your book made or lost money, using the second-order Taylor expansion that unites all the Greeks:

```
ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)² + Θ·Δt + ν·Δσ                        (12.1)
```

using **portfolio** Greeks. Each term is one Greek's contribution: Delta (price), Gamma (curvature of the price move), Theta (time), Vega (volatility). Add them and you have explained the day.

**Worked attribution.** Take our book (Δ +29.9, Γ −0.046, Θ +₹643.5/day, ν −₹1,001.6/vol pt). Suppose today NIFTY rose 50 points, India VIX fell 1 point, and one day passed:

```
Delta: +29.9 × 50            = +₹1,495
Gamma: ½ × (−0.046) × 50²    = −₹57.5
Theta: +643.5 × 1            = +₹643.5
Vega:  −1,001.6 × (−1)       = +₹1,001.6
Total ΔP                     ≈ +₹3,083
```

You can now state precisely: *"We made ₹3,083 today: +₹1,495 from the market rising, −₹57.5 from Gamma, +₹643.5 from time decay, and +₹1,001.6 because IV fell."* This is the single most valuable habit in options — it turns confusing outcomes into diagnosis. If a day surprises you, attribution shows which Greek you mis-read.

> **Professional Insight — Attribute every day, especially the good ones.** Losing days force attention; *winning* days are where traders fool themselves. A desk attributes P&L daily precisely to catch the trap of "I made money, so I was right." You might have made ₹3,083 today because IV fell (a Vega windfall you did not forecast), while your actual thesis (a rally) contributed only half. Without attribution, you would credit your skill and repeat a trade whose real profit was luck. Attribution separates process from outcome.

---

### 3.5 Scenario analysis — stress before it happens

Attribution explains the past; **scenario analysis** rehearses the future. You apply equation (12.1) across a grid of possible moves to see your P&L in each — *before* the market delivers one. The most useful grid for an Indian book is **NIFTY move × VIX change**, because those are the two forces (price and volatility) that dominate, and they often move together.

Table 12.1 stress-tests our book across a 3×3 grid (instantaneous, i.e., before any Theta; add the +₹643.5/day separately for a full session). It uses the Delta, Gamma, and Vega terms of (12.1).

**Table 12.1 — Scenario matrix: P&L (₹) by NIFTY move × VIX change (instantaneous; book Δ+29.9, Γ−0.046, ν−₹1,001.6)**

| | VIX −2 | VIX unchanged | VIX +2 |
| --- | ---: | ---: | ---: |
| **NIFTY −300** | −9,037 | −11,040 | −13,043 |
| **NIFTY unchanged** | +2,003 | 0 | −2,003 |
| **NIFTY +300** | +8,903 | +6,900 | +4,897 |

Read the corners. The book's **best case** is a rally with falling VIX (+₹8,903) — its bullish Delta and short Vega both pay. Its **worst case** is a fall with rising VIX (−₹13,043) — the short Gamma bites on the drop *and* the short Vega bleeds on the spike. This bottom-left corner is the "crash scenario," and for a bullish, short-Gamma, short-Vega book it is the danger to size for. Scenario analysis makes that worst corner visible today, so you can decide whether you can survive it *before* it arrives.

*(Because a 300-point move is large, the Greek-based estimate is an approximation — the Greeks themselves shift over such a move — but it is more than accurate enough to reveal the shape of the risk.)*

---

### 3.6 The higher-order Greeks — practical interpretation

The five main Greeks assume the *other* inputs hold still while one moves. In reality they move together, and the **higher-order Greeks** capture how the main Greeks themselves change. You will not compute these by hand; you need only their practical meaning.

* **Charm (∂Δ/∂t) — "Delta decay."** How your Delta changes as *time passes*, even with the index flat. Near expiry, an OTM option's Delta drifts toward 0 and an ITM option's toward 1 just from the clock. *Practical implication:* a position that is Delta-neutral at today's close can open tomorrow with a Delta, purely from Charm — which is why overnight and weekend Delta drift catches sellers who "hedged and left."

* **Vanna (∂Δ/∂σ = ∂ν/∂S) — the Delta–volatility cross.** How your Delta changes when *IV* moves (equivalently, how your Vega changes when the *spot* moves). *Practical implication:* when volatility spikes, your Delta shifts even if the index has not moved, so your Delta hedge silently goes stale during a VIX event. Vanna is why hedging around events is harder than it looks — the thing you hedged (Delta) moves because of the thing you did not (IV).

* **Volga / Vomma (∂ν/∂σ) — "Vega of Vega."** How your Vega changes as IV moves. Vega is not constant: for OTM options, Vega *rises* as IV rises (positive Volga). *Practical implication:* in a large IV spike, your short-Vega loss accelerates — the Vega itself grows against you — so the linear "Vega × ΔIV" estimate understates the damage in a big volatility move, just as Gamma made Delta understate a big price move.

The pattern is consistent: **the second-order Greeks all warn that a linear estimate understates risk in a large move** — Gamma for price, Volga for volatility, Vanna and Charm for the cross-effects. Retail traders can safely manage with the five main Greeks *most* of the time, but must remember that around big events, the higher-order effects make reality worse than the first-order numbers suggest.

---

### 3.7 Greek hedging priorities and dynamic management

When your book's Greeks drift out of your comfort zone, which do you fix first? The practical hierarchy is **Delta first, then Vega, then Gamma:**

1. **Delta first.** It is the largest and fastest source of P&L, and it is the *cheapest and easiest to hedge* — one futures trade neutralises it instantly (Chapter 8). Always bring Delta into line first.
2. **Vega second.** Event and IV-spike risk is the next biggest exposure, especially for sellers. You hedge Vega with *options* (buying options to offset short Vega), which is costlier and slower than a futures trade — so it is second, not first.
3. **Gamma last.** Gamma is the hardest to hedge (it also requires options, and hedging it changes your Vega and Theta), and it only bites on large moves. You manage it mainly through *sizing and position selection* rather than active hedging — by not being too short Gamma in the first place.

**Dynamic hedging** is the ongoing application of this: as the underlying moves, Gamma changes your Delta (Chapter 9), so you re-trade futures to keep Delta in range. A high-Gamma book needs frequent re-hedging (and pays the slippage cost); a low-Gamma book can be left longer. The art is re-hedging often enough to control risk without churning away your edge in transaction costs.

---

### 3.8 Making adjustment decisions

Portfolio Greeks turn "should I adjust?" from a gut feeling into a rule. You set **thresholds** on each Greek and act when they are breached. A simple decision framework:

* **If |net Delta| exceeds one futures lot's worth (±65 units):** hedge with futures to bring it back toward your target (short a future if too long, buy if too short).
* **If net Vega grows too negative ahead of an event:** buy options (or close some short legs) to reduce the short-Vega exposure before IV can spike.
* **If net Gamma is too short as expiry nears:** reduce size or roll to a further expiry — do not try to trade through an expiry-day Gamma bomb (Chapter 9).
* **If a tested short leg's Delta runs past a set level:** roll it (to a further strike or expiry) or close it, per a pre-defined rule — not "when it feels scary."

The key discipline: **set the thresholds before the trade, when you are calm**, and act mechanically when they trigger. Adjustment decisions made in the heat of a losing move are almost always worse.

---

## 4. Examples (Real-World)

**Example 1 — Two safe-looking legs, one dangerous book.** A trader is comfortable being short one 25,000 call and, separately, short one 24,200 put. Summed, the book is short a strangle — net short Gamma and short Vega — and a single volatile session can hurt both legs at once. Neither leg alarmed them; the *portfolio* should have.

**Example 2 — The winning day that was luck.** A trader's bullish book makes ₹4,000 on a day NIFTY rose only 20 points. Attribution shows +₹690 from Delta and +₹3,300 from a falling VIX (Vega). Their thesis barely worked; a Vega windfall carried the day. Without attribution, they would have congratulated their direction call and over-sized the next one.

**Example 3 — The stale overnight hedge.** A trader delta-hedges to zero at Friday's close. Over the weekend, Charm drifts the Delta and the option's own decay shifts the book, so Monday opens with a live Delta and a gap move immediately produces P&L. "I was hedged" — on Friday, not on Monday.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, 10 DTE, lot 65; per-unit Greeks from Chapters 8–11.

### Numerical Example 1 — Building the portfolio Greeks table

A five-position NIFTY book. Per-unit Greeks: 25,000 CE (Δ 0.26, Γ 0.000608, Θ −8.5, ν 13.1); 24,200 PE (Δ −0.20, Γ 0.000522, Θ −7.3, ν 11.3); 25,200 CE (Δ 0.15, Γ 0.000443, Θ −6.2, ν 9.56); 24,000 PE (Δ −0.11, Γ 0.000350, Θ −4.9, ν 7.53); 24,600 CE (Δ 0.54, Γ 0.000754, Θ −10.6, ν 16.3). Each contribution = Greek × Q × 65.

**Table 12.2 — Portfolio Greeks for a 5-position NIFTY book**

| Position | Δ | Γ | Θ (₹/day) | ν (₹/vol pt) |
| --- | ---: | ---: | ---: | ---: |
| Short 2 × 25,000 CE | −33.80 | −0.0790 | +1,105.0 | −1,703.0 |
| Short 2 × 24,200 PE | +26.00 | −0.0679 | +949.0 | −1,469.0 |
| Long 1 × 25,200 CE | +9.75 | +0.0288 | −403.0 | +621.4 |
| Long 1 × 24,000 PE | −7.15 | +0.0228 | −318.5 | +489.5 |
| Long 1 × 24,600 CE | +35.10 | +0.0490 | −689.0 | +1,059.5 |
| **Portfolio total** | **+29.9** | **−0.046** | **+643.5** | **−1,001.6** |

**Interpretation.** The book is **+Δ, −Γ, +Θ, −ν**: mildly bullish (long ~29.9 Deltas, under half a futures lot), short Gamma (hurt by big moves), earning ₹643.5/day from time, and short ~₹1,001.6/vol point of Vega (hurt by a VIX spike). It is a premium-seller book with a slight bullish lean — read entirely off one summary line.

### Numerical Example 2 — P&L attribution for a day

NIFTY +50, VIX −1, one day passes:

```
Delta: +29.9 × 50         = +₹1,495
Gamma: ½ × (−0.046) × 50² = −₹57.5
Theta: +643.5 × 1         = +₹643.5
Vega:  −1,001.6 × (−1)    = +₹1,001.6
Total                     ≈ +₹3,083
```

The day's ₹3,083 gain breaks down as: mostly the rally (₹1,495) and the falling IV (₹1,001.6), with time (₹643.5) helping and Gamma (−₹57.5) a minor drag.

### Numerical Example 3 — Scenario stress test

Applying the Delta, Gamma, and Vega terms across a grid gives Table 12.1. The two corners that matter:

```
Best  (NIFTY +300, VIX −2): +29.9×300 + ½×(−0.046)×300² + (−1,001.6)×(−2)
     = +8,970 − 2,070 + 2,003 = +₹8,903
Worst (NIFTY −300, VIX +2): +29.9×(−300) + ½×(−0.046)×(−300)² + (−1,001.6)×(+2)
     = −8,970 − 2,070 − 2,003 = −₹13,043
```

The worst case (a fall with a VIX spike) is about 1.5× the best case in magnitude — the short-Gamma, short-Vega asymmetry laid bare. Add +₹643.5 of Theta for a full day in each cell.

### Numerical Example 4 — An adjustment to Delta-neutral (keeping positive Theta)

The book's net Delta is +29.9. To neutralise it *without* touching the options (which would change Theta and Vega), hedge with futures:

```
Futures to hedge = Net Delta ÷ Lot size = 29.9 ÷ 65 ≈ 0.46 lots
```

You would short about half a futures lot — not tradable in whole lots — so you short 0 or 1 lot and carry a small residual Delta. Crucially, hedging with a *future* leaves Theta (+₹643.5/day) and Vega (−₹1,001.6) untouched: you have removed direction while keeping the income and the volatility bet intact. This is why futures, not options, are the tool of choice for Delta adjustments.

---

## 6. Calculations (the reusable recipes)

**(a) Portfolio Greeks**

```
Portfolio Greek = Σ (Greek_i × Quantity_i × Lot size)     (Q negative for short legs)
```

**(b) P&L attribution / scenario P&L (master equation, portfolio Greeks)**

```
ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)² + Θ·Δt + ν·Δσ
     (price) (curvature)   (time)  (volatility)
```

**(c) Delta hedge with futures (preserves Theta and Vega)**

```
Futures lots to hedge = Net Delta ÷ Lot size
```

**(d) The seller's / buyer's identity**

```
Seller: Short Gamma ≈ Long Theta ≈ Short Vega
Buyer:  Long Gamma  ≈ Short Theta ≈ Long Vega
```

**(e) Higher-order Greeks (definitions; practical use only)**

```
Charm = ∂Δ/∂t          (Delta drifts with time — overnight/weekend drift)
Vanna = ∂Δ/∂σ = ∂ν/∂S  (Delta moves when IV moves; Vega moves when spot moves)
Volga = ∂ν/∂σ          (Vega grows as IV rises — short-Vega losses accelerate)
```

---

## 7. Practical Insights

* **Manage the book, not the legs.** Your risk is the *net* of five portfolio Greeks; sum them first and read that line before judging any position.
* **Read the sign profile as a fingerprint.** +Δ/−Γ/+Θ/−ν is a seller; +Δ/+Γ/−Θ/+ν is a buyer. The signs tell you instantly what helps and what hurts.
* **Attribute your P&L every day — especially winners.** It is the only way to tell skill from luck and to catch which Greek you mis-read.
* **Stress the worst corner before it happens.** For most income books the danger is "fall + VIX spike"; run that scenario and confirm you can survive it, in advance.
* **Hedge Delta first (with futures), Vega second (with options), Gamma by sizing.** And set adjustment thresholds when calm, then act mechanically.

> **Professional Insight — Delta-neutral is the most dangerous phrase in options.** More retail accounts are blown up by "but I was Delta-neutral" than by any single bad directional call. Delta-neutral removes one of five risks; the four that remain — Gamma, Theta, Vega, and the higher-order cross-effects — are exactly what a short-premium book is most exposed to. A professional never says "I'm hedged"; they say "I'm Delta-hedged, short 0.046 Gamma and ₹1,002 of Vega, and here's my worst-case corner." Precision about *which* risks remain is the whole discipline.

---

## 8. Common Mistakes

* **Judging risk position-by-position.** Comfortable-looking legs can sum to a dangerous net short-Gamma or short-Vega book.
* **Equating Delta-neutral with risk-neutral.** Neutralising Delta leaves Gamma, Vega, and time risk fully live — the introduction's ₹12,800 loss.
* **Skipping attribution on winning days.** Crediting your thesis when a Vega windfall did the work, then over-sizing the next trade.
* **Forgetting Charm — the stale overnight hedge.** A Delta-neutral close can open with a live Delta from time drift; "hedged Friday" is not "hedged Monday."
* **Ignoring the higher-order Greeks around events.** Vanna and Volga make big-move losses worse than the linear Greek estimate — the first-order numbers flatter you in exactly the moments that matter.
* **Hedging Gamma with more options in a panic.** Gamma is best managed by *sizing*; trying to buy it back mid-crisis usually adds cost and new Vega risk.

---

## 9. Case Study — "The Perfectly Hedged Portfolio That Lost Money"

**Context.** A trader runs a NIFTY short strangle — the archetypal income position — and does everything the textbooks (up to Chapter 8) told them: they **hedge the Delta to exactly zero** with futures, so the book is directionally flat, and it carries a healthy **positive Theta** of about **+₹1,000/day**. They describe it, proudly, as "market-neutral, earning money every day." Their portfolio Greeks, however, read: **Δ ≈ 0, Γ ≈ −0.06, Θ ≈ +₹1,000/day, ν ≈ −₹1,500/vol point.** Figures are illustrative but representative.

**What happened.** In a single session, a global shock sent **NIFTY down 400 points and India VIX up 6 points.** The "perfectly hedged" book's P&L, by attribution (equation 12.1):

| Greek | Driver | Contribution |
| --- | --- | ---: |
| Delta | Started at zero (hedged) | ≈ ₹0 |
| Gamma | ½ × (−0.06) × (−400)² | **−₹4,800** |
| Vega | −1,500 × (+6) | **−₹9,000** |
| Theta | +1,000 × 1 day | +₹1,000 |
| **Net** | | **≈ −₹12,800** |

A **₹12,800 loss on a Delta-neutral, Theta-positive book** — in one day.

**The analysis.** The trader hedged the *one* Greek they were watching and left the *two* that actually fired:

* **Gamma (−₹4,800):** the book was short Gamma, so as NIFTY fell, its Delta ran negative (it got *longer* into the drop — Chapter 9). The "Delta-neutral" hedge was true only at the starting price; the move itself created a losing Delta the futures hedge did not cover.
* **Vega (−₹9,000):** the book was short Vega, and the 6-point VIX spike revalued every short option higher — the largest single loss, and one that had nothing to do with direction (Chapter 11).
* **Theta (+₹1,000):** the day's decay income was real but trivial against the Gamma and Vega losses — one day's rent against a crash.

The two disasters arrived *together*, exactly as the seller's identity (Section 3.3) warns: volatility spiked *because* the market moved violently, so short Gamma and short Vega both lost in the same session.

**What would have helped.** Nothing in the trader's process monitored Gamma or Vega. Had they read their full portfolio Greeks, they would have seen a large short-Gamma, short-Vega exposure and could have: sized smaller; bought cheap wings to cap the Gamma and reduce the Vega (turning the strangle into a condor); reduced size before a known-risk event; or set a scenario limit ("if my worst corner exceeds ₹X, cut"). "Delta-neutral" gave them false comfort precisely because it hid the risks that mattered.

**The lesson.** Delta-neutral is not risk-neutral. A position is only as safe as its *full* Greek profile, and for a short-premium book the dangers live in Gamma and Vega — the two Greeks that a Delta hedge does nothing about. Monitor all five, stress the worst corner, and never mistake "hedged against the risk I was watching" for "hedged."

*(Takeaway: read your whole Greek line, not just Delta — the risk that ends accounts is almost always the Greek you were not looking at.)*

---

## 10. Chapter Summary

* **Portfolio Greeks** = Σ(Greek × quantity × lot size) collapse an entire book into five numbers that fully describe how it will make or lose money.
* The **sign profile** is a fingerprint: **+Δ/−Γ/+Θ/−ν** is a premium seller (our worked book); **+Δ/+Γ/−Θ/+ν** is a buyer.
* The **seller's identity** — Short Gamma ≈ Long Theta ≈ Short Vega — shows that "selling premium" is *one* bet with three faces, which is why its two disasters (big move, IV spike) strike together.
* **P&L attribution** via `ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)² + Θ·Δt + ν·Δσ` explains any day exactly — do it daily, especially on winners, to separate skill from luck.
* **Scenario analysis** (NIFTY move × VIX change) rehearses the future; for a bullish, short-Gamma, short-Vega book the worst corner is "fall + VIX spike."
* **Higher-order Greeks** — Charm (Delta drifts with time), Vanna (Delta moves with IV), Volga (Vega grows with IV) — all warn that linear estimates understate risk in big moves.
* **Hedging priority:** Delta first (futures, cheap and fast), Vega second (options), Gamma by sizing; set adjustment thresholds when calm and act mechanically.
* **Delta-neutral is not risk-neutral** — the "perfectly hedged" book lost ₹12,800 in a day to the Gamma and Vega it never neutralised.

---

## 11. Key Takeaways

* **Sum your book into five portfolio Greeks and read that line first** — it is the complete statement of your risk.
* **Attribute every day's P&L to its Greeks** — the winners lie to you more than the losers.
* **Stress your worst corner (fall + VIX spike, usually) in advance** and size so you can survive it.
* **Never confuse Delta-neutral with safe** — monitor Gamma, Vega, and time too, because the Greek that blows up accounts is the one you were not watching.

---

## 12. Practice Questions

**Q1 (Definition).** Write the formula for a portfolio Greek and explain in one sentence why aggregating matters.

**Q2 (Sign profile).** A book reads Δ +40, Γ −0.06, Θ +₹900/day, ν −₹1,300/vol point. Describe its risk profile in plain English.

**Q3 (Identity).** State the seller's fundamental identity and explain why a short strangle's two worst scenarios tend to arrive together.

**Q4 (Portfolio Greeks).** You hold long 2 lots of an option with Δ 0.40 and short 1 lot of an option with Δ 0.55 (lot 65). Compute the net portfolio Delta.

**Q5 (Attribution).** A book has Δ +30, Γ −0.05, Θ +₹700/day, ν −₹1,100/vol pt. NIFTY rises 40, VIX falls 2, one day passes. Attribute the P&L to each Greek and give the total.

**Q6 (Scenario).** For the Q5 book, compute the instantaneous P&L (ignore Theta) if NIFTY falls 250 and VIX rises 3.

**Q7 (Hedging priority).** State the practical order in which you hedge Delta, Vega, and Gamma, and give one reason for Delta being first.

**Q8 (Delta hedge).** A book's net Delta is +160 units (lot 65). How many futures lots, and in which direction, bring it closest to neutral, and what happens to the book's Theta and Vega?

**Q9 (Higher-order).** Explain, in one sentence each, the practical warning given by Charm, Vanna, and Volga.

**Q10 (Judgement).** A trader says, "My short strangle is Delta-neutral, so I'm safe over the RBI policy tomorrow." Explain why this is dangerously wrong.

---

## 13. Detailed Solutions

**A1.** Portfolio Greek = Σ(Greek_i × Quantity_i × Lot size), with quantity negative for short legs. Aggregating matters because your P&L is driven by the *net* exposure across all legs, not by any single position — offsetting or compounding effects only appear once summed.

**A2.** The book is mildly **bullish** (+Δ 40, ~half a futures lot long), **short Gamma** (−0.06 → hurt by big moves in either direction, wants calm), **Theta-positive** (+₹900/day → earns money as time passes), and **short Vega** (−₹1,300/vol pt → hurt by a VIX spike, helped by an IV crush). It is a premium-seller book with a bullish tilt.

**A3.** The seller's identity is **Short Gamma ≈ Long Theta ≈ Short Vega.** A short strangle's two worst scenarios — a large move (short Gamma) and an IV spike (short Vega) — tend to arrive together because implied volatility spikes precisely when the market moves violently, so both losing exposures fire in the same session.

**A4.** Net Delta = (2 × 0.40 × 65) + (−1 × 0.55 × 65) = 52 − 35.75 = **+16.25 units** (net slightly long).

**A5.** Delta: 30 × 40 = +₹1,200; Gamma: ½ × (−0.05) × 40² = −₹40; Theta: +700 × 1 = +₹700; Vega: −1,100 × (−2) = +₹2,200. **Total ≈ +₹4,060.** (Mostly the falling VIX and the rally.)

**A6.** Delta: 30 × (−250) = −₹7,500; Gamma: ½ × (−0.05) × (−250)² = ½ × (−0.05) × 62,500 = −₹1,563; Vega: −1,100 × (+3) = −₹3,300. **Instantaneous total ≈ −₹12,363** — the classic worst corner (fall + VIX spike) for a short-Gamma, short-Vega book.

**A7.** Order: **Delta first, then Vega, then Gamma.** Delta is first because it is the largest, fastest P&L driver and the cheapest to hedge — a single futures trade neutralises it instantly, whereas Vega and Gamma require options (costlier and slower), and Gamma is best managed by sizing.

**A8.** Futures lots = 160 ÷ 65 ≈ 2.46, so **short 2 lots** of NIFTY futures (leaving a small residual Delta of 160 − 130 = +30; two lots is closer to neutral than three, which would overshoot to −35). Because you hedged with *futures*, the book's **Theta and Vega are unchanged** — you removed direction while keeping the income and volatility exposure intact.

**A9.** **Charm:** your Delta drifts as time passes (even with the index flat), so a Delta-neutral position can open with a Delta after a night or weekend. **Vanna:** your Delta moves when IV moves, so a Delta hedge goes stale during a volatility event. **Volga:** your Vega grows as IV rises, so short-Vega losses accelerate in a big IV spike beyond the linear estimate.

**A10.** Delta-neutral removes only directional risk. Over the RBI policy, the two biggest dangers to a short strangle are a **large move** (short Gamma — the announcement can gap the index) and a **volatility change** (short Vega — IV is elevated before the event and can crush after, or spike on a shock). A Delta hedge does nothing about either. The position is exposed to exactly the Greeks that an event moves most, so "Delta-neutral" is false comfort — the trader is heavily short Gamma and short Vega into the event.

---

## 14. Mini Glossary

* **Portfolio (position) Greeks** — the net Delta, Gamma, Theta, Vega, and Rho of an entire book: Σ(Greek × quantity × lot size). → this chapter.
* **Sign profile** — the pattern of signs across the portfolio Greeks that identifies a strategy's risk (e.g., +Δ/−Γ/+Θ/−ν = premium seller). → this chapter.
* **Seller's identity** — Short Gamma ≈ Long Theta ≈ Short Vega; the three faces of selling optionality. → this chapter.
* **P&L attribution** — decomposing a period's P&L into Delta, Gamma, Theta, and Vega contributions via the master equation. → this chapter.
* **Master equation** — ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)² + Θ·Δt + ν·Δσ. → this chapter.
* **Scenario analysis** — computing P&L across a grid of possible moves (e.g., NIFTY move × VIX change) before they occur. → this chapter.
* **Dynamic hedging** — continuously re-adjusting the Delta hedge as Gamma changes it. → this chapter.
* **Hedging priority** — Delta first (futures), Vega second (options), Gamma by sizing. → this chapter.
* **Charm** — the rate of change of Delta with time (∂Δ/∂t); causes overnight/weekend Delta drift. → this chapter.
* **Vanna** — the Delta–volatility cross-Greek (∂Δ/∂σ = ∂ν/∂S); Delta moves when IV moves. → this chapter.
* **Volga / Vomma** — the rate of change of Vega with IV (∂ν/∂σ); short-Vega losses accelerate in big IV moves. → this chapter.
* **Delta-neutral ≠ risk-neutral** — the principle that hedging Delta leaves Gamma, Vega, and time risk fully live. → this chapter.

---

<!-- End of Chapter 12 (Rev 2, Part III capstone, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026 revision) — 5-position book RE-SUMMED: Δ+29.9, Γ−0.046, Θ+₹643.5/day, ν−₹1,001.6/vol pt (verified column sums from unchanged per-unit Ch8-11 Greeks). P&L attribution (NIFTY+50, VIX−1, 1 day) = +₹3,083. Scenario matrix corners: best (+300,−2)=+₹8,903; worst (−300,+2)=−₹13,043 (~1.5× best). Delta hedge 29.9/65≈0.46 lots (preserves Θ,ν). Adjustment threshold ±65 units (one lot). Q4 net Δ +16.25; Q8 160/65≈2.46 → short 2 lots, residual +30. Case study (Δ-neutral short strangle Γ−0.06, ν−₹1,500, Θ+₹1,000; shock NIFTY−400/VIX+6 → Gamma −₹4,800, Vega −₹9,000, Theta +₹1,000, net −₹12,800) and Q5/Q6 use standalone round illustrative Greeks — valid at lot 65, unchanged. No transaction costs → Apr-2026 STT change not applicable. Higher-order Greeks at practical level only. IV = implied volatility. No forward chapter-number references. -->
