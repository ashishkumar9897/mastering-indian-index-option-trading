<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapter 8. Target length ~8,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65; BANKNIFTY lot 30 (NSE Jan-2026 revision). BANKNIFTY is monthly-only (expiry-day case sits on a monthly expiry). Gamma values computed from the Ch6/Ch8 BSM setup (S=24,600, r=6.5%, σ=13%): ATM Gamma ≈0.00043 (30 DTE), ≈0.00106 (5 DTE), ≈0.00238 (1 DTE) — a √T explosion; all lot-independent and unchanged. Only per-lot conversions rescaled to lot 65/30. No transaction costs → Apr-2026 STT change not applicable. P&L uses ΔP≈Δ·ΔS+½·Γ·(ΔS)² with POSITION Greeks (signs matter). Theta values here are illustrative previews consistent with Ch5; Theta is formalised next chapter. IV = implied volatility. -->

# Chapter 9 — Gamma: The Rate of Change of Delta

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Define Gamma and explain why it matters.
2. Recognise that Gamma is highest for ATM options and explodes near expiry.
3. Understand Gamma risk for option sellers, especially on expiry day.
4. Sharpen your P&L estimates beyond Delta alone, using the Delta + Gamma expansion.
5. Grasp the Gamma–Theta tradeoff — the fundamental tension at the heart of options.

Chapter 8 ended with a warning: Delta is not constant. **Gamma is the Greek that measures exactly how fast Delta changes** — and it is the reason a position that looks harmless can become dangerous in a single move.

---

## 2. Introduction

At 2:30 PM on a BANKNIFTY expiry day, a trader is short an at-the-money straddle. The position looks perfect: near-zero Delta, time value bleeding away in their favour, a small profit already banked as the premiums decay hour by hour. With one hour to expiry, they are relaxed.

Then, in the final hour, BANKNIFTY moves 500 points. By 3:30 PM the trader has lost more than the trade could ever have earned. The Delta they thought was zero had swung violently against them as the index moved — they got shorter and shorter into the rally, unable to hedge fast enough. The position that was "flat" at 2:30 was a live grenade, and Gamma pulled the pin.

This is the chapter that explains that grenade. **Gamma is the rate at which Delta changes.** It is the difference between a position's risk *today* and its risk *after a move*. For option buyers, Gamma is a friend — it makes gains accelerate and losses cushion. For option sellers, Gamma is the enemy that turns a quiet, income-collecting position into a catastrophe on a big move. And Gamma is not evenly spread: it concentrates at the money and **explodes as expiry approaches**, which is precisely why expiry-day selling is the most dangerous game in the Indian market.

We build Gamma from the Chapter 8 Delta foundation, compute it across strikes and time, quantify the "Delta + Gamma" P&L, and meet the unbreakable tradeoff between Gamma and Theta. Setting throughout: **NIFTY at 24,600, lot 65** (and BANKNIFTY, lot 30, for the expiry case).

---

## 3. Core Concepts

### 3.1 What Gamma is

Gamma is the flagship of this chapter.

**What is it?** **Gamma (Γ)** is the rate of change of **Delta** for a 1-point move in the underlying. If an option has Delta 0.50 and Gamma 0.002, then a 1-point rise in the index lifts its Delta to about 0.502; a 100-point rise lifts it by about 0.002 × 100 = 0.20, to ~0.70. Mathematically, Gamma is the *second* derivative of the option price with respect to the underlying: `Γ = ∂²C/∂S² = ∂Δ/∂S`.

**Why does it exist?** Because Delta is not fixed (Chapter 8). An option's sensitivity to the index changes as the index moves — a call goes from barely reactive (OTM) to fully reactive (ITM) as it crosses the strike. Gamma measures that change. It is the "acceleration" to Delta's "speed."

**Why should a trader care?** Because Gamma tells you **how fast your risk changes** — how quickly a controlled position can spiral out of control. A position with low Gamma behaves predictably; a position with high Gamma can flip from safe to dangerous in a few points. Gamma is, quite literally, the measure of how quickly you can lose control.

**Intuitive explanation.** If Delta is your car's speed, **Gamma is the accelerator pedal.** A high-Gamma position is a car that goes from 0 to 100 in an instant — thrilling if it's going your way, terrifying if it isn't. Near expiry, at the money, the accelerator is floored: the tiniest move sends Delta racing.

