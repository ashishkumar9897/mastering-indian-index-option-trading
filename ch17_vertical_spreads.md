<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapters 8, 10, 11, 16. Target length ~10,000 words. Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65; BANKNIFTY lot 30 (NSE Jan-2026 revision). Uses the standard strategy template. Per-unit premiums (skew-consistent, 10 DTE, NIFTY 24,600), credits/debits, breakevens, R/R, probabilities, and ROI% (=credit/max-loss) are all lot-independent — unchanged. Lot-scaled rupee figures updated to lot 65: naked-put margin ~₹1.35→~₹1.17 lakh (preserves 7.1% ROI), spread margin=max-loss ₹11,250→₹9,750 (preserves 33.3%), bull-put credit ₹3,250/lot, bull-call debit ₹6,955/lot, naked max loss ~₹15.9 lakh. Width-analysis table (17.3) lot-independent, unchanged. Case study BANKNIFTY lot 30: max profit ₹4,500/lot, max loss ₹10,500/lot, unrealised loss −₹3,900/lot; roll corrected from "next weekly" to "next monthly" (BANKNIFTY monthly-only since Nov 2024). Q5/A5 self-contained abstract exercise — unchanged. No transaction costs shown (gross P&L) → Apr-2026 STT change not applicable. Margin for spreads = max loss (SEBI). IV = implied volatility. -->

# Chapter 17 — Vertical Spreads: Defined-Risk Directional Trading

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Construct and analyse bull call spreads and bear put spreads (debit spreads).
2. Construct and analyse bull put spreads and bear call spreads (credit spreads).
3. Understand why spreads are the workhorse of professional options trading.
4. Select the optimal spread width and short-strike distance.
5. Manage and adjust a spread when the trade goes against you.

Chapter 16 gave you the single-leg directional trade, with its two uncomfortable extremes: buy an option and bleed Theta with limited odds, or sell one and carry large, margin-hungry risk. The **vertical spread** is the elegant middle path — and it is the single most useful structure in options trading.

---

## 2. Introduction

The naked option forces a bad bargain. Buy one, and you pay Theta every day and must be right on direction, size, *and* timing to overcome the premium — you win rarely. Sell one, and you collect Theta and win often, but you post ₹1.17 lakh of margin per lot and carry a loss that can dwarf the premium — the "one big loss" that ends accounts (Chapters 10, 12). Neither is how professionals trade directionally most of the time.

The **vertical spread** solves the problem by pairing two options of the same type and expiry at different strikes. Sell the option you want to sell, then *buy a cheaper, further option as insurance against the tail*. In one stroke this **defines your maximum loss**, **slashes your margin** (SEBI charges margin equal to the capped risk, not the naked risk), and **improves your capital efficiency** dramatically. You give up some premium and some upside — but you trade an open-ended, capital-heavy position for a bounded, capital-light one. That trade-off is so favourable that spreads, not naked options, are the everyday tool of serious traders.

This chapter builds the four vertical spreads — two you *pay* for (debit) and two you *collect* for (credit) — shows exactly why the credit-spread-with-a-wing crushes the naked option on margin and risk, teaches you to choose the width and the short strike (two separate levers), and walks through adjusting a spread in real time when the market moves against you. Setting: **NIFTY at 24,600, lot 65**, with skew-consistent premiums from the Part IV surface.

---

## 3. Core Concepts

### 3.1 What a vertical spread is — and why it's the workhorse

The vertical spread is the flagship of this chapter.

**What is it?** A **vertical spread** is a two-leg position combining a long and a short option of the *same type* (both calls or both puts) and *same expiry*, at *different strikes*. "Vertical" refers to the strikes being stacked vertically on the option chain. There are four:

* **Debit spreads** (you pay a net premium): **bull call spread** and **bear put spread**.
* **Credit spreads** (you collect a net premium): **bull put spread** and **bear call spread**.

**Why does it exist?** To fix the naked option's two flaws. A naked short option has open-ended risk and huge margin; a naked long option bleeds full Theta and needs a big move. The spread pairs the position you want with an offsetting option that **caps the risk** (for the seller) or **cheapens the cost** (for the buyer). The far leg is insurance — you sacrifice a little to bound the outcome.

**Why should a trader care?** Because the spread transforms the economics of a directional trade. For a credit spread, it **defines the maximum loss, cuts the margin to that maximum loss (a fraction of the naked requirement), and raises the return on capital** — while keeping most of the naked position's high probability of profit. For a debit spread, it **cheapens the trade and reduces Theta and Vega drag**, at the cost of capping the upside. Either way, you get a bounded, efficient, professional-grade position.

**Intuitive explanation.** A credit spread is **selling insurance while buying cheaper reinsurance.** You collect a premium for insuring the market (the short leg), then hand a slice of it to a reinsurer (the long leg) who caps your payout if disaster strikes. You earn less than the naked insurer, but you can never be wiped out — and you tie up far less capital. A debit spread is the mirror: **buying insurance and selling back the part you don't need**, cheapening your coverage.

