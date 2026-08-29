<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 11, 15, 17. Target length ~8,500 words. Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Uses standard strategy template. Per-unit debits, premiums, Greeks, breakevens all lot-independent — unchanged; only "/lot" conversions rescaled to lot 65 (calendar debit ₹6,240/lot, max profit ₹5,265/lot, RBI debit ₹14,495/lot, Scenario A +₹7,605/lot, Scenario B −₹13,195/lot, condor max loss ₹7,800/lot). Calendars on NIFTY (weekly Tuesday expiry retained → weekly-to-weekly & weekly-to-monthly valid); no BANKNIFTY; gross debits/P&L → Apr-2026 STT change not applicable. Calendar = short near-term + long far-term, SAME strike. ATM 24,600 calendar (near 3 DTE @₹116, far 10 DTE @₹212): debit ₹96, max profit ~₹81 at strike at near expiry. Greeks (the flagship anomaly): Δ~0, Θ +8.7/day (positive), ν +7.4/vol pt (POSITIVE — unusual), Γ −0.00062 (negative). Θ from 1/√T term structure (near decays faster), ν from √T term structure (far has more Vega). Calendar vs iron condor: same tent shape, OPPOSITE Vega (calendar +ν, condor −ν). Case study: RBI calendar (sell event-week, buy month) — differential IV crush +₹117 on modest move, −₹203 on big move. IV = implied volatility. -->

# Chapter 19 — Calendar and Diagonal Spreads: Trading Time and Term Structure

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Construct and manage calendar spreads (horizontal spreads).
2. Construct and manage diagonal spreads.
3. Understand how these strategies profit from differential time decay *and* IV changes.
4. Apply calendars to India's weekly/monthly expiry structure.
5. Recognise when the term structure makes a calendar favourable or unfavourable.

Every strategy so far has traded within a single expiry. The **calendar spread** does something new — it trades *across* expiries, exploiting the term structure of both Theta (Chapter 10) and Vega (Chapter 11). The result is a position with a genuinely unusual Greek signature, and a tool you cannot build any other way.

---

## 2. Introduction

There is a rule of thumb, true for almost every strategy in this book: *if you collect Theta, you are short Vega.* Selling options earns time decay but loses when volatility rises (Chapter 12's seller's identity). The calendar spread breaks that rule. It is **positive Theta *and* positive Vega at the same time** — it earns money as time passes *and* profits when implied volatility rises. That combination sounds impossible, and understanding *why* it is possible is the key that unlocks this chapter.

The trick is that the calendar trades the *term structure*. It sells a near-term option and buys a far-term option at the *same strike*. Because Theta accelerates near expiry (∝ 1/√T, Chapter 10), the near-term option you are short decays *faster* than the far-term option you are long — so you collect net time decay (positive Theta). And because Vega grows with time to expiry (∝ √T, Chapter 11), the far-term option you are long has *more* Vega than the near-term one you are short — so you are net long volatility (positive Vega). One structure, harvesting two different term structures at once.

This makes the calendar a distinctive tool: a range-bound, income-collecting position that *also* benefits from rising IV — ideal for a quiet market with cheap volatility that you expect to increase. It looks like an iron condor on a payoff chart (a tent-shaped profit zone) but is its Vega opposite. This chapter builds the calendar and its cousin the diagonal, contrasts them sharply with the condor, and shows how professionals use a calendar around an event like an RBI policy to harvest the differential collapse of near- versus far-term event premium. Setting: **NIFTY at 24,600, lot 65**, with Greeks from the Part III/IV term structures.

---

## 3. Core Concepts

### 3.1 What a calendar spread is

The calendar spread is the flagship of this chapter.

**What is it?** A **calendar spread** (also called a *horizontal* or *time* spread) sells a **near-term** option and buys a **far-term** option at the **same strike** (and same type — both calls or both puts). You pay a net debit (the far costs more than the near), and the position profits primarily from the near-term option decaying faster than the far-term one.

**Why does it exist?** To trade the *term structure* — the differences in Theta and Vega across expiries — which no single-expiry strategy can capture. The calendar is the only way to be simultaneously short the fast-decaying near-term and long the Vega-rich far-term.

**Why should a trader care?** Because the calendar gives a combination available nowhere else: **positive Theta *and* positive Vega.** It lets you collect time decay in a quiet market while *also* being positioned to profit if IV rises — the ideal structure when volatility is cheap (low IV) and you expect it to increase, or ahead of an event that will inflate IV.

