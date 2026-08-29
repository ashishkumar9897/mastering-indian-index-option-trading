<!-- Difficulty: Level 2/5 (Beginner-Intermediate). Dependency: Chapter 4. Target length ~8,000 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision). r = 6.5% used illustratively (no current-rate claim). No transaction costs in examples, so the Apr-2026 STT change does not affect this chapter's numbers. Budget-day case is HISTORICAL (23 July 2024, a Tuesday; that week's NIFTY expiry Thu 25 Jul 2024) — kept on 2024 rules, not the post-Sep-2025 Tuesday cycle. Qualitative sensitivities only (+/- signs; no partial derivatives). Time-value decay modelled with the √T relationship for illustration. The Greeks are named as previews (Delta/Theta/Vega/Rho) but not deep-dived. IV reserved for implied volatility; intrinsic value spelled out. -->

# Chapter 5 — What Moves an Option's Price: The Six Factors

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Identify the six factors that determine an option's premium and explain what each one does.
2. State the direction — and the rough magnitude — of each factor's effect on calls and puts.
3. Judge which factor is likely to dominate a premium's movement in different market conditions.
4. Recognise each factor's formal sensitivity by name — Delta, Theta, Vega, Rho — so you are ready for the measures that quantify them later in the book.

Chapter 4 split a premium into intrinsic value and time value. This chapter asks the next question every trader asks after their first trade: *why did the price change?* The answer is always some combination of six forces. Learn them, and "the option moved and I don't know why" stops happening.

---

## 2. Introduction

A trader buys a NIFTY at-the-money call the afternoon before the Union Budget. The next morning NIFTY opens 120 points higher — exactly the direction they wanted — and yet the call is worth *less* than they paid. They are baffled, and, like many before them, they reach for the word "manipulation."

Nothing was manipulated. Three of the six forces that move an option's price pushed against the trader at once: the fall in implied volatility after the event ("IV crush"), one day of time decay, and the fact that even a 120-point gap was smaller than the move the elevated premium had been pricing in. The favourable *direction* was real; it was simply outvoted.

This is the chapter that prevents that confusion. Every rupee of change in an option's premium comes from movement in one or more of **six factors**: the underlying price, the strike, time to expiry, volatility, interest rates, and dividends. Two of them (volatility and time) are the ones retail traders chronically ignore — and they are precisely the two that most often decide whether a "correct" trade makes or loses money.

We will treat the factors qualitatively here — the direction and rough size of each effect — and leave the exact measurement to the Greeks later in the book. The goal is intuition solid enough that you can look at a premium change and name the culprit. Setting throughout: **NIFTY at 24,600, lot size 65**, illustrative but realistic premiums.

---

## 3. Core Concepts

### 3.1 The six factors, at a glance

An option's fair premium is a function of six inputs:

1. **Underlying price (S)** — the level of the index (in practice, the future, per Chapter 2).
2. **Strike price (K)** — fixed for a given contract; matters when comparing strikes.
3. **Time to expiry (T)** — how long the option has left to live.
4. **Volatility (σ)** — how much the index is expected to move; the market's estimate is the *implied volatility*.
5. **Interest rate (r)** — the risk-free rate, anchored in India by the RBI's policy rates.
6. **Dividends (q)** — dividends expected from the index constituents before expiry.

Of these, only one is truly under nobody's direct control and constantly in motion in ways that surprise people: **volatility**. It is the factor this chapter treats as king, and the one Section 3.4 gives the full framework.

---

### 3.2 The sensitivity matrix — direction of each effect

For each factor we ask: if it *increases* (all else held constant), does the premium rise or fall? Table 5.1 answers for both calls and puts. A **+** means the premium rises, **−** means it falls, and the size (large/small) is noted. A *decrease* in any factor simply flips the sign.

**Table 5.1 — Effect on premium when each factor increases (all else constant)**

| Factor increases → | Call | Put | Magnitude (short-dated index option) |
| --- | :---: | :---: | --- |
| **Underlying price (S)** | **+** | **−** | Large |
| **Strike price (K)** | **−** | **+** | Large (comparing strikes) |
| **Time to expiry (T)** | **+** | **+** | Moderate–large |
| **Volatility (σ)** | **+** | **+** | Large |
| **Interest rate (r)** | **+** | **−** | Small |
| **Dividends (q)** | **−** | **+** | Small (rare for index) |

