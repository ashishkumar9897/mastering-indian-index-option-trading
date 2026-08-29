<!-- Difficulty: Level 3/5 (Intermediate) — the hardest maths in the first third. Dependency: Chapter 5. Target length ~7,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision). r = 6.5% used illustratively (no current-rate claim; not changed, to preserve the worked BSM example). BSM math (d1=0.283, d2=0.261, C≈₹288.3) is lot-independent — only the lot-terms conversion updated (288.3×65≈₹18,740). No transaction costs, so the Apr-2026 STT change does not affect this chapter. Binomial trimmed to a single intuition pass (Edition 2). BSM worked in spot form (per architecture Required Math) and reconciled to the futures/Black-76 form. Risk-neutral caveat included. IV = implied volatility throughout. A short standard-normal table is provided so calculations are self-contained. -->

# Chapter 6 — Introduction to Options Pricing Models

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Explain the Black–Scholes–Merton (BSM) model conceptually — what it does and why it works — not just recite the formula.
2. Identify the five inputs BSM needs and know where to source each in the Indian market.
3. Calculate a NIFTY option's fair value with BSM, step by step.
4. State BSM's assumptions and the specific ways they break down for Indian index options.
5. Understand the binomial model as an intuition-builder and grasp risk-neutral pricing.
6. Understand how implied volatility is reverse-engineered from a market price.

> **Beginner Alert — This is the steepest chapter so far, and you may take it out of order.** Chapter 6 carries the heaviest mathematics in the first third of the book. If the formulas feel overwhelming on a first read, you may skip ahead to the next chapter (reading the option chain), which is concrete and practical, and return here once you are comfortable. Nothing later in *this* chapter is needed to read the chain. That said, the ideas here — especially implied volatility and risk-neutral pricing — pay off enormously, so do come back.

---

## 2. Introduction

In Chapter 5 you learned the six forces that move an option's price and the *direction* of each. This chapter answers the harder question: given all six, what is the option actually *worth*? For that you need a **pricing model** — a formula that takes the inputs and returns a fair premium.

The dominant model, the one embedded in every broker platform and analytics tool you will ever use, is **Black–Scholes–Merton**. You will almost never compute it by hand in live trading — the machine does that. But you must understand what it is doing, for three reasons. First, it turns the qualitative sensitivities of Chapter 5 into exact numbers (the Greeks, later in the book, are simply the derivatives of this formula). Second, it defines **implied volatility** — the single most important number on the option chain — which is nothing but BSM "run backwards." Third, knowing where the model is *wrong* is itself an edge: the gaps between the model's price and the market's price are where much of the professional game is played.

We will build BSM piece by piece, compute it fully for a real NIFTY option, meet the risk-neutral idea that makes it work, learn to invert it for implied volatility, and — crucially — map out exactly where it fails in the Indian market. Setting: **NIFTY at 24,600, lot size 65**, `r = 6.5%`.

---

## 3. Core Concepts

### 3.1 What a pricing model is, and why we need one

A pricing model answers a deceptively simple question: *what premium makes an option a fair bet for both buyer and seller, given today's information?* "Fair" here has a precise meaning — a price at which **no one can construct a risk-free profit** by combining the option with the underlying. This is the **no-arbitrage** principle, and it is the foundation of all option pricing.

The genius of BSM (published in 1973 by Fischer Black, Myron Scholes, and Robert Merton) was to show that an option's payoff can be *replicated* by continuously holding a precise, changing amount of the underlying plus cash. If you can replicate the option's payoff exactly, then the option must cost the same as the replicating portfolio — otherwise a risk-free profit exists. BSM computes the cost of that replicating portfolio. That is the whole idea; the formula is just the arithmetic.

---

### 3.2 The five inputs, and where to find them in India

BSM needs five numbers. Table 6.1 lists them with their Indian sources.

**Table 6.1 — The five BSM inputs and their Indian sources**

| Input | Symbol | What it is | Where to get it (India) |
| --- | :---: | --- | --- |
| Underlying | S (or F) | Index spot, or the future | NSE/BSE live quote; professionals use the **future** F |
| Strike | K | The contract's strike | The contract you choose |
| Time to expiry | T | Years to expiry | (Calendar days to expiry) ÷ 365 |
| Volatility | σ | Annualised volatility | The one input you must *estimate* (or read as IV) |
| Risk-free rate | r | Annualised risk-free rate | RBI-anchored: repo rate / short-term T-bill yield (~6.5% in the illustration) |

