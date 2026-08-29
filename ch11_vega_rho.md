<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapters 8, 9, 10. Target length ~8,000 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Vega computed from σ=13% BSM basis: ν=S·√T·n(d₁)/100 per 1 vol point. ATM Vega ≈ ₹28@30d, ₹16.3@10d, ₹11.5@5d, ₹5.1@1d — Vega ∝ √T (FALLS near expiry, opposite of Gamma/Theta); all per-unit values lot-independent and unchanged. Only per-lot conversions rescaled to lot 65 (NE1 ₹2,340; NE6 Position Vega −₹475/lot → ₹4,750 per 10-pt spike; A2 −₹4,875). No transaction costs → Apr-2026 STT change not applicable. Rho: ρ_call=K·T·e^(−rT)·N(d₂); 60-day ATM ≈ ₹20/100bps. IV crush case anchored to 4 June 2024 election results (historical), labelled illustrative. IV = implied volatility throughout; "vol point" = 1 percentage point of IV. -->

# Chapter 11 — Vega and Rho: Volatility and Interest-Rate Sensitivity

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Define Vega and explain why it is the most important Greek in the Indian market.
2. Quantify how much a premium changes per 1 percentage point of implied volatility.
3. Recognise that Vega is highest for at-the-money, longer-dated options.
4. Understand why Vega is the Greek retail traders most underestimate.
5. Introduce Rho — interest-rate sensitivity — and its small but real role in India.
6. See how a modest IV change can offset days of Theta, and how the Greeks interact.

Delta, Gamma, and Theta measured your exposure to *price* and *time*. **Vega measures your exposure to volatility itself** — and in a market as event-driven as India's, it is the Greek that most often decides whether a trade lives or dies.

---

## 2. Introduction

Twice in this book you have met a trader who was right on direction and still lost money. The first time (Chapter 4) the culprit was time decay. The second (Chapter 5) it was a fall in implied volatility. Now we can name that second killer precisely.

On the evening before the 2024 general-election results, a trader buys a NIFTY call. Implied volatility is enormous — around 30% — because the market is braced for a huge move. The next day NIFTY does move, and *in the trader's direction*. Yet by the close their call is worth less than half what they paid. The move they predicted arrived, and they still lost more than fifty per cent.

The reason is **Vega**. Before the event, uncertainty had inflated every premium (an "IV expansion"). Once the result was known, uncertainty collapsed, IV crashed from ~30% to ~14% (an "IV crush"), and the premium deflated with it — faster than the price move could lift it. The trader owned the right direction but was crushed by the wrong volatility.

This chapter is about that force. **Vega is the change in an option's premium for a 1 percentage-point change in implied volatility** — and because IV in India swings violently around budgets, RBI meetings, elections, and global shocks, Vega is the Greek that turns "correct" trades into losses and "safe" income into disaster. We also meet **Rho**, the interest-rate Greek — small for the short-dated options most readers trade, but real for longer horizons. Setting throughout: **NIFTY at 24,600, lot 65, σ = 13%**, on the same BSM basis as Chapters 6, 8, 9, and 10.

---

## 3. Core Concepts

### 3.1 What Vega is

Vega is the flagship of this chapter.

**What is it?** **Vega (ν)** is the change in an option's premium for a **1 percentage-point change in implied volatility** (one "vol point" — e.g., IV moving from 13% to 14%). If an ATM NIFTY call has a Vega of ₹16, its premium rises about ₹16 when IV rises one point and falls about ₹16 when IV falls one point — *with the index, time, and rates unchanged*.

**Why does it exist?** Because volatility is one of the six price factors (Chapter 5), and it is the only one that is both unobservable and prone to violent, independent swings. Vega is the derivative of the BSM price with respect to σ: `ν = ∂C/∂σ`. It exists to measure the exposure that Chapter 5 called "the king factor."

**Why should a trader care?** Because IV can change by several points in a single session — far more than the other inputs — and Vega converts that into rupees. A trader who tracks Delta and Theta but ignores Vega is blind to the force that most often surprises them. As the introduction shows, Vega can overwhelm Delta entirely.