Read the table carefully, because two rows behave differently from the rest:

* **Time and volatility raise *both* calls and puts.** More time and more expected movement increase optionality on both sides — good news for every buyer, bad for every seller. (Contrast this with price, rate, and dividends, which help one side and hurt the other.)
* **Strike is not a "moving" factor for a held option** — it is fixed the moment you choose a contract. It appears here because it explains why, across the chain, higher-strike calls are cheaper and higher-strike puts dearer.

> **Beginner Alert — "All else constant" almost never happens.** The matrix isolates one factor at a time, which is how you *learn* the effects. In the real market several factors move together — as in the Budget-day story — and the net premium change is their tug-of-war. The skill this chapter builds is spotting *which* factor won.

---

### 3.3 Time to expiry — and why decay accelerates

Time is the one factor guaranteed to move: every day, T shrinks by one day, and with it the option's **time value** (Chapter 4). The loss of premium purely from the passage of time is what the Greek **Theta** will measure. Two features matter now.

**Both calls and puts lose time value as expiry nears.** More time means more chance for a favourable move, so time value is a decreasing function of how little time is left.

**The decay is non-linear — it accelerates.** Time value does not bleed away evenly; it drains slowly at first and then rushes out in the final days. A useful mental model (introduced here conceptually, not derived) is that an at-the-money option's time value shrinks roughly with the **square root of the time remaining**:

```
Time value ≈ A × √T        (A is a constant for a given option and volatility)
```

Because of the square root, the *per-day* loss grows as expiry approaches. Table 5.2 makes this concrete for an ATM NIFTY call whose time value is ₹210 at 30 days, with the underlying held flat.

**Table 5.2 — ATM time value decay with the underlying flat (illustrative, √T model)**

| Days to expiry | Time value (₹) | Decay over the interval | Decay per day (₹) |
| ---: | ---: | --- | ---: |
| 30 | 210.0 | — | — |
| 20 | 171.4 | 30 → 20 | 3.9 |
| 10 | 121.2 | 20 → 10 | 5.0 |
| 5 | 85.7 | 10 → 5 | 7.1 |
| 3 | 66.4 | 5 → 3 | 9.7 |
| 1 | 38.3 | 3 → 1 | 14.1 |
| 0 | 0.0 | 1 → 0 | 38.3 |

The per-day decay climbs from under ₹4 a day a month out to ₹38 on the final day — a tenfold acceleration. This single table explains why holding a long option "just a bit longer" near expiry is so punishing, and why option *sellers* concentrate their activity in the last days where the decay they collect is fastest.

> **Market Note — Weekly options decay about twice as fast per day as monthlies.** Under the √T rule, a monthly ATM option (≈28 days) carries about twice the time value of a weekly (≈7 days) — because √28 ≈ 2 × √7 — but it must decay over four times as many days. The result: the *weekly* loses time value roughly **twice as fast per day**. India's weekly NIFTY options are, by construction, high-decay instruments. We quantify this in Numerical Example 2.

---

### 3.4 Volatility — the misunderstood king

Volatility deserves the full framework, because it is the factor that most often decides an option trade and the one beginners understand least.

**What is it?** Volatility is a measure of how much the index is expected to move, up or down, over a period — expressed as an annualised percentage. The market's forward-looking estimate, embedded in option prices, is the **implied volatility (IV)**; the market-wide gauge for NIFTY is the **India VIX**.

**Why does it exist as a price factor?** Because an option pays off only if the index moves far enough. The *more* the index is expected to swing, the more likely the option finishes deep in the money — so the more it is worth. Volatility is, quite literally, the price of expected movement.

