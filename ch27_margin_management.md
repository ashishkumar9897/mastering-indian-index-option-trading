<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 3, 12, 25, 26. Target length ~8,500 words. CLOSES Part VII. SPAN scans 16 scenarios (±1/2/3σ × vol up/down), margin = max-loss scenario + exposure. Naked NIFTY PE ~₹1.25L (SPAN 0.95L + exposure 0.30L). Margin by strategy: naked ₹1.25L, bull put spread ₹9,750, iron condor ₹7,800, calendar ~₹17.5k (benefit removed expiry day). Spread margining: add long 24,100 PE @₹60 (₹3,900) to naked 24,600 PE → margin 1.25L→₹23,530, frees ₹1,01,470 (26×). Margin efficiency = P&L/margin × 365/hold: IC ~1,640% vs naked strangle ~204% (theoretical). Peak margin: 4 random snapshots; penalty 0.5–5% of shortfall/day. Case study: over-utilized (88%) condor + VIX spike → MTM −50k + exposure +30k → shortfall → forced exit −35k (would've been +25k); fix = 30-40% buffer. IV = implied volatility. Rev 2 (5 Aug 2026): lot 75→65; all NIFTY margin figures rescaled (naked ₹1.45L→₹1.25L per revised Ch3, bull put ₹11,250→₹9,750, IC ₹9,000→₹7,800); efficiency ratios/26× preserved (num+denom both scale); account-level case/peak-margin figures unchanged. -->

# Chapter 27 — Margin Management and Portfolio Greeks in Practice

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Understand the SEBI SPAN margin framework for Indian index options.
2. Calculate and optimise margin requirements across strategies.
3. Manage portfolio-level Greeks in real time.
4. Understand the margin impact of SEBI's peak-margin rules.
5. Avoid margin shortfall and forced-liquidation scenarios.

This chapter closes Part VII by turning risk management (Chapter 25) and position sizing (Chapter 26) into the *operational reality* of trading: how margin is computed, how to optimise it, and how to manage a live book of Greeks without being forced out by a margin call. Margin is the constraint that governs *how much* you can trade and *whether you survive an intraday spike* — and managing it is a practical skill most traders learn only after a painful margin call.

---

## 2. Introduction

Margin is where risk management meets the broker's terminal. You can have the perfect risk framework and the ideal position size, but if you do not understand how margin is calculated, how it *changes* intraday, and how much buffer to keep, you can be *forced out of a winning position at the worst possible moment* — by a margin call you did not see coming. This chapter is the operational layer: the mechanics that determine whether your carefully sized, well-hedged book survives contact with a volatile session.

Two ideas dominate. First, **margin efficiency** — the same edge deployed through a defined-risk structure ties up a fraction of the capital a naked position demands, so *how you structure a trade determines how much of it you can do*. Adding a cheap hedge to a naked short can free lakhs of margin, transforming the trade's return on capital (Chapter 17's lesson, now made mechanical). Second, **margin buffer** — because margin *rises intraday* on a volatility spike, and because SEBI samples your margin at random moments (peak margin), a trader running near-full utilisation can be forced to liquidate — even a *profitable* position — when the spike hits and a snapshot catches the shortfall. The buffer is not optional; it is what stands between you and a forced exit.

This chapter builds the SPAN margin framework from the ground up, shows margin by strategy (and the enormous savings of defined risk), teaches margin optimisation and efficiency, explains the peak-margin rules and their traps, and covers real-time portfolio-Greek management. It closes with the case that every income trader must study — the margin call on a *winning* position, and the buffer that would have prevented it. Setting: **NIFTY at 24,600, lot 65**, building on the margin basics of Chapter 3 and the portfolio Greeks of Chapter 12.

---

## 3. Core Concepts

### 3.1 The SEBI SPAN margin framework

The SPAN framework is the flagship concept of this chapter — how margin is actually computed.

**What is it?** **SPAN (Standard Portfolio Analysis of Risk)** is the system SEBI's clearing corporations use to compute the margin on option and futures positions. It works by **scanning the position's loss across a grid of scenarios** and charging margin equal to the *worst-case loss*.

**How it works.** SPAN evaluates the position under **16 risk scenarios** — combinations of **price moves** (±1σ, ±2σ, ±3σ, and extreme moves) and **volatility moves** (up and down) — computing the position's loss in each. The **SPAN margin** is the largest loss across these scenarios: the worst plausible one-day outcome. On top of this sits the **exposure margin**, an additional buffer. So:

```
Combined margin = SPAN margin (worst-case scenario loss) + Exposure margin
```

For **buyers**, only the **premium margin** applies — the premium paid in full, upfront (Chapter 3), because a buyer's maximum loss is that premium.