**Numerical feel.** Selling a naked NIFTY 24,400 put collects ₹128 but demands ~₹1.17 lakh of margin and carries huge tail risk. Turning it into a bull put spread (buying the 24,200 put for ₹78) collects only ₹50 — but caps the loss at ₹9,750, cuts the margin to ₹9,750, and *quadruples* the return on capital (Section 3.4). You gave up ₹78 of credit to buy away the tail; the capital efficiency more than repays it.

**Professional interpretation.** Professionals express most directional and income views through spreads, not naked options, precisely because of this capital and risk efficiency. A desk running credit spreads can deploy far more positions on the same capital, each with a known worst case — which is exactly what disciplined, scalable trading requires.

**Common mistake.** Selling naked options for the larger premium while ignoring that the spread's higher *return on capital* and defined risk usually make it the better trade (Section 3.4).

**Practical takeaway.** **The vertical spread is the workhorse of directional and income trading — it defines your risk, slashes your margin, and multiplies your return on capital; reach for a spread before a naked option almost every time.**

---

### 3.2 The four vertical spreads

Table 17.1 is the standardised trade sheet for all four, using the NIFTY surface (spot 24,600, 10 DTE, 200-point widths).

**Table 17.1 — The four vertical spreads (NIFTY 24,600, 200-wide, illustrative)**

| | **Bull Call Spread** (debit) | **Bear Put Spread** (debit) | **Bull Put Spread** (credit) | **Bear Call Spread** (credit) |
| --- | --- | --- | --- | --- |
| View | Bullish | Bearish | Bullish/neutral | Bearish/neutral |
| Buy | 24,600 CE @₹212 | 24,600 PE @₹198 | 24,200 PE @₹78 | 25,000 CE @₹48 |
| Sell | 24,800 CE @₹105 | 24,400 PE @₹128 | 24,400 PE @₹128 | 24,800 CE @₹105 |
| Net | Debit ₹107 | Debit ₹70 | Credit ₹50 | Credit ₹57 |
| Max profit | ₹93 (width − debit) | ₹130 | ₹50 (credit) | ₹57 (credit) |
| Max loss | ₹107 (debit) | ₹70 | ₹150 (width − credit) | ₹143 |
| Breakeven | 24,707 | 24,530 | 24,350 | 24,857 |
| Risk-reward | 0.87 | 1.86 | 0.33 | 0.40 |
| Net Delta | +0.15 | −0.14 | +0.12 | −0.13 |
| Prob. max profit | ~40% | ~55% | ~68% | ~61% |

Read the structure by pairs:

**Debit spreads** (you pay, betting on a move):

* **Bull call spread** — buy a lower call, sell a higher call. You pay a net debit, profit as the index rises, with both loss (the debit) and profit (width − debit) capped. Cheaper than a naked call (the short leg funds part of it), with reduced Theta and Vega drag — but the upside is capped at the higher strike.
* **Bear put spread** — buy a higher put, sell a lower put. The bearish mirror.

**Credit spreads** (you collect, betting on *not* a move against you):

* **Bull put spread** — sell a higher put, buy a lower put. You collect a net credit, keep it if the index stays above the short strike, with loss capped at (width − credit). A bullish/neutral income trade with a *high probability of profit* (~68% here) and defined risk.
* **Bear call spread** — sell a lower call, buy a higher call. The bearish/neutral mirror.

Notice the credit spreads' high probability of max profit (61–68%) against their modest reward-to-risk (0.33–0.40) — they **win often and small**, the seller's profile (Chapter 16) but with the tail cut off. The debit spreads win less often but pay more relative to risk — the buyer's profile, made cheaper and bounded.

---

### 3.3 The math of vertical spreads

Every vertical spread's outcome is fully defined by four numbers. The formulas:

```
CREDIT SPREADS (bull put, bear call):
  Max profit = Net credit received
  Max loss   = Spread width − Net credit
  Breakeven (bull put) = Short strike − Net credit
  Breakeven (bear call) = Short strike + Net credit

DEBIT SPREADS (bull call, bear put):
  Max profit = Spread width − Net debit
  Max loss   = Net debit
  Breakeven (bull call) = Lower strike + Net debit
  Breakeven (bear put)  = Higher strike − Net debit

BOTH:
  Risk-reward ratio = Max profit / Max loss
  Probability of max profit ≈ 1 − |Delta of the short strike|   (credit spreads)
```

**Worked example (bull put spread).** Sell the 24,400 PE (₹128, Δ−0.32), buy the 24,200 PE (₹78); width 200:

```
Net credit   = 128 − 78 = ₹50
Max profit   = ₹50 (₹3,250/lot)
Max loss     = 200 − 50 = ₹150 (₹9,750/lot)
Breakeven    = 24,400 − 50 = 24,350
Risk-reward  = 50 / 150 = 0.33
Prob. max profit ≈ 1 − 0.32 = 0.68 (68%)
```

