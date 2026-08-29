<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 11, 17, 18. Target length ~7,500 words. Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Uses standard strategy template. Per-unit premiums/debits/credits/breakevens/Greeks lot-independent — unchanged; "/lot" conversions rescaled to lot 65 (ratio debit ₹4,875/lot, max profit ₹14,625/lot; backspread credit ₹520/lot, max loss ₹18,980/lot, crash payoff ₹21,970/lot); naked-leg margin ~₹1.3→~₹1.13 lakh (65/75 scaling). NIFTY only (no BANKNIFTY); gross P&L → Apr-2026 STT not applicable. Ratio call spread (buy 24,500 CE ₹285, sell 2× 24,800 CE ₹105): debit ₹75, max profit ₹225 at 24,800, BE 24,575/25,025, UNLIMITED above 25,025; Greeks Δ−0.17, Γ−0.00077, Θ+10.7, ν−16.7. Put backspread (sell 24,300 PE ₹100, buy 2× 24,000 PE ₹46): credit ₹8, max loss ₹292 at 24,000, lower BE 23,708; Greeks Δ+0.03, Γ+, Θ−0.3, ν+0.8. Case study election backspread (per unit): rally +₹8, crash 22,600 +₹1,108, valley 24,100 −₹192. IV = implied volatility. -->

# Chapter 20 — Ratio Spreads and Backspreads: Asymmetric Payoffs

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Construct ratio spreads (selling more options than you buy).
2. Construct backspreads (buying more options than you sell).
3. Understand the risk profiles — ratio spreads are short-volatility, backspreads are long-volatility.
4. Apply both in the Indian index market for event-based and directional-volatility trades.
5. Understand the margin implications and manage the tail risk of the extra leg.

Every spread so far has paired *equal* numbers of long and short options. The ratio spread and its mirror, the backspread, break that symmetry — buying and selling *unequal* quantities. That single change creates the most asymmetric payoffs in the book: a structure that can be entered for zero cost, profit from a moderate move, and either explode into unlimited risk or pay off spectacularly on a crash.

---

## 2. Introduction

Imbalance is the theme of this chapter. Take a vertical spread and add an extra option to one side, and you transform a bounded, symmetric position into a lopsided one with a dramatically different character. Sell *more* than you buy — a **ratio spread** — and you collect extra premium (often reducing the cost to zero), gain positive Theta, but expose yourself to a naked leg and its unlimited risk. Buy *more* than you sell — a **backspread** — and you create cheap, sometimes free, protection that loses a little in a moderate move but pays off enormously on a large one.

These are the professional's tools for two specific jobs. The **ratio spread** is a short-volatility, income structure for a trader who expects a *moderate* move to a target and calm thereafter — it monetises the volatility skew by selling the extra rich option. The **backspread** is a long-volatility, tail-protection structure — most valuably the **put backspread**, which the Indian market uses as *cheap crash insurance* before events: it costs little (sometimes nothing), does almost nothing in a normal market, and turns a crash into a windfall.

Both are advanced because their asymmetry demands respect: the ratio spread's extra short leg carries open-ended risk and heavy margin, and the backspread has a "valley of loss" in the moderate-move zone. This chapter builds both, contrasts their Greeks (short-vol vs long-vol), compares them to the vertical and the butterfly (the ratio spread is a butterfly with a wing removed — which is where the unlimited risk comes from), and shows the put backspread as an election-eve crash hedge. Setting: **NIFTY at 24,600, lot 65**, with skew-consistent premiums from Part V.

---

## 3. Core Concepts

### 3.1 The asymmetric family — ratio spreads and backspreads

The ratio/backspread family is the flagship of this chapter.

**What is it?** A **ratio spread** buys and sells *unequal* quantities of options of the same type and expiry — classically a 1×2, buying 1 and selling 2 (more short than long). A **backspread** is the inverse — buying 2 and selling 1 (more long than short). The extra leg is what creates the asymmetry.

**Why does it exist?** To build payoffs that vertical spreads cannot. The ratio spread's extra short leg **collects additional premium** (often making the position zero-cost or a credit) and adds positive Theta — ideal for monetising a moderate-move view or a rich skew. The backspread's extra long leg **creates convex, explosive upside** on a large move for little or no cost — ideal for cheap tail protection.

**Why should a trader care?** Because these structures do jobs nothing else does. Nothing else lets you enter a directional-ish trade for *zero cost* with positive Theta (the ratio spread), and nothing else gives you *free-or-cheap crash insurance that pays off huge* on a real move (the backspread). But both come with a sting — the ratio spread's naked leg (unlimited risk, heavy margin) and the backspread's moderate-move loss zone — that you must understand before using them.

