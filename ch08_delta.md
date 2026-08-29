<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapter 6. Target length ~8,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision); one futures lot = 65 Deltas. Opens Part III (The Greeks). Deltas computed from the Ch6 BSM setup (S=24,600, r=6.5%, T=10/365, σ=13% flat) — lot-independent, unchanged. All Position-Delta figures recomputed at lot 65. No transaction costs, so the Apr-2026 STT change does not affect this chapter. Risk-neutral-probability caveat included (Edition 2). Parity relation stated correctly as Call Δ − Put Δ = 1. Delta quoted as change in premium per 1-point index move; ranges 0..1 (calls), −1..0 (puts). IV = implied volatility. -->

# Chapter 8 — Delta: Direction and Probability

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Define Delta and interpret it in three complementary ways.
2. Use Delta to size positions and measure your true directional exposure.
3. Relate Delta to moneyness and to the (risk-neutral) probability of finishing in the money.
4. Apply Delta-neutral hedging — and understand why "neutral" is not "safe."
5. Recognise how Delta itself changes as the index moves (a first look at Gamma).

Welcome to Part III. The Greeks are the instruments on your cockpit dashboard, and **Delta is the first and most-used dial.** Everything in Chapter 5 was qualitative — *which way* a factor pushes. From here on we put numbers on it.

---

## 2. Introduction

A trader is short one lot of an out-of-the-money NIFTY 24,800 call, collected for ₹60. The option's Delta is 0.39, so the trader reasons: "If NIFTY rises 100 points, I lose about ₹39 a unit — manageable." Comfortable with that, they walk away from the screen.

NIFTY does not rise 100 points. It rallies 500, to 25,100. The trader returns to find the call now worth about ₹343 — a loss of roughly ₹283 a unit, ₹18,395 on the lot. Far more than "₹39 per 100 points" implied. What went wrong?

Nothing, except that the trader treated Delta as a **constant**. It is not. As NIFTY climbed, the option went from out-of-the-money to deep in-the-money, and its Delta climbed with it — from 0.39 to 0.74. The average Delta over the move was far higher than the 0.39 they started with, so the loss compounded. Delta told the truth for the *first* point; it changed for every point after.

This chapter builds Delta from the ground up: what it measures, the three ways professionals read it, how to use it to size and hedge a position, and — crucially — its two most dangerous subtleties. First, Delta is only *approximately* a probability, and a *risk-neutral* one at that. Second, Delta is not fixed; it moves as the index moves (that movement is Gamma, the next chapter). Master Delta and you can measure exactly how much market risk you are carrying at any instant. We work from the Chapter 6 setup throughout: **NIFTY at 24,600, lot size 65**, a ~10-day expiry.

---

## 3. Core Concepts

### 3.1 What Delta is

Delta is the flagship of this chapter, so we take it in full.

**What is it?** **Delta (Δ)** is the rate of change of an option's premium for a **1-point move in the underlying** (the index, strictly its future). If a call has a Delta of 0.54, its premium rises by about ₹0.54 (per unit) when the index rises one point, and falls by about ₹0.54 when it drops one point.

**Why does it exist?** Delta is the first derivative of the BSM price with respect to the underlying (Chapter 6) — mathematically, `Δ_call = N(d₁)`. It exists because the *whole point* of an option is to give exposure to the underlying, and Delta measures exactly *how much* exposure you have right now. It is the bridge between "the index moved X" and "my premium moved Y."

**Why should a trader care?** Because Delta is your **directional risk, quantified**. Without it, "I'm long some calls" is a vague statement; with it, "my position has +72 Deltas" tells you precisely that you will gain or lose ₹72 for every point NIFTY moves. You cannot size a trade, hedge it, or know your true exposure without Delta.

**Intuitive explanation.** Delta is the option's "**speed** relative to the index." A Delta of 1 means the option keeps pace with the index one-for-one (like holding the future itself). A Delta of 0 means the option barely reacts. A Delta of 0.5 means it moves at half the index's speed. As the option's moneyness changes, so does its speed.

