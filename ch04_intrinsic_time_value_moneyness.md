<!-- Difficulty: Level 2/5 (Beginner-Intermediate). Dependency: Chapter 2. Target length ~7,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision); BANKNIFTY lot 30. NIFTY weekly expiry = Tuesday (since 1 Sep 2025). Costs ignored in examples, so the Apr-2026 STT change does not affect this chapter's numbers. Payoff diagrams rendered as labelled ASCII schematics + P&L tables (manuscript figures to be drawn per Style Guide §9). Intrinsic value uses the spot convention (consistent with Ch2); parity uses the futures price. IV reserved for implied volatility; intrinsic value always spelled out. -->

# Chapter 4 — Intrinsic Value, Time Value, and Moneyness

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Decompose any option premium into its two parts — intrinsic value and time value.
2. Classify any option by moneyness, from deep in-the-money to deep out-of-the-money.
3. Explain *why* time value exists, what it represents, and why it peaks at the money.
4. Recognise the asymmetric payoff of options — limited risk for buyers, large or unlimited risk for sellers.
5. Draw and read the payoff diagrams for the four basic positions, and use put–call parity to link calls, puts, and futures.

In Chapter 2 you met intrinsic value and time value as definitions. This chapter turns them into working tools: you will decompose a whole option chain, see the shape of every basic position, and understand the single idea — *optionality* — that gives an out-of-the-money option any value at all.

---

## 2. Introduction

Here is a puzzle that troubles almost every new trader. On a Wednesday, with NIFTY at 24,600, a trader buys the 25,000 call for ₹33. Over the following sessions NIFTY drifts up to 24,850 — a move of 250 points in exactly the direction the trader wanted. At the next Tuesday's expiry the option expires worthless. The trader was *right about direction* and still lost every rupee.

Nothing was manipulated. The trader simply did not understand what they had bought. That ₹33 was **pure time value** — a payment for the *possibility* that NIFTY would climb past 25,000 before the Tuesday expiry. It did not, so the possibility expired, and with it the premium.

This chapter dissects that ₹33. Every option premium, without exception, is the sum of two parts: **intrinsic value** (what the option is worth right now) and **time value** (what the market charges for the chance of more). Learn to see those two parts in every price and most beginner mysteries dissolve — why a "cheap" option can be a terrible bet, why an at-the-money option costs the most in time value, and why the same contract is a limited-risk lottery ticket for the buyer and an open-ended liability for the seller.

We use the familiar setting throughout: **NIFTY at 24,600, lot size 65**, a near weekly expiry. All premiums are illustrative but internally consistent, and all P&L figures are per unit unless a lot figure is given.

---

## 3. Core Concepts

### 3.1 The two parts of every premium

Recall from Chapter 2 the two definitions, which we now use constantly:

```
Intrinsic value (call) = max(0, Spot − Strike)
Intrinsic value (put)  = max(0, Strike − Spot)
Time value             = Premium − Intrinsic value
```

Intrinsic value is the **in-the-money amount** — what you would collect if the option settled this instant. It can never be negative (you would simply not exercise a losing option), so it is floored at zero. Time value is **everything left over** — the premium the market charges for the time remaining and the uncertainty within it.

**Worked split (recap and extend).** With NIFTY at 24,600:

* The `24500 CE` at ₹275 → intrinsic value = 24,600 − 24,500 = ₹100; time value = 275 − 100 = **₹175**.
* The `25000 CE` at ₹33 → intrinsic value = 0 (spot is below the strike); time value = **₹33** (the entire premium).
* The `24300 PE` at ₹68 → intrinsic value = 0 (spot is above the strike); time value = **₹68**.

The second and third examples are the puzzle from the introduction: an out-of-the-money option is **100% time value**, a payment for possibility alone.

> **Beginner Alert — "Cheap" is a statement about price, not about value.** A ₹33 option is not "cheap" in any useful sense — it is *entirely time value*, which means you are buying only the slim chance of a move. The low price reflects low odds, not a bargain. Never let a small premium substitute for a real reason to expect the move.

---