**Numerical feel.** The ATM NIFTY 24,600 call has Gamma about 0.00106 with 5 days to expiry. A 100-point NIFTY move changes its Delta by about 0.00106 × 100 = 0.106 — Delta shifts from 0.54 to roughly 0.65 (up) or 0.43 (down). With 1 day to expiry the same option's Gamma is about 0.00238, so a 100-point move shifts Delta by ~0.24 — more than twice as violent.

**Mathematical form (BSM).**

```
Γ = n(d₁) / (S · σ · √T)                                   (9.1)
```

where `n(d₁)` is the standard normal *density* at d₁. Two features fall straight out of (9.1): Gamma is largest when `n(d₁)` is largest (at the money, where d₁ ≈ 0), and it grows as `√T` shrinks — i.e., **as expiry approaches** (Section 3.3).

**Professional interpretation.** Desks watch Gamma as closely as Delta, because Gamma is what forces them to *re-hedge*. A high-Gamma book must be re-hedged constantly (the Delta keeps drifting); a low-Gamma book can be left alone longer. Gamma is the Greek that determines how much *work* — and how much slippage cost — a hedged position demands.

**Common mistake.** Judging a position only by its current Delta. A Delta-neutral position with large negative Gamma (a short straddle) is *not* safe; its Delta will run against you the moment the market moves.

**Practical takeaway.** **Gamma measures how fast your Delta — and therefore your risk — changes; a position's Gamma tells you how quickly it can get away from you.** Always read Gamma alongside Delta, never Delta alone.

---

### 3.2 Gamma by moneyness and time — the surface

Gamma varies across two dimensions at once: **moneyness** (which strike) and **time** (how many days to expiry). Table 9.1 maps this "Gamma surface" for NIFTY calls (spot 24,600, σ = 13%).

**Table 9.1 — Gamma surface: Gamma by strike and days to expiry (NIFTY 24,600; illustrative, from BSM)**

| Strike | 30 DTE | 5 DTE | 1 DTE |
| ---: | ---: | ---: | ---: |
| 24,200 | 0.00036 | 0.00055 | 0.00012 |
| 24,400 | 0.00041 | 0.00089 | 0.00112 |
| **24,600 (ATM)** | **0.00043** | **0.00106** | **0.00238** |
| 24,800 | 0.00043 | 0.00096 | 0.00122 |
| 25,000 | 0.00042 | 0.00065 | 0.00015 |

Read the surface in two directions:

* **Across strikes (down a column): Gamma peaks at the money.** The ATM strike always has the highest Gamma, and it falls away toward the wings. This is because an ATM option is on the knife-edge — a small move flips its moneyness, so its Delta changes fastest.
* **Across time (along a row): Gamma behaves differently at ATM versus the wings.** At the ATM strike, Gamma *rises sharply* as expiry approaches (0.00043 → 0.00106 → 0.00238). But at the wings (24,200, 25,000), Gamma actually *falls* near expiry (0.00036 → 0.00012). This is the crucial subtlety in Section 3.3.

> **Beginner Alert — Gamma "explosion" is an at-the-money phenomenon.** It is tempting to say "Gamma rises near expiry" as a blanket rule. It doesn't — for OTM options, Gamma *falls* near expiry, because an out-of-the-money option running out of time is almost certain to expire worthless, so its Delta stops changing (it heads to zero and stays). Only *at-the-money* options see Gamma explode near expiry. The danger zone is specifically the ATM strike in the final days.

---

### 3.3 Gamma explosion near expiry

The single most important practical fact about Gamma is its behaviour near expiry at the money. Table 9.2 isolates it.

**Table 9.2 — ATM Gamma explosion as expiry approaches (NIFTY 24,600; illustrative)**

| Days to expiry | ATM Gamma | Delta change for a 100-point move |
| ---: | ---: | ---: |
| 30 | 0.00043 | 0.043 |
| 5 | 0.00106 | 0.106 |
| 1 | 0.00238 | 0.238 |

Gamma more than quintuples from 30 days to 1 day. Because Gamma ∝ 1/√T for an ATM option, halving the time multiplies Gamma by √2 ≈ 1.41; going from 30 days to 1 day multiplies it by √30 ≈ 5.5.