**Numerical feel.** For the ATM NIFTY 24,600 call with Delta 0.54: a 20-point rise in NIFTY lifts the premium by about 0.54 × 20 = ₹10.8 per unit, or 10.8 × 65 = ₹702 on a lot. A deep-OTM 25,400 call (Delta 0.08) would gain only about 0.08 × 20 = ₹1.6 per unit on the same move — it barely reacts.

**Mathematical form.**

```
Δ_call = N(d₁)          (ranges 0 to 1)
Δ_put  = N(d₁) − 1      (ranges −1 to 0)
```

where `N(d₁)` comes from BSM (Chapter 6). Calls have positive Delta (they gain when the index rises); puts have negative Delta (they gain when it falls).

**Professional interpretation.** A desk never thinks "I own three calls." It thinks "I am carrying +150 Deltas" — the number that says how the book will move with the index. Positions are built, hedged, and unwound in Delta terms, not in "number of options."

**Common mistake.** Treating Delta as fixed. As the introduction showed, Delta changes as the index moves; a position that looks small in Delta today can become large after a move (the Gamma effect, Section 3.8).

**Practical takeaway.** **Delta is your directional exposure, in numbers — read it before every trade to know exactly how much you will make or lose per point of index movement.** "Long some calls" is not a position; "+72 Deltas" is.

---

### 3.2 The three interpretations of Delta

Delta wears three hats, and professionals switch between them fluidly.

**1. Delta as a hedge ratio.** Delta is literally `N(d₁)` — the number of units of the underlying you must hold to replicate (or hedge) the option (Chapter 6). A call with Delta 0.54 behaves, for a small move, like holding 0.54 units of the index. To hedge one such call, you short 0.54 units of the future. This is the origin of the term "Delta hedging."

**2. Delta as directional exposure.** Multiply Delta by quantity and lot size and you get **Position Delta** — your effective holding in index units (Section 3.4). This is the interpretation you use to size trades and estimate P&L.

**3. Delta as an approximate probability of finishing in the money.** The magnitude of Delta roughly equals the option's chance of expiring in the money: an ATM option (Delta ≈ 0.5) is a coin-flip; a 0.20-Delta OTM option has roughly a 20% chance of finishing in the money. This is the handiest interpretation for strike selection — **but it is a *risk-neutral* approximation, and it must be used with care (Section 3.7).**

---

### 3.3 Delta by moneyness

Delta is not a single number; it runs across the whole chain with moneyness. Table 8.1 gives call and put Deltas for 15 NIFTY strikes, computed from BSM (NIFTY 24,600, ~10 DTE, σ = 13%).

**Table 8.1 — Delta by strike (NIFTY 24,600; illustrative, from BSM)**

| Strike | Call Δ | Put Δ | | Strike | Call Δ | Put Δ |
| ---: | ---: | ---: | --- | ---: | ---: | ---: |
| 24,000 | 0.89 | −0.11 | | 24,800 | 0.39 | −0.61 |
| 24,100 | 0.85 | −0.15 | | 24,900 | 0.32 | −0.68 |
| 24,200 | 0.80 | −0.20 | | 25,000 | 0.26 | −0.74 |
| 24,300 | 0.75 | −0.25 | | 25,100 | 0.20 | −0.80 |
| 24,400 | 0.68 | −0.32 | | 25,200 | 0.15 | −0.85 |
| 24,500 | 0.61 | −0.39 | | 25,300 | 0.11 | −0.89 |
| **24,600 (ATM)** | **0.54** | **−0.46** | | 25,400 | 0.08 | −0.92 |
| 24,700 | 0.46 | −0.54 | | | | |

The pattern is the essential map of Delta:

* **Deep ITM → Delta approaches ±1.** The 24,000 call (deep ITM) has Delta 0.89, closing on 1 — it behaves almost like the future (recall from Chapter 4 that deep-ITM options are nearly all intrinsic value).
* **ATM → Delta ≈ ±0.5.** The 24,600 call sits near a coin-flip.
* **Deep OTM → Delta approaches 0.** The 25,400 call (Delta 0.08) barely responds to the index.