### 3.2 The moneyness spectrum

**Moneyness** places an option on a spectrum according to where the spot sits relative to the strike. For NIFTY at 24,600:

| Region | Call example | Put example | What the premium is made of |
| --- | --- | --- | --- |
| **Deep ITM** | 24,000 CE | 25,200 PE | Mostly intrinsic value; little time value |
| **ITM** | 24,400 CE | 24,800 PE | Intrinsic + meaningful time value |
| **ATM** | 24,600 CE | 24,600 PE | Almost all time value (intrinsic ≈ 0) |
| **OTM** | 24,800 CE | 24,400 PE | All time value |
| **Deep OTM** | 25,200 CE | 24,000 PE | A little time value; cheap and usually worthless |

Two facts you will lean on for the rest of the book:

* **Deep-ITM options behave almost like the future.** Nearly all their value is intrinsic, so they move roughly one-for-one with the index.
* **Deep-OTM options are almost all "hope."** They are cheap because the probability of finishing in the money is small; most expire worthless.

---

### 3.3 Time value — why it exists, and why it peaks at the money

Time value is the deepest idea in this chapter, so we treat it in full.

**What is it?** Time value is the part of the premium *above* intrinsic value — the price of the option's remaining **optionality**, the chance that the underlying moves further in the holder's favour before expiry.

**Why does it exist?** Because an option is a *right without an obligation*. The holder keeps all the upside if the index moves their way and walks away (losing only the premium) if it does not. That one-sided pay-off has value whenever the future is uncertain and there is still time for it to unfold. Remove the uncertainty or remove the time, and time value vanishes.

**Why should a trader care?** Because time value is the battleground between buyers and sellers. The buyer *pays* it and needs the underlying to move enough to justify it; the seller *collects* it and profits if it erodes. Every option strategy is, at bottom, a position on whether time value is too high or too low.

**Intuitive explanation.** Time value is an *insurance premium on possibility*. Insurers charge more when there is more time for something to go wrong and more uncertainty about outcomes. An option seller is that insurer; the buyer is the policyholder paying for coverage that expires on a fixed date.

**Two structural facts, explained:**

* **Time value is greatest at the money.** At the ATM strike the outcome is maximally uncertain — the option is on a knife-edge between finishing worthless and finishing valuable, so the optionality is worth the most. Move deep ITM and the option is almost certain to finish in the money (it behaves like the future, little optionality left); move deep OTM and it is almost certain to finish worthless (little chance to pay for). The peak sits in the uncertain middle.
* **Time value is always ≥ 0 before expiry for European options.** An option can never be worth *less* than its intrinsic value while time remains, because the extra time can only help the holder, never hurt them. (At expiry, time value is exactly zero and only intrinsic value remains.)

**Why deep-OTM options are cheap but usually expire worthless.** Their entire premium is a small payment for a low-probability event. Occasionally one pays off spectacularly; far more often it decays quietly to zero. This is the mathematical heart of the "lottery ticket" trap in Section 9.

**Professional interpretation.** Professionals rarely ask "will the index go up?" They ask "is this time value *rich or cheap* relative to how much the index is likely to move?" Selling richly priced time value and buying cheap time value — not guessing direction — is where much of the professional edge lives.

**Common mistake.** Buying OTM options because the premium is small, without realising that a small premium is *all time value* and that time value decays to zero unless a real move arrives in time.

**Practical takeaway.** **Before you buy any option, ask how much of the premium is time value and what move, by when, would justify paying it.** If you cannot answer, you are buying hope, not a position.

---

### 3.4 Payoff diagrams — the four basic positions

A **payoff diagram** plots an option position's profit or loss (vertical axis, ₹ per unit) against the underlying level at expiry (horizontal axis, points). The characteristic bent-line shape is why they are nicknamed "hockey-stick" graphs. For every position we mark the **breakeven**, the **maximum profit**, and the **maximum loss** — the three numbers you must know before entering any trade.

We use a single strike for clarity: the ATM `24600` options at a premium of **₹205** (both call and put), so the symmetry between the four positions is unmistakable.