The practical meaning is stark. With 30 days left, a 100-point NIFTY move barely nudges an ATM option's Delta (by 0.04). With 1 day left, the same 100-point move swings its Delta by 0.24 — from a coin-flip to heavily directional in a single move. **On expiry day, ATM Delta whips around so fast that a "neutral" position cannot be kept neutral** — you cannot re-hedge quickly enough. This is why expiry-day option selling is the most Gamma-dangerous activity in the market, and it is the engine of the case study in Section 9.

---

### 3.4 Long Gamma versus short Gamma

Every option position is either **long Gamma** or **short Gamma**, and the two live in opposite worlds.

**Long Gamma (option buyers).** When you *buy* options, you are long Gamma (Γ > 0). Your Delta moves *in your favour* as the index moves: you automatically get longer as the market rises and shorter as it falls. Big moves — in either direction — help you. The price you pay for this friendly acceleration is time decay (Theta, Section 3.7).

**Short Gamma (option sellers).** When you *sell* options, you are short Gamma (Γ < 0). Your Delta moves *against you*: you get shorter as the market rises (more short into a rally) and longer as it falls (more long into a decline). Big moves hurt you, and the more the market moves, the faster the loss compounds. Your compensation for bearing this is the time decay you collect.

This asymmetry is the whole story of the expiry-day trap: a short straddle is short Gamma, so a large move makes its Delta run away, and near expiry the Gamma is so large that the runaway is instant.

> **Professional Insight — "Short Gamma" is the phrase behind most option blow-ups.** When you read that a fund or a trader "was short Gamma" going into a crash, it means their Delta accelerated against them as the market moved, forcing them to buy into rallies and sell into declines to hedge — locking in losses at the worst prices. Being short Gamma is a bet that the market will stay calm; it pays a little most of the time and loses a lot occasionally. Know when you are short Gamma, and size for the move you are praying does not come.

---

### 3.5 Gamma and P&L — the second-order term

Delta alone gives a straight-line estimate of P&L. Gamma adds the *curvature* that makes the estimate accurate for larger moves. The standard expansion is:

```
ΔP ≈ Δ · ΔS + ½ · Γ · (ΔS)²                                (9.2)
```

using **position** Delta and **position** Gamma (signs from Chapter 8). The first term is the Delta (linear) P&L; the second is the Gamma (curvature) P&L. Because `(ΔS)²` is always positive:

* For a **long** option (Γ > 0), the Gamma term is **always positive** — it *adds* to gains and *cushions* losses. Long Gamma is a "heads I win more, tails I lose less" curvature.
* For a **short** option (Γ < 0), the Gamma term is **always negative** — it *shrinks* gains and *amplifies* losses. Short Gamma is the opposite curvature.

**Worked example (long ATM call, 5 DTE).** Long the 24,600 call, Δ = 0.54, Γ = 0.00106. NIFTY moves ±200 points:

```
Up 200:   ΔP ≈ 0.54×200 + ½×0.00106×200² = 108 + 21.2 = +₹129.2/unit
Down 200: ΔP ≈ 0.54×(−200) + ½×0.00106×(−200)² = −108 + 21.2 = −₹86.8/unit
```

Delta alone predicted +₹108 up and −₹108 down. Gamma made the up-gain *bigger* (₹129) and the down-loss *smaller* (₹87). That asymmetry — better than linear both ways — is the gift of long Gamma, and exactly what you pay Theta for.

The same expansion with a **short** position flips every sign of the Gamma term, turning that gift into the expiry-day trap (see Numerical Example 3).

---

### 3.6 Rupee Gamma and Position Gamma

Two practical conversions turn the abstract Gamma number into rupees and into portfolio terms.

**Position Gamma** aggregates across legs, exactly like Position Delta:

```
Position Gamma = Σ (Γᵢ × Qᵢ × Lot size)          (Qᵢ negative for short legs)
```

A positive Position Gamma means the book is net long options (Delta helps on moves); negative means net short (Delta hurts on moves).

**Rupee Gamma** (the Indian version of "dollar Gamma") expresses how much your rupee Delta-exposure shifts for a **1% move** in the index:

```
Rupee Gamma = Γ × S² / 100                                 (9.3)
```