**Why the ATM call Delta is 0.54, not exactly 0.50.** Two effects nudge it above one-half. First, the *forward* trades above the spot (positive basis/carry, Chapter 2), so an option struck at the spot is slightly in the money relative to the forward the market actually prices against. Second, the `σ²/2` drift term inside `d₁` adds a small positive push. Both lift the spot-ATM call Delta a touch above 0.50. (Struck at the *forward*, the ATM call Delta would sit right around 0.50.)

---

### 3.4 Position Delta and delta-equivalent exposure

A single option's Delta is only the start. Real positions have several legs, and you must aggregate them.

**Position Delta** sums the Delta of every leg, signed for long/short, scaled by quantity and lot size:

```
Position Delta = Σ (Δᵢ × Qᵢ × Lot size)          (Qᵢ negative for short legs)
```

The result is your **delta-equivalent holding in index units** — the number of units of the index you are effectively long (positive) or short (negative). Two uses follow:

* **Estimate P&L for a move:** `P&L ≈ Position Delta × (points moved)`.
* **Measure true exposure in rupees:** `Delta-equivalent notional = Position Delta × index level`.

**Worked example.** Hold **2 lots long of the 24,500 call** (Δ 0.61) and **1 lot short of the 25,000 call** (Δ 0.26):

```
Position Delta = (2 × 0.61 × 65) + (−1 × 0.26 × 65)
              = 79.3 − 16.9 = +62.4 units
```

You are effectively **long 62.4 units of NIFTY**. For a 100-point rise, P&L ≈ 62.4 × 100 = **₹6,240**. Your true directional exposure is 62.4 × 24,600 ≈ **₹15.35 lakh** of long index — a number far more meaningful than "I own two calls and I'm short one."

**Delta-equivalent, another way.** A 5-lot NIFTY call position with Delta 0.45 carries 5 × 65 × 0.45 = **146.25 units** of NIFTY exposure — as if you were long ~146 units of the index outright.

> **Beginner Alert — "How many lots" is not "how much exposure."** Two traders can each hold "5 lots of calls" and carry wildly different risk: one in deep-ITM calls (Delta ~0.9 → ~293 units of exposure), the other in far-OTM calls (Delta ~0.1 → ~33 units). Always convert lots to **Position Delta** to know your real directional risk. The lot count tells you almost nothing on its own.

---

### 3.5 Delta-neutral hedging — and why "neutral" is not "safe"

If Position Delta is your directional risk, then **zeroing it out removes that risk** — for an instant. This is **Delta-neutral hedging**: you offset your Position Delta with the underlying (index futures).

A NIFTY future has a Delta of 1 per unit, so **one futures lot carries 65 Deltas**. To neutralise a Position Delta of +X units, you short X ÷ 65 lots of futures.

**Worked example.** A position of **2 lots long 24,400 call (Δ 0.68)** and **2 lots short 24,800 call (Δ 0.39)** (deltas from Table 8.1):

```
Position Delta = (2 × 0.68 × 65) + (−2 × 0.39 × 65) = 88.4 − 50.7 = +37.7 units
Futures to hedge = 37.7 ÷ 65 = 0.58 lots
```

To be Delta-neutral you would short **about 0.58 of a lot** of futures — which you cannot do, because contracts trade in whole lots. This **lot-granularity problem** means small positions often cannot be made *exactly* neutral; you round to the nearest lot and carry a small residual Delta.

**Why neutral is not safe.** Here is the trap that ends careers. A Delta-neutral position has *zero directional exposure right now* — but Delta changes as the index moves (Section 3.8). The moment the index moves, your carefully neutralised position develops a Delta again, and if you are short options, that new Delta works *against* you (you get longer as the market falls, shorter as it rises). "Delta-neutral" is a snapshot, not a shield. Keeping it neutral requires constant re-hedging, and the cost and risk of that re-hedging is the subject of the next chapter (Gamma).

> **Professional Insight — Delta-neutral is a starting line, not a finish line.** Market makers run Delta-neutral books not because they are safe, but because they have *removed the bet they don't want* (direction) to isolate the one they do (volatility and time). They then re-hedge continuously as Delta drifts. A retail trader who sets a position "Delta-neutral" and walks away has not removed risk — they have merely hidden it until the next move reveals it.

---

### 3.6 Put–call parity for Delta