**Intuitive explanation.** A ratio spread is a **vertical spread that sold one option too many** — the extra sold option pays for the spread but leaves you exposed like a naked seller beyond a point. A backspread is a **vertical spread that bought one option too many** — the extra bought option is a lottery ticket, financed by the one you sold, that pays off if the market runs.

**Numerical feel.** A 1×2 ratio call spread (buy 24,500 CE, sell 2× 24,800 CE) can be entered for a small ₹75 debit, peaks at ₹225 profit at 24,800 — but carries *unlimited* loss above 25,025. A put backspread (sell 24,300 PE, buy 2× 24,000 PE) is entered for a small *credit* of ₹8, loses at most ₹292 in a moderate fall, but earns ₹1,000+ on a crash.

**Professional interpretation.** Professionals use ratio spreads to *sell the skew* (the extra short is a rich, high-IV OTM option) and backspreads to *own convexity cheaply* (the extra long is cheap tail protection). Both are volatility trades first: ratio spreads are short vol (sell in high IV), backspreads are long vol (buy in low IV).

**Common mistake.** Entering a ratio spread for the "free" premium without registering the naked leg's unlimited risk and large margin — the extra short is a naked option in disguise.

**Practical takeaway.** **Ratio spreads sell an extra option (short vol, positive Theta, naked-leg risk) for a moderate-move/high-IV view; backspreads buy an extra option (long vol, cheap convexity) for tail protection in low IV — the imbalance is the strategy, and its risk.**

---

### 3.2 The ratio call spread — short vol with an unlimited tail

**Setup.** Buy 1 lower-strike call, sell 2 higher-strike calls (1×2). On our surface: **buy 1× 24,500 CE @₹285, sell 2× 24,800 CE @₹105** — net debit ₹285 − ₹210 = **₹75**.

**View.** Neutral-to-moderately-bullish: you expect the index to drift *up to the short strike (24,800)* and stall — not to run past it. High IV is ideal (the extra short is richly priced).

**Payoff and risk/reward.**

```
Below 24,500: all calls expire worthless → loss = debit ₹75 (max downside loss, flat)
Lower breakeven = 24,575 (long call recovers the ₹75 debit)
Max profit = ₹225 at 24,800 (long call intrinsic 300 − debit 75)
Upper breakeven = 25,025 (24,800 + max profit 225)
Above 25,025: UNLIMITED loss (net short one naked call)
```

The payoff is a **hump peaking at the short strike (24,800)**, with a small capped loss on the downside and — critically — an **unlimited loss beyond the upper breakeven** (25,025), because the *second* short call is naked (only one is covered by the long).

**Greeks (at entry).** Net Delta ≈ 0.61 − 2(0.39) = **−0.17**; net Gamma **−0.00077** (short); net Theta **+₹10.7/day** (positive); net Vega **−₹16.7/vol point** (negative — short volatility). It is a **short-volatility, positive-Theta** structure that profits from calm and time, hurt by a volatility spike.

> **Beginner Alert — the ratio spread's current Delta lies about its payoff.** At entry the net Delta is *negative* (−0.17), because the two short calls' delta (0.78) exceeds the one long call's (0.61) *before expiry*. So a fast up-move early can *hurt*. Yet the expiry payoff *peaks* at the higher short strike (24,800), which is *above* the current price — the structure profits from a *gradual* drift up as the two short calls decay. This gap between the current Greeks and the expiry payoff is the defining subtlety of ratio spreads: they are **held-to-expiry, time-decay structures**, and their live delta can point the "wrong" way. Judge them by the expiry payoff and the Theta, not the entry delta.

**When to use.** In **high IV** (the extra short call is richly priced, so you collect more, and short Vega benefits as IV falls), with a view that the market drifts to the short strike and stalls. **Never** hold it through an explosive up-move — the naked leg is the danger.

---

### 3.3 The ratio put spread — the downside mirror

**Setup.** Buy 1 higher-strike put, sell 2 lower-strike puts. A neutral-to-moderately-bearish structure that profits from a moderate *down*-move to the short strike and stalls there.

Its profile mirrors the ratio call spread: a hump peaking at the lower short strike, positive Theta, negative Vega (short vol), a small capped loss if the market rises, and — the danger — **significant loss if the market crashes** below the short strikes (the extra short put). Because a market can only fall to zero, the ratio put spread's downside is "significant" rather than strictly "unlimited," but it is large and arrives exactly when everything else in a portfolio is also falling. Use in high IV with a moderate-bearish view; never hold through a crash.

---

### 3.4 The backspreads — long vol and cheap protection

The **backspread** inverts the ratio: buy *more* than you sell, creating a long-volatility, convex payoff.