**Position 1 — Long Call** (buy `24600 CE` @ ₹205). Risk limited to the premium; profit unlimited above the breakeven.

```
 P&L/unit (₹)
   +   │                     ╱
       │                   ╱
   0 ──┼──────────●──────╱──────────▶ Spot at expiry
       │        24805 ╱  (breakeven)
 −205  │━━━━━━━━━━╱   ← max loss = premium
       │      24600
```

Breakeven = 24,600 + 205 = **24,805**. Max loss = **₹205** (per unit). Max profit = **unlimited**.

**Position 2 — Long Put** (buy `24600 PE` @ ₹205). Risk limited to the premium; profit large as the index falls (capped only because the index cannot fall below zero).

```
 P&L/unit (₹)
   +   │╲
       │  ╲
   0 ──┼────╲──────●──────────────▶ Spot at expiry
       │      ╲  24395 (breakeven)
 −205  │       ╲━━━━━━━━━━━━  ← max loss = premium
       │      24600
```

Breakeven = 24,600 − 205 = **24,395**. Max loss = **₹205**. Max profit = up to 24,395 per unit (if the index went to zero) — large, not infinite.

**Position 3 — Short Call** (sell `24600 CE` @ ₹205). The mirror of the long call: profit capped at the premium, loss **unlimited** as the index rises.

```
 P&L/unit (₹)
 +205  │━━━━━━━━━━╲   ← max profit = premium
   0 ──┼──────────●──────╲──────────▶ Spot at expiry
       │        24805 ╲  (breakeven)
   −   │                 ╲
       │      24600        ╲
```

Breakeven = **24,805**. Max profit = **₹205**. Max loss = **unlimited**.

**Position 4 — Short Put** (sell `24600 PE` @ ₹205). The mirror of the long put: profit capped at the premium, loss large as the index falls (capped at strike − premium).

```
 P&L/unit (₹)
 +205  │        ╱━━━━━━━━━━━  ← max profit = premium
   0 ──┼──────●──────────────────▶ Spot at expiry
       │  24395 ╱ (breakeven)
   −   │      ╱
       │    ╱  24600
```

Breakeven = **24,395**. Max profit = **₹205**. Max loss = up to 24,395 per unit — substantial, not unlimited.

**The asymmetry to burn into memory:** the **buyer's** loss is capped at the premium (a known, small number), while the **seller's** loss is far larger than the premium received — *unlimited* for a short call, *large* for a short put. This is why sellers post margin and buyers do not (Chapter 3), and it is the single most important risk fact in options.

> **Professional Insight — Sellers win often and small; buyers win rarely and big.** The four diagrams encode two opposite businesses. Selling options is like insurance: frequent small gains (the premium) punctuated by occasional large losses. Buying options is the reverse: frequent small losses (decayed premium) and occasional large gains. Neither is "right" — but you must know which pattern of outcomes you are signing up for, because it determines how you size, stop, and stay sane.

---

### 3.5 Put–call parity — the hidden link

Calls, puts, and futures are not three separate worlds; they are bound together by an identity called **put–call parity**. In its practical form for index options:

```
C − P = PV(F − K)
```

where `C` and `P` are the call and put premiums at the same strike `K` and expiry, `F` is the futures price, and `PV(·)` discounts to today (a tiny adjustment for short-dated options). In words: **the call minus the put equals the discounted gap between the future and the strike.**

**Why it must hold.** Recall the synthetic future from Chapter 2: buying a call and selling a put at the same strike reproduces a long futures position. If `C − P` did not line up with `F − K`, you could combine options and the future to lock in risk-free profit — and arbitrageurs would erase the gap instantly. So parity holds, up to transaction costs.

**What it tells a trader.** Parity is why a call and a put are two views of the same thing. It also explains a real-chain observation that confuses beginners: **the spot-ATM call is usually pricier than the spot-ATM put.** Because the future trades a little above the spot (a positive basis, Chapter 2), `F − K` is positive at the spot strike, so `C − P > 0`.