**Why does it exist?** To ensure every participant carrying open-ended risk has posted enough collateral to cover a bad day, so the clearing corporation can guarantee settlement (Chapter 1). SPAN is scenario-based rather than formula-based precisely because option risk is *non-linear* — a simple "X% of notional" would misprice it; scanning scenarios captures the true worst case.

**Why should a trader care?** Because SPAN margin *determines how much you can trade* and *changes intraday with volatility*. Understanding it lets you (a) structure trades to minimise margin (defined risk vs naked, Section 3.2), (b) size within your margin, and (c) anticipate how a volatility spike will raise your margin (Section 3.4) — the difference between surviving a spike and being forced out.

**Numerical feel.** For a naked NIFTY 24,600 put, SPAN scans the scenarios; the worst (a large down-move with vol rising) produces a loss of ~₹95,000, so SPAN margin ≈ ₹95,000, plus ~₹30,000 exposure = **~₹1,25,000 combined** (Chapter 3). A defined-risk iron condor on the same underlying needs only ~₹7,800 — because its worst-case scenario loss is *capped* by the wings (Section 3.2).

**Professional interpretation.** Professionals think in *margin efficiency* — return per rupee of margin (Section 3.3) — not just return on capital, because margin is the binding constraint on how many positions they can run. Structuring for low margin is how they deploy the same edge across more positions.

**Common mistake.** Not knowing that margin *rises* on a volatility spike (even, partly, for defined-risk positions via exposure margin and MTM), and running so close to full utilisation that a spike triggers a call (Section 9).

**Practical takeaway.** **SPAN margin is the scenario-based worst-case loss (plus exposure) that determines how much you can trade and how much margin a volatility spike will demand — structure for low margin and keep a buffer for the spike.**

---

### 3.2 Margin by strategy — the defined-risk advantage

The single biggest driver of margin is *strategy structure*. Table 27.1 compares margin across structures on the same underlying.

**Table 27.1 — Margin by strategy (NIFTY, illustrative, per lot)**

| Strategy | Margin/lot | Why |
| --- | ---: | --- |
| Naked short put/call | ~₹1,25,000 | SPAN worst-case (large move + vol) + exposure — open-ended risk |
| Bull put spread (200-wide) | ~₹9,750 | ≈ max loss (spread width − credit); the long wing caps the risk |
| Iron condor (200-wide) | ~₹7,800 | ≈ max loss of *one* side (only one can be breached at expiry) |
| Calendar spread | ~₹17,500 | Margin on the near-term short, offset by the far long (benefit removed on expiry day) |

The pattern is decisive: **defined-risk structures require a fraction of the naked margin.** The naked short's ~₹1.25 lakh reflects its open-ended risk; the bull put spread's ~₹9,750 is just its capped max loss; the iron condor's ~₹7,800 is even lower because SEBI margins only *one* side (the index cannot breach both the call and put spreads at expiry). Two nuances:

* **Iron condor — one side, not both.** Because the index can finish beyond the calls *or* the puts but not both, SPAN charges the margin of the *wider-risk single side*, not the sum — so an iron condor's margin is roughly *one spread's* max loss, not two. This makes it more margin-efficient than the two spreads separately.
* **Calendar — near leg, benefit removed on expiry day.** A calendar's margin is on the near-term short, reduced by the far-term long. But post-2024, the **calendar-spread margin benefit is removed on the near leg's expiry day** (Chapters 1, 22), so the margin *rises* on expiry day — a trap for calendar holders who do not plan for it.

The takeaway echoes Chapter 17: **defined risk is not just safer, it is dramatically more capital-efficient** — the same capital runs far more defined-risk positions than naked ones.

---

### 3.3 Margin optimisation and efficiency

Given how margin varies, *optimising* it is a core skill.

**Spread margining — the cheapest margin you will ever buy.** Adding a protective long to a naked short converts it into a spread, collapsing the margin. The saving is enormous relative to the hedge's cost:

**Worked example.** A naked short 24,600 PE requires ~₹1,25,000 margin. Add a long 24,100 PE (500 points below) at ₹60 (cost ₹3,900), turning it into a 500-wide bull put spread:

```
New margin ≈ max loss = (500 − net credit ₹138) × 65 ≈ ₹23,530
Margin freed = 1,25,000 − 23,530 = ₹1,01,470, for a hedge costing ₹3,900
```

The ₹3,900 hedge **frees ₹1,01,470 of margin** — about 26 rupees of margin freed for every rupee of hedge cost. This is the "spread margining" benefit: the long wing costs a little but slashes the margin, letting you redeploy the freed capital (and capping your risk as a bonus). It is the single most powerful margin optimisation available.

**Portfolio margining — offsetting positions net down.** When positions partially *offset* each other's risk, SPAN charges margin on the *net* portfolio, not the sum of the parts. A book whose positions hedge one another (e.g., a long future against short calls, or offsetting spreads) requires *less* total margin than the sum of the individual margins — the portfolio-margin benefit. Adding a *hedging* position can therefore *reduce* your total margin, not increase it.