For the ATM 24,600 call with 1 DTE (Γ = 0.00238): Rupee Gamma = 0.00238 × 24,600² / 100 ≈ **₹14,400 per unit**. That is, a 1% index move shifts this one option's rupee delta-exposure by about ₹14,400 near expiry — a vivid measure of how fast exposure changes when Gamma is high. For most practical P&L work, however, the `½ · Γ · (ΔS)²` term of equation (9.2) is the number you will actually compute.

---

### 3.7 The Gamma–Theta tradeoff

Here is the deepest idea in options, and the reason there is no free lunch: **you cannot be long Gamma without paying Theta, and you cannot collect Theta without being short Gamma.** They are two sides of one coin.

* **Long Gamma = negative Theta.** The option buyer enjoys favourable Delta acceleration (long Gamma) but pays for it through daily time decay (negative Theta).
* **Short Gamma = positive Theta.** The option seller collects daily time decay (positive Theta) but bears adverse Delta acceleration (short Gamma).

And the two rise and fall *together*, because both are largest at the money near expiry. Table 9.3 shows an ATM NIFTY call's Gamma and its daily decay side by side (the Theta figures preview Chapter 10's Table 10.1 for the same ATM NIFTY call, and both columns follow the √T law — Gamma ∝ 1/√T and Theta ∝ 1/√T; Theta is formalised in the next chapter).

**Table 9.3 — Gamma and Theta rise together at the money (ATM NIFTY, illustrative)**

| Days to expiry | ATM Gamma | Daily time decay (₹/unit) |
| ---: | ---: | ---: |
| 30 | 0.00043 | ~6 |
| 5 | 0.00106 | ~15 |
| 1 | 0.00238 | ~34 |

The message: the closer to expiry and the closer to the money, the *more* time decay a seller collects — and the *more* Gamma risk they take on to collect it. The rich Theta of expiry-day selling is not free money; it is precisely compensation for the enormous Gamma risk shown in Table 9.2. **High Theta and high Gamma are the same thing seen from two sides.** Any strategy is, at heart, a choice about where to sit on this tradeoff.

---

### 3.8 Gamma scalping and dynamic hedging

Understanding the Gamma–Theta tradeoff explains what market makers actually do all day: **Gamma scalping**.

A market maker who is **long Gamma** and Delta-neutral profits from movement. As the index rises, their Delta turns positive (long Gamma), so they *sell* the future to re-neutralise — selling high. As the index falls, their Delta turns negative, so they *buy* the future — buying low. Each re-hedge "scalps" a small profit from the round trip. Over many oscillations, these scalps accumulate. The catch: they are bleeding Theta the whole time, so Gamma scalping only wins if the market moves *more* than the decay costs — i.e., if realised volatility exceeds the implied volatility they paid.

A trader who is **short Gamma** does the mirror, and it is ruinous on trends: as the index rises they must *buy* the future to hedge (buying high), and as it falls they must *sell* (selling low) — hedging at the worst prices. They collect Theta for the privilege, which is fine in a quiet market and disastrous in a moving one.

This is why **high-Gamma positions demand dynamic hedging** — constant re-adjustment — while low-Gamma positions can be left alone. And it is why the whole game reduces to one question: *will the market move more or less than the options are pricing?* Long Gamma bets "more"; short Gamma bets "less."

---

## 4. Examples (Real-World)

**Example 1 — The friendly acceleration.** A trader buys an ATM NIFTY call before an expected move. When NIFTY jumps 300 points, the call gains *more* than its starting Delta implied, because Gamma lifted the Delta as the move unfolded. The buyer's position accelerated in their favour — long Gamma at work.

**Example 2 — The seller who got shorter.** A trader sells an OTM call for income. NIFTY rallies through the strike; the call's Delta climbs from 0.30 toward 0.70, so the seller becomes rapidly more short into the rising market. Every re-hedge is a buy at a higher price. Short Gamma turned a calm income trade into a chase.

**Example 3 — The calm before expiry.** On expiry morning a short straddle shows near-zero Delta and steady Theta gains; by early afternoon it is comfortably profitable. But its Gamma is enormous (Table 9.2). The position is not safe — it is one sharp move away from disaster, as Section 9 shows.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65; Gamma from Tables 9.1–9.2.

### Numerical Example 1 — Weekly versus monthly ATM Gamma

Compare the ATM NIFTY Gamma at 3 days (weekly) versus 25 days (monthly):