> **Beginner Alert — Time value is symmetric against the *future*, not the spot.** In the clean decomposition table below (Table 4.1) we assume the future equals the spot, so a strike's call and put have equal time value. On a *real* chain the future sits above the spot, so at a given strike the call carries more time value than the put — exactly the amount parity requires. Nothing is wrong; you are simply measuring intrinsic value against the spot while the market prices against the future.

---

### 3.6 The insurance mental model

The cleanest way to hold all of this together is the insurance analogy, now made precise:

* An **OTM put** is portfolio insurance. You pay a premium (time value) for protection below a chosen level (the strike). Most of the time the "disaster" does not happen and the premium is lost — exactly as with home insurance in a year without a flood. When the crash comes, the put pays.
* The **put seller** is the insurance company, collecting premiums and paying out in the bad states.
* **Time value is the price of the coverage**, and it is highest when uncertainty is highest — which is why insurance (and ATM time value) costs more in turbulent times.

Hold this model and you will never again be surprised that a "correct" directional call still lost money: you paid an insurance premium for a possibility, and the possibility did not arrive in time.

---

## 4. Examples (Real-World)

**Example 1 — The right-direction loss.** The introduction's trade: `25000 CE` bought at ₹33 (all time value) with NIFTY at 24,600. NIFTY rises to 24,850 — up 250 points — but stays below 25,000, so the call expires worthless. Being right on direction is worthless if the move does not clear the strike plus the time value paid.

**Example 2 — Deep-ITM behaves like the future.** With NIFTY at 24,600, the `24000 CE` (deep ITM) trades near ₹640 — about ₹600 intrinsic and only ₹40 time value. A 100-point rise in NIFTY lifts it almost 100 points, because it is nearly all intrinsic value. A trader wanting future-like exposure with defined risk sometimes prefers a deep-ITM call for exactly this reason.

**Example 3 — Insurance that paid.** A long-term investor holds a NIFTY-like portfolio and each month buys a 5%-OTM NIFTY put for a small premium. For eleven calm months the premiums are lost — the cost of coverage. In the twelfth, a sharp fall makes the put surge, offsetting much of the portfolio's loss. The lost premiums were the price of the protection that eventually mattered.

---

## 5. Numerical Examples

Setting: **NIFTY spot 24,600, lot 65**, near weekly expiry. Premiums illustrative; Table 4.1 assumes the future equals the spot (zero basis) so the decomposition is clean.

### Numerical Example 1 — Premium decomposition across 15 strikes

**Table 4.1 — Intrinsic value and time value for 15 NIFTY strikes (spot 24,600; illustrative, zero basis)**

| Strike | Call premium | Call intrinsic | Call time value | Put premium | Put intrinsic | Put time value |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 24,300 | 368 | 300 | 68 | 68 | 0 | 68 |
| 24,350 | 342 | 250 | 92 | 92 | 0 | 92 |
| 24,400 | 320 | 200 | 120 | 120 | 0 | 120 |
| 24,450 | 300 | 150 | 150 | 150 | 0 | 150 |
| 24,500 | 275 | 100 | 175 | 175 | 0 | 175 |
| 24,550 | 245 | 50 | 195 | 195 | 0 | 195 |
| **24,600 (ATM)** | **205** | **0** | **205** | **205** | **0** | **205** |
| 24,650 | 195 | 0 | 195 | 245 | 50 | 195 |
| 24,700 | 175 | 0 | 175 | 275 | 100 | 175 |
| 24,750 | 150 | 0 | 150 | 300 | 150 | 150 |
| 24,800 | 120 | 0 | 120 | 320 | 200 | 120 |
| 24,850 | 92 | 0 | 92 | 342 | 250 | 92 |
| 24,900 | 68 | 0 | 68 | 368 | 300 | 68 |
| 24,950 | 48 | 0 | 48 | 398 | 350 | 48 |
| 25,000 | 33 | 0 | 33 | 433 | 400 | 33 |