**Put backspread (the important one).** Sell 1 higher-strike put, buy 2 lower-strike puts. On our surface: **sell 1× 24,300 PE @₹100, buy 2× 24,000 PE @₹46 (₹92)** — net *credit* ₹100 − ₹92 = **₹8** (near zero-cost; you are *paid* to hold crash insurance).

```
Above 24,300: all puts expire worthless → keep the ₹8 credit (small profit)
Between 23,708 and 24,300: loss zone (net short one put) — the "valley"
Max loss = ₹292 at 24,000 (short put ITM 300 − credit 8)
Lower breakeven = 23,708 (24,000 − max loss 292)
Below 23,708: PROFIT, growing steeply (net long one put) — the crash payoff
```

The put backspread is **cheap crash insurance**: it costs almost nothing (here a small credit), earns a tiny profit if the market rises, loses at most ₹292 in a *moderate* fall (the valley between the strikes), and pays off **enormously on a crash** below 23,708 — where the two long puts overwhelm the one short. This is the Indian market's classic **pre-event tail hedge** (Section 9).

**Greeks (at entry).** Net Delta ≈ +0.03 (near-neutral); Gamma slightly **positive** (long); Theta ≈ **−₹0.3/day** (slightly negative); Vega ≈ **+₹0.8/vol point** (positive — long volatility). These are near-zero at entry but **intensify sharply as the market falls**: as NIFTY drops toward and through 24,000, the two long puts' delta, gamma, and vega all surge, the position becomes strongly net short delta and long gamma/vega — the convexity that makes it explode on a crash. A backspread's Greeks are *dynamic*; its long-vol character emerges with movement.

**Call backspread.** Sell 1 lower call, buy 2 higher calls — the upside mirror: cheap, small loss in a moderate up-move, huge profit on an *explosive* up-move. Less used in India (crashes, not melt-ups, are the feared tail), but the same structure for a bullish tail bet.

> **Market Note — the put backspread is India's cheap crash hedge.** Before elections, budgets, and global-risk events, Indian traders and desks use put backspreads to own downside convexity for little or no cost. Unlike a straight long put (which bleeds premium), a put backspread can be *financed to zero* by the short put, so you carry crash protection with almost no carrying cost — paying only in the "valley" if a *moderate* decline lands there. It is the structure of choice when you fear a crash but refuse to pay full price for insurance.

---

### 3.5 The Greeks contrast — short vol versus long vol

The family splits cleanly by volatility exposure, and this is the key to using them:

| | Ratio spread (sell more) | Backspread (buy more) |
| --- | --- | --- |
| Net options | Net short 1 | Net long 1 |
| Theta | **Positive** (collect decay) | **Negative** (pay decay) |
| Vega | **Negative** (short vol) | **Positive** (long vol) |
| Gamma | Negative (near the peak) | Positive (grows on a move) |
| Profits from | a *moderate* move + calm | a *large* move + rising vol |
| Tail risk | the naked extra short (large/unlimited) | none — the extra long *is* the payoff |
| Enter when IV is… | **high** (sell rich premium) | **low** (buy cheap convexity) |

The rule follows directly: **sell ratio spreads in high IV** (you collect the rich extra short, and short Vega profits as IV mean-reverts down) and **buy backspreads in low IV** (cheap long options, and long Vega profits as IV rises). They are volatility trades before they are directional trades.

---

### 3.6 Ratio vs vertical vs butterfly — the missing wing

Comparing the ratio call spread to its relatives reveals *where its unlimited risk comes from*.

**Table 20.1 — Ratio spread vs vertical spread vs butterfly**

| | Bull call spread (vertical) | 1×2 ratio call spread | Long call butterfly |
| --- | --- | --- | --- |
| Legs | +1 lower, −1 higher | +1 lower, −2 higher | +1 lower, −2 middle, +1 upper |
| Risk | Defined both ways | Defined down, **unlimited up** | Defined both ways |
| Payoff | Rising plateau | Hump (peak at short strike) | Tent (peak at middle) |
| Theta | ~Neutral | Positive (short vol) | Positive (short vol) |
| Vega | ~Neutral | Negative (short vol) | Negative (short vol) |
| Cost | Debit | Small debit/credit | Debit |

The crucial insight: **a 1×2 ratio call spread is a long call butterfly with the upper wing removed.** The butterfly's upper long call (+1 upper) is the "insurance" that caps the risk; take it away and you are left with a naked extra short — which is exactly why the ratio spread has *unlimited* upside risk while the butterfly is bounded. Put the wing back (buy an upper call) and the ratio spread becomes a butterfly, capping the tail. This relationship is not academic: **if a ratio spread's naked-leg risk frightens you, add the missing wing to convert it into a defined-risk butterfly.**