Calls and puts at the same strike have Deltas locked together by parity. The correct relation is:

```
Δ_call − Δ_put = 1          (equivalently, Δ_call = Δ_put + 1)
```

Check it on Table 8.1 at the 24,600 strike: 0.54 − (−0.46) = 1.00. At 25,000: 0.26 − (−0.74) = 1.00. Every row obeys it.

This is not a coincidence — it follows directly from the synthetic future (Chapter 4): long a call and short the same-strike put reproduces a long future, which has a Delta of exactly 1. So the call's Delta minus the put's Delta must equal 1. A quick corollary: a call's Delta plus the *magnitude* of the same-strike put's Delta always equals 1 (0.54 + 0.46 = 1.00).

---

### 3.7 Delta as probability — and the risk-neutral caveat

The "Delta ≈ probability of finishing ITM" interpretation is enormously useful for strike selection — a 0.30-Delta OTM option has roughly a 30% chance of expiring in the money, so you can pick strikes by the odds you want. But it comes with two warnings you must internalise, because misusing it is a genuine professional error.

> **Professional Insight — "Delta ≈ probability of ITM" is a *risk-neutral* statement (Edition 2 emphasis).** Two subtleties:
>
> **First, `N(d₂)` is the cleaner probability, not Delta.** Delta is `N(d₁)`, which is slightly *larger* than `N(d₂)` (since d₁ > d₂). For the ATM 24,600 call, Delta = 0.54 but the model's actual ITM probability `N(d₂)` ≈ 0.53; for the 25,000 call, Delta = 0.26 versus `N(d₂)` ≈ 0.25. So Delta modestly *overstates* the chance of finishing ITM. Use `N(d₂)` when you want the model's real probability figure.
>
> **Second — and more important — both are *risk-neutral* probabilities, not real-world ones.** They are computed under the pricing measure where everything drifts at the risk-free rate (Chapter 6), which is a device for arbitrage-free pricing, *not a forecast of what will actually happen*. Because of the equity-index risk premium and the demand for downside protection (the skew), the **real-world** probability of a put finishing ITM is typically *lower* than its Delta suggests. In plain terms: the market prices puts as if crashes are somewhat more likely than history says they are, so a "0.30-Delta put" does not mean a genuine 30% real-world chance of that fall.
>
> **The rule:** use Delta as a *hedging and sizing tool first*, and only as a *rough* probability heuristic second — never as a true likelihood of an outcome.

This caveat is not academic pedantry. Traders who sell "0.15-Delta" options believing they have "an 85% real-world win rate" are systematically over-optimistic, because the real-world odds and the risk-neutral Delta are not the same number.

---

### 3.8 Delta changes as the index moves — meet Gamma

The introduction's disaster came from forgetting that **Delta is not constant**. As the index moves, an option's moneyness changes, and its Delta changes with it. Table 8.2 tracks the 24,800 call's Delta as NIFTY rises.

**Table 8.2 — Delta of the 24,800 call as NIFTY rises (illustrative, from BSM)**

| NIFTY spot | 24,800 call Delta | State of the option |
| ---: | ---: | --- |
| 24,600 | 0.39 | OTM |
| 24,700 | 0.46 | Near ATM |
| 24,800 | 0.54 | ATM |
| 24,900 | 0.61 | Slightly ITM |
| 25,100 | 0.74 | ITM |

Over a 500-point rally, the call's Delta nearly doubled, from 0.39 to 0.74. A trader short this option got *shorter and shorter* as the market rose — the loss accelerated with every point. This rate of change of Delta is the next Greek, **Gamma**, and it is why a position that looks small today can become large after a move. For now, hold the essential lesson: **Delta is a snapshot, valid for the current index level; re-read it after any meaningful move.**

---

## 4. Examples (Real-World)

**Example 1 — Sizing by Delta, not by lots.** A trader wants "the same directional punch" from two different strikes. To match the exposure of 2 lots of a 0.60-Delta call (2 × 65 × 0.60 = 78 units), they would need 78 ÷ (65 × 0.30) = 4 lots of a 0.30-Delta call. Thinking in Deltas — not lots — is the only way to size consistently.