**Intuitive explanation.** If volatility is the "weather forecast" priced into every option (Chapter 5), Vega is **how much your premium changes when the forecast changes.** When a storm is expected, all insurance gets dearer (IV up, premiums up); when the sky clears, it gets cheaper (IV down, premiums down). Vega measures your sensitivity to that shifting forecast.

**Sign convention.** Vega is **always positive for long options** — both calls and puts — because more volatility raises every premium (Chapter 5). So option *buyers* are **long Vega** (they gain when IV rises); option *sellers* are **short Vega** (they gain when IV falls). This is why sellers dread a VIX spike and buyers dread the crush.

**Numerical feel.** An ATM NIFTY call with Vega ₹12, if IV rises from 12% to 15% (a 3-point rise), gains about 12 × 3 = **₹36** per unit — with the index perfectly still. On a lot (×65) that is ₹2,340 created by volatility alone.

**Mathematical form (BSM).**

```
ν = S · √T · n(d₁)          (per 1.00 of σ; divide by 100 for per 1 vol point)   (11.1)
```

where `n(d₁)` is the standard normal density. Two features fall out immediately: Vega is largest when `n(d₁)` is largest (at the money) and it grows with `√T` — so **Vega is highest for at-the-money, longer-dated options** (Sections 3.2–3.3).

**Professional interpretation.** Desks think in Vega constantly, because most professional option strategies are, at heart, *volatility* trades. "Long Vega" and "short Vega" describe a book's core bet more accurately than "bullish" or "bearish." A market maker may be Delta-neutral yet carry a large, deliberate Vega position — that *is* the trade.

**Common mistake.** Ignoring Vega and attributing every premium move to price or time. The "I was right and still lost" experience around events is almost always an unrecognised Vega loss.

**Practical takeaway.** **Vega is your exposure to the market's volatility forecast — the force that can outweigh direction entirely around events; always know whether you are long or short Vega before you hold through anything uncertain.**

---

### 3.2 Vega by moneyness — the ATM is most sensitive

Because Vega ∝ `n(d₁)` (equation 11.1), and the normal density peaks at the money, **at-the-money options have the highest Vega**, falling away toward the wings. Table 11.1 shows Vega across strikes at 10 DTE.

**Table 11.1 — Vega across strikes (NIFTY 24,600, 10 DTE; ₹ per 1 vol point; illustrative)**

| Strike | Moneyness | Vega (₹/1%) |
| ---: | --- | ---: |
| 24,000 | Deep ITM | 7.5 |
| 24,400 | ITM | 14.5 |
| **24,600** | **ATM** | **16.3** |
| 24,800 | OTM | 15.6 |
| 25,000 | OTM | 13.1 |
| 25,200 | Deep OTM | 9.6 |

The ATM strike is most sensitive to IV changes; deep ITM and deep OTM options respond less (a deep-ITM option is mostly intrinsic value, and a deep-OTM option has little value for IV to inflate). Note that Vega is **identical for a call and a put at the same strike** — volatility raises both equally.

---

### 3.3 Vega by time — the mirror of Gamma and Theta

Here is the fact that ties Part III together. Vega grows with `√T` — so **longer-dated options have higher Vega, and Vega *falls* as expiry approaches.** This is the exact *opposite* of Gamma and Theta, which grow as 1/√T and *explode* near expiry. Table 11.2 makes the contrast vivid for an ATM NIFTY option.

**Table 11.2 — ATM NIFTY: how the Greeks behave as expiry approaches (illustrative)**

| Days to expiry | Vega (₹/1%) | Gamma | Theta (₹/day) |
| ---: | ---: | ---: | ---: |
| 30 | 27.8 | 0.00043 | −6.1 |
| 10 | 16.3 | ~0.00075 | −10.6 |
| 5 | 11.5 | 0.00106 | −15.0 |
| 1 | 5.1 | 0.00238 | −33.5 |

Read the three columns together — this is the single most important structural insight of the Greeks:

* **Vega falls into expiry** (√T): a near-expiry option barely reacts to IV changes.
* **Gamma and Theta explode into expiry** (1/√T): a near-expiry option's Delta whips around and its time decay accelerates.