```
Gamma (3 DTE)  ≈ 0.00137
Gamma (25 DTE) ≈ 0.00047
Ratio ≈ 0.00137 ÷ 0.00047 ≈ 2.9×
```

The weekly option's Delta changes about **2.9 times faster** than the monthly's for the same index move (consistent with Gamma ∝ 1/√T: √(25/3) ≈ 2.9). This is why weekly expiries carry so much more Gamma risk — and why they are the sellers' battleground.

### Numerical Example 2 — Delta + Gamma P&L (long option)

Long the ATM 24,600 call (Δ = 0.54, Γ = 0.00106, 5 DTE), NIFTY ±200:

```
Up 200:   0.54×200 + ½×0.00106×200²  = 108 + 21.2 = +₹129.2/unit  (₹8,398/lot)
Down 200: 0.54×(−200) + ½×0.00106×200² = −108 + 21.2 = −₹86.8/unit (−₹5,642/lot)
```

Long Gamma made the gain bigger and the loss smaller than Delta alone predicted (±₹108). The ₹21.2 curvature is the Gamma benefit — paid for with Theta.

### Numerical Example 3 — Delta + Gamma P&L (short option; the trap)

Short the 24,500 call, position Δ = −0.50, position Γ = −0.003, NIFTY up 200:

```
Delta only:   −0.50 × 200 = −₹100/unit
Delta + Gamma: −0.50×200 + ½×(−0.003)×200² = −100 − 60 = −₹160/unit
```

Delta alone predicted a ₹100 loss; the real loss is ₹160 (₹10,400 on a lot vs. the ₹6,500 Delta-only estimate). The extra ₹60 is **short Gamma amplifying the loss** — and this understates the damage near expiry, where Gamma is far larger and itself keeps rising through the move.

### Numerical Example 4 — Rupee Gamma near expiry

ATM 24,600 call, 1 DTE, Γ = 0.00238:

```
Rupee Gamma = Γ × S² / 100 = 0.00238 × 24,600² / 100 ≈ ₹14,400 per unit
```

A 1% NIFTY move (~246 points) shifts this option's rupee delta-exposure by about ₹14,400 — a concrete measure of how explosively exposure changes at the money on expiry day.

### Numerical Example 5 — A near-zero-Delta, positive-Gamma position

Buy the ATM 24,600 call (Δ ≈ +0.54) *and* the ATM 24,600 put (Δ ≈ −0.46) — a **long straddle**:

```
Position Delta ≈ +0.54 − 0.46 = +0.08 (≈ 0, near-neutral)
Position Gamma = strongly positive (both legs long Gamma)
```

This position barely cares about small moves (near-zero Delta) but profits from a **large move in either direction** (positive Gamma), because Gamma turns any big move into a favourable Delta. It profits when the realised move exceeds the time decay (Theta) paid — a pure "movement" bet, the mirror image of the expiry-day short straddle.

---

## 6. Calculations (the reusable recipes)

**(a) Gamma from BSM**

```
Γ = n(d₁) / (S · σ · √T)          (n = standard normal density; peaks at ATM, rises as T → 0)
```

**(b) Delta of an option after a move**

```
New Delta ≈ Old Delta + Γ × (points moved)
```

**(c) Delta + Gamma P&L expansion (use POSITION Greeks, with signs)**

```
ΔP ≈ Position Delta × ΔS + ½ × Position Gamma × (ΔS)²
```

**(d) Position Gamma**

```
Position Gamma = Σ (Γᵢ × Qᵢ × Lot size)     (Qᵢ negative for short legs)
```

**(e) Rupee Gamma (exposure shift per 1% move)**

```
Rupee Gamma = Γ × S² / 100
```

---

## 7. Practical Insights

* **Read Gamma with Delta, always.** Delta tells you today's risk; Gamma tells you how fast that risk will change. A low-Delta, high-Gamma position is a coiled spring.
* **Expiry-day ATM Gamma is the market's most dangerous force.** It makes "neutral" positions un-hedgeable in real time. If you sell options into expiry, size for a violent move, because you cannot re-hedge fast enough when it comes.
* **Long Gamma is a gift you rent; short Gamma is income you insure.** Buyers get favourable acceleration and pay Theta; sellers collect Theta and carry the acceleration risk. Neither is free.
* **The whole game is realised vs. implied movement.** Long Gamma wins if the market moves more than priced; short Gamma wins if it moves less. Frame every option trade this way.
* **High Gamma means high maintenance.** If you must stay hedged, high Gamma means frequent re-hedging and real slippage cost — factor that into whether the trade is worth it.