**Intuitive explanation.** Picture two ice cubes melting: a small one (the near-term option) and a large one (the far-term option). The small cube melts *much* faster. You "sold" the small cube and "bought" the large one — so as both melt, you gain on the fast-melting small one more than you lose on the slow-melting large one. Meanwhile, if the room heats up (IV rises), the large cube — which has more surface area (Vega) — gains more value than the small one. You win on both the melting *and* the heat.

**Numerical feel.** An ATM NIFTY calendar (sell the 3-DTE 24,600 call @₹116, buy the 10-DTE 24,600 call @₹212) costs a net debit of ₹96. Its Greeks: Delta ~0, **Theta +₹8.7/day** (you collect decay), **Vega +₹7.4/vol point** (you gain if IV rises) — the anomaly that defines the strategy (Section 3.3).

**Professional interpretation.** Desks use calendars specifically to be *long Vega with positive carry* — to hold a long-volatility position that does not bleed Theta the way a long straddle does. It is the go-to structure for "I think IV is too cheap and will rise, and I don't want to pay Theta while I wait."

**Common mistake.** Treating a calendar like an iron condor (a short-vol range trade). They share a tent-shaped payoff but have *opposite* Vega — a calendar loses when IV falls, exactly when a condor wins (Section 3.5).

**Practical takeaway.** **A calendar spread is the rare position that is both positive Theta and positive Vega — use it when volatility is cheap and you expect it to rise while the market stays range-bound.**

---

### 3.2 Why the calendar profits — two term structures at once

The calendar's magic comes from exploiting *two* term structures simultaneously (Chapters 10 and 11):

**The Theta term structure (positive Theta).** Time decay accelerates as expiry nears: Theta ∝ 1/√T. The near-term option (3 DTE) decays at ~₹19/day; the far-term (10 DTE) at only ~₹11/day. Being *short* the fast-decaying near and *long* the slow-decaying far, you collect the difference:

```
Calendar Theta = Theta_near − Theta_far = 19.3 − 10.6 = +₹8.7/day    (positive)
```

**The Vega term structure (positive Vega).** Vega grows with time: Vega ∝ √T. The far-term option (10 DTE) has more Vega (₹16.3) than the near-term (3 DTE, ₹8.9). Being *long* the high-Vega far and *short* the low-Vega near, you are net long volatility:

```
Calendar Vega = Vega_far − Vega_near = 16.3 − 8.9 = +₹7.4/vol point    (positive)
```

This is the whole secret: **the positive Theta comes from the 1/√T term structure (near decays faster), and the positive Vega comes from the √T term structure (far has more Vega).** Because these two term structures point in opposite directions with respect to time, the calendar can harvest both — collecting decay *and* being long volatility, which no single-expiry position can do.

> **Beginner Alert — "positive Theta and positive Vega" is the whole point.** Almost every income strategy in this book (short options, credit spreads, condors) is positive Theta but *negative* Vega — you earn decay but fear a volatility spike. The calendar is the exception, and it is *why* the calendar exists. If you remember one thing about calendars, remember this: they let you collect time *and* stay long volatility. That makes them uniquely suited to a cheap-IV, range-bound market you expect to get more volatile.

---

### 3.3 The calendar's Greeks and payoff

**Setup.** Sell the near-term (3 DTE) 24,600 call @₹116, buy the far-term (10 DTE) 24,600 call @₹212. Net debit **₹96** (₹6,240/lot).

**Greeks (per unit).**

| Greek | Near (short) | Far (long) | **Calendar (net)** |
| --- | ---: | ---: | ---: |
| Delta | −0.53 | +0.54 | **≈ +0.01 (neutral)** |
| Theta | +19.3 | −10.6 | **+8.7/day (positive)** |
| Vega | −8.9 | +16.3 | **+7.4/vol pt (positive)** |
| Gamma | −high | +lower | **negative (short Gamma)** |

The signature: **Delta-neutral, positive Theta, positive Vega, negative Gamma.** The positive Theta and Vega are the reward; the negative Gamma is the risk — a *sharp move away from the strike* hurts.

**Payoff shape.** The calendar's P&L at near-term expiry is a **tent centred on the strike** — like a butterfly or condor:

```
 P&L/unit (₹)
 +81 │        ╱╲   ← max profit at the strike (24,600) at near expiry
   0 │──────╱────╲──────▶ Spot at near-term expiry
     │   24,400  24,800  (approx. breakevens)
 −96 │  (wings: near-total loss of debit on a big move either way)
```