---

### 3.7 Margin and tail-risk management — the naked leg

The ratio spread's asymmetry shows up harshly in margin. Because only *one* of the two short calls is covered by the long, the *other* short is effectively **naked** — and SEBI margins it as such:

```
Ratio spread margin ≈ spread margin (small, on the covered pair) + naked-option margin (~₹1.13 lakh on the extra short)
```

So a 1×2 ratio call spread entered for a ₹75 debit still requires **~₹1.13 lakh of margin** for the naked leg — the small debit is *not* the capital commitment. This is the first thing to check: the ratio spread ties up naked-option capital despite its modest cost.

The **backspread**, by contrast, is *net long* options, so it requires little margin — you simply pay (or receive) the small net premium, with no naked-leg margin. This asymmetry in *margin* mirrors the asymmetry in *risk*: the ratio spread's naked short demands both large margin and vigilant tail management; the backspread's extra long needs neither.

**Tail-risk management for ratio spreads:** because the naked leg has open-ended risk, (a) *size small*, (b) set a hard stop or a plan to buy the missing wing if the market approaches the short strike, and (c) never hold through the event that could cause an explosive move. The extra short is a naked option — treat it with the same fear (Chapters 10, 16).

---

### 3.8 When to use them, and the ladder

**When to use — a summary:**

* **Ratio spread:** high IV, a view that the market drifts *moderately* toward the short strike and stalls, and the capital/discipline to manage the naked leg. It monetises the rich skew (the extra short is a high-IV OTM option) and collects Theta.
* **Backspread (put):** low IV, before a feared event, when you want *cheap or free crash insurance* with convex payoff — accepting the small "valley" loss if only a moderate decline lands.

**The Christmas tree / ladder.** A **ladder** (or "Christmas tree") extends the idea across three strikes — e.g., buy 1, sell 1, sell 1 at successively higher strikes (1×1×1) — spreading the short legs to shift the peak and the risk zone. It is a refinement of the ratio spread for shaping the payoff, with the same naked-leg caution (the further-out short adds risk). A tool for experienced traders sculpting a specific view.

---

## 4. Examples (Real-World)

**Example 1 — Selling the skew with a ratio spread.** In high IV, a trader mildly bullish on NIFTY sells a 1×2 ratio call spread, monetising the richly-priced OTM calls (the extra short) and collecting Theta. The market drifts up to the short strike and stalls; the trade earns its max profit. The risk — an explosive rally — did not materialise, but the trader had sized small and planned to buy the wing if it did.

**Example 2 — Free crash insurance.** Before an event, a trader who fears a crash but hates paying for puts sells a put backspread — entering for a small credit. The market rises; the puts expire worthless; the trader keeps the credit. The insurance cost nothing and, this time, was not needed — the ideal outcome for a hedge.

**Example 3 — The insurance that paid.** The same put backspread, held into a different event that *crashed* the market 8%: the two long puts exploded in value, delivering a windfall that dwarfed the tiny entry cost (the case study, Section 9). Cheap convexity, richly rewarded.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, 10 DTE, lot 65; skew-consistent premiums.

### Numerical Example 1 — Ratio call spread, fully worked

Buy 1× 24,500 CE @₹285, sell 2× 24,800 CE @₹105:

```
Net debit = 285 − (2 × 105) = 285 − 210 = ₹75 (₹4,875/lot)
Max downside loss = ₹75 (below 24,500, flat)
Lower breakeven = 24,500 + 75 = 24,575
Max profit = 300 (long call intrinsic at 24,800) − 75 debit = ₹225 (₹14,625/lot), at 24,800
Upper breakeven = 24,800 + 225 = 25,025
Above 25,025: UNLIMITED loss (naked extra short call)
Greeks: Δ −0.17, Γ −0.00077, Θ +₹10.7/day, ν −₹16.7/vol point (short vol)
```

A hump peaking at ₹225 at 24,800, tiny capped loss below, and open-ended risk above 25,025.

### Numerical Example 2 — Put backspread as a tail hedge

Sell 1× 24,300 PE @₹100, buy 2× 24,000 PE @₹46:

```
Net credit = 100 − (2 × 46) = 100 − 92 = ₹8 (₹520/lot) — you are PAID to hold it
Above 24,300: keep ₹8 (small profit)
Max loss = 300 (short put intrinsic at 24,000) − 8 credit = ₹292 (₹18,980/lot), at 24,000
Lower breakeven = 24,000 − 292 = 23,708
Below 23,708: PROFIT, growing 1× per point (net long one put)
Greeks: Δ +0.03, Γ slightly +, Θ −₹0.3/day, ν +₹0.8/vol point (long vol)
```