---

## 8. Common Mistakes

* **Judging a position by Delta alone.** A Delta-neutral short straddle is *not* flat; its large negative Gamma means the next move creates directional risk instantly.
* **Assuming "Gamma rises near expiry" for all strikes.** It rises only at the money; OTM Gamma *falls* near expiry. The danger is specifically ATM in the final days.
* **Selling expiry-day options for the "easy" Theta without respecting the Gamma.** The rich decay is precisely payment for enormous Gamma risk — they are the same thing.
* **Using the starting Delta to size a big move.** Gamma makes Delta run; a short position's loss on a large move far exceeds the Delta-only estimate.
* **Setting a position Delta-neutral and walking away.** With high Gamma, neutrality evaporates on the next move; it must be re-hedged or it is not protection at all.

---

## 9. Case Study — "The Expiry Day Gamma Trap"

**Context.** A trader sells one lot of an at-the-money **BANKNIFTY** straddle on expiry afternoon, with the index at **52,000** and about an hour to go (lot size 30; figures illustrative but representative). They collect a total premium of **₹200** (roughly ₹100 on the call, ₹100 on the put) — the thin time value left near expiry. The position's Delta is near zero (short call Δ ≈ −0.5, short put Δ ≈ +0.5, netting ~0), and it is bleeding time value in their favour. At 2:30 PM it shows a small profit and looks safe.

**What happened.** In the final hour, BANKNIFTY moved **500 points, to 52,500**. At expiry:

* The 52,000 **call** settled deep in the money, worth its intrinsic value of **₹500**.
* The 52,000 **put** expired **worthless (₹0)**.
* The straddle the trader was short was therefore worth **₹500**; they had collected **₹200**.

```
Loss per unit  = 500 − 200 = ₹300
Loss per lot   = 300 × 30 = ₹9,000
Maximum possible gain on the trade = 200 × 30 = ₹6,000
```

A single expiry-hour move turned a trade whose best-case profit was ₹6,000 into a **₹9,000 loss.**

**The Gamma math — why it detonated.** At 2:30 PM the position's Delta was ~0, but its **Gamma was enormous** (ATM, minutes to expiry — off the top of Table 9.2's scale). As BANKNIFTY rose:

* The short call's Delta raced from about −0.5 toward −1.0, and the short put's from about +0.5 toward 0. The **position Delta swung from ~0 to about −1.0** — the trader became fully short one call's worth of index, right as the market rallied.
* The Gamma curvature term `½ · Γ · (ΔS)²` — negative for a short position — dominated the P&L. With the huge near-expiry Gamma, even a crude estimate (position Γ ≈ −0.004, ΔS = 500) gives `½ × (−0.004) × 500² = −₹500` per unit of Gamma-driven loss, swamping the tiny Theta gain the trader had been collecting.
* Critically, the move was **too fast to hedge.** Re-neutralising would have meant buying BANKNIFTY futures into the spike — chasing a runaway Delta at ever-worse prices. Near expiry, the Delta moved faster than any hedge could follow.

*(Note: the exact loss is best read straight off the intrinsic value at expiry, ₹300 per unit; the quadratic Gamma term is an approximation that over- or under-shoots for such large, late moves because Gamma itself changes and Delta caps at ±1. The point is not the exact rupee but the mechanism: short Gamma near expiry converts a small move into an outsized, un-hedgeable loss.)*

**The lesson.** The position was never "safe" — it was **short a mountain of Gamma**. The steady Theta gains it showed at 2:30 were payment for exactly this risk, and the market collected on the payment. Expiry-day option selling offers the richest time decay in the market precisely because it carries the most violent Gamma; the two are inseparable. If you sell into expiry, you must size the position for a large, fast move you cannot hedge — not for the calm you hope for.

*(Takeaway: on expiry day, at-the-money Gamma is so large that a "flat" short position can lose more than its maximum profit in a single move — the rich Theta is the fee you are paid for that risk, not a free lunch.)*

---

## 10. Chapter Summary