**Example 2 — The hedge that had to be repeated.** A market maker sells a straddle and hedges it Delta-neutral with futures at the open. By noon NIFTY has drifted 150 points, the position has picked up Delta, and they must re-hedge. Delta-neutral was true at 9:15 and false by 11:00 — the hedge is a process, not a one-time act.

**Example 3 — Reading the odds off the chain.** Choosing a strike to sell, a trader picks the 0.20-Delta call, reasoning it has roughly a 20% (risk-neutral) chance of finishing ITM — an ~80% chance of expiring worthless in their favour. Useful for framing, but they remember (Section 3.7) that the *real-world* odds are not exactly 80%, and size the trade for the loss, not the win.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65, Deltas from Table 8.1.

### Numerical Example 1 — Position Delta and P&L

Long 2 lots of the 24,500 call (Δ 0.61), short 1 lot of the 25,000 call (Δ 0.26):

```
Position Delta = (2 × 0.61 × 65) − (1 × 0.26 × 65) = 79.3 − 16.9 = +62.4 units
P&L for +100 points ≈ 62.4 × 100 = ₹6,240
P&L for −100 points ≈ 62.4 × (−100) = −₹6,240
```

You are net **long 62.4 Deltas** — a bullish position that gains ₹62.4 per point up and loses ₹62.4 per point down.

### Numerical Example 2 — Delta-equivalent exposure

Your Position Delta of +62.4 units, at NIFTY 24,600, is a directional exposure of:

```
Delta-equivalent notional = 62.4 × 24,600 = ₹15,35,040 ≈ ₹15.35 lakh long
```

Separately, a 5-lot call position with Delta 0.45 carries 5 × 65 × 0.45 = **146.25 units** of exposure (≈ ₹36 lakh at 24,600) — the number that tells you your true risk, not the "5 lots."

### Numerical Example 3 — Making a position Delta-neutral

Position: long 2 lots 24,400 call (Δ 0.68), short 2 lots 24,800 call (Δ 0.39) (deltas from Table 8.1):

```
Position Delta = (2 × 0.68 × 65) − (2 × 0.39 × 65) = 88.4 − 50.7 = +37.7 units
P&L for +100 points ≈ 37.7 × 100 = ₹3,770
Futures needed to neutralise = 37.7 ÷ 65 = 0.58 lots  → not tradable (whole lots only)
```

You would need to short about 0.58 of a futures lot to be exactly neutral. In practice you round to 0 or 1 lot and carry a residual Delta of about ±37.7 — the lot-granularity problem.

### Numerical Example 4 — Delta drifts with the market (Gamma preview)

From Table 8.2, the 24,800 call's Delta over a 500-point rally (24,600 → 25,100):

```
Delta at start (24,600) = 0.39
Delta at end   (25,100) = 0.74
Average Delta over the move ≈ (0.39 + 0.74) / 2 ≈ 0.57
Premium change ≈ 0.57 × 500 ≈ ₹283 per unit  (not 0.39 × 500 = ₹195)
```

Using the *starting* Delta underestimates the move by about ₹88 per unit — the Gamma effect quantified.

### Numerical Example 5 — Delta versus the model's ITM probability

For the ATM 24,600 call: Delta (N(d₁)) = 0.54, but the model's ITM probability N(d₂) ≈ 0.53. For the 25,000 call: Delta = 0.26 versus N(d₂) ≈ 0.25. Delta modestly overstates the (risk-neutral) chance of finishing ITM, and both figures are risk-neutral, not real-world (Section 3.7).

---

## 6. Calculations (the reusable recipes)

**(a) Delta from BSM**

```
Δ_call = N(d₁)          (0 to 1)
Δ_put  = N(d₁) − 1      (−1 to 0)
```

**(b) Position Delta (in index units)**

```
Position Delta = Σ (Δᵢ × Qᵢ × Lot size)     (Qᵢ negative for short legs)
```

**(c) P&L and exposure from Position Delta**

```
P&L for a move ≈ Position Delta × (points moved)
Delta-equivalent notional = Position Delta × index level
```

**(d) Delta-neutral hedge with futures**