The position keeps the full ₹50 if NIFTY finishes above 24,400, breaks even at 24,350, and loses the full ₹150 below 24,200 — a bounded, high-probability, bullish-neutral income trade.

**Probability of max profit.** For a credit spread, the position keeps the full credit if the *short strike* expires out of the money, which happens with probability roughly `1 − |Delta of the short strike|` (recall Delta ≈ risk-neutral probability of finishing ITM, Chapter 8). A 0.32-Delta short put → ~68% chance of max profit. This is why credit-spread sellers choose short strikes by delta: a 0.30-delta short strike targets a ~70% win rate.

> **Beginner Alert — high win rate is not high edge.** A bull put spread that wins 68% of the time sounds like a money machine — until you see its 0.33 risk-reward: the ₹150 loss is three times the ₹50 win. Win 68% and lose 32%, and the expectancy is 0.68 × 50 − 0.32 × 150 = +₹2 per unit — thin, before costs. Credit spreads are *not* free money; their high probability is balanced by an unfavourable reward-to-risk, exactly as the variance-risk-premium edge (Chapter 14) predicts. The edge is real but small, and one un-managed loss erases many wins.

---

### 3.4 Naked versus spread — the case for the wing

The clearest way to see why spreads dominate is to compare a naked short put with the bull put spread built on the *same* short strike. Table 17.2 does this for the 24,400 PE.

**Table 17.2 — Naked short put vs bull put spread (same short strike 24,400)**

| | Naked short 24,400 PE | Bull put spread (24,400/24,200) |
| --- | --- | --- |
| Net credit | ₹128 (₹8,320/lot) | ₹50 (₹3,250/lot) |
| Max loss | Huge (to 24,400 × 65 ≈ ₹15.9 lakh) | ₹150 (₹9,750/lot) — **defined** |
| Margin | ~₹1,17,000 | ~₹9,750 (= max loss, SEBI) |
| Net Delta | +0.32 | +0.12 |
| Net Vega | −₹large | −₹small |
| **ROI on margin** (if kept) | 8,320 / 1,17,000 = **7.1%** | 3,250 / 9,750 = **33.3%** |

The spread collects less absolute premium (₹50 vs ₹128) — but look at what the ₹78 spent on the long 24,200 put buys:

* **Defined risk.** The max loss falls from a catastrophic ~₹15.9 lakh to a known ₹9,750.
* **Margin cut by ~92%.** SEBI charges margin equal to the *capped* risk (Chapter 3), so ₹9,750 instead of ₹1.17 lakh.
* **Return on capital nearly 5× higher.** 33.3% vs 7.1% — because the tiny margin transforms the modest credit into a large return on the capital actually tied up.

This is the whole argument for spreads. You "lose" ₹78 of credit and cap your upside, but you gain defined risk, a fraction of the margin, and a far higher return on the capital you deploy. The naked put's larger premium is an illusion of superiority; on the metric that matters — **return on capital at risk** — the spread wins decisively. This capital efficiency is *why* spreads are the professional workhorse and why the same capital can run many spreads instead of a few naked positions.

> **Professional Insight — judge income trades by return on margin, not premium.** Beginners compare "₹128 naked vs ₹50 spread" and pick the naked put for the bigger number. Professionals compare "7% vs 33% return on the capital blocked" and pick the spread — then run several spreads on the freed-up capital, each with a known worst case. The premium is the headline; the return on margin is the business. Never let a bigger premium seduce you into an open-ended, capital-heavy position.

---

### 3.5 Two separate levers — width and short-strike distance

New traders conflate two independent choices. Keep them separate:

**Lever 1 — the short-strike distance (sets the probability and the payout).** Moving the *short* strike further from the money raises the probability of profit but lowers the credit. A 0.30-delta short strike wins ~70% of the time for a small credit; a 0.45-delta short strike wins ~55% of the time for a larger credit. This is the **probability-versus-payout tradeoff** — governed by *where you place the short strike*, i.e., its delta.

**Lever 2 — the spread width (sets the risk and the credit size, at constant probability).** Holding the short strike fixed and moving the *long* wing further away widens the spread — collecting more credit but risking more, with the probability of max profit *unchanged* (it depends only on the short strike). Table 17.3 shows this for a bull put spread with the short 24,400 PE fixed.

**Table 17.3 — Spread width analysis (bull put, short 24,400 PE @₹128 fixed)**

| Width | Long wing | Credit | Max loss | Risk-reward | ROI on margin | Prob. max profit |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 100 | buy 24,300 PE @₹100 | ₹28 | ₹72 | 0.39 | 38.9% | ~68% |
| 200 | buy 24,200 PE @₹78 | ₹50 | ₹150 | 0.33 | 33.3% | ~68% |
| 500 | buy 23,900 PE @₹36 | ₹92 | ₹408 | 0.23 | 22.5% | ~68% |