**Max profit and breakevens.** Max profit (~₹81, ₹5,265/lot) occurs if the underlying sits *at the strike* at near-term expiry: the short near-term option expires worthless, while the long far-term option retains its remaining time value. The breakevens (roughly 24,400 and 24,800 here) are where the far-term option's remaining value at near expiry just covers the debit — **computing them exactly requires an options pricing model** (you must price the far-term option at the near-term expiry date), which is why calendar breakevens are estimated, not read off a simple formula. A move too far in *either* direction (negative Gamma) collapses the far's time value and loses most of the debit.

**Why max profit is at the strike.** At the strike, at near expiry, the short near-term option decays to zero (its whole job) while the long far-term option is ATM with maximum remaining time value — the widest possible gap between the two legs, and thus the calendar's peak value.

---

### 3.4 The calendar as a volatility (term-structure) trade

The positive Vega makes the calendar fundamentally a **volatility trade**, not just a time trade. It profits when IV *rises* and loses when IV *falls* — the reverse of every short-premium strategy.

This has a sharp implication for *when* to use it:

* **Enter calendars when IV is low** (low IV Rank, Chapter 14) and you expect it to rise — you are buying cheap far-term Vega. As IV rises, the long far-term leg gains more than the short near-term leg loses.
* **Avoid calendars when IV is high** and likely to fall — the IV crush would hurt your long Vega. (This is exactly when an iron condor, which is *short* Vega, shines instead — Section 3.5.)

The calendar also cares about the **term-structure shape** (Chapter 15). It works best in normal **contango** (far IV ≥ near IV) or when the near-term IV is *elevated relative to the far* and expected to crush more — which is precisely the event-calendar setup (the RBI case, Section 9). It works *worst* when the term structure is **inverted (backwardation)** in a way that then normalises against you — if the near IV you are short *rises* relative to the far you are long.

---

### 3.5 Calendar versus iron condor — same shape, opposite Vega

This is the most important practical distinction in the chapter. On a payoff chart, a calendar and an iron condor look almost identical: a tent-shaped profit zone that pays if the underlying stays range-bound. But their Greek profiles are *opposite in Vega*, and that changes everything.

**Table 19.1 — Calendar spread vs iron condor**

| | Calendar spread | Iron condor |
| --- | --- | --- |
| Structure | 1 strike, 2 expiries | 4 strikes, 1 expiry |
| Payoff shape | Tent (range-bound) | Tent (range-bound) |
| Delta | ~0 | ~0 |
| Theta | Positive | Positive |
| Gamma | Negative | Negative |
| **Vega** | **Positive (long vol)** | **Negative (short vol)** |
| Profits when IV… | **rises** | **falls** |
| Best entered when IV is… | **low** (expect rise) | **high** (expect fall) |
| Max loss | Net debit paid | Wing width − credit (larger) |

The decisive difference is **Vega**. Both want the market to stay range-bound (both are negative Gamma, positive Theta) — but the calendar wants IV to *rise* while the condor wants IV to *fall*. This gives a clean rule:

> **When IV is cheap and you expect it to rise, trade a calendar (long Vega). When IV is rich and you expect it to fall, trade an iron condor (short Vega).** Same neutral view on direction; opposite view on volatility; opposite structure.

This is why the two strategies are complements, not substitutes — and why "which range-bound structure?" is really the question "which way is IV going?"

---

### 3.6 Diagonal spreads — strike and expiry together

A **diagonal spread** is a calendar with a *twist*: the two legs have **different strikes *and* different expiries.** You sell a near-term option at one strike and buy a far-term option at a *different* strike — combining the calendar's time-decay harvest with a directional tilt from the strike difference.

**Example (bullish diagonal).** Sell the this-week 24,600 CE, buy the next-month 24,400 CE. The far-term 24,400 call is *in the money* (higher delta), giving the position a **bullish bias** (positive net Delta) on top of the calendar's positive Theta/Vega. It profits if NIFTY rises modestly and stays below the short strike at near expiry — you collect the near-term decay while the ITM far-term leg gains on the up-move.

Diagonals are versatile: by choosing the far strike, you dial in a directional lean while keeping the calendar's term-structure benefits. A deep-ITM far-term long call financed by rolling short near-term calls is the well-known **"poor man's covered call"** — a capital-efficient way to run a call-overwriting-style position (Chapter 16) without owning the underlying. The trade-off is added complexity and a directional exposure that must be managed alongside the term-structure Greeks.

---

### 3.7 Double calendars, the Indian application, and dividends