```
Futures lots to hedge = Position Delta ÷ Lot size     (one futures lot = Lot size Deltas)
```

**(e) Put–call parity for Delta**

```
Δ_call − Δ_put = 1
```

---

## 7. Practical Insights

* **Think in Deltas, not in lots.** "Five lots" is meaningless without the Delta; "+169 units of exposure" is your actual risk. Convert every position to Position Delta before you judge its size.
* **Delta is a live number, not a label.** Read it before entering, and re-read it after any real move — a position's Delta today is not its Delta tomorrow.
* **Delta-neutral is a snapshot.** It removes direction only for an instant; the market's next move re-creates directional risk, especially for sellers. If you neutralise, plan to re-hedge.
* **Use Delta for odds cautiously.** It is a fine *rough* guide to the chance of finishing ITM for strike selection, but it is a risk-neutral, slightly overstated figure — never a real-world win rate.
* **Mind lot granularity.** Small positions often cannot be made exactly neutral; know your residual Delta and whether you can live with it.

---

## 8. Common Mistakes

* **Treating Delta as constant.** The introduction's short-call loss came from assuming Delta 0.39 would hold; it climbed to 0.74. Always account for Delta drift (Gamma).
* **Sizing by lot count instead of Delta.** Two "5-lot" positions can carry 10× different exposure depending on the strikes' Deltas.
* **Believing Delta-neutral means safe.** It removes directional risk only momentarily; unhedged, it returns with the next move — against you if you are short options.
* **Reading Delta as a real-world probability.** A 0.15-Delta option is *not* an 85% real-world win — that is a risk-neutral, slightly inflated figure that ignores the risk premium and skew.
* **Ignoring the sign on short legs.** A short call has positive Delta *magnitude* but contributes *negatively* to a long-biased book; getting the sign wrong inverts your risk read.

---

## 9. Case Study — "Delta Surprise"

**Context.** A trader sells one lot of the OTM **NIFTY 24,800 call** with the index at 24,600, collecting a premium of about **₹60** (₹3,900 for the lot). They check the Delta — **0.39** — and reason that even a decent 100-point rally would cost only about 0.39 × 100 = ₹39 a unit, a manageable ₹2,535 on the lot. Comfortable, they leave the position unattended. Figures are illustrative but representative.

**What happened.** Over the next two sessions NIFTY rallied hard, **500 points to 25,100**. The trader expected a bad-but-bounded loss based on the 0.39 Delta. Instead:

* As NIFTY rose, the 24,800 call moved from OTM toward deep ITM, and its **Delta climbed from 0.39 to 0.74** (Table 8.2).
* The **average Delta** over the move was about 0.57, not 0.39.
* The premium rose from ~₹60 to about **₹343** — a loss of roughly **₹283 a unit, ₹18,395 on the lot.**

The naive estimate (starting Delta × move = 0.39 × 500 = ₹195 a unit) understated the loss by about **₹88 a unit** — the extra damage done because Delta itself grew as the market moved against the short position.

**The analysis.** The trader made two linked errors. First, they treated Delta as a **constant**, when it rises for a call as the index rallies — so a short call gets *shorter* and loses faster the further the market runs (negative Gamma, next chapter). Second, they sized the trade on the *comfortable starting Delta* rather than on a **stress scenario** — what happens if the move is 500 points, not 100? Had they asked "what is my loss if NIFTY jumps 500?", the accelerating Delta would have been obvious before the trade, not after.

**The lesson.** Delta is the truth for the *current* index level and the *next* point — no further. For any position, especially a short option, estimate the loss under a *large* move using the fact that Delta will move against you, and size for that stress, not for the calm starting number.

*(Takeaway: a short option's Delta is a moving target that accelerates against you — never size a trade on the assumption that today's Delta will hold through a big move.)*

---

## 10. Chapter Summary