**Why should a trader care?** Because IV can change violently and independently of price, and it moves *both* calls and puts the same way. A spike in IV inflates every premium (great for holders, painful for sellers); a collapse in IV — the "IV crush" after an event — deflates every premium, which is how an option buyer can be right on direction and still lose (the introduction's trader).

**Intuitive explanation.** Volatility is the "weather forecast" priced into insurance. When a storm is expected, all insurance gets dearer regardless of which house is being insured; once the storm passes and the sky clears, premiums fall for everyone. IV is that forecast, and option premiums rise and fall with it.

**Numerical feel.** For an at-the-money option, the premium is roughly *proportional* to IV. With NIFTY at 24,600 and 7 days to expiry, an ATM call worth about **₹177 at 13% IV** is worth about **₹273 at 20% IV** — a 54% jump in premium from a 54% jump in IV, *with the index unchanged* (worked in Numerical Example 3). This is the formal sensitivity the Greek **Vega** will measure.

**Professional interpretation.** Professionals frame almost everything in volatility terms: is IV *rich* or *cheap* relative to how much the index is actually likely to move? They buy options when IV looks cheap and sell when it looks rich, often with little directional view at all. To a professional, "the option went up" is an incomplete statement until you say how much came from price and how much from IV.

**Common mistake.** Buying options right before a big scheduled event "because a big move is coming." By then the event is already priced in through elevated IV; when the event passes, the IV crush frequently costs the buyer more than the move earns them.

**Practical takeaway.** **Before you trade, ask whether volatility is high or low and which way it is likely to move — it will often matter more than direction.** Volatility is not background noise; for a short-dated option it is frequently the main event.

---

### 3.5 Interest rate and dividends — the small factors

The last two factors are real but minor for the short-dated index options most readers will trade.

**Interest rate (r).** A higher risk-free rate slightly *raises* calls and *lowers* puts, through the cost of carrying the position (it reduces the present value of the strike you would pay). In India the anchor is the **RBI repo rate** and short-term government yields. The effect — the Greek **Rho** — is tiny for weekly options and only becomes noticeable for options a few months out. As a number: a 100 basis-point change in rates moves a 60-day ATM NIFTY option's fair value by only about ₹20 per unit, and a weekly option by a rupee or two (Numerical Example 4).

**Dividends (q).** Higher expected dividends *lower* calls and *raise* puts. For index options this rarely matters day to day, because the index is traded through the **future**, which already embeds expected dividends in its basis (Chapter 2). Dividends make a visible dent only around dividend-heavy stretches, and even then modestly for short tenors.

> **Market Note — Why you can usually ignore r and q, but should not forget them.** For the weekly and monthly NIFTY options that dominate Indian trading, rate and dividend effects are dwarfed by price, time, and volatility. But for longer-dated positions, and when the RBI is actively changing policy, Rho is no longer negligible. "Small" is not "zero."

---

### 3.6 The dominance hierarchy — what actually decides your P&L

New traders fixate on **direction** — will the index go up or down? — and under-weight time and volatility. Yet for a short-dated option, on a typical day, the premium change is often dominated *not* by the modest index drift the trader watched, but by:

* **Volatility changes** — an IV move of a few points can swamp a small index move (and does, around events); and
* **Time decay** — a day's decay, accelerating near expiry, quietly erodes every long position.

The practical hierarchy to carry, especially for short-dated options, is: **volatility and time frequently overwhelm small directional moves.** This is the mechanism behind Chapter 4's "right on direction, wrong on P&L." It does not mean price is unimportant — a large, fast move dominates everything (that is Delta and its acceleration at work). It means that the two factors beginners ignore are the two that most often surprise them.

The order of your *attention*, then, should roughly match the order of *impact*: respect volatility first, time second, and never assume that being right on direction is the same as being right on the trade.

> **Professional Insight — Attribute every P&L to a factor.** After a trading day, a professional does not just note "+₹8,000." They decompose it: how much came from the index moving (price), how much from IV changing (volatility), how much from a day passing (time)? Building this habit now — even qualitatively — is how you turn confusing outcomes into learning, and it is exactly what the Greeks will let you do precisely later.

---

## 4. Examples (Real-World)

**Example 1 — Time decay in isolation.** Over a quiet 30-day stretch with NIFTY drifting sideways, an ATM call bleeds from ₹210 of time value toward zero, losing value faster each week (Table 5.2). Nothing "happened" to the index — time alone did the damage. This is the pure Theta experience.

**Example 2 — Volatility in isolation.** On a day NIFTY closes almost exactly flat but India VIX jumps from 13 to 16 ahead of a policy announcement, *every* ATM premium rises — calls and puts together. A trader short a straddle loses money on a flat day; a trader long options gains. Price did nothing; volatility did everything.

**Example 3 — The tug-of-war.** The introduction's Budget-morning call: the index gapped up (price factor, +), but IV collapsed (volatility, −) and a day passed (time, −). The two negatives outweighed the one positive, and the "correct" call lost. Real premium changes are almost always this kind of contest.

---

## 5. Numerical Examples

Setting: **NIFTY 24,600, lot 65**, illustrative premiums.

### Numerical Example 1 — Reading the sensitivity signs

You hold a NIFTY ATM call. Overnight, three things change: the future rises 50 points (S ↑), one day passes (T ↓), and India VIX falls 1 point (σ ↓). Using Table 5.1:

* S ↑ → call **+** (helps you).
* T ↓ → call **−** (hurts you; time value lost).
* σ ↓ → call **−** (hurts you).

Two of three forces oppose your long call, so a small up-move can still leave you down — the sign table predicts the direction of the surprise before you even open the platform.

### Numerical Example 2 — Weekly versus monthly decay per day

Using the √T model with the same constant as Table 5.2 (A ≈ 38.34):

* Monthly ATM (28 days): time value ≈ 38.34 × √28 ≈ **₹203** → average decay ≈ 203 ÷ 28 ≈ **₹7.3 per day**.
* Weekly ATM (7 days): time value ≈ 38.34 × √7 ≈ **₹101** → average decay ≈ 101 ÷ 7 ≈ **₹14.4 per day**.

The monthly costs about twice the weekly to buy, but the **weekly decays roughly twice as fast per day** — the mathematical reason weekly options are prized by sellers and dangerous for complacent buyers.

### Numerical Example 3 — Volatility moves a flat market

ATM call, 7 days to expiry, index unchanged at 24,600. Using the at-the-money approximation (premium ≈ 0.4 × S × σ × √T):

* At **σ = 13%**: ≈ 0.4 × 24,600 × 0.13 × √(7/365) ≈ 0.4 × 24,600 × 0.13 × 0.1385 ≈ **₹177**.
* At **σ = 20%**: ≈ 0.4 × 24,600 × 0.20 × 0.1385 ≈ **₹273**.

A jump in IV from 13% to 20% lifts the ATM premium from ~₹177 to ~₹273 — **+54%** — with the index perfectly flat. In lot terms that is (273 − 177) × 65 = **₹6,240** of premium change created by volatility alone. A 10% IV rise (13% → 14.3%) would add roughly 10%, about ₹18 per unit.

### Numerical Example 4 — The small interest-rate effect

The present value of the strike is `PV(K) = K × e^(−rT)`. For K = 24,600 and T = 60/365:

* At r = 6.5%: PV(K) = 24,600 × e^(−0.065 × 0.1644) ≈ 24,600 × 0.98937 ≈ **24,338.5**.
* At r = 7.5%: PV(K) = 24,600 × e^(−0.075 × 0.1644) ≈ 24,600 × 0.98775 ≈ **24,298.6**.

A 100 bps rate rise lowers PV(K) by about ₹40, which raises a 60-day ATM call's fair value by roughly **₹20** (and lowers the put by about the same). For a *weekly* option the effect is a rupee or two — negligible against the ₹96 that volatility moved in Example 3.

---

## 6. Calculations (the reusable recipes)

**(a) Directional sensitivity (qualitative signs, factor increasing)**

```
S ↑ : Call +, Put −      K ↑ : Call −, Put +      T ↑ : Call +, Put +
σ ↑ : Call +, Put +      r ↑ : Call +, Put −      q ↑ : Call −, Put +
(A decrease in any factor flips the sign.)
```

**(b) Non-linear time decay (ATM, conceptual)**

```
Time value ≈ A × √T        →   per-day decay grows as T → 0
```

**(c) Present value of the strike (interest-rate channel)**

```
PV(K) = K × e^(−rT)        →   higher r lowers PV(K) → raises calls, lowers puts
```

**(d) At-the-money premium feel (rough)**

```
ATM premium ≈ 0.4 × S × σ × √T      →   premium scales roughly with IV and with √T
```

*(These are teaching approximations. The exact measures — Delta, Theta, Vega, Rho — are developed later in the book.)*

---

## 7. Practical Insights

* **Name the culprit for every premium move.** Was it price (S), time (T), or volatility (σ)? Ninety per cent of the time it is one of these three. Diagnosing it turns confusion into a lesson.
* **Volatility and time are the "silent" factors.** They move premiums even when the index sits still, and they are the two beginners ignore. Give them at least as much attention as direction.
* **Weekly options are high-decay by design.** If you *buy* them, you are fighting the fastest time decay in the market; if you *sell* them, that decay is your income — but with correspondingly sharp risk near expiry.
* **Do not buy into elevated IV before an event and expect the move to save you.** The event is already priced; the IV crush afterwards often outweighs the move.
* **Treat r and q as small, not absent.** They barely register on weeklies but matter for longer-dated positions and around active RBI policy.

---

## 8. Common Mistakes

* **Watching only direction.** Fixating on "up or down" while ignoring the IV and time decay that frequently decide the P&L.
* **Buying options just before a scheduled event.** Paying inflated, event-rich IV and then losing to the crush — the classic pre-Budget / pre-results trap.
* **Assuming a favourable move must mean profit.** A small up-move can be outvoted by decay and an IV drop, as the sign table warns.
* **Ignoring that weeklies decay faster.** Holding a weekly long "a little longer" near expiry, into the steepest part of the decay curve.
* **Over-crediting interest rates and dividends.** They are minor for the short-dated index options most readers trade; do not build a thesis around them.

---

## 9. Case Study — "Budget Day 2024": all six factors at once

**Context.** The Union Budget presented on **23 July 2024** is a textbook example of the six factors colliding in a single session. The numbers below are **illustrative and representative** of the budget-day *pattern* (event IV build-up, a gap-and-swing, then an IV crush into the weekly expiry) rather than exact ticks — verify actual levels from the archives — but the mechanics are precisely what unfolds around such events.

**The build-up.** In the days before the Budget, traders hedged and speculated, pushing India VIX up from a calm baseline (≈11) to an elevated level (≈14). NIFTY sat near 24,500 with a weekly expiry two days after the event. The event-rich IV made every ATM premium expensive: the `24500 CE` traded around **₹180** and the `24500` straddle (call + put) around **₹360** — both inflated by the volatility forecast, not by any move that had yet happened.

**Budget day.** NIFTY gapped and then swung sharply intraday on tax-related headlines — a range of a few hundred points — before settling only modestly changed on the day. As soon as the event's uncertainty resolved, IV collapsed: India VIX fell from ≈14 back toward ≈11 (a classic **IV crush**), and one more day of accelerated, near-expiry **time decay** bled the premiums further.

**The tug-of-war, resolved (illustrative snapshots).**

| Position (24500 strike) | Pre-Budget premium | Post-Budget premium | Outcome |
| --- | ---: | ---: | ---: |
| Long ATM Call | ₹180 | ₹150 | −₹30/unit despite an up-swing |
| Long Straddle (buyer) | ₹360 | ₹250 | −₹110/unit — hurt by IV crush + decay |
| Short Straddle (seller) | ₹360 | ₹250 | +₹110/unit — profited from the vol collapse |

**The analysis.** All six factors were in play. *Price (S)* moved — but not enough to overcome the two headwinds. *Volatility (σ)* fell hard — the dominant factor, crushing every long premium. *Time (T)* decayed fast into the weekly expiry. *Strike (K)* was fixed; *interest rate (r)* and *dividends (q)* were negligible over a day. The option **buyer** who focused only on "the Budget will move the market" was right about the move and still lost, because volatility and time outvoted direction. The **seller** who understood that event IV was rich — and would crush once the event passed — collected the difference.

**The lesson.** On event days, the *dominant* factor is usually volatility, not direction. Before an event, ask not only "which way?" but "is IV rich, and what happens to it after the event?" The trader who can name the dominant factor in advance is positioned; the one who watches only price is guessing.

*(Takeaway: a premium is a bundle of six forces. Winning event trades come from identifying which force will dominate, not from predicting the headline.)*

---

## 10. Chapter Summary

* Six factors set an option's premium: **underlying price (S), strike (K), time to expiry (T), volatility (σ), interest rate (r), and dividends (q)**.
* **Direction of effect (factor ↑):** S — call +, put −; K — call −, put +; **T — both +**; **σ — both +**; r — call +, put −; q — call −, put +.
* **Time decay is non-linear and accelerates** (time value ≈ A × √T); per-day decay is small far out and largest near expiry — and **weeklies decay about twice as fast per day** as monthlies.
* **Volatility is the king factor:** it moves calls and puts the same way, can change violently and independently of price, and often decides a trade — its formal measure is **Vega**.
* **Interest rate (Rho) and dividends are small** for short-dated index options — real but usually dwarfed by price, time, and volatility.
* For short-dated options, **volatility and time frequently overwhelm small directional moves** — the reason a "correct" direction can still lose.
* Each factor maps to a Greek you will meet later: price → **Delta**, time → **Theta**, volatility → **Vega**, rate → **Rho**.

---

## 11. Key Takeaways

* **Diagnose every premium change by factor** — price, time, or volatility is almost always the answer.
* **Give volatility and time the attention beginners give only to direction;** for short-dated options they usually matter more.
* **Never buy inflated event IV expecting the move to rescue you** — the IV crush frequently wins.
* **Remember weeklies are high-decay instruments** — a headwind for buyers, income (with sharp risk) for sellers.

---

## 12. Practice Questions

**Q1 (Signs).** Using the sensitivity matrix, state the effect on a **put** premium if (a) the underlying rises, (b) volatility rises, (c) time passes, (d) interest rates rise.

**Q2 (Multiple choice).** Which two factors raise the premium of *both* calls and puts when they increase?
(a) price and strike; (b) time and volatility; (c) interest rate and dividends; (d) price and volatility.

**Q3 (Concept).** Explain why an option buyer can be right about direction and still lose money, naming the two factors most likely responsible.

**Q4 (Decay).** Using Table 5.2, compare the per-day time decay from 30→20 days with that from 1→0 days. What does the comparison illustrate?

**Q5 (Weekly vs monthly).** Using the √T model with A ≈ 38.34, estimate the time value and the average per-day decay of a 7-day ATM option versus a 28-day ATM option. Which decays faster per day, and by roughly how much?

**Q6 (Volatility).** An ATM call is worth ₹177 at 13% IV with the index flat. Using proportionality, estimate its value if IV rises to 20%. Express the change per unit and per lot (lot 65).

**Q7 (Interest rate).** Explain why interest-rate changes barely affect a weekly NIFTY option but can be felt on a 60-day option. Roughly what is the effect of a 100 bps move on a 60-day ATM option?

**Q8 (Dominance).** On event day, which factor most often dominates the premium change, and why is watching direction alone dangerous?

**Q9 (Application).** Before a scheduled RBI policy, India VIX is elevated. A trader wants to buy a straddle "because the market will move." Using this chapter's ideas, what is the risk they are overlooking?

**Q10 (Diagnosis).** Overnight, a long ATM call falls in value even though the future rose 40 points. Give two factor-based explanations.

---

## 13. Detailed Solutions

**A1.** For a put, when the factor increases: (a) underlying rises → **−** (puts fall as the index rises); (b) volatility rises → **+** (higher σ raises both puts and calls); (c) time passes (T decreases) → **−** (time value is lost); (d) interest rates rise → **−** (higher r lowers puts).

**A2.** **(b) time and volatility.** Both increase optionality for holders, so both raise calls and puts together.

**A3.** Because a small favourable move in the underlying can be outweighed by **time decay** (Theta) and a **fall in implied volatility** (an IV crush, Vega). The direction was right, but those two factors moved against the position by more than the price move earned.

**A4.** From Table 5.2, the 30→20 interval decays about **₹3.9 per day**, while the final 1→0 day decays **₹38.3** — roughly ten times faster. It illustrates that time decay is **non-linear and accelerates sharply near expiry**.

**A5.** Time value ≈ 38.34 × √T. For 7 days: 38.34 × 2.646 ≈ **₹101**, decay ≈ 101 ÷ 7 ≈ **₹14.4/day**. For 28 days: 38.34 × 5.292 ≈ **₹203**, decay ≈ 203 ÷ 28 ≈ **₹7.3/day**. The **weekly decays about twice as fast per day** (≈14.4 vs ≈7.3), because √28 ≈ 2 × √7 but the days are 4×.

**A6.** ATM premium is roughly proportional to IV, so at 20% IV: 177 × (20 ÷ 13) ≈ **₹272** (≈ ₹273 by direct calculation). Change per unit ≈ +₹95–96; per lot ≈ 96 × 65 ≈ **₹6,240** — created by volatility alone, with the index flat.

**A7.** The interest-rate effect works through the present value of the strike, `K × e^(−rT)`; with a tiny T (7/365), the exponent is minuscule, so a rate change moves the premium by only a rupee or two. Over 60 days, T is larger, so the same rate change has more leverage — about **₹20 per unit** on a 60-day ATM option for a 100 bps move (raising the call, lowering the put).

**A8.** **Volatility** most often dominates on event day: implied volatility is elevated beforehand and typically **crushes** once the event resolves, moving every premium sharply and the same way. Watching direction alone is dangerous because even a correct directional call can be outweighed by the IV crush and time decay.

**A9.** The straddle is being bought when **IV is already elevated** (event-rich). After the policy is announced, IV usually **crushes**, and the straddle loses value on both legs unless the actual move is *larger* than the elevated premium was pricing in. The trader is overlooking that they are paying for a move the market has already priced, and that the post-event volatility collapse can outweigh the move.

**A10.** Two explanations: (i) **Time decay** — a day (or overnight) passed, and the time value lost exceeded the ~40-point price benefit, especially near expiry. (ii) **Falling implied volatility** — IV dropped overnight, deflating the premium (Vega) by more than the price move added. (A third: the 40-point move may simply have been smaller than the option's sensitivity implied once decay and IV are netted.)

---

## 14. Mini Glossary

* **Underlying price (S)** — the index (in practice the future) whose level drives the option; call + / put − when it rises. → this chapter.
* **Strike price (K)** — the fixed level of a contract; across strikes, higher K means cheaper calls, dearer puts. → this chapter.
* **Time to expiry (T)** — time remaining; more time raises both calls and puts; its loss is time decay. → this chapter.
* **Volatility (σ)** — expected size of index movement, annualised; the market's estimate is implied volatility. Raises both calls and puts. → this chapter.
* **Implied volatility (IV)** — the volatility embedded in an option's market price. → this chapter.
* **India VIX** — the NSE's index of expected 30-day NIFTY volatility; the market's fear gauge. → this chapter.
* **IV crush** — a sharp fall in implied volatility, typically after a scheduled event, deflating premiums. → this chapter.
* **Interest rate (r)** — the risk-free rate (RBI-anchored); a small factor that raises calls and lowers puts. → this chapter.
* **Dividends (q)** — expected index dividends; a small factor that lowers calls and raises puts, usually embedded in the future. → this chapter.
* **Time decay** — the loss of time value as expiry approaches; non-linear and accelerating (formally, Theta). → this chapter.
* **Square-root-of-time relationship** — the approximation that time value scales with √T, so per-day decay accelerates near expiry. → this chapter.
* **Sensitivity matrix** — the table of +/− effects of each factor on calls and puts. → this chapter.
* **Delta / Theta / Vega / Rho** — the formal measures of sensitivity to price, time, volatility, and interest rate, introduced later in the book. → this chapter.

---

<!-- End of Chapter 5 (Rev 2, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026 revision) in the four lot-dependent spots — setting lines, NE3 lot figure (96×65=₹6,240), Q6 (lot 65), A6 (96×65=₹6,240). Per-unit figures (₹177→₹273, ₹96/unit) unchanged — no lot dependence. Time-decay table uses √T with A≈38.34 (consistent across weekly/monthly examples). Volatility example uses ATM≈0.4·S·σ·√T (₹177 at 13% → ₹273 at 20%). Rate example: PV(K)=K·e^(−rT), 100 bps → ~₹20 on 60-day ATM (r illustrative). Budget-day case HISTORICAL (23 July 2024; that week's expiry Thu 25 Jul) — 2024 rules retained. No transaction costs, so Apr-2026 STT change does not affect numbers. Greeks named as previews only; no chapter-number forward references. IV reserved for implied volatility. -->