Read across: **wider spreads collect more credit (₹28 → ₹50 → ₹92) but risk more (₹72 → ₹408), with worse reward-to-risk and lower return on capital — and the same probability of profit** (68%, because the short strike never moved). The narrow spread is the most capital-efficient per rupee of risk; the wide spread collects more absolute credit (approaching the naked put) but at worse efficiency. Choose the width by how much capital you are willing to risk and how close to "naked-like" credit you want — not by probability, which the short strike alone controls.

> **Beginner Alert — probability comes from the short strike, not the width.** It is tempting to think a "narrow" spread is safer. Narrowing the *width* (moving the long wing closer) does not change your probability of profit at all — it only lowers your risk and your credit together. Your probability of profit is set entirely by *where the short strike sits* (its delta). Separate the two levers or you will mis-design every spread.

---

### 3.6 Entry timing — IV, skew, and the mental model

*When* and *which side* you put on a spread matters as much as the structure:

* **Credit spreads in high IV; debit spreads in low IV.** A credit spread is *short* premium and short Vega — sell it when IV is rich (high IV Rank, Chapter 14), so you collect fat premium and benefit as IV mean-reverts down. A debit spread is *long* premium and mildly long Vega — buy it when IV is cheap, so you pay less and have room for IV to rise. Match the spread's Vega sign to the IV regime.
* **Favour the put side (the skew).** Because of the volatility skew (Chapter 15), OTM puts carry higher IV than equidistant OTM calls, so a **bull put spread collects more credit than an equidistant bear call spread**. For a neutral-to-bullish view, selling the richer put side is better-compensated — a structural edge from the skew. (At 400 points OTM on our surface, a bull put's short 24,200 PE fetches ₹78 versus the bear call's short 25,000 CE at ₹48 — the put side is richer.)
* **The mental model — a credit spread is selling capped insurance.** You collect a premium to insure the market against breaching your short strike, and you buy cheaper reinsurance (the long wing) that caps your payout. You earn less than a naked insurer but can never be ruined — the professional way to sell insurance.

---

### 3.7 Adjusting a spread that goes against you

A spread's defined risk means you *can* simply let it lose its capped maximum — but often you will want to adjust when the short strike is threatened. The main techniques, in order of aggressiveness:

* **Roll up/down and out.** Close the tested spread and open a new one further from the money (and often in a later expiry) for a fresh credit. This buys room (the new short strike is safer) but usually **locks in a realised loss** on the closed spread and collects less credit.
* **Widen or roll the short strike.** Adjust the strikes within the structure to move the short leg away from the money — trading credit for breathing space.
* **Convert to an iron condor.** If a bear call spread is tested by a rally (but you still expect range-bound trade), *add a bull put spread below*. The new put-side credit adds to your total premium and improves the overall breakeven — but it **adds downside risk** (you now lose if the market falls through the put spread too). This converts a one-sided credit spread into a two-sided iron condor (the subject of the next chapter).

**The rolling trap.** The danger in all adjustment is **rolling a loser indefinitely** — repeatedly closing losing spreads and opening new ones, each time convincing yourself the next roll will work, while the realised losses pile up. Adjustment should have a *limit*: a pre-defined point (a maximum number of rolls, or a total-loss stop) beyond which you simply take the defined loss and walk away. A spread's greatest virtue is that its loss is *capped and known*; the rolling trap throws that virtue away by turning one capped loss into many.

> **Market Note — adjustments are not free, and the best one is often none.** Every roll or conversion crosses the bid-ask spread on multiple legs (Chapter 3) and can lock in a loss. Frequently the best "adjustment" is the one made *before* entry: sizing the position so its capped max loss is survivable, and pre-committing to take that loss if the short strike is breached. Adjust with a plan and a limit — not as a reflex to avoid realising a loss.

---

## 4. Examples (Real-World)

**Example 1 — The naked put, tamed.** A trader wants to sell the 24,400 put but balks at the ₹1.17 lakh margin and open-ended risk. Buying the 24,200 put as a wing turns it into a bull put spread: ₹9,750 margin, ₹9,750 max loss, and a 33% return on capital instead of 7%. Same view, professional structure.

**Example 2 — The skew picks the side.** Two neutral-to-directional traders. One sells a bull put spread (the rich put side); the other an equidistant bear call spread (the cheap call side). The put seller collects meaningfully more credit for the same width — the skew (Chapter 15) rewarding the put side.

**Example 3 — The adjustment that added risk.** A bear call spread on BANKNIFTY is tested by a rally. The trader converts it to an iron condor by adding a bull put spread, collecting extra credit and improving the breakeven — but now carries downside risk too. The adjustment bought room on the upside at the cost of new risk on the downside (the case study, Section 9).

---

## 5. Numerical Examples

Setting: NIFTY 24,600, 10 DTE, lot 65; skew-consistent premiums.