Notice the asymmetry: four of the five inputs are **observable** (you can look them up), but **volatility is not** — it is a forecast about the future. This is why volatility is the heart of options trading (Chapter 5) and why, in practice, we usually run the model *backwards*: we take the market premium as given and solve for the volatility the market is assuming (Section 3.6).

> **Market Note — Dividends are the "sixth input" you rarely enter directly.** Classic BSM as written assumes no dividends. For an index that pays them, you either add a dividend-yield term or — the Indian practitioner's shortcut — feed the **futures price F** instead of the spot, because F already embeds expected dividends through its basis (Chapter 2). We reconcile the two approaches in Section 3.8.

---

### 3.3 The Black–Scholes–Merton formula, piece by piece

This is the flagship of the chapter, so we take it slowly.

**What is it?** BSM gives the fair price of a European call as:

```
C = S·N(d₁) − K·e^(−rT)·N(d₂)                                (6.1)
```

*In words:* the call's value is **what you expect to receive** if it finishes in the money (the `S·N(d₁)` term) **minus what you expect to pay** for the shares/index at the strike (the discounted `K·e^(−rT)·N(d₂)` term).
*Units:* C, S, K in ₹/points; N(·) is a probability (dimensionless).

**The two helper terms** are:

```
d₁ = [ ln(S/K) + (r + σ²/2)·T ] / (σ·√T)                     (6.2)
d₂ = d₁ − σ·√T                                               (6.3)
```

**Why does it exist?** Because the two pieces of (6.1) are exactly the cost of the replicating portfolio from Section 3.1: hold `N(d₁)` units of the index (that is the hedge ratio, which you will later recognise as **Delta**) and borrow the present value of the strike weighted by `N(d₂)`. The formula is the price tag on that hedge.

**Why should a trader care?** Because (6.1) is the parent of everything that follows. The Greeks are its rates of change; implied volatility is it inverted; the option chain's theoretical prices are it, computed thousands of times a second. Understanding (6.1) is understanding the machinery under the entire market.

**Intuitive reading of each piece:**

* `S·N(d₁)` — the present value of receiving the index *if* the option ends in the money, weighted by a probability-like term.
* `K·e^(−rT)·N(d₂)` — the present value of paying the strike *if* exercised. The `e^(−rT)` discounts the future payment to today.
* The **difference** is the option's fair value — what is left after you net the expected receipt against the expected payment.

**The put** follows directly from put–call parity (Chapter 4): `P = C − S + K·e^(−rT)`, or equivalently `P = K·e^(−rT)·N(−d₂) − S·N(−d₁)`.

> **Math Made Simple — the shape of the formula.** Strip away the symbols and (6.1) says: *value = (chance-weighted thing you get) − (discounted, chance-weighted thing you pay).* The N(d) terms are the "chances," e^(−rT) is the discounting, and S and K are the amounts. Every option formula you will ever see is a variation on this one sentence.

---

### 3.4 d₁, d₂, and N(·) — what they actually mean

The forbidding-looking `d₁` and `d₂` have clean interpretations.

* **N(·) is the standard normal cumulative distribution function (CDF)** — for any value x, `N(x)` is the probability that a standard normal random variable is below x. It rises from 0 (far left) through 0.5 (at x = 0) to 1 (far right). You read it from a table or a calculator; a short table appears in Numerical Example 1.
* **d₂ and N(d₂):** `N(d₂)` is the **risk-neutral probability that the option finishes in the money** — that the index ends above the strike at expiry, under the model's pricing measure. The numerator of `d₁`/`d₂` measures how far in the money the option is (via `ln(S/K)`) plus the drift, scaled by the volatility over the remaining time (`σ√T`). More moneyness or more time pushes `d₂` up and the ITM probability toward 1.
* **d₁ and N(d₁):** `N(d₁)` is the option's **hedge ratio (Delta)** — how many units of the index you hold to replicate the call. It also acts as a probability-like weight on the receipt term.

The two differ only by `σ√T` (equation 6.3), which is the "one standard deviation of movement" over the option's life. Everything in BSM is ultimately organised around that quantity — how far the index might drift in the time remaining.

---

### 3.5 Risk-neutral pricing and a one-step binomial

Where do those probabilities come from, and why do they feel detached from any real forecast? The answer is **risk-neutral pricing**, and the cleanest way to see it is a single-step **binomial tree**.

**The toy example.** An index sits at 100. Over one period it can rise to 110 or fall to 95 — nothing in between. A 100-strike call therefore pays **10** if the index rises and **0** if it falls. Assume the risk-free rate over the period is ≈ 0 for simplicity.

The binomial model prices this by finding the **risk-neutral probability** `p`:

```
p = (e^(rΔt) − d) / (u − d)                                  (6.4)
```