**Double calendar.** Run a calendar on *both* a call strike (above the money) *and* a put strike (below), e.g., a 24,800 call calendar plus a 24,400 put calendar. This *widens the profit tent* (two peaks instead of one) while keeping the positive-Theta, positive-Vega profile — a way to give the calendar more room for the underlying to wander while staying long volatility.

**The Indian weekly/monthly application.** India's expiry structure (Chapters 1–2) makes calendars especially natural. The **weekly-to-weekly calendar** (sell this-week NIFTY CE, buy next-week CE at the same strike) exploits the rapid decay of the near weekly against the slower far weekly — a short-horizon calendar. The **weekly-to-monthly calendar** sells the fast-decaying weekly against a monthly leg, harvesting the weekly's steep Theta while holding a longer-Vega monthly. Because weekly options decay ~2× faster per day than monthlies (Chapter 10), the Indian weekly structure gives calendars an unusually rich near-term decay to sell.

**Dividends and corporate actions.** For *index* options these effects are **minimal** — the index's dividends are diffuse and already embedded in the futures basis (Chapter 2), so calendars on NIFTY are largely unaffected by dividends. (This is a bigger consideration for single-stock calendars, which are out of scope.) Worth noting, not worrying about.

---

### 3.8 When calendars fail

The calendar's two risks are the mirror of its two rewards:

* **A sharp move in either direction (negative Gamma).** The calendar's max profit is at the strike; a large move away collapses the far-term option's time value, and the position loses most of its debit. A calendar is a *range* bet — it fails on a big move, exactly like a condor. This is the primary risk.
* **A fall in implied volatility (positive Vega).** Because the calendar is long Vega, an IV *crush* hurts it — the long far-term leg loses value. Entering a calendar when IV is high and about to fall is a classic error (Section 3.4).
* **Term-structure inversion.** If the near-term IV you are short *rises* relative to the far-term IV you are long (the term structure inverts against you), the calendar loses even without a big move — the short leg gains value faster than the long leg.

The through-line: a calendar wants a **quiet market with rising (or holding) IV and a normal term structure.** It fails on a big move, an IV crush, or an adverse term-structure shift.

---

## 4. Examples (Real-World)

**Example 1 — The cheap-IV calendar.** In a dull, low-VIX market, a trader expects volatility to pick up but does not want to pay Theta on a long straddle while waiting. They put on an ATM calendar: positive Theta (they collect while waiting) and positive Vega (they profit when IV rises). The calendar lets them be long volatility *with* positive carry.

**Example 2 — Same chart, opposite trade.** Two traders both expect NIFTY to stay range-bound. One, seeing *high* IV likely to fall, sells an iron condor (short Vega). The other, seeing *low* IV likely to rise, buys a calendar (long Vega). Identical directional view, opposite volatility view, opposite structure — and only one is right about IV.

**Example 3 — The event calendar.** Before an RBI policy, a trader sells the event-week option (rich with event premium) and buys the next-month option (less event-inflated). After the policy, the near-term event premium crushes far more than the far-term's — the calendar captures the differential (the case study, Section 9).

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65; ATM 24,600 calendar (near 3 DTE, far 10 DTE).

### Numerical Example 1 — Calendar debit and Greeks

```
Sell near 24,600 CE (3 DTE) @₹116;  Buy far 24,600 CE (10 DTE) @₹212
Net debit = 212 − 116 = ₹96 (₹6,240/lot) — this is the max loss
Delta = −0.53 + 0.54 = +0.01 (neutral)
Theta = +19.3 − 10.6 = +₹8.7/day (positive — collects decay)
Vega  = +16.3 − 8.9 = +₹7.4/vol point (positive — long volatility)
Gamma = negative (short the higher-Gamma near-term)
```

The signature no single-expiry position can match: neutral, positive Theta, *and* positive Vega.

### Numerical Example 2 — P&L at near-term expiry

At near expiry (near = 0 DTE, far = 7 DTE), with the underlying **at the strike (24,600)**:

```
Near 24,600 CE (0 DTE, ATM): worthless → short leg P&L = +₹116
Far 24,600 CE (7 DTE, ATM): value ≈ ₹177 (7-DTE ATM time value) → long leg P&L = 177 − 212 = −₹35
Net P&L = 116 − 35 = +₹81 (₹5,265/lot) — the max profit, at the strike
```

Position value at near expiry = far − near = 177 − 0 = ₹177; minus the ₹96 debit = **+₹81**. If the underlying instead moves sharply to, say, 25,200, both calls go deep ITM, the time-value gap collapses, and the calendar loses most of the ₹96 debit — the negative-Gamma risk.

### Numerical Example 3 — Vega impact (the long-volatility feature)