**Margin efficiency — the true measure.** The right metric for an income strategy is not return on capital but **return per rupee of margin**, annualised:

```
Margin efficiency = (Strategy P&L / Margin deployed) × (365 / holding period in days)
```

**Comparison.** An iron condor making ₹3,500 on ₹7,800 margin over 10 days versus a naked strangle making ₹7,000 on ₹1,25,000 over 10 days:

```
Iron condor: (3,500 / 7,800) × (365/10) = 0.449 × 36.5 ≈ 1,640% (annualised, theoretical)
Naked strangle: (7,000 / 1,25,000) × 36.5 = 0.056 × 36.5 ≈ 204% (annualised, theoretical)
```

The iron condor is ~8× more margin-efficient despite the *lower* absolute profit — because its tiny margin turns a modest profit into a huge return on the capital tied up. *(These annualised figures are theoretical maxima assuming continuous, always-winning redeployment; real returns are far lower with losses. Use margin efficiency to compare structures, not as a promised return.)*

> **Professional Insight — margin efficiency, not premium, decides what to trade.** A trader chasing the naked strangle's larger premium (₹7,000 vs ₹3,500) is optimising the wrong number. The professional sees that the iron condor deploys margin ~8× more efficiently and — crucially — frees capital to run *more* positions with *capped* risk. Over a year, the margin-efficient, defined-risk book compounds faster *and* survives the spike that ends the naked seller. Structure for margin efficiency; it is the constraint that governs how much of your edge you can actually deploy.

---

### 3.4 Peak margin and intraday snapshots

SEBI's **peak-margin** framework is where margin management becomes an intraday discipline, and where the unwary get penalised.

**How it works.** Rather than checking margin only at end-of-day, the clearing system takes **four random snapshots during the day** and requires that you had the *full applicable margin* at each snapshot. The *highest* margin requirement across the day's snapshots is your **peak margin**, and a shortfall at any snapshot triggers a **penalty**.

**The penalty.** A margin shortfall is penalised at **0.5% to 5% of the shortfall amount per day** — the rate rising for larger shortfalls, larger fractions of the applicable margin, and *repeated* offences (a habitual short-fall attracts the higher 5% rate). Illustratively, a ₹50,000 shortfall at 1% is ₹500/day; a repeated shortfall at 5% is ₹2,500/day — and the reputational/operational cost (broker restrictions) can exceed the rupee penalty.

**The peak-margin trap.** The danger is a *transient* margin spike caught by a random snapshot. If you **add positions mid-day before closing others** — so that, for a few minutes, both are open and margin is temporarily high — a random snapshot in that window can catch the spike and charge a peak-margin penalty, *even though your end-of-day margin is fine.* The margin you needed was only high for minutes, but the snapshot froze it.

**Sequencing to avoid the trap.** The fix is **trade sequencing**: *close before you open.* When rolling or restructuring, close the leg you are exiting *first* (freeing its margin), then open the new leg — so your margin never spikes above your available balance. For multi-leg entries, ensure you have peak margin covered for the *fully assembled* position before you start, or sequence the legs so the running margin stays within your balance. Never assume a transient mid-day spike is safe just because it will resolve by close — a snapshot does not care about your intentions.

> **Market Note — the snapshot does not know your plan.** "I was only over-margined for two minutes while I rolled" is no defence — if a random peak-margin snapshot lands in those two minutes, the penalty applies. Sequence every roll and restructure as *close-then-open*, and keep a buffer, so no transient spike can be caught above your available margin. The peak-margin system rewards the disciplined sequencer and penalises the careless one.

---

### 3.5 Portfolio Greeks management in practice

Chapter 12 taught the theory of portfolio Greeks; this is the *operational practice* of managing them live.