with `u = 1.10` (up factor) and `d = 0.95` (down factor). With r ≈ 0:

```
p = (1 − 0.95) / (1.10 − 0.95) = 0.05 / 0.15 = 0.333
```

The call's value is the risk-neutral-probability-weighted payoff, discounted:

```
Call = e^(−rΔt) × [ p × 10 + (1 − p) × 0 ] ≈ 0.333 × 10 = ₹3.33
```

**The crucial insight — and the caveat.** The `p = 0.333` we used is **not** the real-world probability of the index rising. The *actual* chance of an up-move might be 60%. We deliberately ignore it. Risk-neutral pricing works by building a hedged, risk-free portfolio, and in that construction the real-world odds cancel out — what remains is `p`, an artificial probability under which every asset grows at the risk-free rate. It is a **pricing device, not a forecast.**

This carries a warning you must hold for the rest of the book:

> **Beginner Alert — "Probability of finishing ITM" is a risk-neutral statement.** When BSM (or your broker) says an option has, say, a 60% chance of expiring in the money via `N(d₂)`, that is the *risk-neutral* probability — the one that makes pricing arbitrage-free — not the real-world likelihood. Because of the equity risk premium and the market's demand for downside protection, the real-world odds differ (usually the real chance of a fall is lower than the puts' pricing implies). Use these model probabilities to price and hedge, not as literal forecasts of what will happen.

**From one step to BSM.** A single step is a toy. Chop the option's life into many small steps, with up and down factors set by the volatility — `u = e^(σ√Δt)` and `d = 1/u` — and the binomial tree's price **converges to the Black–Scholes price**. BSM is, in effect, the binomial model with infinitely many infinitesimal steps. For our NIFTY option in Numerical Example 1, that limit is ₹288.

**Why we do not dwell on the binomial.** The binomial model's practical advantage is handling **early exercise** (American options). Indian index options are **European** (Chapter 2), so that advantage does not apply. We use the binomial only for the intuition above and then work with BSM directly.

---

### 3.6 Implied volatility — running the model backwards

Four of BSM's inputs are observable; volatility is not. But the *market price* of the option is observable. So we invert the problem: **what volatility, fed into BSM, reproduces the market price?** That number is the **implied volatility (IV)** — the market's consensus forecast of volatility, extracted from the price.

There is no algebra to solve BSM for σ directly (σ is tangled inside the N(d) terms), so we solve it **iteratively**. The standard method, **Newton–Raphson**, uses the option's sensitivity to volatility (its Vega) as the step size:

1. Guess a σ, compute the BSM price.
2. Compare to the market price; note the gap.
3. Adjust σ by (gap ÷ Vega) — Vega tells you how many rupees the price moves per 1% of IV.
4. Repeat until the model price matches the market price.

We work a full example in Numerical Example 3. The output — IV — is the number professionals actually trade around, because it strips out everything observable and isolates the one thing in dispute: how much the market expects the index to move.

---

### 3.7 The assumptions — and where BSM breaks in India

BSM is built on idealised assumptions, and knowing where they fail is where model-users become traders. The main assumptions:

* **Continuous trading** — you can hedge at every instant.
* **No jumps** — prices move smoothly, never gapping.
* **Constant volatility** — σ is the same for all strikes and does not change.
* **Log-normal returns** — the index follows a smooth, bell-curve-of-log-returns path.
* **No transaction costs or taxes.**

Every one of these is violated in the Indian index market, in specific and important ways:

* **Overnight and event gaps break "continuous, no-jumps."** The market is shut from 3:30 PM to 9:15 AM, and it routinely gaps on global cues, results, and policy. You cannot hedge through a gap, and BSM's smooth path never happened.
* **Fat tails break "log-normal."** Real index returns have **fat tails (excess kurtosis)** — crashes and spikes far larger and more frequent than a bell curve predicts. The 2020 COVID fall (Chapter 1) was a many-sigma event that log-normal maths says should almost never occur.
* **The volatility smile/skew breaks "constant volatility."** If you back out IV from market prices across strikes, you do *not* get one number — you get a **skew**: OTM puts carry higher IV than OTM calls (Numerical Example 4). The market charges extra for crash protection, something a constant-σ model cannot express.
* **Event premium breaks "constant volatility" over time.** IV rises before events and crushes after (Chapter 5) — σ is anything but constant.

None of this makes BSM useless. It makes BSM a **common language**: a shared reference against which the market quotes its real opinion. The *deviations* from BSM — the skew, the event premium, the fat-tail pricing — are the information.

---

### 3.8 Forward versus spot — feed F, not S