So **volatility risk lives in longer-dated options; price-acceleration and decay risk live in near-dated options.** If you want to trade volatility (an IV view), you use longer-dated options for the Vega. If you want to harvest decay or scalp Gamma, you use near-dated options. The tenor you choose *is* a choice about which Greek dominates your position.

> **Beginner Alert — Vega and Gamma pull in opposite directions on the calendar.** It is easy to lump "the Greeks" together as "all worse near expiry." Not so. Near expiry, Gamma and Theta are at their most dangerous, but Vega is at its *weakest*. Far from expiry, Vega is large but Gamma and Theta are small. This is why an IV spike hurts a monthly seller far more than a weekly seller, even though the weekly seller carries more Gamma risk.

---

### 3.4 Vega risk for option sellers — the VIX spike

For a premium seller, Vega is the hidden landmine beneath the steady Theta income. A seller is **short Vega**: they profit when IV falls but lose when it rises. And IV can rise *fast* — a geopolitical shock, a surprise policy, a global sell-off can send India VIX up 5–10 points in hours.

When that happens, every option the seller is short gains value, and the seller's mark-to-market loss can **wipe out weeks of accumulated Theta income in a single session** — before the underlying has even moved far. This is the Vega counterpart to the Gamma trap of Chapter 9: the Theta harvester collects small daily income and is exposed to two occasional disasters — a big *move* (short Gamma) and a big *IV spike* (short Vega). Often they arrive together, because volatility spikes precisely when the market moves violently.

> **Market Note — India VIX can double in a crisis.** In calm markets India VIX sits in the low teens; in the 2020 COVID crash it reached ~83 (Chapter 1), and around elections and shocks it routinely jumps to the mid-20s. A seller short, say, ₹475 of Position Vega per vol point (see Numerical Example 6) loses ₹4,750 for every 10-point VIX spike — from Vega alone, instantly, regardless of direction. Size short-Vega positions for the spike, not the calm.

---

### 3.5 Vega and events — the IV expansion/crush cycle

Vega is inseparable from India's event calendar. Around any scheduled event — budget, RBI policy, election results, major global data — implied volatility follows a predictable cycle (introduced in Chapter 5, now quantified through Vega):

* **IV expansion (before):** as the event nears, uncertainty rises, IV inflates, and every premium climbs — a gain for anyone long Vega, a loss for shorts.
* **IV crush (after):** once the outcome is known, uncertainty collapses, IV falls sharply, and premiums deflate — a gain for shorts, a loss for longs.

This is why **buying options just before an event is a Vega trap** (Chapter 5): you pay inflated, event-rich IV, and the crush afterwards frequently costs you more Vega than the move earns you in Delta. It is also why the **"vol crush trade"** — selling elevated IV before an event to profit from the post-event collapse — is a staple professional strategy, albeit one that carries the full move risk if the outcome surprises. The election case study in Section 9 is this cycle in its most extreme form.

---

### 3.6 The Vega–Theta interplay

Vega and Theta constantly push against each other for an option holder, and comparing them reveals how the Greeks net out day to day. Consider an ATM NIFTY option at 10 DTE: Vega ≈ ₹16.3 per vol point, Theta ≈ −₹10.6 per day.

A **3-point rise in IV** adds about 3 × 16.3 = **₹49** — which offsets roughly **5 days** of the ₹10.6/day Theta decay. So a buyer bleeding Theta can be rescued (temporarily) by an IV rise, and a seller collecting Theta can be overwhelmed by one. Conversely, an IV *fall* compounds the buyer's Theta bleed and adds to the seller's Theta gain.

The practical lesson: on any given day, a premium's change is a tug-of-war between Delta (price), Theta (time), and Vega (volatility). Attributing the change to only one of them — usually price — is why premium moves so often feel mysterious. A 3% IV shift can swamp a week of decay; ignore it and your P&L will keep surprising you.

---

### 3.7 Rho — interest-rate sensitivity

**Rho (ρ)** is the change in an option's premium for a 1 percentage-point (100 bps) change in the risk-free interest rate. From BSM:

```
ρ_call = K · T · e^(−rT) · N(d₂)          (per 1.00 of r; ×0.01 per 100 bps)      (11.2)
```