* **Delta (Δ)** is the change in an option's premium per 1-point move in the underlying; `Δ_call = N(d₁)` (0 to 1), `Δ_put = N(d₁) − 1` (−1 to 0).
* Delta has **three interpretations**: hedge ratio, directional exposure, and (risk-neutral) probability of finishing ITM.
* Delta runs with **moneyness**: deep ITM ≈ ±1, ATM ≈ ±0.5, deep OTM ≈ ±0; the spot-ATM call sits slightly above 0.50 because of the forward basis and drift.
* **Position Delta** = Σ(Δ × Q × lot size) is your delta-equivalent index units; P&L ≈ Position Delta × points moved, and notional exposure = Position Delta × index level.
* **Delta-neutral** hedging offsets Position Delta with futures (one lot = lot-size Deltas), but it is a *snapshot*, not safety — the next move re-creates directional risk, and lot granularity prevents exact neutrality for small positions.
* Parity ties the Greeks: **Δ_call − Δ_put = 1** at any strike.
* "Delta ≈ probability of ITM" is a **risk-neutral, slightly overstated** figure (N(d₂) is cleaner); the **real-world** probability differs — use Delta to hedge and size, only loosely to gauge odds.
* **Delta is not constant** — it changes as the index moves (Gamma); a short option's Delta accelerates against you in a big move.

---

## 11. Key Takeaways

* **Measure every position in Position Delta** — your exposure in index units — not in lot count.
* **Re-read Delta after every meaningful move;** it is a live snapshot, not a fixed label.
* **Treat Delta-neutral as a starting line** that must be re-hedged, not a safe resting state.
* **Use Delta for odds only loosely** — it is a risk-neutral, inflated proxy, never a real-world win rate — and always size a short position for a *large* adverse move, because Delta accelerates against you.

---

## 12. Practice Questions

**Q1 (Definition).** Define Delta in one sentence, and give the range of Delta for calls and for puts.

**Q2 (Interpretations).** Name Delta's three interpretations and state which one you would use to (a) hedge an option, (b) estimate P&L for a 50-point move, (c) pick a strike by its rough odds.

**Q3 (Moneyness).** From Table 8.1, give the Delta of a deep-ITM call, an ATM call, and a deep-OTM call, and explain the pattern in one sentence.

**Q4 (Position Delta).** You are long 3 lots of the 24,600 call (Δ 0.54) and short 2 lots of the 24,900 call (Δ 0.32). Compute your Position Delta (lot 65).

**Q5 (P&L and exposure).** For the position in Q4, estimate the P&L if NIFTY rises 80 points, and compute your delta-equivalent notional exposure at 24,600.

**Q6 (Delta-neutral).** For the Q4 position, how many NIFTY futures lots (and which direction) would move you closest to Delta-neutral?

**Q7 (Parity).** A 24,700 call has Delta 0.46. Using parity, find the Delta of the 24,700 put.

**Q8 (Probability caveat).** A trader sells a 0.12-Delta call and says, "I have an 88% chance of winning." Give two reasons this statement is not quite right.

**Q9 (Delta drift).** A short OTM call has Delta 0.35 with NIFTY at 24,600. NIFTY rallies 400 points and the Delta rises to 0.68. Why does the loss exceed a naive "0.35 × 400" estimate?

**Q10 (Judgement).** A trader sets a position Delta-neutral at 9:15 AM and leaves for the day, believing it is now risk-free. Explain why this is a mistake.

---

## 13. Detailed Solutions

**A1.** Delta is the change in an option's premium for a 1-point move in the underlying. Range: **0 to 1 for calls**, **−1 to 0 for puts**.

**A2.** The three interpretations are **hedge ratio**, **directional exposure**, and **(risk-neutral) probability of finishing ITM**. Use (a) the **hedge ratio** to hedge, (b) **directional exposure** (Position Delta) to estimate P&L, (c) the **probability** interpretation to pick a strike by its rough odds.

**A3.** Deep-ITM call ≈ **0.89** (24,000); ATM call ≈ **0.54** (24,600); deep-OTM call ≈ **0.08** (25,400). Delta rises toward 1 as the option goes deeper in the money (it tracks the index more closely) and falls toward 0 as it goes further out (it barely reacts).

**A4.** Position Delta = (3 × 0.54 × 65) − (2 × 0.32 × 65) = 105.3 − 41.6 = **+63.7 units** (net long).

**A5.** P&L ≈ 63.7 × 80 = **₹5,096**. Delta-equivalent notional = 63.7 × 24,600 ≈ **₹15.67 lakh** long.