One loose end from Chapter 2: we said Indian index options are priced off the **future**, yet formula (6.1) uses the **spot** S. Both are correct, and here is why.

Look again at `d₁` (6.2): the term `(r)·T` inside it grows the spot to its **forward value** `S·e^(rT)`. In other words, **the spot-form BSM already prices off the forward** — the risk-free growth term does the conversion internally. If you instead use the futures form (called **Black-76**), you feed F directly and drop the separate growth term:

```
C = e^(−rT) · [ F·N(d₁) − K·N(d₂) ],   with d₁ = [ln(F/K) + (σ²/2)T] / (σ√T)
```

When `F = S·e^(rT)` (no dividends), the two forms give **identical prices**. The practical advantage of the futures form is dividends: the observed future F already contains the market's real dividend expectations in its basis, so feeding F handles dividends automatically, with nothing to estimate.

> **Professional Insight — Why desks quote off the future.** Professionals feed the live futures price into the model rather than the spot, precisely because it sidesteps dividend estimation and matches how the option actually hedges (you hedge a call with the future, Chapter 2). When you later see analytics that price NIFTY options off "the 24,620 future," this is why — and it is the same BSM, just fed its more convenient input.

---

## 4. Examples (Real-World)

**Example 1 — The model as a shared language.** Every trader's screen shows a "theoretical price" and an IV for each strike, all computed from BSM. Two traders disagreeing about an option are really disagreeing about one input — volatility — because the other four are public facts. BSM reduces the argument to its essence.

**Example 2 — The skew as information.** On an ordinary NIFTY chain, the 5%-OTM put shows an IV of, say, 15% while the 5%-OTM call shows 11.5%. A constant-volatility model says these should be equal; the market says protection against a fall is worth more. That gap is the market pricing crash risk — information BSM alone cannot give you, revealed only by comparing model to market.