* **Gamma (Γ)** is the rate of change of Delta per 1-point move — the "acceleration" of an option; `Γ = n(d₁)/(S·σ·√T)`.
* Gamma **peaks at the money**; across time it **explodes at the ATM near expiry** (0.00043 → 0.00238 from 30 to 1 DTE) but *falls* in the wings near expiry — the danger is specifically ATM in the final days.
* **Long Gamma** (buyers) has Delta move *for* you (gains accelerate, losses cushion); **short Gamma** (sellers) has Delta move *against* you (losses amplify) — the source of most option blow-ups.
* P&L is `ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)²`; the Gamma term *adds* for longs and *subtracts* for shorts, using position Greeks with their signs.
* **Position Gamma** = Σ(Γ × Q × lot size); **Rupee Gamma** = Γ × S²/100 measures exposure shift per 1% move.
* The **Gamma–Theta tradeoff** is unbreakable: long Gamma costs Theta, short Gamma earns Theta, and both peak together at the money near expiry — rich decay is payment for Gamma risk.
* **Gamma scalping** is how long-Gamma market makers profit from movement (sell rallies, buy dips to re-hedge), winning only if realised volatility beats implied — the whole game is *movement vs. what was priced*.
* **The expiry-day trap:** a "flat," Theta-collecting short straddle is short enormous, un-hedgeable Gamma, and a single late move can lose more than the trade's maximum profit.

---

## 11. Key Takeaways

* **Never judge risk by Delta alone** — Gamma tells you how fast that risk will change, and a neutral high-Gamma position is a coiled spring.
* **Respect ATM expiry-day Gamma above all** — it makes short positions un-hedgeable and turns small moves into outsized losses.
* **Know your sign:** long Gamma rents favourable acceleration for Theta; short Gamma sells insurance and must be sized for the move it fears.
* **Frame every option trade as realised vs. implied movement** — that single question decides whether long or short Gamma wins.

---

## 12. Practice Questions

**Q1 (Definition).** Define Gamma in one sentence, and state its relationship to Delta.

**Q2 (Moneyness/time).** From Table 9.1, where is Gamma highest across strikes, and what happens to ATM Gamma as expiry approaches?

**Q3 (Multiple choice).** Near expiry, Gamma explodes for:
(a) all options; (b) only deep-OTM options; (c) only at-the-money options; (d) only deep-ITM options.

**Q4 (Delta drift).** An ATM option has Delta 0.54 and Gamma 0.00106. Estimate its new Delta after NIFTY rises 150 points.

**Q5 (Delta + Gamma, long).** Long an option with Δ = 0.50, Γ = 0.0012. Estimate the per-unit P&L for a +250-point move using (a) Delta only and (b) Delta + Gamma.

**Q6 (Delta + Gamma, short).** Short an option with position Δ = −0.40, position Γ = −0.0012. Estimate the per-unit P&L for a +250-point move using Delta + Gamma, and compare with the Delta-only figure.

**Q7 (Weekly vs monthly).** Why does a weekly ATM option carry roughly 2.9× the Gamma of a monthly ATM option, and what practical risk does this create?

**Q8 (Tradeoff).** State the Gamma–Theta tradeoff in one sentence, and explain why rich expiry-day Theta is "not free money."

**Q9 (Long/short Gamma).** You are short a straddle. As the index rallies, does your Delta become more positive or more negative, and does this help or hurt you?

**Q10 (Judgement).** A trader sells an expiry-day ATM straddle for ₹180, saying "it's Delta-neutral, so it's safe." Explain, using Gamma, why this is dangerous.

---

## 13. Detailed Solutions

**A1.** Gamma is the rate of change of an option's Delta per 1-point move in the underlying (Γ = ∂Δ/∂S) — it is the "acceleration" of Delta, i.e., how fast Delta itself changes.

**A2.** Across strikes, Gamma is highest **at the money** (it falls toward the wings). As expiry approaches, **ATM Gamma rises sharply** (explodes) — from 0.00043 at 30 DTE to 0.00238 at 1 DTE in Table 9.1.

**A3.** **(c) only at-the-money options.** OTM (and ITM) Gamma actually *falls* near expiry because those options' Deltas head to a fixed value (0 or 1) and stop changing.

**A4.** New Delta ≈ 0.54 + 0.00106 × 150 = 0.54 + 0.159 = **≈ 0.70**.