Hold the calendar; the underlying is unchanged but IV rises 3 points:

```
ΔP from Vega ≈ Position Vega × ΔIV = +7.4 × 3 = +₹22.2/unit (₹1,443/lot)
```

The calendar *gains* ₹22 from a 3-point IV rise — with the underlying flat. An iron condor, being short Vega, would *lose* on the same IV rise. This is the calendar's defining edge in a rising-IV environment.

### Numerical Example 4 — Calendar vs iron condor, side by side

| | ATM Calendar | Iron condor (30Δ, 200 wings) |
| --- | ---: | ---: |
| Cost/credit | Debit ₹96 | Credit ₹80 |
| Max loss | ₹96 (debit) | ₹120 (₹7,800/lot) |
| Theta | +₹8.7/day | positive |
| **Vega** | **+₹7.4 (long vol)** | **negative (short vol)** |
| Profits if IV… | rises | falls |
| Use when IV is… | low | high |

Both are range-bound, positive-Theta, negative-Gamma tents — but the calendar is long Vega (use in cheap IV) and the condor is short Vega (use in rich IV). The IV regime, not the payoff shape, decides which to trade.

### Numerical Example 5 — Bullish diagonal

```
Sell this-week 24,600 CE @₹116;  Buy next-month (32 DTE) 24,400 CE @₹430 (ITM, Δ~0.65)
Net debit ≈ 430 − 116 = ₹314
Net Delta ≈ −0.53 (short near) + 0.65 (long far ITM) = +0.12 (bullish tilt)
```

The diagonal keeps the calendar's positive Theta/Vega but adds a **bullish bias** (+0.12 Delta) via the ITM far-term long call — it profits if NIFTY drifts up modestly while the near-term option decays. It is a calendar with a directional lean, dialled in by the strike choice.

---

## 6. Calculations (the reusable recipes)

**(a) Calendar spread cost and Greeks**

```
Debit = Far premium − Near premium (= max loss)
Calendar Theta = Theta_near − Theta_far (positive; near decays faster)
Calendar Vega  = Vega_far − Vega_near (positive; far has more Vega)
Calendar Gamma = Gamma_far − Gamma_near (negative; near has more Gamma)
Delta ≈ 0 (same strike, both legs offset near the money)
```

**(b) Max profit and breakevens**

```
Max profit ≈ (far-term value at near expiry, at the strike) − Debit, occurring AT the strike
Breakevens: where far-term value at near expiry = Debit + near intrinsic
            → requires an options pricing model (estimate, not a closed formula)
```

**(c) Vega P&L (the long-volatility feature)**

```
ΔP from IV change ≈ Position Vega × ΔIV   (positive: calendar gains when IV rises)
```

**(d) Diagonal net Delta**

```
Net Delta = Delta_far (chosen strike) − Delta_near   (tilt bullish with an ITM far call / bearish with an ITM far put)
```

---

## 7. Practical Insights

* **The calendar is your positive-carry long-volatility trade.** When you think IV is too cheap and will rise but do not want to bleed Theta on a long straddle, the calendar collects decay *and* stays long Vega — a combination nothing else offers.
* **Match the range-bound structure to the IV regime.** Cheap IV expected to rise → calendar (long Vega); rich IV expected to fall → iron condor (short Vega). Same neutral view, opposite volatility bet.
* **Respect the negative Gamma.** A calendar is a range bet; a sharp move in either direction collapses it. Size it as a defined-risk trade (max loss = the debit) and do not treat it as safe just because it is Delta-neutral.
* **Exploit India's weekly decay.** The weekly-to-monthly calendar sells the market's fastest-decaying option (the weekly) against a longer-Vega monthly — a rich near-term Theta to harvest.
* **Compute breakevens with a model, not a formula.** The far-term leg's value at near expiry needs pricing; use a calculator or platform to find the true profit range, and never assume a simple ± band.

> **Professional Insight — the calendar is a term-structure trade in disguise.** When a professional puts on a calendar, the *dominant* view is often about the *shape of the volatility term structure* — that near-term IV is too high relative to far-term (event calendars), or that the whole curve is too cheap and will rise. The range-bound payoff is almost a by-product. If you think only "the market will stay still," you are missing half the trade; the other half — and often the profit — is the term-structure and IV view embedded in the positive Vega.

---

## 8. Common Mistakes