**Read the pattern.** Time value (either column) peaks at ₹205 at the ATM strike and falls smoothly in both directions — the "time-value curve" the architecture asks us to visualise. Deep-ITM and deep-OTM options carry little time value; the ATM carries the most. Note also that the deep-OTM call (25,000 at ₹33) and deep-OTM put (24,300 at ₹68) are *entirely* time value.

### Numerical Example 2 — P&L at expiry for the four basic positions

Using the ATM `24600` options at ₹205 (per unit; costs ignored).

**Table 4.2 — P&L per unit at various expiry levels**

| Spot at expiry | Long Call | Short Call | Long Put | Short Put |
| ---: | ---: | ---: | ---: | ---: |
| 24,000 | −205 | +205 | +395 | −395 |
| 24,200 | −205 | +205 | +195 | −195 |
| 24,395 | −205 | +205 | 0 | 0 |
| 24,600 | −205 | +205 | −205 | +205 |
| 24,805 | 0 | 0 | −205 | +205 |
| 25,000 | +195 | −195 | −205 | +205 |
| 25,200 | +395 | −395 | −205 | +205 |

Notice the mirror symmetry: Long Call = −(Short Call), and Long Put = −(Short Put), at every level. Options are zero-sum between the two sides (Chapter 1) — one column is exactly the negative of its pair.

### Numerical Example 3 — Breakevens (all four positions)

```
Long/Short Call breakeven = Strike + Premium = 24,600 + 205 = 24,805
Long/Short Put  breakeven = Strike − Premium = 24,600 − 205 = 24,395
```

In lot terms, the ATM long call risks 205 × 65 = **₹13,325** to make unlimited profit above 24,805; the short call earns at most ₹13,325 while risking far more above 24,805.

### Numerical Example 4 — Verifying put–call parity (with a real basis)

Now assume the future `F = 24,700` (basis +100 over spot), `r = 6.5%`, `T = 10/365`, so the discount factor `e^(−rT) ≈ 0.9982`. Parity predicts `C − P = 0.9982 × (F − K)`.

**Table 4.3 — Put–call parity check (illustrative premiums, F = 24,700)**

| Strike K | Call C | Put P | C − P (observed) | 0.9982 × (F − K) (predicted) |
| ---: | ---: | ---: | ---: | ---: |
| 24,600 | 256 | 156 | +100 | +99.8 |
| 24,700 | 200 | 200 | 0 | 0.0 |
| 24,800 | 155 | 255 | −100 | −99.8 |

Parity holds to within rounding. At the strike equal to the future (24,700), the call and put are equal; below it the call is richer, above it the put is richer — precisely the tilt the basis creates.

---

## 6. Calculations (the reusable recipes)

**(a) Intrinsic value and time value**

```
Call intrinsic value = max(0, Spot − Strike)
Put  intrinsic value = max(0, Strike − Spot)
Time value = Premium − Intrinsic value          (≥ 0 before expiry; = 0 at expiry)
```

**(b) P&L at expiry (per unit; multiply by lot size for rupees)**

```
Long Call  = max(0, Spot − Strike) − Premium
Short Call = Premium − max(0, Spot − Strike)
Long Put   = max(0, Strike − Spot) − Premium
Short Put  = Premium − max(0, Strike − Spot)
```

**(c) Breakevens**

```
Call breakeven = Strike + Premium
Put  breakeven = Strike − Premium
```

**(d) Maximum profit / maximum loss**

```
Long Call:  max loss = Premium;        max profit = unlimited
Long Put:   max loss = Premium;        max profit = Strike − Premium (index → 0)
Short Call: max profit = Premium;      max loss = unlimited
Short Put:  max profit = Premium;      max loss = Strike − Premium (index → 0)
```

**(e) Put–call parity (practical form)**

```
C − P = PV(F − K) ≈ (F − K) for short-dated options
```

---

## 7. Practical Insights