### Numerical Example 1 — Bull put spread, fully worked

Sell 24,400 PE @₹128, buy 24,200 PE @₹78 (width 200):

```
Net credit = 128 − 78 = ₹50 (₹3,250/lot)
Max profit = ₹50; Max loss = 200 − 50 = ₹150 (₹9,750/lot)
Breakeven = 24,400 − 50 = 24,350
Risk-reward = 50/150 = 0.33; Prob. max profit ≈ 1 − 0.32 = 68%
```

A crude "win the full ₹50 or lose the full ₹150" expectancy would give 0.68 × 50 − 0.32 × 150 = −₹14/unit — apparently negative. But this crude figure *overstates* the loss, because most losing outcomes are *partial* (the index finishes between the two strikes, so you lose only part of the ₹150, not all of it). Accounting for the full payoff distribution, the true expectancy is close to zero-to-slightly-positive — the thin variance-risk-premium edge (Chapter 14). The lesson holds either way: the 68% win rate is offset by the 0.33 reward-to-risk, so the edge is small and depends on capturing the VRP and managing the tested side well.

### Numerical Example 2 — Bull call spread (debit)

Buy 24,600 CE @₹212, sell 24,800 CE @₹105 (width 200):

```
Net debit = 212 − 105 = ₹107 (₹6,955/lot)
Max profit = 200 − 107 = ₹93 (₹6,045/lot); Max loss = ₹107 (₹6,955/lot)
Breakeven = 24,600 + 107 = 24,707; Risk-reward = 93/107 = 0.87
```

Compared with a *naked* 24,600 call (₹212 cost, unlimited upside), the spread costs half as much (₹107) and has reduced Theta/Vega drag — but caps the profit at ₹93 above 24,800. A better trade when you expect a *moderate* move to ~24,800, not a runaway rally.

### Numerical Example 3 — Naked vs spread: return on capital

From Table 17.2, on the 24,400 short strike:

```
Naked short put: keep ₹128 × 65 = ₹8,320 on ~₹1,17,000 margin → ROI = 7.1%
Bull put spread: keep ₹50 × 65 = ₹3,250 on ~₹9,750 margin → ROI = 33.3%
```

The spread's return on capital is ~4.7× the naked put's, with a *defined* ₹9,750 max loss instead of an open-ended one. The ₹78 wing was cheap insurance that transformed the trade's economics.

### Numerical Example 4 — Width analysis

From Table 17.3, holding the short 24,400 PE fixed:

```
100-wide: credit ₹28, max loss ₹72, R/R 0.39, ROI 38.9%
200-wide: credit ₹50, max loss ₹150, R/R 0.33, ROI 33.3%
500-wide: credit ₹92, max loss ₹408, R/R 0.23, ROI 22.5%
```

All three have the *same* ~68% probability of profit (same short strike). The narrow spread is most capital-efficient; the wide spread collects the most absolute credit but with the worst reward-to-risk. Width is a risk/credit choice, not a probability choice.

### Numerical Example 5 — The skew favours the bull put

Compare equidistant (400-point OTM) credit spreads:

```
Bull put: sell 24,200 PE @₹78, buy 24,000 PE @₹46 → credit ₹32
Bear call: sell 25,000 CE @₹48, buy 25,200 CE @₹22 → credit ₹26
```

Same width (200) and distance (400 OTM), but the bull put collects ~23% more credit (₹32 vs ₹26) because OTM puts are richer than equidistant OTM calls (the skew, Chapter 15). For a neutral view, selling the put side is the better-compensated choice.

---

## 6. Calculations (the reusable recipes)

**(a) Credit spreads (bull put, bear call)**

```
Max profit = Net credit;   Max loss = Width − Net credit
Breakeven (bull put) = Short strike − Net credit
Breakeven (bear call) = Short strike + Net credit
```

**(b) Debit spreads (bull call, bear put)**

```
Max profit = Width − Net debit;   Max loss = Net debit
Breakeven (bull call) = Lower strike + Net debit
Breakeven (bear put) = Higher strike − Net debit
```

**(c) Risk-reward and probability**

```
Risk-reward = Max profit / Max loss
Prob. max profit (credit spread) ≈ 1 − |Delta of short strike|
```

**(d) Margin and return on capital**

```
Spread margin ≈ Max loss (SEBI rules)
Return on margin = Net credit (or profit) / Margin
```

---

## 7. Practical Insights

* **Reach for a spread before a naked option.** The wing costs some premium and caps the upside, but it defines your risk, slashes your margin, and multiplies your return on capital — the trade professionals make almost every time.
* **Judge income trades by return on margin, not premium.** ₹50 on ₹9,750 (33%) beats ₹128 on ₹1.17 lakh (7%) — and frees capital to run more positions.
* **Keep the two levers separate.** The short strike sets probability and payout; the width sets risk and credit size at constant probability. Design each deliberately.
* **Match the spread's Vega to the IV regime, and favour the put side.** Sell credit spreads in high IV, buy debit spreads in low IV, and prefer bull put spreads (richer, thanks to the skew) over equidistant bear call spreads for neutral-to-bullish views.
* **Adjust with a plan and a limit.** Rolling and converting can buy room, but the rolling trap turns one capped loss into many — pre-commit to a maximum, then take the defined loss.