* **Treating a calendar like an iron condor.** They share a tent payoff but have *opposite* Vega; a calendar loses when IV falls, precisely when a condor wins.
* **Entering calendars in high IV.** Being long Vega, a calendar is hurt by the IV crush that follows high IV — use condors (short Vega) in rich IV instead.
* **Ignoring the negative Gamma.** A sharp move collapses the far-term time value and loses most of the debit; a calendar is a range bet, not a safe neutral position.
* **Assuming a simple breakeven formula.** Calendar breakevens depend on the far-term option's value at near expiry and require a pricing model — a naive ± band mis-estimates the profit zone.
* **Forgetting the term-structure risk.** If the near IV you are short rises relative to the far IV you are long (an adverse term-structure shift), the calendar loses even in a quiet market.
* **Over-complicating with diagonals before mastering calendars.** The diagonal adds a directional exposure on top of the term-structure Greeks — manage the calendar first.

---

## 9. Case Study — "Calendar Spread Around RBI Policy"

**Context.** The RBI's bi-monthly monetary policy is a scheduled, market-moving event (Chapter 5) that reliably inflates near-term implied volatility. A trader uses a **calendar spread to harvest the differential IV crush**: sell the event-week (near-term) option, whose IV is bloated with event premium, and buy the next-month (far-term) option, whose IV is far less event-inflated. After the policy, the near-term event premium collapses much more than the far-term's — and the calendar captures the difference. Figures are illustrative but representative.

**The setup (a few days before RBI).** NIFTY is at 24,600. The event-week 24,600 call carries an elevated **18% IV** (event premium), pricing at **₹185**. The next-month 24,600 call carries a calmer **14% IV**, pricing at **₹408** (more time value, less event-inflation per unit of its longer life). The trader sells the near and buys the far:

```
Sell event-week 24,600 CE @₹185 (IV 18%);  Buy next-month 24,600 CE @₹408 (IV 14%)
Net debit = 408 − 185 = ₹223 (₹14,495/lot) — the max loss
```

The position is long Vega (it will gain if IV rises further into the event), positive Theta, and — crucially — set up to profit from the *differential* collapse of near- versus far-term IV after the policy.

**Scenario A — RBI passes with a modest move (the base case).** The policy is broadly as expected; NIFTY moves only to 24,650. The event is over, so the **near-term IV crushes hard** (18% → 11%) while the **far-term IV crushes only mildly** (14% → 13%):

```
Near 24,600 CE (now ~expiry, NIFTY 24,650, IV 11%): ≈ ₹60 (mostly the ₹50 intrinsic)
Far 24,600 CE (now ~27 DTE, NIFTY 24,650, IV 13%): ≈ ₹400
Calendar value = 400 − 60 = ₹340;  P&L = 340 − 223 = +₹117/unit (+₹7,605/lot)
```

The profit came overwhelmingly from the **near-term IV crush**: the near call fell from ₹185 to ₹60 (and the trader was *short* it — a ₹125 gain), while the far call barely moved (₹408 → ₹400, an ₹8 loss on the long). The calendar captured the differential — the event premium collapsed on the leg the trader was short, and held on the leg they were long. This is the calendar's edge around a scheduled event.

**Scenario B — RBI triggers a big move (the risk).** Suppose instead the policy shocks the market and NIFTY jumps to 25,200 (+600). Both calls go deep in the money, and the calendar's time-value gap collapses:

```
Near 24,600 CE (expiry, 25,200): ≈ ₹600 (all intrinsic) → short-leg loss
Far 24,600 CE (27 DTE, 25,200, deep ITM): ≈ ₹620 (mostly intrinsic, little TV)
Calendar value = 620 − 600 = ₹20;  P&L = 20 − 223 = −₹203/unit (−₹13,195/lot)
```

The big move (negative Gamma) destroyed the position — both legs became nearly all intrinsic, the time-value differential vanished, and the trader lost most of the ₹223 debit. This is the calendar's Achilles heel: it needs the event to pass *without* a large move.

**The analysis.** The RBI calendar is a bet on **two things at once**: that the near-term event IV is over-inflated relative to the far (it usually is), *and* that the policy will not cause a large move (usually true, occasionally not). When both hold (Scenario A), the differential IV crush delivers a clean profit with the near-term premium collapsing on the short leg. When the event surprises with a big move (Scenario B), the negative Gamma overwhelms the IV edge and the debit is largely lost. The trade's defined risk (the ₹223 debit) is its saving grace — the loss is capped and known — but the trader must size it as a bet that can lose its full debit on a surprise.