Rho is **positive for calls** (higher rates raise call values, via the cost-of-carry channel of Chapter 5) and **negative for puts**. Its defining feature is that it scales with `T` — so **Rho matters more for longer-dated options and is negligible for weeklies.**

* For a **60-day** ATM NIFTY call, Rho ≈ ₹20 per 100 bps — so a **25 bps rate cut lowers the call by about ₹5** (and raises the same-strike put by about ₹5).
* For a **weekly** option, the same 25 bps move changes the premium by well under a rupee — effectively zero.

In India, the anchor is the **RBI repo rate** and short-term government yields. Rho is the Greek you can safely ignore for the weekly and monthly trades that dominate retail activity, but it becomes relevant for 2–3 month positions, and around an active RBI rate-cutting or -hiking cycle. It is small — but, as Chapter 5 warned, "small" is not "zero."

---

### 3.8 Vega-neutral strategies

Just as you can neutralise Delta (Chapter 8), you can neutralise Vega — construct a position whose **net Vega is zero**, so that IV changes do not move its value. You do this by balancing long-Vega legs against short-Vega legs (typically options of different strikes or expiries, since Vega varies with both).

Why bother? Because sometimes you want to isolate a *different* Greek. A trader with a pure directional view (Delta) or a pure decay view (Theta) may want to strip out Vega so that an unexpected IV swing does not spoil the trade. Calendar spreads, ratio structures, and certain multi-leg positions are often built or adjusted to target a specific Vega — long Vega if you expect IV to rise, short Vega if you expect it to fall, or Vega-neutral if you have no IV view and want the other Greeks clean. The point is that **Vega is a dial you can set deliberately**, not just a risk you passively carry.

---

## 4. Examples (Real-World)

**Example 1 — The flat-market premium jump.** NIFTY closes almost unchanged, but India VIX rises from 13 to 16 ahead of an RBI meeting. Every ATM premium climbs — calls and puts together — purely on Vega. A straddle buyer profits on a flat day; a straddle seller loses. Price did nothing; Vega did everything.

**Example 2 — The pre-event trap.** A trader buys a NIFTY straddle before the budget when IV is elevated. The budget moves the market, but IV crushes afterwards; the straddle loses because the Vega crush outweighs the Delta gain. Paying rich event IV and hoping the move saves you is a Vega bet disguised as a direction bet.

**Example 3 — The monthly seller's bad hour.** A trader short a monthly strangle (high Vega, being longer-dated) is hit by a global shock that spikes VIX 8 points. Their mark-to-market loss is severe — not because NIFTY moved much, but because their large short Vega revalued instantly. A weekly seller with less Vega would have felt the IV spike far less.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65, σ = 13%; Vega per 1 vol point.

### Numerical Example 1 — Premium change from an IV move

An ATM NIFTY call has Vega ₹12. IV rises from 12% to 15% (a 3-point rise):

```
ΔC ≈ ν × Δσ = 12 × 3 = ₹36 per unit  (₹2,340 on a lot)
```

The premium rises ₹36 with the index perfectly still — the pure Vega effect.

### Numerical Example 2 — Vega by time (weekly vs monthly)

Compare ATM Vega at 1 week (7 DTE) versus 4 weeks (28 DTE):

```
Weekly  (7 DTE):  Vega ≈ ₹13.6 per vol point
Monthly (28 DTE): Vega ≈ ₹27.2 per vol point
```

The monthly is about **twice as sensitive to IV** (Vega ∝ √T; √(28/7) = 2). So an IV spike hurts a monthly position far more than a weekly one — the opposite of Gamma, where the weekly is the danger.

### Numerical Example 3 — A VIX spike across strikes

India VIX jumps from 12 to 22 (a +10 vol-point spike). Using the 10-DTE Vega from Table 11.1, the premium impact per unit:

| Strike | Vega (₹/1%) | Premium change (+10 vol points) |
| ---: | ---: | ---: |
| 24,600 (ATM) | 16.3 | +₹163 |
| 24,800 (OTM) | 15.6 | +₹156 |
| 25,000 (OTM) | 13.1 | +₹131 |
| 25,200 (deep OTM) | 9.6 | +₹96 |