* **Real-time monitoring.** Modern broker platforms display **position-level and aggregate Greeks** (net Delta, Gamma, Theta, Vega) for your book in real time. Set up this dashboard as your primary risk view — you manage the *aggregate* Greeks (Chapter 12), not the individual legs.
* **Alert thresholds.** Set **alerts** for when any aggregate Greek breaches your limits — e.g., "alert if net Delta exceeds ±100 units," or "if net Vega exceeds −₹2,000/vol point." The alerts turn passive monitoring into active management: when a threshold trips, you adjust (Chapter 12's hierarchy — Delta first with futures, then Vega with options, then Gamma by sizing).
* **Daily Greek reconciliation.** Your broker's Greeks and your own calculations can *differ* — because they may use a different IV (last-traded vs a model IV), a different reference (spot vs future), or a different model. **Reconcile daily**: compare the broker's aggregate Greeks with your own, and understand any divergence (usually an IV-input difference). Trading off Greeks you have not reconciled means managing risk with a possibly-wrong instrument.
* **Adjustment to target ranges.** When the book's Greeks drift outside your target ranges (from market moves, Charm, Vanna — Chapter 12), bring them back with the least-cost adjustment: futures for Delta (cheap, preserves Theta/Vega), options for Vega, and sizing/structure for Gamma. The goal is to keep the *aggregate* Greek profile within pre-set bounds, not to react to every leg.

The practical loop: **monitor the aggregate Greeks live, alert on threshold breaches, reconcile daily, and adjust to target ranges** — the operational discipline that keeps a live book within the risk framework of Chapter 25.

---

### 3.6 Avoiding margin shortfall — the buffer

The chapter's ultimate practical lesson: **never run near-full margin utilisation — keep a buffer.**

Margin is not static. Intraday, your *required* margin can *rise* (a volatility spike raises exposure margin and SPAN scenario losses), and your *available* margin can *fall* (an unrealised MTM loss debits your balance). A trader running at, say, 90% utilisation has only a 10% buffer — and a volatility spike can easily consume it through the combination of a higher requirement and a lower balance, triggering a shortfall at a peak-margin snapshot. The result is a **margin call and forced liquidation** — often at the worst intraday prices, in the middle of the spike (Section 9).

The fix is a **margin buffer**: run at a *fraction* of your available margin — commonly **50–60% utilisation, keeping 30–40% free** — so that a spike's higher requirement and MTM drawdown can be absorbed *without* a shortfall. The buffer is the operational counterpart of position sizing (Chapter 26): sizing limits your *risk*, and the buffer ensures a *transient margin event* does not force you out of a position your risk framework says you can hold. As the case study shows, even a *winning* position can be lost to a margin call if the buffer is too thin.

> **Beginner Alert — full margin utilisation is a forced-exit waiting to happen.** The temptation is to deploy all your margin to maximise positions and premium. But margin *rises* when volatility spikes, exactly when you most want to hold — and if you have no buffer, the spike forces you out, often at a loss, on a position that would have been profitable. Never use more than ~60% of your available margin; the 30–40% buffer is what lets you *hold through* the spike instead of being liquidated by it.

---

## 4. Examples (Real-World)

**Example 1 — The ₹3,900 hedge that freed ₹1.01 lakh.** A trader holding a naked short NIFTY put (₹1.25 lakh margin) adds a long put 500 points below for ₹3,900. The position becomes a bull put spread; the margin collapses to ~₹23,530, freeing ₹1.01 lakh of capital (and capping the risk). The spread-margining benefit turned a capital-hungry naked short into an efficient, defined-risk position for a small hedge cost.

**Example 2 — The peak-margin penalty.** A trader rolls an iron condor by *opening* the new condor before *closing* the old one. For three minutes both are open and margin spikes above their balance; a random snapshot lands in that window, and they are penalised for the shortfall — despite the end-of-day margin being fine. Sequencing (close-then-open) would have avoided it.

**Example 3 — The buffer that saved the trade.** Two traders hold the same profitable iron condor into a VIX spike. One runs at 55% margin utilisation and absorbs the spike's higher requirement and MTM swing comfortably, holding to a profitable expiry. The other runs at 90%, gets a margin call at the spike, and is force-liquidated at a loss (Section 9). The only difference was the buffer.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65.

### Numerical Example 1 — SPAN scenario scan for a naked put

SPAN scans a naked short 24,600 PE across price × volatility scenarios; the worst-case loss sets the margin:

**Table 27.2 — SPAN scenario scan (naked short 24,600 PE, illustrative losses)**

| Scenario | Position loss |
| --- | ---: |
| −1σ move, vol up | ₹35,000 |
| −2σ move, vol up | ₹68,000 |
| −3σ move, vol up | **₹95,000 (worst)** |
| +2σ move, vol down | ₹0 (put gains) |

```
SPAN margin = worst-case loss = ₹95,000
Combined margin = SPAN ₹95,000 + Exposure ₹30,000 = ₹1,25,000
```

The margin equals the loss in the *worst* scenario (a large down-move with rising vol) — capturing the naked put's true one-day risk.

### Numerical Example 2 — The spread-margining benefit

Convert the naked short 24,600 PE (₹1,25,000 margin) into a spread by buying a long 24,100 PE at ₹60:

```
Hedge cost = 60 × 65 = ₹3,900
New (spread) margin ≈ (500 − 138 net credit) × 65 ≈ ₹23,530
Margin freed = 1,25,000 − 23,530 = ₹1,01,470
Margin freed per rupee of hedge = 1,01,470 / 3,900 ≈ 26×
```

The ₹3,900 hedge frees ₹1,01,470 of margin — 26 rupees freed per rupee spent — *and* caps the risk. The cheapest, most powerful margin optimisation there is.

### Numerical Example 3 — Margin efficiency comparison

```
Iron condor: ₹3,500 profit on ₹7,800 margin, 10-day hold
   Efficiency = (3,500/7,800) × (365/10) = 0.449 × 36.5 ≈ 1,640% (theoretical annualised)
Naked strangle: ₹7,000 profit on ₹1,25,000 margin, 10-day hold
   Efficiency = (7,000/1,25,000) × 36.5 = 0.056 × 36.5 ≈ 204% (theoretical annualised)
```

Despite the naked strangle's *double* the absolute profit, the iron condor is ~8× more margin-efficient — the tiny margin is what makes the modest profit a large return on capital deployed. (Theoretical figures for comparison, not promised returns.)

### Numerical Example 4 — Peak-margin penalty

A trader is short ₹40,000 of margin at a random snapshot (a transient roll spike):

```
First offence (0.5–1%): penalty ≈ 40,000 × 1% = ₹400 for the day
Repeated offence (5%): penalty = 40,000 × 5% = ₹2,000 for the day
```

A ₹400 penalty for a two-minute lapse is annoying; a habit of it (₹2,000/day at the 5% rate, plus possible broker restrictions) is expensive. Sequencing (close-then-open) avoids the shortfall entirely.

### Numerical Example 5 — Utilisation and the buffer

A ₹5 lakh account running an iron condor book at different utilisation levels, facing a VIX spike that raises the margin requirement by ₹30,000 and causes a ₹50,000 MTM drawdown:

```
At 90% utilisation (₹4.5L used, ₹0.5L buffer):
   Available after MTM = 5,00,000 − 50,000 = ₹4,50,000
   Required after spike = 4,50,000 + 30,000 = ₹4,80,000 → SHORTFALL ₹30,000 → margin call
At 55% utilisation (₹2.75L used, ₹2.25L buffer):
   Available after MTM = ₹4,50,000; Required = 2,75,000 + 30,000 = ₹3,05,000 → no shortfall, holds
```

The over-utilised account is force-liquidated by the spike; the buffered account absorbs it and holds to a profitable expiry. The buffer is the difference between surviving the spike and being forced out.

---

## 6. Calculations (the reusable recipes)

**(a) SPAN and combined margin**

```
SPAN margin = worst-case loss across the 16 price × volatility scenarios
Combined margin = SPAN margin + Exposure margin   (buyers: premium margin only)
```

**(b) Spread-margining benefit**

```
Margin freed = naked margin − spread margin;  Efficiency = margin freed / hedge cost
```

**(c) Margin efficiency**

```
Margin efficiency = (Strategy P&L / Margin deployed) × (365 / holding period in days)
```

**(d) Peak-margin penalty**

```
Penalty = shortfall × penalty rate (0.5%–5%/day, rising with size/repetition)
```

**(e) Margin buffer**

```
Utilisation = margin used / available margin;  keep utilisation ≤ ~60% (30–40% buffer)
```

---

## 7. Practical Insights

* **Structure for margin efficiency, not premium.** Defined-risk structures (spreads, condors) require a fraction of the naked margin and free capital to run more positions — the constraint that governs how much of your edge you can deploy.
* **Buy the spread-margining benefit — it is the cheapest margin you will ever get.** A small protective long collapses a naked short's margin (≈26× the hedge cost freed here) *and* caps the risk.
* **Sequence every roll as close-then-open** to avoid the peak-margin trap; a random snapshot does not care that the spike was transient.
* **Manage the aggregate Greeks live, alert on breaches, and reconcile daily** — trade off Greeks you have verified, adjusting Delta with futures, Vega with options, Gamma by sizing.
* **Never run above ~60% margin utilisation.** Margin *rises* on a volatility spike while your balance *falls* on MTM; the 30–40% buffer is what lets you hold a good position through the spike instead of being liquidated by it.

> **Professional Insight — margin management is where good risk plans die.** A trader can size perfectly (Chapter 26) and still be forced out by a margin call if they run no buffer — because margin is *dynamic*, rising exactly when volatility spikes. The professional treats available margin like a fuel gauge: never runs it near empty, sequences every trade to avoid transient spikes, and keeps enough buffer that an intraday volatility event is a non-event. The margin call on a winning position (Section 9) is the signature failure of a trader with a good strategy and no margin discipline.

---

## 8. Common Mistakes

* **Running near-full margin utilisation.** No buffer means a volatility spike (higher requirement + MTM drawdown) forces liquidation — even of a winning position.
* **Chasing naked premium over margin efficiency.** Optimising the larger absolute premium while ignoring that defined risk deploys margin ~8× more efficiently and survives the spike.
* **The peak-margin sequencing trap.** Opening a new position before closing the old, creating a transient spike a random snapshot can penalise.
* **Not knowing margin rises on a vol spike.** Assuming margin is static and being surprised when a spike raises the requirement mid-position.
* **Trading off unreconciled Greeks.** Managing risk with the broker's Greeks without reconciling them to your own, when an IV-input difference can misstate the exposure.
* **Forgetting the calendar-spread expiry-day margin.** Holding a calendar into its near leg's expiry day, when the margin benefit is removed and the requirement rises.

---

## 9. Case Study — "The Margin Call on a Winning Position"

**Context.** This is the operational failure that catches even careful traders: being *forced out of a profitable position* by a margin call, not because the trade was wrong, but because of thin margin buffer. It follows a trader ("M") running iron condors — a *defined-risk* strategy — who nonetheless loses a winning trade to a margin call during an intraday volatility spike. The culprit is not the strategy (which was sound and profitable) but **over-utilisation**. Figures are illustrative but representative; M has a ₹5 lakh account.

**The setup.** M is confident in iron condors (defined risk, high probability) and, seeing their capped loss, deploys aggressively — running a large condor book requiring **₹4.4 lakh of margin, 88% utilisation**, leaving only a **₹60,000 buffer**. The condors are, at entry, comfortably profitable and, if held to expiry in a range-bound market, would earn a solid profit. M reasons that because the risk is *defined*, running near-full margin is safe. This is the fatal misconception: *defined risk* limits the *loss*, but it does not prevent a *margin call* if the buffer is too thin.

**The spike.** Mid-cycle, a global risk event spikes India VIX. Two things happen at once, in the direction that consumes M's buffer:

* **The margin requirement *rises*.** The volatility spike increases the exposure margin and the SPAN scenario losses on M's short options — the requirement climbs by ~₹30,000.
* **The available margin *falls*.** The condors move against M intraday (an unrealised MTM loss of ~₹50,000 as the index approached a short strike during the spike) — debiting the available balance.

The combination is lethal to a thin buffer:

```
Available margin after MTM = 5,00,000 − 50,000 = ₹4,50,000
Required margin after spike = 4,40,000 + 30,000 = ₹4,70,000
Shortfall = 4,70,000 − 4,50,000 = ₹20,000 → margin call at a peak-margin snapshot
```

**The forced exit.** With a ₹20,000 shortfall caught at a random snapshot, M faces a margin call and, unable to add funds immediately, the broker **auto-squares off part of the position** — in the middle of the volatility spike, at the *worst intraday prices* (wide spreads, Chapter 3). The forced liquidation realises a loss of ~**₹35,000.**

**The cruel irony.** By expiry, the index reverted (the spike passed, as spikes do — Chapter 13's mean reversion), and the condors that were force-closed *would have expired for a profit of ~₹25,000.* M's sound, profitable, defined-risk strategy delivered a **₹35,000 realised loss instead of a ₹25,000 profit** — a ₹60,000 swing — *entirely* because of the margin call. The trade was right; the margin management was wrong.

**What would have prevented it.** The fix is not the strategy (the condor was correct) but the **margin buffer**:

* **Run at ~55% utilisation, not 88%.** At ₹2.75 lakh used and a ₹2.25 lakh buffer, the spike's ₹30,000 higher requirement and ₹50,000 MTM drawdown would have been absorbed comfortably — no shortfall, no call, and M holds to the profitable expiry (Numerical Example 5).
* **Recognise that margin is dynamic.** M's error was believing "defined risk" meant "safe to run at full margin." Defined risk caps the *loss*, but margin *rises* on a spike; the buffer is what lets you hold through it.

**The analysis.** This is the signature failure of a trader who has learned strategy and risk sizing but not *margin management*: a correct, well-sized, defined-risk position lost to a margin call because the buffer was too thin to absorb a routine volatility spike. The strategy did its job (capped risk, profitable at expiry); the *operational layer* — margin buffer — failed. It is a reminder that survival requires not just the right strategy and size, but the operational discipline to hold the position *through* the intraday events that a thin buffer converts into forced exits.

**The lesson.** Even a winning, defined-risk position can be lost to a margin call if you run without a buffer. Margin is dynamic — it rises on volatility spikes while your balance falls on MTM — so never run above ~60% utilisation. The 30–40% buffer is not idle capital; it is what lets you *hold your good positions through the spike* rather than being liquidated by it at the worst possible price.

*(Takeaway: margin is dynamic and rises on volatility spikes, so even a profitable defined-risk position can be force-liquidated without a buffer — never exceed ~60% margin utilisation, so an intraday spike is a non-event rather than a forced exit.)*

---

## 10. Chapter Summary

* **SPAN margin** is the scenario-based worst-case loss across 16 price × volatility scenarios; **combined margin = SPAN + exposure** (buyers pay only the premium margin).
* **Margin by strategy:** naked ~₹1.25 lakh (open-ended risk) vs bull put spread ~₹9,750 vs iron condor ~₹7,800 (one side only) vs calendar ~₹17,500 (benefit removed on expiry day) — **defined risk is dramatically more margin-efficient**.
* **Spread margining** is the cheapest margin optimisation: a ₹3,900 hedge frees ~₹1.01 lakh of margin (≈26×) *and* caps risk; **portfolio margining** nets offsetting positions down.
* **Margin efficiency** (P&L/margin × 365/hold) is the true metric — an iron condor is ~8× more efficient than a naked strangle despite lower absolute profit.
* **Peak margin:** four random daily snapshots require full margin at each; a **transient spike** (opening before closing) can be penalised (0.5–5% of shortfall/day) — **sequence close-then-open**.
* **Manage aggregate Greeks live** — dashboard, alert thresholds, daily reconciliation, and adjustment to target ranges (Delta via futures, Vega via options, Gamma via sizing).
* **Keep a margin buffer** — margin *rises* on a spike while balance *falls* on MTM, so never exceed ~60% utilisation; the 30–40% buffer lets you hold good positions through the spike.
* The **"Margin Call on a Winning Position"** case shows a profitable, defined-risk condor force-liquidated (−₹35,000 instead of +₹25,000) purely from 88% utilisation — the operational failure a buffer prevents.

---

## 11. Key Takeaways

* **Structure for margin efficiency** — defined-risk structures free capital and survive spikes; the spread-margining benefit frees far more margin than the hedge costs.
* **Sequence every roll close-then-open** to avoid the peak-margin trap; a random snapshot does not care that the spike was transient.
* **Manage and reconcile the aggregate Greeks live**, adjusting to target ranges with the least-cost tool (futures for Delta).
* **Never run above ~60% margin utilisation** — margin is dynamic and rises on spikes, and the 30–40% buffer is what lets you hold a winning position through the spike instead of being force-liquidated.

---

## 12. Practice Questions

**Q1 (SPAN).** In one or two sentences, how does SPAN compute the margin on a naked option, and what are the two components of the combined margin?

**Q2 (Margin by strategy).** Rank a naked short put, a bull put spread, and an iron condor by margin required, and explain why the iron condor is the lowest.

**Q3 (Spread margining).** A naked short put requires ₹1,25,000 margin. Adding a long put (cost ₹5,000) reduces the margin to ₹30,000. Compute the margin freed and the freed-margin-per-rupee-of-hedge.

**Q4 (Margin efficiency).** Strategy A makes ₹5,000 on ₹10,000 margin over 15 days; Strategy B makes ₹9,000 on ₹1,50,000 over 15 days. Compute each margin efficiency (annualised) and state which is better.

**Q5 (Peak margin).** Why can a trader who is over-margined for only two minutes (while rolling) still incur a penalty?

**Q6 (Sequencing).** What is the correct trade sequence when rolling a position, and why?

**Q7 (Penalty).** A trader has a ₹60,000 margin shortfall at a snapshot. Compute the penalty at the 1% and 5% daily rates.

**Q8 (Buffer).** A ₹5 lakh account runs at 85% utilisation. A spike raises the margin requirement by ₹40,000 and causes a ₹40,000 MTM loss. Is there a shortfall? Show the arithmetic.

**Q9 (Greeks in practice).** Name two reasons a broker's displayed Greeks might differ from your own calculations, and why reconciliation matters.

**Q10 (Case judgement).** In "The Margin Call on a Winning Position," the strategy was sound and would have expired profitable. What single change would have prevented the loss, and why?

---

## 13. Detailed Solutions

**A1.** SPAN computes margin by **scanning the position's loss across 16 price × volatility scenarios and charging the worst-case (largest) loss** as the SPAN margin. The combined margin is **SPAN margin + exposure margin** (an additional buffer). (Option buyers pay only the premium margin.)

**A2.** Margin required: **naked short put (~₹1.25 lakh) > bull put spread (~₹9,750) > iron condor (~₹7,800)**. The naked short has open-ended risk (high SPAN worst case); the bull put spread's margin is its capped max loss; the iron condor is *lowest* because the index can breach only *one* side (calls or puts, not both) at expiry, so SPAN margins only the single wider-risk side, not both spreads.

**A3.** Margin freed = 1,25,000 − 30,000 = **₹95,000**. Freed per rupee of hedge = 95,000 / 5,000 = **19×** — the ₹5,000 hedge frees ₹95,000 of margin (and caps the risk).

**A4.** A: (5,000/10,000) × (365/15) = 0.50 × 24.33 = **1,217%**. B: (9,000/1,50,000) × 24.33 = 0.06 × 24.33 = **146%**. **Strategy A is far more margin-efficient** (1,217% vs 146%) despite the lower absolute profit, because its tiny margin makes the modest profit a large return on capital deployed. (Theoretical annualised figures for comparison.)

**A5.** Because SEBI takes **four *random* snapshots during the day** and requires full margin at each. If a random snapshot lands in the two-minute window when the trader is over-margined (a transient spike from opening before closing), the shortfall at that instant is penalised — regardless of the trader's intention to resolve it moments later. The snapshot captures the instantaneous margin, not the plan.

**A6.** **Close the leg you are exiting *first*, then open the new leg** ("close-then-open"). This frees the closed position's margin *before* the new position adds its own, so the running margin never spikes above the available balance — avoiding a transient over-margin that a random peak-margin snapshot could penalise.

**A7.** At 1%: 60,000 × 1% = **₹600 per day**. At 5%: 60,000 × 5% = **₹3,000 per day**. The 5% rate applies to larger or repeated shortfalls, so a habitual shortfall is five times as costly (plus possible broker restrictions).

**A8.** Available after MTM = 5,00,000 − 40,000 = ₹4,60,000. Margin used at 85% = 4,25,000; required after spike = 4,25,000 + 40,000 = ₹4,65,000. Shortfall = 4,65,000 − 4,60,000 = **₹5,000 — yes, a shortfall.** The thin 15% buffer (₹75,000) was consumed by the combination of the higher requirement (₹40,000) and the MTM loss (₹40,000), triggering a call.

**A9.** Two reasons: (i) **different IV input** — the broker may use the last-traded IV while you use a model or mark IV, changing every Greek; (ii) **different reference or model** — spot vs futures as the underlying, or a different pricing model. Reconciliation matters because you *manage risk off the Greeks*; if the displayed Greeks are wrong (a stale or divergent IV), you are adjusting your book with a faulty instrument and may mis-hedge your true exposure.

**A10.** **Running a margin buffer** — e.g., ~55% utilisation instead of 88%. With a larger buffer (~₹2.25 lakh free instead of ₹60,000), the spike's higher margin requirement (₹30,000) and the MTM drawdown (₹50,000) would have been absorbed *without* a shortfall, so no margin call, no forced liquidation — and M would have held the sound, defined-risk condor to its profitable expiry. The strategy was correct; only the operational margin buffer was missing.

---

## 14. Mini Glossary

* **SPAN margin** — the worst-case loss across 16 price × volatility scenarios, charged as margin on option/futures positions. → this chapter.
* **Exposure margin** — an additional buffer margin on top of SPAN. → this chapter.
* **Combined margin** — SPAN + exposure (the total margin for sellers; buyers pay premium margin). → this chapter.
* **Spread margining** — the reduction in margin from adding a protective long to a naked short (converting it to a spread). → this chapter.
* **Portfolio margining** — the netting of offsetting positions' risk, reducing total margin below the sum of the parts. → this chapter.
* **Margin efficiency** — return per rupee of margin, annualised; the true measure of capital use for income strategies. → this chapter.
* **Peak margin** — the requirement that full margin be available at four random daily snapshots; the highest snapshot sets it. → this chapter.
* **Peak-margin trap** — a transient mid-day margin spike (opening before closing) caught by a random snapshot and penalised. → this chapter.
* **Margin shortfall penalty** — 0.5%–5% of the shortfall per day, rising with size and repetition. → this chapter.
* **Margin buffer** — the unused margin (≈30–40%) kept free to absorb intraday requirement increases and MTM swings. → this chapter.
* **Greek reconciliation** — comparing the broker's displayed Greeks with your own to catch IV/model differences. → this chapter.

---

<!-- End of Chapter 27 (CLOSES Part VII). Rev 2 (5 Aug 2026): lot 75→65; NIFTY margins rescaled (naked ₹1.45L→₹1.25L per revised Ch3, bull put ₹11,250→₹9,750, IC ₹9,000→₹7,800, calendar ₹20k→₹17.5k); efficiency ratios/26× preserved; account-level case + peak-margin figures unchanged. SPAN 16 scenarios (Table 27.2), naked PE margin ₹1.25L (SPAN 0.95L + exposure 0.30L). Margin by strategy Table 27.1 (naked 1.25L, bull put 9,750, IC 7,800 one side, calendar 17.5k benefit removed expiry day). Spread margining: long 24,100 PE @₹60 (₹3,900) → margin 1.25L→₹23,530, frees ₹1,01,470 (26×). Margin efficiency: IC ~1,640% vs naked strangle ~204% (theoretical). Peak margin 4 snapshots, penalty 0.5-5%. Buffer: never >60% utilisation. Case study: 88% utilisation condor + VIX spike (req +30k, MTM −50k) → ₹20k shortfall → forced exit −₹35k (would've been +₹25k); fix 55% utilisation (account-level, unchanged). Q3 freed ₹95,000 (19×), Q4 A 1,217% vs B 146%; Q7 ₹600/₹3,000; Q8 ₹5,000 shortfall. Ch3 margin, Ch12 Greeks. IV = implied volatility. Part VIII previewed without number. -->