> **Professional Insight — the credit spread is the retail trader's best friend, misunderstood.** Its high win rate (68%) seduces beginners into treating it as easy income, and its unfavourable reward-to-risk (0.33) then punishes them when one loss erases three wins. The correct frame is the variance risk premium (Chapter 14): the credit spread harvests a small, real edge with defined risk and superb capital efficiency — *if* you size it so the capped loss is survivable and manage the tested side with discipline. It is not a money machine; it is an efficient way to sell insurance without being ruined.

---

## 8. Common Mistakes

* **Preferring the naked option for its bigger premium.** The spread's higher return on capital and defined risk usually make it the better trade; the naked premium is an illusion of superiority.
* **Confusing the two levers.** Believing a narrow *width* raises probability (it doesn't — the short strike sets probability; width sets risk/credit).
* **Treating the 68% win rate as easy money.** The unfavourable 0.33 reward-to-risk means one un-managed loss wipes out several wins; credit spreads are a thin, real edge, not free income.
* **Selling the cheap side of the skew.** Building bear call spreads when an equidistant bull put spread would collect more for the same risk.
* **Mismatching Vega to IV.** Selling credit spreads in cheap IV (thin premium) or buying debit spreads in rich IV (overpaying).
* **The rolling trap.** Rolling a loser indefinitely to avoid realising a loss, converting one capped, survivable loss into a series of them.

---

## 9. Case Study — "Spread Adjustment in Real Time"

**Context.** A trader is neutral-to-mildly-bearish on BANKNIFTY at 52,000 and sells a **bear call spread**: sell the 53,000 CE @₹280, buy the 53,500 CE @₹130, for a net credit of **₹150** (width 500; lot 30). Max profit ₹150 (₹4,500/lot); max loss 500 − 150 = ₹350 (₹10,500/lot); breakeven 53,150. Then, over three days, BANKNIFTY rallies — the wrong way — toward the short 53,000 strike. Figures are illustrative but representative.

**The trade goes against them.** By day 3, BANKNIFTY is at 52,900, just below the short strike. The spread, which the trader sold for ₹150, now costs about **₹280 to buy back** — an unrealised loss of (280 − 150) × 30 = **−₹3,900/lot**. The short call's delta has risen toward 0.45; the position is under pressure. The trader faces a decision, and we walk through the options.

**Adjustment 1 — Roll up and out.** Close the tested 53,000/53,500 spread (pay ₹280, realising the −₹130/unit loss) and open a new 53,500/54,000 bear call spread in the next monthly expiry (BANKNIFTY has no weekly contracts) for a fresh credit of ₹120.

* *Effect:* the new short strike (53,500) sits above the current 52,900, restoring room. But the trader has **locked in −₹130/unit** on the old spread and collected only ₹120 on the new — so the position is now behind, and needs the new spread to profit just to recover. *Buys room, at a realised loss.*

**Adjustment 2 — Convert to an iron condor.** Instead of rolling, *keep* the bear call spread and *add* a bull put spread below: sell the 51,500 PE @₹120, buy the 51,000 PE @₹60, for an extra credit of ₹60.

* *Effect:* total credit rises from ₹150 to **₹210**, and the added put-side premium *improves the overall breakeven* on the call side (the extra credit cushions the tested call spread). Max profit is now ₹210 if BANKNIFTY finishes between 51,500 and 53,000. But the position now **also loses if BANKNIFTY falls** through the put spread — the trader has added downside risk to solve an upside problem. *Adds credit and room, at the cost of new risk on the other side.*

**How it resolves.** Suppose BANKNIFTY stalls at 52,900 and drifts back to 52,400 by expiry. Outcomes:

* **Un-adjusted bear call spread:** 52,400 < 53,000, so it expires worthless — the trader keeps the full ₹150. (The panic was unnecessary; the original position was fine.)
* **Rolled-up spread:** the trader realised −₹130 on the roll, then the new 53,500 spread expired worthless (+₹120) — net −₹10, *worse* than doing nothing.
* **Iron condor:** both spreads expire worthless — the trader keeps ₹210, *better* than doing nothing — but only because the market did not fall; had BANKNIFTY dropped below 51,500, the added put spread would have lost.

**The analysis.** This is the honest lesson of spread adjustment: **the "best" adjustment is only known in hindsight.** Rolling up locked a loss that turned out to be unnecessary (the market reversed). Converting to a condor collected more, but only because the downside risk it added never materialised — a different path would have punished it. The un-adjusted spread, sized so its ₹10,500 max loss was survivable, was fine all along. Adjustments are not magic; they trade one risk for another, cost money to execute, and can make things worse. They are justified when your *view has genuinely changed* or your *risk limit is breached* — not as a reflex to avoid the discomfort of a losing mark.

**The lesson.** A vertical spread's defining virtue is its *capped, known loss* (here ₹10,500/lot). The disciplined trader sizes the position so that capped loss is acceptable, sets a pre-defined point at which they will simply take it, and adjusts only with a clear rationale and a hard limit — never falling into the rolling trap of endlessly deferring a loss the structure was designed to bound in the first place.

*(Takeaway: adjust a spread only with a changed view or a breached limit — sized correctly, its greatest strength is that you can let the capped loss happen rather than trade your way into a bigger one.)*

---

## 10. Chapter Summary

* A **vertical spread** pairs a long and short option of the same type and expiry at different strikes; the far leg is insurance that **defines the risk, cuts the margin, and raises the return on capital**.
* **Debit spreads** (bull call, bear put) you pay for — cheaper than a naked option with capped upside; **credit spreads** (bull put, bear call) you collect — high probability, defined risk, modest reward-to-risk.
* **The math:** credit spread max profit = credit, max loss = width − credit; debit spread max profit = width − debit, max loss = debit; probability of max profit ≈ 1 − |short-strike delta|.
* **Naked vs spread:** the wing turns an open-ended, ₹1.17 lakh-margin naked put into an ₹9,750-margin, ₹9,750-max-loss spread with ~5× the return on capital (33% vs 7%) — the case for spreads.
* **Two separate levers:** the *short strike* sets probability and payout; the *width* sets risk and credit at constant probability.
* **Entry:** sell credit spreads in high IV, buy debit spreads in low IV, and favour the richer **put side** (the skew) for neutral-to-bullish views.
* A high win rate (68%) is offset by an unfavourable reward-to-risk (0.33) — a thin, real edge (the VRP), not free money.
* **Adjust with a plan and a limit** (roll, widen, convert to iron condor), avoiding the **rolling trap**; the spread's virtue is a capped loss you can afford to take.

---

## 11. Key Takeaways

* **Reach for a spread before a naked option** — defined risk, a fraction of the margin, and a far higher return on capital.
* **Judge income trades by return on margin, not premium** (33% on ₹9,750 beats 7% on ₹1.17 lakh).
* **Design the short strike (probability) and the width (risk/credit) as separate decisions**, and favour the put side thanks to the skew.
* **Respect the thin edge and adjust with discipline** — the 68% win rate hides a 0.33 reward-to-risk, so size for the capped loss and never roll a loser indefinitely.

---

## 12. Practice Questions

**Q1 (Construction).** Name the two legs of a bull put spread and a bear call spread, and state the market view of each.

**Q2 (Credit spread math).** Sell the 24,500 PE @₹160, buy the 24,300 PE @₹100. Compute the net credit, max profit, max loss, breakeven, and risk-reward.

**Q3 (Debit spread math).** Buy the 24,600 CE @₹212, sell the 24,900 CE @₹72 (width 300). Compute the net debit, max profit, max loss, and breakeven.

**Q4 (Probability).** A bull put spread's short strike has a delta of −0.28. Estimate the probability of max profit.

**Q5 (Naked vs spread).** A naked short put collects ₹150 on ₹1,40,000 margin; the equivalent bull put spread collects ₹55 on ₹14,500 margin. Compute each return on margin and state which is more capital-efficient.

**Q6 (Width).** Holding the short strike fixed, you widen a bull put spread from 100 to 300 points. What happens to the credit, the max loss, the reward-to-risk, and the probability of profit?

**Q7 (Skew).** Why does a bull put spread usually collect more credit than an equidistant bear call spread?

**Q8 (Entry timing).** IV Rank is 85 and you are neutral-to-bullish. Which spread do you use, and why?

**Q9 (Win rate trap).** A credit spread wins 70% of the time but has a reward-to-risk of 0.30. Compute the crude expectancy (max profit ₹40, max loss ₹133) and comment.

**Q10 (Adjustment judgement).** Your bull put spread is tested as the market falls toward the short strike. Give one valid reason to adjust and one situation in which you should simply take the defined loss.

---

## 13. Detailed Solutions

**A1.** **Bull put spread:** sell a higher-strike put, buy a lower-strike put — **bullish/neutral** (profits if the index stays above the short strike). **Bear call spread:** sell a lower-strike call, buy a higher-strike call — **bearish/neutral** (profits if the index stays below the short strike).

**A2.** Net credit = 160 − 100 = **₹60**. Max profit = **₹60**. Max loss = width − credit = 200 − 60 = **₹140**. Breakeven = 24,500 − 60 = **24,440**. Risk-reward = 60/140 = **0.43**.

**A3.** Net debit = 212 − 72 = **₹140**. Max profit = width − debit = 300 − 140 = **₹160**. Max loss = **₹140**. Breakeven = 24,600 + 140 = **24,740**.

**A4.** Probability of max profit ≈ 1 − |Delta of short strike| = 1 − 0.28 = **0.72 (72%)**.

**A5.** Naked: 150/1,40,000 = **10.7%**. Spread: 55/14,500 = **37.9%**. The **spread is far more capital-efficient** (~3.5× the return on margin), with defined risk as a bonus.

**A6.** The **credit increases** (wider spread sells the same short but buys a cheaper, further wing), the **max loss increases** (width grows faster than credit), the **reward-to-risk worsens**, and the **probability of profit is unchanged** (it depends only on the short strike, which did not move).

**A7.** Because of the **volatility skew** (Chapter 15): OTM puts trade at higher implied volatility than equidistant OTM calls, so the short put in a bull put spread is *richer* than the short call in an equidistant bear call spread — collecting more credit for the same width and distance.

**A8.** A **bull put spread (credit)**. IV Rank 85 means options are rich, favouring *selling* premium (short Vega benefits from IV mean-reverting down); the neutral-to-bullish view points to the put side; and the skew makes the put side better-compensated. All three factors point to a bull put spread.

**A9.** Crude expectancy = 0.70 × 40 − 0.30 × 133 = 28 − 39.9 = **−₹11.9/unit** — *negative* on this crude basis. It shows that a high win rate with a poor reward-to-risk is not automatically profitable; the edge depends on the true payoff distribution (many losses are partial, not maximal) and the variance risk premium, and one un-managed maximal loss can erase many small wins. High win rate ≠ high edge.

**A10.** **Valid reason to adjust:** your *view has genuinely changed* (e.g., a breakdown that invalidates your bullish thesis), or your *risk limit is breached* (the position now exceeds the loss you pre-committed to) — then rolling down/out or reducing size is justified. **Simply take the loss:** if nothing has changed except the market moving against a still-valid, correctly-sized position, and adjusting would only be to avoid the discomfort of a losing mark — take the capped, survivable loss the spread was designed to bound, rather than risk the rolling trap.

---

## 14. Mini Glossary

* **Vertical spread** — a two-leg position of the same option type and expiry at different strikes; defines risk and reduces margin. → this chapter.
* **Debit spread** — a spread you pay a net premium for (bull call, bear put); capped cost and capped profit. → this chapter.
* **Credit spread** — a spread you collect a net premium for (bull put, bear call); high probability, defined risk. → this chapter.
* **Bull call spread** — buy lower call, sell higher call; bullish debit spread. → this chapter.
* **Bear put spread** — buy higher put, sell lower put; bearish debit spread. → this chapter.
* **Bull put spread** — sell higher put, buy lower put; bullish/neutral credit spread. → this chapter.
* **Bear call spread** — sell lower call, buy higher call; bearish/neutral credit spread. → this chapter.
* **Spread width** — the distance between the two strikes; sets risk and credit at constant probability. → this chapter.
* **Short-strike distance** — how far the short strike sits from the money; sets probability and payout. → this chapter.
* **Probability of max profit** — for a credit spread, ≈ 1 − |delta of the short strike|. → this chapter.
* **Return on margin** — profit ÷ margin (= max loss for spreads); the true measure of an income trade's efficiency. → this chapter.
* **Rolling trap** — repeatedly rolling a losing spread to avoid realising a loss, turning one capped loss into many. → this chapter.
* **Iron condor (preview)** — a bull put spread plus a bear call spread; a two-sided defined-risk structure. → this chapter.

---

<!-- End of Chapter 17 (Rev 2, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65, BANKNIFTY lot 35→30 (NSE Jan-2026). Per-unit spread economics (Table 17.1 credits/debits/max profit-loss in points, breakevens, R/R, probabilities) lot-independent — unchanged. Lot-scaled rupee/margin figures recomputed: naked margin ~₹1.17 lakh, spread margin=max loss ₹9,750, bull-put credit ₹3,250/lot, naked credit ₹8,320/lot, naked max loss ~₹15.9 lakh, bull-call debit ₹6,955/lot (max profit ₹6,045); ROI 7.1% and 33.3% PRESERVED (both numerator and denominator scale by lot). Width analysis (Table 17.3) lot-independent — unchanged. Skew: bull put ₹32 vs bear call ₹26 at 400 OTM (per-unit, unchanged). Case study BANKNIFTY lot 30 (53,000/53,500 @₹150): max profit ₹4,500/lot, max loss ₹10,500/lot, unrealised loss −₹3,900/lot; roll corrected "next weekly"→"next monthly" (BANKNIFTY monthly-only since Nov 2024). Q5/A5 self-contained — unchanged. No transaction costs (gross P&L) → Apr-2026 STT change not applicable. Margin=max loss (SEBI). Prob max profit ≈ 1−|short delta|. IV = implied volatility. -->