Every long option gains; the ATM gains most (highest Vega). A trader short these strikes loses the same amounts — instantly, before the index has moved.

### Numerical Example 4 — The Vega–Theta interplay

ATM option at 10 DTE: Vega ₹16.3, Theta −₹10.6/day. A 3-point IV rise:

```
Vega gain = 3 × 16.3 = +₹49
Days of Theta offset = 49 ÷ 10.6 ≈ 4.6 days
```

A 3-point IV rise wipes out roughly **five days** of time decay — which is why an option buyer can be "saved" by rising IV and a seller ambushed by it.

### Numerical Example 5 — Rho on a 60-day option

A 60-day ATM NIFTY call has Rho ≈ ₹20 per 100 bps. The RBI cuts rates by 25 bps:

```
ΔC ≈ ρ × Δr = 20 × (−0.25) = −₹5 per unit  (call falls)
Put change ≈ +₹5 per unit  (put rises)
```

A tiny effect — and on a *weekly* option it would be a fraction of a rupee. Rho is real but minor for the tenors most readers trade.

### Numerical Example 6 — Position Vega of a short iron condor

A short iron condor (short 25,000 CE / long 25,200 CE, short 24,200 PE / long 24,000 PE) using 10-DTE Vegas:

```
Call side: short 25,000 CE (Vega 13.1) + long 25,200 CE (Vega 9.6) → net −3.5
Put side:  short 24,200 PE (Vega 11.3) + long 24,000 PE (Vega 7.5) → net −3.8
Position Vega (per unit) = −3.5 − 3.8 = −7.3
Position Vega (per lot)  = −7.3 × 65 ≈ −₹475 per vol point
```

The short iron condor is **net short Vega**: a 10-point VIX spike would cost about 10 × 475 ≈ **₹4,750** from Vega alone — a reminder that credit strategies bleed on IV spikes, not just on big moves.

---

## 6. Calculations (the reusable recipes)

**(a) Vega from BSM (per 1 vol point)**

```
ν = S · √T · n(d₁) / 100      (peaks at ATM; grows with √T → higher for longer-dated)
```

**(b) Premium change from an IV move**

```
ΔC ≈ ν × Δσ      (Δσ in vol points; e.g., IV 13% → 16% is Δσ = 3)
```

**(c) Position Vega (per vol point; use POSITION signs)**

```
Position Vega = Σ (νᵢ × Qᵢ × Lot size)     (negative for short legs → short Vega)
```

**(d) Rho (per 100 bps)**

```
ρ_call = K · T · e^(−rT) · N(d₂) × 0.01      (positive for calls, negative for puts; grows with T)
```

**(e) The tenor rule for the volatility Greeks**

```
Vega ∝ √T   → higher for longer-dated (falls into expiry)
Gamma, Theta ∝ 1/√T → higher for shorter-dated (explode into expiry)
```

---

## 7. Practical Insights

* **Always know your Vega sign.** Buyers are long Vega (helped by IV spikes, hurt by crushes); sellers are short Vega (the reverse). Around any uncertain event, this sign often matters more than your Delta.
* **Match tenor to the Greek you want.** Want a volatility bet? Use longer-dated options for the Vega. Want decay or Gamma? Use near-dated. Vega and Gamma/Theta live at opposite ends of the calendar.
* **Never buy inflated event IV expecting the move to save you.** The post-event IV crush frequently costs more Vega than the move earns in Delta — the introduction's trader, and the Section 9 case.
* **Size short-Vega positions for the spike.** A VIX jump can erase weeks of Theta income instantly, before the market moves. Judge credit strategies by their Position Vega, not just their Position Delta.
* **Ignore Rho on weeklies, respect it on quarterlies.** For short-dated trades it is noise; for 2–3 month positions and active RBI cycles it is a small but real factor.

> **Professional Insight — Most option trades are volatility trades in disguise.** When a professional puts on a "bullish" or "range" position, the *dominant* Greek is very often Vega, not Delta. They ask first: "Is implied volatility rich or cheap, and which way will it move?" — because getting the volatility call right (long Vega into an IV rise, short Vega into a crush) is frequently what makes or loses the money. If you track only Delta and Theta, you are trading a volatility instrument half-blind.