**A5.** (a) Delta only: 0.50 × 250 = **+₹125/unit**. (b) Delta + Gamma: 0.50 × 250 + ½ × 0.0012 × 250² = 125 + ½ × 0.0012 × 62,500 = 125 + 37.5 = **+₹162.5/unit** (long Gamma adds ₹37.5).

**A6.** Delta + Gamma: (−0.40 × 250) + ½ × (−0.0012) × 250² = −100 − 37.5 = **−₹137.5/unit**. Delta only gives −0.40 × 250 = −₹100; short Gamma **amplifies** the loss by ₹37.5.

**A7.** Gamma ∝ 1/√T, so with about 1/8 the time to expiry (3 vs 25 days), Gamma is about √(25/3) ≈ 2.9× larger. Practically, a weekly ATM option's Delta changes far faster for the same index move, so weekly short positions carry much greater risk of Delta running away — the reason weekly expiries are the sellers' danger zone.

**A8.** You cannot be long Gamma without paying Theta, nor collect Theta without being short Gamma — they are inseparable. Rich expiry-day Theta is not free money because it is precisely the compensation for the enormous ATM Gamma risk you take on to collect it; the two peak together.

**A9.** Short a straddle, you are short Gamma. As the index rallies your Delta becomes **more negative** (the short call's Delta grows toward −1). This **hurts** you — you become increasingly short into a rising market, so the loss accelerates.

**A10.** "Delta-neutral" only means the position is directionally flat *at this instant*. An expiry-day ATM straddle has **enormous negative Gamma**, so the moment the index moves, its Delta swings hard against the seller (short Gamma), and near expiry the move is too fast to hedge. A single sharp move can lose more than the ₹180 collected — the position is neutral in Delta but extremely exposed in Gamma.

---

## 14. Mini Glossary

* **Gamma (Γ)** — the rate of change of Delta per 1-point move in the underlying; the second derivative of price with respect to the underlying. → this chapter.
* **Gamma surface** — how Gamma varies across strikes (peaks at ATM) and time (explodes at ATM near expiry). → this chapter.
* **Gamma explosion** — the sharp rise in ATM Gamma as expiry approaches (an at-the-money phenomenon only). → this chapter.
* **Long Gamma** — an option-buyer position whose Delta moves favourably as the underlying moves (gains accelerate, losses cushion). → this chapter.
* **Short Gamma** — an option-seller position whose Delta moves adversely (losses amplify); the source of most blow-ups. → this chapter.
* **Delta + Gamma expansion** — ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)²; the second-order P&L estimate. → this chapter.
* **Position Gamma** — Σ(Γ × quantity × lot size); the portfolio's net Gamma. → this chapter.
* **Rupee (dollar) Gamma** — Γ × S²/100; the shift in rupee delta-exposure per 1% move. → this chapter.
* **Gamma–Theta tradeoff** — the inseparable link: long Gamma costs Theta, short Gamma earns Theta; both peak at ATM near expiry. → this chapter.
* **Gamma scalping** — a long-Gamma market maker's practice of re-hedging (sell rallies, buy dips) to profit from movement, winning only if realised beats implied volatility. → this chapter.
* **Dynamic hedging** — continuously re-adjusting a hedge as Delta drifts; required for high-Gamma positions. → this chapter.

---

<!-- End of Chapter 9 (Rev 2, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65, BANKNIFTY lot 35→30 (NSE Jan-2026 revision) — per-lot conversions rescaled: NE2 ₹8,398/₹5,642 per lot; NE3 ₹10,400 vs ₹6,500; expiry case loss ₹300/unit=₹9,000/lot > max gain ₹6,000. Gamma values, all per-unit figures (₹129.2/₹86.8/₹160/₹300 per unit, Rupee Gamma ₹14,400/unit), and √T scaling are lot-independent — unchanged. Gamma surface & explosion from Ch6/Ch8 BSM setup (ATM Γ: 0.00043 @30DTE, 0.00106 @5DTE, 0.00238 @1DTE; √30≈5.5×). Weekly(3d)≈0.00137 vs monthly(25d)≈0.00047, ratio 2.9×=√(25/3). BANKNIFTY monthly-only; expiry-day case sits on a monthly expiry. No transaction costs → Apr-2026 STT change not applicable. Theta values illustrative previews consistent with Ch5; formalised next chapter. IV = implied volatility. No forward chapter-number references. -->