If NIFTY drops 5% to 23,370 at expiry: long 2× 24,000 PE intrinsic = 2 × (24,000 − 23,370) = 2 × 630 = 1,260; short 24,300 PE intrinsic = 24,300 − 23,370 = 930; net = 1,260 − 930 = 330, plus ₹8 credit = **+₹338/unit (₹21,970/lot)** — the crash payoff, for an entry cost of nothing.

### Numerical Example 3 — Ratio spread vs butterfly (the missing wing)

Compare the ratio call spread (buy 24,500, sell 2× 24,800) with the butterfly that adds the missing wing (buy 24,500, sell 2× 24,800, **buy 25,100 CE @₹32**):

```
Ratio call spread: debit ₹75, max profit ₹225 at 24,800, UNLIMITED loss above 25,025
Butterfly (+ 25,100 wing): debit 75 + 32 = ₹107, max profit 300 − 107 = ₹193 at 24,800,
    max loss capped at ₹107 (both directions) — no unlimited risk
```

Adding the ₹32 upper wing converts the ratio spread into a defined-risk butterfly: it costs ₹32 more and lowers the peak profit by ₹32, but it **eliminates the unlimited tail**. This is the ratio spread's relationship to the butterfly made concrete — the wing is the price of survivability.

### Numerical Example 4 — The margin reality

```
Ratio call spread (buy 24,500, sell 2× 24,800): debit only ₹4,875, but margin ≈ ₹1.13 lakh (naked extra short)
Put backspread (sell 24,300, buy 2× 24,000): credit ₹520, margin ≈ negligible (net long options)
```

The ratio spread's tiny debit hides a ₹1.13 lakh capital commitment (the naked leg); the backspread, being net long, ties up almost nothing. Judge these structures by their *margin and tail risk*, not their entry cost.

---

## 6. Calculations (the reusable recipes)

**(a) 1×2 ratio call spread (buy 1 lower, sell 2 higher)**

```
Net cost = Lower premium − 2 × Higher premium (debit if positive, credit if negative)
Max profit = (Short strike − Long strike) − Net debit, at the short strike
Lower breakeven = Long strike + Net debit
Upper breakeven = Short strike + Max profit
Above the upper breakeven: unlimited loss (naked extra short)
```

**(b) Put backspread (sell 1 higher, buy 2 lower)**

```
Net credit = Higher-put premium − 2 × Lower-put premium (credit if positive)
Max loss = (Higher strike − Lower strike) − Net credit, at the lower strike
Lower breakeven = Lower strike − Max loss
Below the lower breakeven: profit grows 1× per point (net long one put)
```

**(c) Greeks (signs)**

```
Ratio spread (net short 1): Theta +, Vega −, Gamma − (short vol)
Backspread (net long 1):   Theta −, Vega +, Gamma + (long vol)
```

**(d) Margin**

```
Ratio spread margin ≈ spread margin + naked-option margin on the uncovered short (~₹1.13 lakh)
Backspread margin ≈ negligible (net long options; pay/receive the small net premium)
```

---

## 7. Practical Insights

* **These are volatility trades first.** Sell ratio spreads in high IV (rich extra short, short Vega), buy backspreads in low IV (cheap extra long, long Vega). Get the IV regime right before the direction.
* **The put backspread is cheap-to-free crash insurance.** It is the Indian market's pre-event tail hedge — convex downside payoff for little or no carrying cost, paying only the small "valley" loss if a moderate decline lands.
* **Respect the ratio spread's naked leg.** Its tiny debit hides ~₹1.13 lakh of margin and unlimited risk; size small, plan to add the missing wing near the short strike, and never hold through an event that could cause an explosive move.
* **Judge ratio spreads by the expiry payoff, not the entry Delta.** Their live delta can point the "wrong" way; they are held-to-expiry, time-decay structures whose hump materialises as the shorts decay.
* **The missing wing is always available.** Any ratio spread becomes a defined-risk butterfly by buying the wing you left out — cheap insurance against the tail whenever the naked-leg risk frightens you.

> **Professional Insight — asymmetry is the point, and the price.** Professionals reach for these structures precisely *because* they are asymmetric: the ratio spread monetises the skew and time with a cheap entry, the backspread owns convexity for nothing. But the asymmetry that gives them their edge is the same asymmetry that makes them dangerous — the extra leg is either a naked risk (ratio) or a payoff you paid almost nothing for (backspread). The discipline is to use ratio spreads only where you can manage the naked leg, and backspreads only where the cheap convexity is worth the "valley" — and to always know which side of the asymmetry you are on.

---

## 8. Common Mistakes