---

## 8. Common Mistakes

* **Ignoring Vega entirely.** Attributing every premium move to price or time, and being repeatedly blindsided by IV changes — the most common intermediate-trader gap.
* **Buying options into an event's inflated IV.** Paying rich event volatility and losing to the crush even when right on direction.
* **Selling monthly premium and forgetting the Vega.** Longer-dated shorts carry large Vega; a VIX spike revalues them brutally, independent of the move.
* **Confusing Vega's calendar with Gamma's.** Assuming Vega, like Gamma, is worst near expiry — it is actually weakest there and largest for longer-dated options.
* **Over-weighting Rho.** Building a thesis around interest-rate effects on short-dated options, where they are negligible.
* **Judging a credit strategy only by Delta.** A "market-neutral" iron condor is short Vega; an IV spike hurts it even if the index sits still.

---

## 9. Case Study — "IV Crush After the 2024 Election Results"

**Context.** The 2024 general-election results were declared on **4 June 2024**, one of the most volatility-charged events in recent Indian market history. In the run-up, India VIX spiked into the mid-20s (around 26–27 at its peak) as the market braced for a decisive move; premiums were enormously inflated, with many strikes' implied volatility near or above **30%**. The numbers below are **illustrative and representative** of what buyers experienced — verify exact levels from the archives — but the mechanism is precisely what unfolded.

**The setup.** A trader, expecting a market-friendly result, buys a near-ATM NIFTY **call** the evening before results, paying about **₹320** per unit. Implied volatility is ~30% — the premium is bloated with event uncertainty. The trader's directional thesis is essentially correct: over the next couple of sessions NIFTY ends *higher*.

**What happened.** Despite the favourable direction, the call collapsed:

* Once the result was known, uncertainty evaporated and **India VIX crushed from ~27 to ~14** within a day or two — an IV fall of roughly **15 vol points.**
* The call, bought at ~30% IV, revalued at ~14% IV. Even with the index up modestly and the option now slightly in the money, the premium fell to about **₹150** — a loss of roughly **₹170 per unit, over 50%**, on a trade whose *direction was right.*

**The P&L attribution (illustrative).** Decomposing the ~₹170 loss into its Greeks makes the lesson unmistakable:

| Greek | Driver | Contribution |
| --- | --- | ---: |
| Delta | NIFTY up modestly in the buyer's direction | **+₹30** |
| Vega | IV crush of ~15 vol points × Vega (~₹11–12) | **−₹170** |
| Theta | ~2 days of decay near expiry | **−₹30** |
| **Net** | | **≈ −₹170** |

The **Vega loss (−₹170) dwarfed the Delta gain (+₹30) by more than five to one.** The trader was right about the market and still lost half their money, because they were **long Vega into an IV crush** — they had, without realising it, made a volatility bet, not a direction bet.

**The analysis.** The error was structural, not analytical. The trader's directional call was fine; their mistake was *buying* options when IV was at an extreme, guaranteeing a large Vega headwind the moment uncertainty resolved. The market-friendly outcome the trader predicted was already priced into that 30% IV; there was no "surprise upside volatility" left to capture, only a crush to suffer. The traders who *profited* from the same event were those who **sold** the inflated IV before results (short Vega), collecting the crush — accepting, in exchange, the risk that a shock result could move the market beyond the rich premium they collected.

**The lesson.** Around a major event, the dominant Greek is **Vega, not Delta.** Before trading an event, ask not only "which way?" but "is IV rich, and what will it do after the event?" Buying options at event-inflated IV is a bet that the *realised* move will exceed the enormous *implied* move already priced — a high bar that a "correct" direction alone does not clear.

*(Takeaway: at events, you are trading volatility whether you mean to or not — being long options into an IV crush can lose even when your direction is exactly right.)*

---

## 10. Chapter Summary