* **Split every premium before you trade it.** Intrinsic value is what you own; time value is what you are betting will be justified. Knowing the mix tells you instantly whether you are buying substance or hope.
* **The ATM is where time value — and therefore decay — is richest.** Sellers gravitate to the money to collect the most time value; buyers of ATM options pay the most for it. Neither is free.
* **Deep-ITM options are the closest thing to a defined-risk future.** When you want directional exposure that moves nearly one-for-one with the index but with capped downside, a deep-ITM option is often the cleaner tool than a far-OTM lottery ticket.
* **Respect the seller's asymmetry.** A short call's loss is unlimited and a short put's loss is large; the premium you collect is small by comparison. Selling can be a fine business, but only sized and hedged with that asymmetry in mind.
* **Parity keeps you honest.** If a call and put at the same strike seem wildly inconsistent with the future, you have mis-measured something (usually the basis) — not found free money.

---

## 8. Common Mistakes

* **Buying OTM options because they are "cheap."** A low premium is entirely time value — a payment for low odds. Cheapness signals a poor probability, not a bargain (quantified in Section 9).
* **Confusing "right on direction" with "profitable."** As the introduction shows, a favourable move that fails to clear strike + time value still loses. Direction alone is not enough for a buyer.
* **Ignoring time value when selling, and thinking the risk equals the premium.** The premium is the reward; the risk is the far larger payoff you may owe.
* **Expecting a strike's call and put to have equal premiums.** They only match when the strike equals the future. The basis tilts them, exactly as parity says.
* **Treating a deep-OTM position as "small risk because it's small money."** You can lose 100% of it, repeatedly, and the base rate of doing so is high.

---

## 9. Case Study — "The OTM Lottery Ticket Trap"

**Context.** The most common single mistake among new option buyers in India is buying cheap, far-out-of-the-money weekly options — "lottery tickets." They cost little, occasionally multiply many times over, and feel like a low-risk shot at a big win. The numbers tell a harsher story. The study below is **illustrative and representative** — modelled on the pattern SEBI's retail-loss findings describe (Chapter 1), not a specific dataset — but the structure is exactly what real far-OTM buying produces.

**The setup.** Track **1,000** purchases of far-OTM NIFTY weekly calls, each bought at an average premium of **₹30** (per unit), i.e., 30 × 65 = **₹1,950 per trade**. Total capital deployed = 1,000 × 1,950 = **₹19,50,000**. Costs are ignored (they would make the result worse).

**What happened.**

**Table 4.4 — Outcome distribution of 1,000 far-OTM call purchases (illustrative)**

| Outcome | Share | Trades | Average P&L per trade (₹) | Contribution (₹) |
| --- | ---: | ---: | ---: | ---: |
| Expired worthless | 80% | 800 | −1,950 | −15,60,000 |
| Small win | 15% | 150 | +1,300 | +1,95,000 |
| Big win (multi-bagger) | 5% | 50 | +7,800 | +3,90,000 |
| **Total** | 100% | 1,000 | | **−9,75,000** |

**The analysis.**

* **Win rate = 20%** (only 200 of 1,000 trades made money), and **80% were total losses**.
* **Expectancy per trade** = 0.80 × (−1,950) + 0.15 × (+1,300) + 0.05 × (+7,800) = −1,560 + 195 + 390 = **−₹975**.
* Across 1,000 trades the book lost **₹9,75,000 — a −50% return** on capital deployed, *even though* the occasional big win returned 4× its premium.

The reason is structural, and it is the whole point of this chapter: a far-OTM option is **100% time value**, a small payment for a low-probability event. The rare 4× winner cannot offset a base rate of 80% total losses. The lottery has negative expectancy by design — which is exactly why the *sellers* of these options, collecting that time value, are usually on the winning side over many expiries.

**The lesson.** Cheapness is not opportunity. Before buying any OTM option, state the specific move and deadline that would justify the time value you are paying, and be honest about its probability. If your only reason is "it's cheap," you are buying a lottery ticket with a negative expected value.