* **Entering a ratio spread for the "free" premium, ignoring the naked leg.** The extra short is a naked option with unlimited risk and ~₹1.13 lakh margin — the small debit is not the risk.
* **Holding a ratio spread through an explosive move.** The naked leg's unlimited loss is realised exactly on the big move you hoped would not come; exit or add the wing first.
* **Judging a ratio spread by its entry Delta.** The live delta can point away from the payoff peak; these are held-to-expiry structures, judged by the expiry hump and the Theta.
* **Buying a straight long put when a backspread would be cheaper.** A put backspread can be financed to zero, carrying crash protection with almost no cost — versus a long put that bleeds full premium.
* **Forgetting the backspread's "valley."** The put backspread *loses* in a moderate decline (between the strikes); it protects against a *crash*, not a mild drift down.
* **Using a ratio spread in low IV or a backspread in high IV.** Backwards on volatility: the ratio (short vol) wants high IV; the backspread (long vol) wants low IV.

---

## 9. Case Study — "The Backspread Before the Election"

**Context.** Ahead of a major general election, a trader is worried about a crash if the result surprises, but implied volatility is only *moderately* elevated and buying outright puts feels expensive. They use a **put backspread** as cheap crash insurance: sell 1× 24,300 PE @₹100, buy 2× 24,000 PE @₹46, for a small net **credit of ₹8** — carrying downside convexity for essentially no cost. NIFTY is at 24,600. Figures are illustrative but representative; per unit (lot 65).

**The structure's promise.** The backspread does almost nothing in a normal market, loses a little if a *moderate* decline lands in the valley, and pays off enormously on a *crash* — the exact shape a tail-fearing trader wants before a binary event.

**Scenario A — the market rallies (result reassures).** The election delivers a market-friendly outcome; NIFTY jumps 3% to ~25,300. All three puts expire worthless. The trader **keeps the ₹8 credit** — a tiny profit. The insurance was not needed and cost *nothing* (indeed, paid ₹8). This is the ideal hedge outcome: free protection that expired unused.

```
NIFTY 25,300: all puts OTM → P&L = +₹8/unit (+₹520/lot)
```

**Scenario B — the market crashes (result shocks).** The result stuns the market; NIFTY falls 8% to ~22,600. The two long 24,000 puts explode:

```
Long 2× 24,000 PE: 2 × (24,000 − 22,600) = 2 × 1,400 = ₹2,800
Short 1× 24,300 PE: (24,300 − 22,600) = −₹1,700
Net = 2,800 − 1,700 = ₹1,100, plus ₹8 credit = +₹1,108/unit (+₹72,020/lot)
```

The backspread turned a crash into a **₹1,108/unit windfall** — for an entry that cost nothing. This is the payoff the cheap convexity was for: a small credit at entry, a massive gain on the tail event.

**Scenario C — the moderate decline (the valley).** Suppose instead the result is mildly negative and NIFTY drifts down only to 24,100 — landing in the backspread's loss zone:

```
Short 24,300 PE ITM 200 → −₹200; long 24,000 PE OTM → ₹0
Net = −200 + 8 credit = −₹192/unit (−₹12,480/lot) — near the max loss of ₹292 at 24,000
```

Here the backspread *loses*: a moderate decline into the valley (between 24,300 and 23,708) is the one outcome it does not like. The protection is against a *crash*, not a mild slide.

**The analysis.** The put backspread did exactly what it was designed to do across all three outcomes. It cost *nothing* to hold (a small credit), paid a *tiny* profit if the market rose (Scenario A), delivered a *huge* payoff on the crash it was insuring against (Scenario B), and lost only in the *moderate-decline valley* (Scenario C) — the acceptable price of free crash insurance. The key was the *shape*: the trader was not predicting the election result, but positioning so that the feared tail (a crash) was cheaply covered while a rally or calm cost nothing. The one weakness — the valley — is the trade-off for the zero cost; a straight long put would have covered the moderate decline too, but at the price of bleeding premium in the (more likely) no-crash outcomes.

**The lesson.** A put backspread is the tool for owning downside convexity *cheaply* before a binary event: it makes the crash you fear pay off big, costs almost nothing if the crash does not come, and asks only that you accept a small loss if a *moderate* decline lands in the valley. Use it when you fear a tail and refuse to pay full price for insurance — and remember it protects against the crash, not the drift.