* **Vega (ν)** is the change in premium per 1 vol point of implied volatility; `ν = S·√T·n(d₁)/100`. It is **always positive for long options** — buyers are long Vega, sellers short Vega.
* **Vega peaks at the money** (∝ n(d₁)) and is **identical for a call and put at the same strike.**
* **Vega grows with √T** — highest for **longer-dated** options and *falling* into expiry — the exact mirror of Gamma and Theta, which explode into expiry.
* **Sellers are short Vega:** a VIX spike can wipe out weeks of Theta income in hours, before the index moves.
* Vega drives the **event cycle** — IV expansion before, IV crush after — making pre-event option buying a Vega trap and pre-event selling a "vol crush" trade.
* A modest IV change is large: a **3-point IV rise ≈ 5 days of Theta** for a 10-DTE ATM option.
* **Rho (ρ)** is interest-rate sensitivity (`ρ_call = K·T·e^(−rT)·N(d₂)`), positive for calls, negative for puts; it scales with T — ~₹20 per 100 bps on a 60-day ATM call, negligible on weeklies.
* Vega can be **set deliberately** (long, short, or neutral) — most professional option trades are volatility trades at heart.

---

## 11. Key Takeaways

* **Know whether you are long or short Vega before holding through anything uncertain** — around events it outweighs direction.
* **Match tenor to intent:** longer-dated for volatility (Vega), near-dated for decay/Gamma — they sit at opposite ends of the calendar.
* **Never buy event-inflated IV expecting the move to rescue you;** the IV crush usually wins, as the 2024 election case shows.
* **Judge credit strategies by their Position Vega, not just Delta,** and size short-Vega positions for a VIX spike — the income can vanish in an hour.

---

## 12. Practice Questions

**Q1 (Definition).** Define Vega in one sentence, and state its sign for long calls and long puts.

**Q2 (Calculation).** An ATM option has Vega ₹15. IV falls from 18% to 13%. Estimate the premium change per unit and per lot (65).

**Q3 (Moneyness).** From Table 11.1, where is Vega highest across strikes, and why?

**Q4 (Tenor).** Which has higher Vega — a 7-DTE or a 28-DTE ATM option — and by roughly what factor? Contrast this with Gamma.