**The lesson.** A calendar around an event harvests the *differential collapse* of near- versus far-term event premium — a genuine, repeatable edge when the market grasps that event IV is concentrated in the near expiry. But it is still a *range* bet: a large event-day move collapses the time-value gap and takes the debit. Use the event calendar when you expect the event premium to over-inflate the near expiry *and* the actual move to be contained — and size it as the defined-risk, can-lose-the-debit trade it is.

*(Takeaway: sell the near-term event premium and buy the far-term against it to capture the differential IV crush — but only when you expect the event to pass without a large move, because the calendar's negative Gamma loses on a big surprise.)*

---

## 10. Chapter Summary

* A **calendar spread** sells a near-term and buys a far-term option at the *same strike*, paying a net debit; it profits mainly from the near-term decaying faster.
* Its defining signature is **positive Theta *and* positive Vega** — the Theta from the 1/√T term structure (near decays faster) and the Vega from the √T term structure (far has more Vega). It also carries **negative Gamma** (the risk).
* The payoff is a **tent centred on the strike**; max profit occurs at the strike at near expiry, and **breakevens require a pricing model** to compute (the far-term leg must be priced at near expiry).
* The calendar is a **long-volatility, term-structure trade**: enter when **IV is cheap and expected to rise**; it *loses* when IV falls or the underlying moves sharply.
* **Calendar vs iron condor:** same range-bound tent, but *opposite Vega* — the calendar is long vol (use in cheap IV), the condor is short vol (use in rich IV). The IV regime chooses the structure.
* A **diagonal spread** (different strike *and* expiry) adds a directional tilt to the calendar's term-structure Greeks; the "poor man's covered call" is a deep-ITM diagonal.
* **Double calendars** widen the tent; India's **weekly structure** gives calendars rich near-term decay; **dividends** barely matter for index calendars.
* The **RBI event calendar** sells the over-inflated near-term event premium against the far-term, capturing the **differential IV crush** on a modest move — but loses the debit on a large surprise (negative Gamma).

---

## 11. Key Takeaways

* **Reach for a calendar when you want to be long volatility with positive carry** — cheap IV expected to rise, market range-bound. It is the only positive-Theta, positive-Vega structure.
* **Choose calendar vs condor by the IV regime** — long-Vega calendar in cheap IV, short-Vega condor in rich IV — not by the (identical) payoff shape.
* **Respect the negative Gamma** — a calendar is a range bet that loses on a big move; size it as defined-risk (max loss = the debit).
* **Around events, sell the near-term event premium and buy the far** to capture the differential IV crush — but only when you expect a contained move.

---

## 12. Practice Questions

**Q1 (Definition).** In one sentence, define a calendar spread and state its two defining Greek signs (Theta and Vega).

**Q2 (Why it works).** Explain, using the term structures of Theta and Vega, why a calendar is both positive Theta and positive Vega.

**Q3 (Greeks).** A calendar's near leg has Theta −₹18/day and Vega ₹9; the far leg has Theta −₹10/day and Vega ₹17. Compute the calendar's net Theta and net Vega.

**Q4 (Debit).** You sell a near 24,600 CE @₹120 and buy a far 24,600 CE @₹230. Compute the net debit and state the max loss.

**Q5 (Vega P&L).** A calendar has Vega +₹7. If IV rises 4 points with the underlying unchanged, estimate the P&L per unit.

**Q6 (Calendar vs condor).** IV Rank is 15 (very low) and you expect a range-bound market with rising IV. Should you use a calendar or an iron condor, and why?

**Q7 (Max profit location).** At near-term expiry, where does a calendar achieve its maximum profit, and why?

**Q8 (Failure modes).** Name the two ways a calendar loses money, tying each to a Greek.

**Q9 (Diagonal).** You sell a this-week 24,600 CE and buy a next-month 24,300 CE (deep ITM, Δ 0.70). Is the net Delta bullish or bearish, and roughly what is it if the near Δ is 0.53?

**Q10 (Event calendar judgement).** A trader puts on an RBI event calendar and it profits handsomely. What were the two conditions that had to hold, and what single outcome would have caused a large loss?

---

## 13. Detailed Solutions

**A1.** A calendar spread sells a near-term and buys a far-term option at the same strike; it is **positive Theta** (collects net time decay) and **positive Vega** (long volatility).

**A2.** **Theta ∝ 1/√T**, so the near-term option decays faster than the far — being short the near and long the far, you collect the difference (positive Theta). **Vega ∝ √T**, so the far-term option has more Vega than the near — being long the far and short the near, you are net long volatility (positive Vega). The two term structures point opposite ways in time, so the calendar harvests both.

**A3.** Net Theta = Theta_near − Theta_far = 18 − 10 = **+₹8/day** (positive; you collect more decay on the short near than you pay on the long far). Net Vega = Vega_far − Vega_near = 17 − 9 = **+₹8/vol point** (positive).

**A4.** Net debit = far − near = 230 − 120 = **₹110** (₹7,150/lot). The max loss is the **net debit, ₹110** (₹7,150/lot).

**A5.** ΔP ≈ Vega × ΔIV = 7 × 4 = **+₹28/unit** (₹1,820/lot) — the calendar gains from rising IV even with the underlying flat.

**A6.** Use a **calendar**. Low IV (Rank 15) expected to rise favours a **long-Vega** structure, and the calendar is positive Vega — it profits as IV rises while collecting Theta in the range-bound market. An iron condor is *short* Vega and would lose as IV rose; it is the wrong tool for a rising-IV environment.

**A7.** Maximum profit occurs **at the strike, at near-term expiry** — there the short near-term option decays to zero (worthless at the money) while the long far-term option is ATM with its maximum remaining time value, giving the widest gap between the two legs and thus the calendar's peak value.

**A8.** (i) A **sharp move** in the underlying (negative **Gamma**) — the far-term time value collapses and most of the debit is lost. (ii) A **fall in IV** (positive **Vega**) — the long far-term leg loses value in an IV crush. (Also acceptable: an adverse term-structure shift where the short near IV rises relative to the long far IV.)

**A9.** **Bullish.** Net Delta = Delta_far − Delta_near = 0.70 − 0.53 = **+0.17** — the deep-ITM far-term long call gives the diagonal a bullish tilt on top of the calendar's positive Theta/Vega.

**A10.** The two conditions: (i) the **near-term event IV was over-inflated relative to the far-term** and crushed more after the event (the differential IV crush the trade harvests), and (ii) the **policy caused only a modest move** (so the negative Gamma did not bite). The single outcome that would have caused a large loss: a **big market move** on the policy (a surprise), which collapses the time-value differential and loses most of the debit.

---

## 14. Mini Glossary

* **Calendar (horizontal/time) spread** — sell a near-term and buy a far-term option at the same strike; positive Theta and positive Vega. → this chapter.
* **Diagonal spread** — a calendar with different strikes as well as different expiries; adds a directional tilt. → this chapter.
* **Term structure (of Theta and Vega)** — the variation of Theta (∝ 1/√T) and Vega (∝ √T) across expiries that the calendar exploits. → this chapter.
* **Positive Theta and positive Vega** — the calendar's defining, unusual combination (collects decay *and* is long volatility). → this chapter.
* **Calendar Theta** — Theta_near − Theta_far (positive; near decays faster). → this chapter.
* **Calendar Vega** — Vega_far − Vega_near (positive; far has more Vega). → this chapter.
* **Double calendar** — calendars on both a call strike and a put strike; widens the profit tent. → this chapter.
* **Poor man's covered call** — a deep-ITM long-dated call financed by rolling short near-term calls; a diagonal. → this chapter.
* **Differential IV crush** — the near-term event premium collapsing more than the far-term's after an event; the event-calendar edge. → this chapter.
* **Term-structure inversion (risk)** — the near-term IV (short leg) rising relative to the far-term (long leg), hurting the calendar. → this chapter.

---

<!-- End of Chapter 19 (Rev 2, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026) — per-unit debits/premiums/Greeks/breakevens unchanged; "/lot" conversions rescaled: calendar debit ₹6,240/lot, max profit ₹5,265/lot, NE3 Vega P&L ₹1,443/lot, condor max loss ₹7,800/lot, RBI debit ₹14,495/lot, Scenario A +₹7,605/lot, Scenario B −₹13,195/lot; A4 ₹7,150/lot, A5 ₹1,820/lot. Calendar ATM 24,600 (near 3 DTE @₹116, far 10 DTE @₹212): debit ₹96, max profit ~₹81. Greeks: Δ+0.01, Θ +8.7/day (19.3−10.6), ν +7.4/vol pt (16.3−8.9), Γ negative. Positive-Theta/positive-Vega anomaly via Θ∝1/√T (near faster) and ν∝√T (far more). Calendar vs iron condor: same tent, opposite Vega — calendar long-vol (low IV), condor short-vol (high IV). Diagonal net Δ +0.12 bullish. RBI case: debit ₹223; Scenario A +₹117/unit, Scenario B −₹203/unit. Calendars on NIFTY (weekly Tuesday retained); gross P&L → Apr-2026 STT not applicable. IV = implied volatility. -->