*(Takeaway: an option's price is information — a low premium is the market telling you the odds are low. Listen to it.)*

---

## 10. Chapter Summary

* Every premium = **intrinsic value** (max(0, Spot − Strike) for calls; max(0, Strike − Spot) for puts) **+ time value** (the rest).
* **Moneyness** runs from deep ITM (mostly intrinsic, moves like the future) to deep OTM (all time value, usually worthless).
* **Time value** is the price of optionality — the one-sided right to gain. It is **≥ 0 before expiry**, **zero at expiry**, and **peaks at the money**, where uncertainty is greatest.
* The four basic **payoff diagrams** show the core asymmetry: buyers risk only the premium; a short **call**'s loss is **unlimited** and a short **put**'s loss is **large** — far exceeding the premium collected.
* **Breakevens**: call = strike + premium; put = strike − premium.
* **Put–call parity** (`C − P = PV(F − K)`) binds calls, puts, and futures; it explains why the spot-ATM call is dearer than the put and keeps your pricing honest.
* An **OTM put is portfolio insurance**; time value is the price of the coverage, highest when uncertainty is highest.
* The **OTM lottery ticket** has negative expectancy — 100% time value, a low-probability bet whose rare wins cannot offset its frequent total losses.

---

## 11. Key Takeaways

* **Decompose before you trade:** know how much of any premium is intrinsic value (substance) versus time value (a bet on a move by a deadline).
* **Time value peaks at the money and decays to zero at expiry** — the central fact behind both selling income and buying decay.
* **Never mistake a cheap OTM option for a good one;** its low price is the market pricing low odds.
* **Respect the buyer/seller asymmetry** encoded in the four payoff diagrams — it dictates your risk, your margin, and your survival.

---

## 12. Practice Questions

**Q1 (Decomposition).** With NIFTY at 24,600, the `24400 CE` trades at ₹320. Find its intrinsic value, time value, and moneyness.

**Q2 (Decomposition).** With NIFTY at 24,600, the `24800 CE` trades at ₹120. Find its intrinsic value and time value. What does the answer tell you about the option?

**Q3 (Multiple choice).** Time value is greatest for options that are:
(a) deep in the money; (b) at the money; (c) deep out of the money; (d) already expired.

**Q4 (Payoff / breakeven).** You buy a `NIFTY 24500 CE` at ₹200. State the breakeven, maximum loss, and maximum profit (per unit).

**Q5 (Payoff — short).** You sell a `BANKNIFTY 52000 PE` at ₹300 (lot size 30). State the breakeven, maximum profit, and maximum loss, and compute the maximum profit in rupees.

**Q6 (P&L at expiry).** For the long `24600 CE` at ₹205, compute the P&L per unit if NIFTY expires at (a) 24,500, (b) 24,805, (c) 25,100.

**Q7 (Parity).** The future is 24,700. At the 24,600 strike the put trades at ₹150. Using `C − P ≈ F − K`, estimate the call premium.

**Q8 (Concept).** Explain in one or two sentences why a strike's call is usually more expensive than its put when the future is above the spot.

**Q9 (Expectancy).** A far-OTM option is bought at ₹40. Suppose it expires worthless 85% of the time and, the other 15%, returns an average net profit of ₹150 per unit. What is the expectancy per unit, and what does it imply?

**Q10 (Judgement).** A beginner says, "I'll buy deep-OTM weekly calls — they're cheap, so my risk is tiny." Give two reasons, using this chapter's ideas, why this reasoning is flawed.

---

## 13. Detailed Solutions

**A1.** Intrinsic value = 24,600 − 24,400 = **₹200**; time value = 320 − 200 = **₹120**; the spot is above the strike, so it is **in the money (ITM)**.

**A2.** Intrinsic value = max(0, 24,600 − 24,800) = **₹0**; time value = 120 − 0 = **₹120**. The option is **out of the money** and its premium is **entirely time value** — a payment purely for the chance of a move above 24,800.

**A3.** **(b) at the money.** Uncertainty about finishing in or out of the money is greatest there, so optionality — and time value — is maximised.

**A4.** Breakeven = 24,500 + 200 = **24,700**; maximum loss = **₹200** per unit (the premium); maximum profit = **unlimited** above 24,700.

**A5.** Breakeven = 52,000 − 300 = **51,650**; maximum profit = **₹300** per unit (the premium); maximum loss = large, up to 52,000 − 300 = **₹51,700** per unit (if the index fell to zero). Maximum profit in rupees = 300 × 30 = **₹9,000**.

**A6.** Long `24600 CE` at ₹205: (a) at 24,500 → max(0, 24,500 − 24,600) − 205 = **−₹205**; (b) at 24,805 → 205 − 205 = **₹0** (breakeven); (c) at 25,100 → 500 − 205 = **+₹295**.

**A7.** `C − P ≈ F − K = 24,700 − 24,600 = 100`, so `C ≈ P + 100 = 150 + 100 =` **₹250** (a touch less after discounting).

**A8.** By put–call parity, `C − P = PV(F − K)`. When the future is above the spot, `F − K` is positive at the spot strike, so `C − P > 0` — the call must be priced higher than the put to prevent an arbitrage using the synthetic future.

**A9.** Expectancy = 0.85 × (−40) + 0.15 × (+150) = −34 + 22.5 = **−₹11.5 per unit**. It is **negative**, so repeatedly buying such options loses money on average, despite the occasional win — the lottery-ticket trap.

**A10.** Two reasons: (i) A cheap OTM option is **100% time value**, a payment for a **low-probability** event — the low price reflects poor odds, not low risk; you can lose the entire premium, and usually will. (ii) You can be **right on direction and still lose** if the move does not clear the strike plus the time value paid before expiry. "Cheap" describes the price, not the quality of the bet, and the expectancy of such buying is typically negative.

---

## 14. Mini Glossary

* **Intrinsic value** — the in-the-money amount of an option: max(0, Spot − Strike) for calls, max(0, Strike − Spot) for puts; never negative. → this chapter.
* **Time value** — premium minus intrinsic value; the price of the option's remaining optionality; ≥ 0 before expiry, 0 at expiry. → this chapter.
* **Optionality** — the value of a one-sided right (gain if it moves your way, walk away if not) under uncertainty and remaining time. → this chapter.
* **Moneyness** — an option's position on the spectrum from deep ITM to deep OTM, set by the spot relative to the strike. → this chapter.
* **ITM / ATM / OTM** — in / at / out of the money. → this chapter.
* **Payoff diagram** — a plot of a position's expiry P&L against the underlying level; the "hockey-stick" graph. → this chapter.
* **Breakeven** — the underlying level at which a bought option exactly recovers its premium (strike ± premium). → this chapter.
* **Maximum loss / maximum profit** — the worst and best outcomes of a position; asymmetric between buyers and sellers. → this chapter.
* **Put–call parity** — the identity C − P = PV(F − K) linking a call, a put, and the future at the same strike and expiry. → this chapter.
* **Synthetic future** — a futures-equivalent position built from options (long call + short put at one strike). → this chapter.
* **Basis** — the gap between the futures price and the spot; tilts a strike's call value versus its put value. → this chapter.
* **Expectancy** — the probability-weighted average outcome of a trade; negative for the far-OTM lottery ticket. → this chapter.

---

<!-- End of Chapter 4 (Rev 2, current as of 4 Aug 2026). Rev 2 updates: NIFTY lot 75→65 and BANKNIFTY lot 35→30 (NSE Jan-2026 revision); intro expiry day corrected to Tuesday (NIFTY, since 1 Sep 2025). Lot-dependent numbers recomputed: NE3 (205×65=13,325); case study (30×65=1,950/trade; total ₹19,50,000; table −15,60,000/+1,95,000/+3,90,000; total −₹9,75,000; expectancy −₹975; still −50% return and 4× big-win premium — per-unit expectancy unchanged at −₹15); Q5/A5 (BANKNIFTY 300×30=₹9,000). Per-unit tables (4.1, 4.2, 4.3) and parity example (F=24,700, basis +100) have no lot dependence — unchanged. Costs ignored throughout, so Apr-2026 STT change does not affect numbers. Premium tables internally consistent (time value peaks ₹205 at ATM). Lottery-ticket case study labelled illustrative/representative, consistent with SEBI retail-loss findings. IV reserved for implied volatility. No forward references to later chapters. -->