**Q5 (Seller's risk).** You are short a strangle collecting ₹675/day of Theta (per lot). India VIX spikes 8 points and your Position Vega is −₹500 per vol point (per lot). Estimate the immediate Vega P&L and compare it with your daily Theta income.

**Q6 (Event cycle).** Explain, in terms of Vega, why buying a straddle just before an event is often a poor trade even if a big move follows.

**Q7 (Interplay).** An ATM option at 10 DTE has Vega ₹16 and Theta −₹10/day. How many days of Theta does a 4-point IV rise offset?

**Q8 (Rho).** Why does a 25 bps RBI rate cut barely affect a weekly option but is noticeable on a 90-day option?

**Q9 (Attribution).** A call buyer is right on direction over an event but loses 50%. Decompose, in words, the likely Delta, Vega, and Theta contributions.

**Q10 (Judgement).** A trader says, "I only watch Delta and Theta; Vega is too abstract." Explain, with an example, why this is dangerous in the Indian market.

---

## 13. Detailed Solutions

**A1.** Vega is the change in an option's premium for a 1 percentage-point change in implied volatility. It is **positive for both long calls and long puts** (more volatility raises every premium).

**A2.** IV falls 5 points, so ΔC ≈ 15 × (−5) = **−₹75 per unit**, or −75 × 65 = **−₹4,875 per lot**. (A long holder loses; a short holder gains.)

**A3.** Vega is highest **at the money** (16.3 at the 24,600 strike), because Vega ∝ n(d₁), the normal density, which peaks at the money; deep ITM/OTM options have less time value for IV to inflate.

**A4.** The **28-DTE** option has higher Vega — about **twice** the 7-DTE (Vega ∝ √T, √(28/7) = 2). This is the *opposite* of Gamma, where the shorter-dated (7-DTE) option has the higher, more dangerous value.

**A5.** Vega P&L ≈ −500 × 8 = **−₹4,000** immediately (short Vega, IV up). Against Theta income of ₹675/day, that single spike wipes out about 4,000 ÷ 675 ≈ **6 days** of decay income — instantly, before the index has moved. The lesson: one VIX spike can undo nearly a week of a seller's patient Theta collection.

**A6.** Before an event, IV is inflated, so the straddle is expensive (you pay rich Vega). After the event, IV crushes, and being **long Vega**, you lose as premiums deflate. Unless the *realised* move exceeds the large *implied* move already priced into that inflated premium, the IV crush outweighs the Delta gain and the straddle loses — even with a big move.

**A7.** Vega gain = 4 × 16 = ₹64; days of Theta offset = 64 ÷ 10 = **6.4 days**. A 4-point IV rise offsets more than six days of decay.

**A8.** Rho scales with time to expiry (`ρ ∝ T`). A weekly option's T is tiny (7/365), so the rate term is minuscule and a 25 bps move changes the premium by a fraction of a rupee. A 90-day option's larger T gives it meaningfully more Rho, so the same rate move has a small but noticeable effect.

**A9.** **Delta:** positive but modest — the index moved in the buyer's favour, adding some value. **Vega:** large and negative — the post-event IV crush deflated the premium sharply (the dominant term). **Theta:** negative — a day or two of decay near expiry. The Vega loss overwhelms the Delta gain, so the net is a large loss despite the correct direction.

**A10.** It is dangerous because IV in India swings violently around frequent events (budget, RBI, elections, global shocks), and Vega converts those swings into large P&L that Delta and Theta cannot explain. Example: buying a call before election results with IV at 30%, being right on direction, and still losing over 50% when IV crushes to 14% — a pure Vega loss invisible to anyone watching only Delta and Theta.

---

## 14. Mini Glossary

* **Vega (ν)** — the change in an option's premium per 1 percentage point (vol point) of implied volatility; positive for all long options. → this chapter.
* **Vol point** — one percentage point of implied volatility (e.g., IV from 13% to 14%). → this chapter.
* **Long Vega / short Vega** — a position that gains when IV rises (option buyers) / gains when IV falls (option sellers). → this chapter.
* **Vega by moneyness** — highest at the money, falling toward the wings (∝ n(d₁)). → this chapter.
* **Vega by time** — grows with √T; higher for longer-dated options, falling into expiry (opposite of Gamma/Theta). → this chapter.
* **IV expansion / IV crush** — the rise in implied volatility before an event and its sharp fall afterwards. → this chapter.
* **Vol crush trade** — selling elevated pre-event IV to profit from the post-event collapse (short Vega). → this chapter.
* **Position Vega** — Σ(ν × quantity × lot size); the portfolio's exposure to IV changes. → this chapter.
* **Vega-neutral** — a position with zero net Vega, used to isolate other Greeks from IV changes. → this chapter.
* **Rho (ρ)** — the change in premium per 100 bps change in the interest rate; positive for calls, negative for puts; scales with T. → this chapter.

---

<!-- End of Chapter 11 (Rev 2, current as of 4 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026 revision) — per-lot conversions rescaled: numerical-feel ₹2,340; VIX-spike note ₹475/lot → ₹4,750 per 10-pt spike; NE1 ₹2,340; NE6 Position Vega −7.3×65 ≈ −₹475/lot, 10-pt spike ≈ ₹4,750; A2 −75×65 = −₹4,875. Per-unit Vega values and all IV-crush attribution figures are lot-independent — unchanged. Vega from σ=13% BSM basis (ν=S√T·n(d₁)/100): ATM 27.8@30d, 16.3@10d, 11.5@5d, 5.1@1d (∝√T, falls into expiry). Weekly(7d)≈13.6 vs monthly(28d)≈27.2, factor 2=√(28/7). Rho 60-day ATM ≈₹20/100bps → 25bps cut ≈ −₹5 call. Election IV-crush case (4 June 2024, historical): call ₹320→₹150 (−53%), attribution Vega −₹170 >> Delta +₹30. Q5 uses standalone hypothetical per-lot Greeks (₹675 Theta, −₹500 Vega) — self-contained, unchanged. No transaction costs → Apr-2026 STT change not applicable. Table 11.2 contrasts Vega (√T) vs Gamma/Theta (1/√T). IV = implied volatility. No forward chapter-number references. -->