*(Takeaway: the put backspread buys cheap or free crash convexity — huge payoff on a real crash, near-zero cost if the market rises — at the price of a small loss in the moderate-decline "valley"; it is the pre-event tail hedge for a trader who won't pay full price for puts.)*

---

## 10. Chapter Summary

* **Ratio spreads** sell more than they buy (e.g., 1×2); **backspreads** buy more than they sell — the *imbalance* creates the asymmetric payoff.
* A **1×2 ratio call spread** (buy 1 lower, sell 2 higher) is **short volatility** (positive Theta, negative Vega), peaks at the short strike, has a small capped downside loss, and **unlimited risk** above the upper breakeven from the naked extra short.
* Its **live Delta can point the "wrong" way** (negative at entry) while the expiry payoff peaks *above* — judge it by the expiry hump and Theta, as a held-to-expiry structure.
* A **put backspread** (sell 1 higher, buy 2 lower) is **long volatility** (negative Theta, positive Vega), often entered for a small credit, with a small profit if the market rises, a "valley" loss in a moderate decline, and a **huge payoff on a crash** — India's classic cheap pre-event tail hedge.
* The family splits by **Vega:** ratio spreads are short vol (use in **high IV**); backspreads are long vol (use in **low IV**).
* A **1×2 ratio spread is a butterfly with the missing wing** — adding the wing converts it to a defined-risk butterfly, eliminating the unlimited tail.
* **Margin:** the ratio spread's naked leg demands ~₹1.13 lakh (its tiny debit hides the risk); the backspread, net long, needs almost nothing.
* The **election backspread** case shows the shape: +₹8 on a rally, +₹1,108 on a crash, −₹192 in the moderate-decline valley — cheap convexity, richly rewarded on the tail.

---

## 11. Key Takeaways

* **Trade the imbalance for what it is** — ratio spreads sell an extra option (short vol, naked-leg risk) for a moderate-move/high-IV view; backspreads buy an extra option (long vol, cheap convexity) for tail protection in low IV.
* **The put backspread is cheap-to-free crash insurance** — huge payoff on a crash, near-zero cost otherwise, a small "valley" loss on a moderate decline; the pre-event tail hedge.
* **Respect the ratio spread's naked leg** — ~₹1.13 lakh margin, unlimited risk; size small, add the missing wing near the short strike, and never hold through an explosive move.
* **Judge these by margin, tail risk, and the expiry payoff, not the entry cost** — the imbalance is both the edge and the danger.

---

## 12. Practice Questions

**Q1 (Construction).** Describe the legs of a 1×2 ratio call spread and a put backspread, and state which is short-vol and which is long-vol.

**Q2 (Ratio call spread math).** Buy 1× 24,600 CE @₹212, sell 2× 24,900 CE @₹72. Compute the net cost, the max profit and where it occurs, and the upper breakeven.

**Q3 (Ratio risk).** For the Q2 structure, what happens above the upper breakeven, and why?

**Q4 (Backspread math).** Sell 1× 24,400 PE @₹128, buy 2× 24,100 PE @₹60. Compute the net credit/debit, the max loss and where it occurs, and the lower breakeven.

**Q5 (Backspread payoff).** For the Q4 backspread, compute the P&L if NIFTY falls to 23,500 at expiry.

**Q6 (Greeks).** State the sign of Theta and Vega for (a) a ratio spread and (b) a backspread, and what each implies about the ideal IV regime to enter.

**Q7 (Missing wing).** How do you convert a 1×2 ratio call spread into a defined-risk butterfly, and what is the trade-off?

**Q8 (Margin).** A ratio call spread is entered for a ₹60 debit. Why is the margin requirement far larger than ₹60 × 65?

**Q9 (Delta nuance).** Why can a ratio call spread have a negative net Delta at entry even though its payoff peaks above the current price?

**Q10 (Judgement).** A trader fears a crash before an event but says buying puts is "too expensive." What structure fits, and what is the one outcome it handles poorly?

---

## 13. Detailed Solutions

**A1.** A **1×2 ratio call spread**: buy 1 lower-strike call, sell 2 higher-strike calls — **short volatility** (positive Theta, negative Vega). A **put backspread**: sell 1 higher-strike put, buy 2 lower-strike puts — **long volatility** (negative Theta, positive Vega).

**A2.** Net cost = 212 − (2 × 72) = 212 − 144 = **₹68 debit**. Max profit = (24,900 − 24,600) − 68 = 300 − 68 = **₹232, at 24,900**. Upper breakeven = 24,900 + 232 = **25,132**.

**A3.** Above 25,132 the position loses money, **growing without limit**, because the *second* short 24,900 call is naked (only one is covered by the long 24,600 call) — beyond the long's coverage, you are effectively short one naked call with unlimited upside risk.

**A4.** Net credit = 128 − (2 × 60) = 128 − 120 = **₹8 credit**. Max loss = (24,400 − 24,100) − 8 = 300 − 8 = **₹292, at 24,100**. Lower breakeven = 24,100 − 292 = **23,808**.

**A5.** At 23,500: long 2× 24,100 PE = 2 × (24,100 − 23,500) = 2 × 600 = 1,200; short 24,400 PE = (24,400 − 23,500) = −900; net = 1,200 − 900 = 300, plus ₹8 credit = **+₹308/unit (+₹20,020/lot)** — the crash payoff.

**A6.** (a) A **ratio spread** is **Theta-positive, Vega-negative** (short vol) — enter in **high IV** (rich extra short, and short Vega gains as IV falls). (b) A **backspread** is **Theta-negative, Vega-positive** (long vol) — enter in **low IV** (cheap extra long, and long Vega gains as IV rises).

**A7.** Add the **missing upper wing** — buy a further OTM call (e.g., buy 1× 25,100 CE) so the structure becomes buy 1 lower / sell 2 middle / buy 1 upper (a long call butterfly). The trade-off: it **costs a bit more** (the wing's premium) and **lowers the peak profit** by that amount, but it **eliminates the unlimited upside risk** (caps the loss).

**A8.** Because only one of the two short calls is covered by the long call; the **second short call is naked**, and SEBI margins it as a naked option (~₹1.13 lakh). The ₹60 debit is merely the net premium paid — the capital commitment is dominated by the naked-leg margin, not the debit.

**A9.** Because *before expiry*, the **two short calls' combined delta can exceed the one long call's delta** (e.g., 2 × 0.39 = 0.78 > 0.61), making the net delta negative. The expiry *payoff* peaks at the higher short strike because, held to expiry, the short calls decay to zero while the long call's intrinsic value grows — a time-decay effect the live delta does not capture. Judge the ratio spread by its expiry payoff, not its entry delta.

**A10.** A **put backspread** — cheap or free crash insurance (convex downside payoff for a small credit). The outcome it handles **poorly is a *moderate* decline** that lands in the "valley" between the strikes: there it takes its max loss, whereas it profits hugely on a crash and costs almost nothing on a rally. It protects against a crash, not a mild slide.

---

## 14. Mini Glossary

* **Ratio spread** — a spread with unequal legs, selling more than buying (e.g., 1×2); short volatility, with a naked extra leg. → this chapter.
* **Backspread** — a spread buying more than selling (e.g., 1×2 the other way); long volatility, with a convex payoff. → this chapter.
* **1×2 ratio call spread** — buy 1 lower call, sell 2 higher calls; hump payoff, unlimited upside risk. → this chapter.
* **Ratio put spread** — buy 1 higher put, sell 2 lower puts; hump payoff, large downside risk. → this chapter.
* **Put backspread** — sell 1 higher put, buy 2 lower puts; cheap crash insurance with a "valley" loss zone. → this chapter.
* **Call backspread** — sell 1 lower call, buy 2 higher calls; a bullish tail bet. → this chapter.
* **The valley** — the moderate-move loss zone of a backspread, between the short and long strikes. → this chapter.
* **The missing wing** — the leg whose absence gives a ratio spread its unlimited risk; adding it makes a butterfly. → this chapter.
* **Naked leg** — the uncovered short option in a ratio spread; the source of its open-ended risk and heavy margin. → this chapter.
* **Christmas tree / ladder** — a multi-strike extension of the ratio idea (e.g., 1×1×1) that reshapes the payoff. → this chapter.

---

<!-- End of Chapter 20 (Rev 2, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026) — per-unit premiums/debits/credits/breakevens/Greeks unchanged; "/lot" conversions rescaled: ratio debit ₹4,875/lot, max profit ₹14,625/lot; backspread credit ₹520/lot, max loss ₹18,980/lot; NE2 crash payoff ₹21,970/lot; case Scenario A +₹520/lot, B +₹72,020/lot, C −₹12,480/lot; A5 +₹20,020/lot. Naked-leg margin ~₹1.3→~₹1.13 lakh (65/75). Ratio call spread (buy 24,500 CE ₹285, sell 2× 24,800 CE ₹105): debit ₹75, max profit ₹225 at 24,800, BE 24,575/25,025, unlimited above 25,025; Greeks Δ−0.17, Γ−0.00077, Θ+10.7, ν−16.7 (short vol). Put backspread (sell 24,300 PE ₹100, buy 2× 24,000 PE ₹46): credit ₹8, max loss ₹292 at 24,000, lower BE 23,708; Greeks Δ+0.03, Γ+, Θ−0.3, ν+0.8 (long vol). Ratio-vs-butterfly: add 25,100 wing (₹32) caps risk (butterfly debit ₹107, max profit ₹193). Case study election (per unit): rally +₹8, crash 22,600 +₹1,108, valley 24,100 −₹192. NIFTY only; gross P&L → Apr-2026 STT not applicable. IV = implied volatility. -->