**Example 3 — When the model price is "wrong" on purpose.** The day before a major event, BSM (fed yesterday's volatility) may say a straddle is worth ₹300 while it trades at ₹380. The model is not broken; the market is pricing an elevated, forward-looking volatility the historical number does not contain. The ₹80 gap *is* the event premium.

---

## 5. Numerical Examples

Setting: NIFTY, lot 65, `r = 6.5%`. A short standard-normal table for the values we need:

| x | 0.26 | 0.27 | 0.28 | 0.29 |
| --- | --- | --- | --- | --- |
| N(x) | 0.6026 | 0.6064 | 0.6103 | 0.6141 |

### Numerical Example 1 — Full BSM calculation (NIFTY 24500 CE)

We price the `NIFTY 24500 CE` with **S = 24,600, K = 24,500, T = 10/365, r = 6.5%, σ = 13%**.

**Step 1 — the building blocks.**

```
T        = 10/365 = 0.027397
σ√T      = 0.13 × √0.027397 = 0.13 × 0.16552 = 0.021518
σ²/2     = 0.13² / 2 = 0.00845
ln(S/K)  = ln(24,600 / 24,500) = ln(1.004082) = 0.004073
```

**Step 2 — d₁ and d₂ (equations 6.2, 6.3).**

```
d₁ = [0.004073 + (0.065 + 0.00845)(0.027397)] / 0.021518
   = [0.004073 + 0.002012] / 0.021518
   = 0.006086 / 0.021518 = 0.283
d₂ = 0.283 − 0.021518 = 0.261
```

**Step 3 — the normal probabilities (from the table).**

```
N(d₁) = N(0.283) ≈ 0.6113
N(d₂) = N(0.261) ≈ 0.6031
```

**Step 4 — assemble the price (equation 6.1).**

```
e^(−rT)      = e^(−0.065 × 0.027397) = 0.99822
K·e^(−rT)    = 24,500 × 0.99822 = 24,456.4
C = S·N(d₁) − K·e^(−rT)·N(d₂)
  = 24,600 × 0.6113 − 24,456.4 × 0.6031
  = 15,038.0 − 14,749.7
  ≈ ₹288.3 per unit
```

**Sanity check.** Intrinsic value = 24,600 − 24,500 = ₹100; so time value ≈ ₹188 — a touch below the pure-ATM time value, exactly as expected for a slightly in-the-money option. The put, by parity, is `P = C − S + K·e^(−rT) = 288.3 − 24,600 + 24,456.4 = ₹144.7`. In lot terms the call is worth 288.3 × 65 ≈ **₹18,740**.

> **Math Made Simple — why a calculator may say ₹290, not ₹288.3.** The final step subtracts two large, nearly equal numbers (≈15,038 − ≈14,750), so the answer is extremely sensitive to the *fourth* decimal of N(·): an error of just 0.0001 in N(d₁) shifts the price by 24,600 × 0.0001 ≈ ₹2.5. Reading N(·) from a two-decimal table (as above) gives ≈ ₹288; a precise calculator, carrying N(d₁) ≈ 0.61134 and N(d₂) ≈ 0.60307, returns ≈ **₹290**. Both are "correct" — the gap is rounding, not error. The lesson: when pricing by hand, carry N(·) to at least four decimals, and never treat a hand-computed premium as exact to the rupee.

### Numerical Example 2 — The one-step binomial (intuition)

From Section 3.5: index at 100, up to 110 or down to 95, a 100-strike call paying 10 or 0, r ≈ 0.

```
p    = (1 − 0.95) / (1.10 − 0.95) = 0.333
Call = 0.333 × 10 + 0.667 × 0 = ₹3.33
```

The value uses the **risk-neutral** p = 0.333, not any real-world probability of the up-move. Refine into many small steps (`u = e^(σ√Δt)`) and this converges to the BSM value — for the NIFTY option above, to ₹288.

### Numerical Example 3 — Solving for implied volatility

The `24500 CE` above is worth ₹288.3 at σ = 13%. Suppose it actually **trades at ₹300** in the market. What volatility does the market imply?

* **Vega** (price change per 1% IV) for this option ≈ `S·√T·n(d₁)`, where `n(d₁) = 0.3833` (the normal density at d₁). So Vega ≈ 24,600 × 0.16552 × 0.3833 ≈ **₹1,561 per 1.00 of σ**, i.e., **≈ ₹15.6 per 1% of IV**.
* **Iterate (Newton–Raphson):** the market price (₹300) exceeds the model price at 13% (₹288.3) by ₹11.7. Step σ up by 11.7 ÷ 15.6 ≈ **0.75%**, to σ ≈ **13.75%**.
* Recompute BSM at 13.75%: the price rises to ≈ ₹300. Converged.

**The implied volatility is ≈ 13.75%.** The market is paying for a touch more volatility than our 13% guess. This backing-out is exactly what your broker does to display "IV" against every strike.

### Numerical Example 4 — The volatility smile (skew) across strikes

If BSM's constant-σ assumption held, backing out IV from every strike's market price would give one number. It does not. Table 6.2 shows a representative NIFTY chain (spot 24,600).

**Table 6.2 — Implied volatility by strike (illustrative; reveals the skew)**

| Strike | 23,600 | 24,000 | 24,200 | 24,600 (ATM) | 25,000 | 25,200 | 25,400 |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Implied volatility | 16.8% | 15.3% | 14.4% | 13.0% | 12.1% | 11.8% | 11.6% |

IV falls as the strike rises — lower strikes (OTM puts / crash protection) carry higher IV than higher strikes (OTM calls). This downward-sloping **skew** is the market's statement that a crash is feared more than a melt-up. A single-σ model cannot represent this; the skew is precisely where BSM's simplification and the market's real opinion diverge.

### Numerical Example 5 — Price is near-linear in volatility (for the ATM)

Holding everything else fixed and varying σ, the option price rises almost linearly (because Vega is roughly stable across this range for a near-the-money option), ≈ ₹15.6 per 1% IV:

| σ | 10% | 12% | 13% | 14% | 16% | 18% | 20% |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| BSM price (₹, approx.) | 241 | 273 | 288 | 304 | 335 | 366 | 397 |

The near-straight line is why "a 1% rise in IV adds about ₹15.6" is a usable rule of thumb near the money — and a preview of Vega.

---

## 6. Calculations (the reusable recipes)

**(a) Black–Scholes call (spot form)**

```
C = S·N(d₁) − K·e^(−rT)·N(d₂)
d₁ = [ln(S/K) + (r + σ²/2)T] / (σ√T)
d₂ = d₁ − σ√T
```

**(b) Black–Scholes put (via parity)**

```
P = C − S + K·e^(−rT)
```

**(c) Futures (Black-76) form — feed F, dividends handled automatically**

```
C = e^(−rT)·[F·N(d₁) − K·N(d₂)],  d₁ = [ln(F/K) + (σ²/2)T]/(σ√T)
(identical to the spot form when F = S·e^(rT))
```

**(d) One-step binomial (risk-neutral pricing)**

```
p = (e^(rΔt) − d)/(u − d);   Value = e^(−rΔt)·[p·(up payoff) + (1−p)·(down payoff)]
Many small steps with u = e^(σ√Δt), d = 1/u  →  converges to BSM
```

**(e) Implied volatility (Newton–Raphson step)**

```
σ_next = σ_guess + (Market price − Model price) ÷ Vega
Vega ≈ S·√T·n(d₁)   (n = standard normal density);  per 1% IV, divide by 100
```

---

## 7. Practical Insights

* **You will not compute BSM by hand — but you must know what it computes.** The value of this chapter is not manual calculation; it is understanding that IV, the Greeks, and every "theoretical price" on your screen come from this one formula.
* **Trade implied volatility, not the model price.** The model price is only as good as the σ you feed it. The market's own σ — implied volatility — is the number that matters, and it is BSM inverted.
* **The model's errors are the opportunity.** The skew, the event premium, and fat-tail pricing are all places where the market disagrees with constant-σ BSM. Learning to read those disagreements is more valuable than the formula itself.
* **Feed the future.** Using the live futures price (Black-76) sidesteps dividend estimation and matches how options hedge. It is the same BSM with a cleaner input.
* **Respect the gaps BSM ignores.** The model assumes smooth, continuous, hedgeable markets. India gaps overnight and on events, and its tails are fat. Never let a model price lull you into believing a large move "cannot" happen.

> **Professional Insight — The model is a ruler, not a crystal ball.** Professionals do not use BSM to predict prices; they use it to *measure* — to convert messy premiums into a common unit (IV) they can compare across strikes, expiries, and time. The trading decisions come from comparing those measurements, not from trusting the model's price as truth.

---

## 8. Common Mistakes

* **Believing the model price is the "right" price.** BSM is a reference built on false-in-India assumptions; the market's price reflects skew, event premium, and fat tails the model omits. When they differ, the market is usually telling you something, not making an error.
* **Reading N(d₂) as a real-world probability.** It is the *risk-neutral* probability of finishing ITM — a pricing device, not a forecast of what will actually happen.
* **Feeding the spot and forgetting dividends/carry.** For anything beyond very short tenors, use the future (or a dividend adjustment); the raw spot mis-prices via the basis.
* **Assuming one volatility fits all strikes.** The skew is real; a single σ across the chain contradicts the market and will mis-price OTM options, especially puts.
* **Trusting the model through gaps.** BSM assumes continuous hedging; you cannot hedge through the overnight or event gaps that define Indian trading, and its thin tails understate crash risk.

---

## 9. Case Study — "Why the Model Price Differs from the Market Price"

**Context.** New traders, on discovering BSM, often "catch" the market being wrong: their calculator says a NIFTY option is worth ₹300, but it trades at ₹360, and they conclude the option is "overpriced" and sell it. Usually, the market is right and the trader has mis-modelled. This case shows the three most common reasons model and market diverge in India. Figures are **illustrative** but typical.

**Situation 1 — Event premium (the model is stale on volatility).** Two days before a major policy event, a trader prices a NIFTY ATM straddle with BSM using the recent *historical* volatility of 12%, getting ₹300. The market quotes ₹380. The gap is not an error: the market is pricing **forward-looking, event-elevated IV** (say 15–16%), because a big move is expected. The trader who "sells the overpriced straddle" is really selling event volatility — and if the move that arrives exceeds what ₹380 priced, they lose. *The model used the wrong σ; the market used the right one.*

**Situation 2 — Overnight gap risk (the model assumes continuity).** A far-OTM NIFTY put looks "too expensive" versus BSM. But BSM assumes smooth, continuous, hedgeable prices; the market knows the index can **gap overnight or on global cues**, and that a seller cannot hedge through the gap. The extra premium is compensation for un-hedgeable jump risk — a real cost the smooth model cannot see. *The model omitted gap risk; the market priced it.*

**Situation 3 — Supply–demand and the skew (the model assumes one volatility).** OTM puts persistently trade at higher IV than OTM calls because institutions and investors constantly **buy downside protection**, pushing up put prices, while call demand is thinner. BSM with a single σ says they should match; the market's skew says protection is dearer. A trader who ignores the skew and sells "cheap-looking" OTM calls against "expensive-looking" OTM puts is trading against a persistent, rational imbalance. *The model assumed constant σ; the market expressed a skew.*

**The analysis.** In all three cases the model was not "beaten" — it was *mis-fed* or *too simple*. Event premium is a volatility-input problem; gap risk is a broken-assumption problem; skew is a constant-σ problem. The professional does not treat model–market gaps as free money; they diagnose *which* assumption the gap represents, and only then decide whether it is an opportunity or a warning.

**The lesson.** BSM tells you what an option *would* be worth in an idealised world. The market tells you what it *is* worth in the real one. The distance between them is not noise — it is event premium, gap risk, and skew, each of which you can now name.

*(Takeaway: when the model and the market disagree, assume the market knows something your inputs or assumptions have missed — and find out what.)*

---

## 10. Chapter Summary

* A pricing model finds the **no-arbitrage** fair value; BSM does so by pricing the portfolio that **replicates** the option's payoff.
* **BSM:** `C = S·N(d₁) − K·e^(−rT)·N(d₂)` — the chance-weighted receipt minus the discounted, chance-weighted payment; the put follows from parity.
* Its **five inputs** are S (or F), K, T, σ, r; four are observable, but **volatility must be estimated** — which is why we usually run the model backwards.
* `N(d₂)` is the **risk-neutral** probability of finishing ITM and `N(d₁)` is the hedge ratio (Delta); the risk-neutral probability is a **pricing device, not a forecast**.
* The **binomial model** (risk-neutral p) builds the intuition and converges to BSM; its early-exercise advantage does not apply to European index options, so we use BSM directly.
* **Implied volatility** is BSM inverted — the market's σ, solved iteratively (Newton–Raphson, stepping by gap ÷ Vega); it is the number professionals trade.
* BSM's assumptions **fail in India** via overnight/event **gaps**, **fat tails**, and the **volatility skew**; the deviations from the model are information, not error.
* Feed the **future (Black-76)** to handle dividends automatically; it equals the spot form when `F = S·e^(rT)`.

---

## 11. Key Takeaways

* **Understand what BSM computes; let the machine do the arithmetic.** Your job is to read IV and the model's limits, not to grind the formula by hand.
* **Trade implied volatility, not the model price** — the price is only as good as the σ you assume, and IV is the market's own answer.
* **Treat "probability of ITM" as risk-neutral,** a pricing convention, not a real-world forecast.
* **Read model–market gaps as event premium, gap risk, or skew** — diagnose which before calling anything mispriced, and never trust a smooth model through a market that jumps.

---

## 12. Practice Questions

**Q1 (Concept).** In one or two sentences, what does a pricing model compute, and what principle guarantees the answer is "fair"?

**Q2 (Inputs).** List BSM's five inputs. Which one is not directly observable, and how do traders get around that?

**Q3 (Interpretation).** State the meaning of `N(d₁)` and `N(d₂)` in BSM.

**Q4 (Calculation).** Using the standard-normal table in Section 5 and the worked steps, confirm d₁, d₂, N(d₁), N(d₂) and the price for the `24500 CE` (S = 24,600, K = 24,500, T = 10/365, r = 6.5%, σ = 13%).

**Q5 (Binomial).** An index at 200 can go to 220 or 180 in one period; r ≈ 0. Find the risk-neutral probability p and the value of a 200-strike call.

**Q6 (Risk-neutral).** A model says an option has a 70% chance (via N(d₂)) of finishing ITM. Why should you *not* treat this as "there is a 70% real-world chance the index ends above the strike"?

**Q7 (Implied volatility).** The `24500 CE` is worth ₹288 at σ = 13%, with Vega ≈ ₹15.6 per 1% IV. If it trades at ₹272, estimate the implied volatility in one Newton–Raphson step.

**Q8 (Skew).** On a NIFTY chain, the 24,000 put shows 15.3% IV and the 25,200 call shows 11.8%. What does this pattern tell you, and which BSM assumption does it violate?

**Q9 (Assumptions).** Name two BSM assumptions that fail specifically in the Indian index market and give a one-line reason for each.

**Q10 (Judgement).** A trader's calculator prices a straddle at ₹300 the day before the Budget; it trades at ₹380, so the trader sells it as "overpriced." Explain the likely flaw in this reasoning.

---

## 13. Detailed Solutions

**A1.** A pricing model computes the fair premium at which neither buyer nor seller can construct a risk-free profit — the **no-arbitrage** price — by valuing the portfolio that replicates the option's payoff.

**A2.** Inputs: **S (or F), K, T, σ, r.** Volatility (σ) is **not directly observable**; traders either estimate it (from historical volatility) or, more usefully, back it out of the market price as **implied volatility**.

**A3.** `N(d₁)` is the option's **hedge ratio (Delta)** — units of the underlying needed to replicate the call — and a probability-like weight on the receipt term. `N(d₂)` is the **risk-neutral probability that the option finishes in the money**.

**A4.** d₁ = [0.004073 + (0.07345)(0.027397)] / 0.021518 = 0.006086 / 0.021518 = **0.283**; d₂ = 0.283 − 0.021518 = **0.261**; N(0.283) ≈ **0.6113**, N(0.261) ≈ **0.6031**; C = 24,600 × 0.6113 − (24,500 × 0.99822) × 0.6031 = 15,038.0 − 14,749.7 ≈ **₹288.3**.

**A5.** u = 220/200 = 1.10, d = 180/200 = 0.90, r ≈ 0. p = (1 − 0.90)/(1.10 − 0.90) = 0.10/0.20 = **0.50**. Call payoff: 20 (up), 0 (down). Value = 0.50 × 20 + 0.50 × 0 = **₹10**.

**A6.** Because `N(d₂)` is the **risk-neutral** probability — computed under the pricing measure where all assets drift at the risk-free rate — not the real-world probability. The real-world odds differ because of the equity risk premium and demand for downside protection; the model number is for pricing and hedging, not forecasting.

**A7.** Gap = market − model = 272 − 288 = −₹16. Step = −16 ÷ 15.6 ≈ **−1.0%**, so σ ≈ 13% − 1.0% = **≈ 12.0%**. (The lower market price implies lower volatility.)

**A8.** Lower strikes carry higher IV than higher strikes — a **downward skew** — meaning the market prices downside (crash) protection more richly than upside. It violates BSM's assumption of **constant volatility across strikes**.

**A9.** Any two, e.g.: **No jumps / continuous trading** — the market shuts overnight and gaps on events, so it cannot be hedged continuously. **Log-normal returns** — real index returns have **fat tails**, with crashes far larger and more frequent than the bell curve allows. (Also acceptable: **constant volatility** — contradicted by the skew and by event-driven IV changes.)

**A10.** The trader almost certainly priced the straddle with **stale historical volatility**, while the market is pricing **forward-looking, event-elevated implied volatility** ahead of the Budget. The ₹80 gap is the **event premium**, not mispricing. Selling it is selling event volatility; if the actual post-Budget move exceeds what ₹380 priced, the trade loses. The flaw is treating a wrong σ input as proof the market is wrong.

---

## 14. Mini Glossary

* **Pricing model** — a formula that returns an option's fair (no-arbitrage) premium from its inputs. → this chapter.
* **No-arbitrage** — the principle that prices must leave no risk-free profit; the basis of option pricing. → this chapter.
* **Replication** — reproducing an option's payoff with a changing position in the underlying plus cash; its cost is the option's fair price. → this chapter.
* **Black–Scholes–Merton (BSM)** — the standard European option pricing formula, `C = S·N(d₁) − K·e^(−rT)·N(d₂)`. → this chapter.
* **d₁, d₂** — BSM's auxiliary terms; d₁ underlies the hedge ratio, d₂ the ITM probability. → this chapter.
* **N(·)** — the standard normal cumulative distribution function; converts d-values into probabilities. → this chapter.
* **Risk-neutral pricing** — valuing by discounting expected payoffs under an artificial probability where all assets grow at the risk-free rate; a pricing device, not a forecast. → this chapter.
* **Risk-neutral probability (p, N(d₂))** — the probability used in pricing, distinct from real-world odds. → this chapter.
* **Binomial model** — a step-by-step tree that prices via risk-neutral probabilities and converges to BSM. → this chapter.
* **Implied volatility (IV)** — the volatility that makes BSM match the market price; the market's forecast, found by inverting the model. → this chapter.
* **Newton–Raphson** — the iterative method for solving BSM backwards for IV, stepping by (price gap ÷ Vega). → this chapter.
* **Volatility skew** — the pattern of IV differing by strike (higher for lower strikes in equity indices); violates BSM's constant-σ assumption. → this chapter.
* **Fat tails (kurtosis)** — the tendency of real returns to have more extreme moves than a normal distribution predicts. → this chapter.
* **Black-76** — the futures form of BSM; feed F to handle dividends and carry automatically. → this chapter.

---

<!-- End of Chapter 6 (Rev 2, current as of 4 Aug 2026). Rev 2 updates: NIFTY lot 75→65 (NSE Jan-2026 revision) in setting lines and lot-terms conversion (288.3×65≈₹18,740); fixed garbled NE1 heading ("15… using the exercise inputs" → clean title). BSM worked in spot form to the architecture's Required Math; d1=0.283, d2=0.261, N=0.6113/0.6031, C≈₹288.3 (all lot-independent, unchanged). Verified against put via parity (P≈₹144.7). r=6.5% illustrative (unchanged). No transaction costs → Apr-2026 STT change not applicable. Binomial kept to a one-step intuition pass (Edition 2 trim) plus convergence statement. Risk-neutral caveat included. Forward/Black-76 reconciliation closes the Ch2 loop. Standard-normal values provided inline. IV = implied volatility throughout. No forward chapter-number references. -->