**A6.** One futures lot = 65 Deltas. To offset +63.7 you **short 1 lot** of NIFTY futures (63.7 ÷ 65 ≈ 0.98 lots, rounded to 1). This leaves a small residual Delta of about 63.7 − 65 = −1.3 units — as close to neutral as whole lots allow.

**A7.** By parity, Δ_put = Δ_call − 1 = 0.46 − 1 = **−0.54**.

**A8.** Two reasons: (i) Delta (N(d₁)) slightly **overstates** the model's ITM probability — the cleaner figure is N(d₂), which is a bit lower — so the "88%" is inflated. (ii) Both are **risk-neutral** probabilities, not real-world ones; the actual real-world chance differs because of the risk premium and skew, so "88% chance of winning" is not a true win rate.

**A9.** Because Delta **rose** from 0.35 to 0.68 as the index climbed — the option went from OTM toward ITM, so the short position got progressively shorter. The *average* Delta over the move (~0.52) was well above the starting 0.35, so the actual loss (~0.52 × 400 = ₹208 a unit) far exceeds the naive 0.35 × 400 = ₹140 estimate. This is the Gamma effect.

**A10.** Delta-neutral removes directional risk only **at that instant**. As soon as the index moves, the position's Delta changes (Gamma), so it is no longer neutral — and for a short-option position the new Delta works against them. Neutrality must be *re-hedged* as the market moves; setting it once and leaving is not risk-free, merely risk-hidden until the next move.

---

## 14. Mini Glossary

* **Delta (Δ)** — the change in an option's premium per 1-point move in the underlying; the option's directional exposure. → this chapter.
* **Hedge ratio** — Delta viewed as the units of underlying needed to replicate or hedge the option. → this chapter.
* **Position Delta** — the sum of leg Deltas × quantity × lot size; your delta-equivalent holding in index units. → this chapter.
* **Delta-equivalent notional** — Position Delta × index level; true directional exposure in rupees. → this chapter.
* **Delta-neutral** — a position with zero net Delta; directionally flat for an instant, requiring re-hedging as the market moves. → this chapter.
* **Delta by moneyness** — deep ITM ≈ ±1, ATM ≈ ±0.5, deep OTM ≈ ±0. → this chapter.
* **N(d₁) / N(d₂)** — the BSM terms giving Delta and the (risk-neutral) ITM probability, respectively. → this chapter.
* **Risk-neutral probability** — the probability used in pricing (all assets drift at the risk-free rate); differs from the real-world probability. → this chapter.
* **Lot granularity** — the constraint that contracts trade in whole lots, preventing exact Delta-neutrality for small positions. → this chapter.
* **Gamma (preview)** — the rate at which Delta itself changes as the underlying moves. → this chapter.

---

<!-- End of Chapter 8 (Rev 2, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026 revision) — one futures lot now 65 Deltas; all Position-Delta figures recomputed (§3.4 worked ex +62.4 units/₹15.35L; 5-lot 0.45Δ = 146.25 units/₹36L; BeginnerAlert ~293/~33 units; §3.5 & NE3 +32.5 units, 0.5 futures lots preserved; NE1 +62.4/₹6,240; NE2 ₹15.35L; Ex1 78 units→4 lots preserved; Delta Surprise ₹60→₹3,900/lot, loss ₹18,395/lot; Q4/A4 +63.7 units; A5 ₹5,096/₹15.67L; A6 65 Deltas/lot, residual −1.3). Delta values from Ch6 BSM setup (ATM 24,600 Δ=0.54, deep-ITM 24,000 Δ=0.89, deep-OTM 25,400 Δ=0.08) and all per-unit figures (₹283/unit, ₹88/unit) are lot-independent — unchanged. Parity stated correctly as Δcall − Δput = 1 (corrects the architecture's erroneous "Put Δ + Call Δ ≈ −1"). Risk-neutral probability caveat included per Edition 2 (Delta overstates N(d2); both risk-neutral). No transaction costs → Apr-2026 STT change not applicable. All figures illustrative. IV = implied volatility. No forward chapter-number references; Gamma named as preview only. -->
