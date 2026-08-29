<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 13, 14, 15, 18, 19. Target length ~9,500 words. Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Per-unit values (straddle premiums, IV crush /unit, gap loss /unit, Vega) lot-independent — unchanged; only "/lot" conversions rescaled to lot 65. Events not tied to expiry weekday (Budget 1 Feb, RBI bi-monthly) → no Tuesday/Thursday change; gross P&L → Apr-2026 STT change not applicable to numbers. IV cycle (Budget straddle, NIFTY 24,600): Day−10 IV13% ₹250 → Day−1 IV20% ₹400 (peak) → crush → normalize. Expected move = eve straddle ₹400 = ±400. IV crush profit = short straddle Vega (−32.6/vol pt) × crush 7 = +₹228/unit (₹14,820/lot). Gap risk: short strangle 24,200PE/24,800CE credit ₹183 (₹11,895/lot); gap to 23,400 → −₹617/unit (₹40,105/lot). Sizing: 3%×₹10L=₹30,000 → naked 0 lots, condor (₹7,800/lot) 3 lots. Case study Budget 2024 (+120, +₹150/unit=₹9,750/lot) vs 2025 (+550, −₹160/unit=−₹10,400/lot): same strategy, opposite outcome by move vs priced ±400 → probabilistic. Q6 rescaled to lot 65 (naked ₹35,750/lot → 1 lot; condor ₹8,000 → 5 lots). IV = implied volatility. -->

# Chapter 23 — Event-Based Trading: Budget, RBI, Elections, and Global Triggers

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Identify and categorise the major market-moving events for Indian index options.
2. Understand the IV cycle around events — build-up, peak, and crush.
3. Deploy the right strategies before, during, and after events.
4. Size positions correctly for event risk.
5. Understand overnight gap risk and its impact on option positions.

India's market runs on a calendar of events — the Budget, RBI policy, elections, global data — each one a scheduled collision of uncertainty and opportunity. This chapter turns the volatility work of Part IV (the IV cycle, Chapters 5, 11, 13) and the strategies of Part V into a systematic approach to trading around those events, where implied volatility is the dominant force and gap risk the dominant danger.

---

## 2. Introduction

Every event trader faces the same paradox. An event — the Union Budget, an RBI decision, an election result — is *guaranteed* to move the market, and yet trading it is treacherous, because the market *knows the event is coming* and has already priced it in. By the eve of the Budget, implied volatility has inflated every option, so a trader who buys a straddle "because the Budget will move things" pays a premium so rich that even a large move may not cover it — and the post-event **IV crush** deflates the premium the moment the outcome is known. The event delivers the move and the buyer still loses. This is the central lesson of Chapter 11, now made into a discipline.

Event trading is therefore not about *predicting* the outcome — it is about understanding the **IV cycle** and positioning for it *probabilistically*. Implied volatility follows a reliable arc around every scheduled event: it builds up in the days before, peaks on the eve, and crushes immediately after. The professional does not bet on which way the Budget moves the market; they bet on the *volatility* — selling the inflated pre-event premium to capture the crush, using calendars to harvest the differential, and sizing tiny to survive the overnight gap that no hedge can protect against.

This chapter maps India's event calendar, dissects the IV cycle, shows the pre- and post-event strategies (the vol-crush sell, the pre-event calendar, the directional post-gap play), quantifies the gap risk that makes naked shorts over events so dangerous, and teaches event position sizing. It closes with the case that proves the thesis: the *same* pre-event strategy, run through two consecutive Budgets, profiting once and losing once — because event trading is probabilistic, not predictive. Setting: **NIFTY at 24,600, lot 65**, drawing on the IV work of Part IV and the strategies of Part V.

---

## 3. Core Concepts

### 3.1 India's event calendar

Event trading starts with knowing *which* events move the market and *when*. India's calendar has four tiers:

* **Scheduled events** (known dates): the **Union Budget** (annually, 1 February), **RBI Monetary Policy** (bi-monthly), **quarterly earnings season** (constituent results moving the index), and **GST Council meetings**. These have fixed dates, so the IV cycle around them is predictable and tradable.
* **Quasi-scheduled events** (known window, uncertain timing): **general elections** (every five years) and **state elections** (periodic). The dates are known but the market impact is binary and large.
* **Global triggers** (external, scheduled or not): **US Fed decisions**, **US data (NFP, CPI)**, **geopolitical events**, and **crude oil spikes** — India is not insulated, and global cues gap the NIFTY overnight.
* **Surprise events** (unscheduled): **regulatory changes** (SEBI circulars), **geopolitical crises**, and **pandemic-type shocks**. These have no IV build-up (no one saw them coming), so they *spike* IV rather than crush it — a crucial distinction (Section 3.5).

The key division is **scheduled vs surprise**: scheduled events let IV *build up and then crush* (you sell the inflation before the event); surprise events *spike* IV with no warning (you sell the elevation after, as it reverts). Most event trading is around the scheduled events, whose IV cycle is the subject of the next section.

---

### 3.2 The IV cycle around events

The IV cycle is the flagship concept of this chapter — the reliable arc that makes scheduled events tradable.

**What is it?** Around every scheduled event, implied volatility follows a predictable four-phase cycle: **build-up → peak → crush → normalise.**

* **Build-up (5–10 days before):** as the event nears, uncertainty rises and traders buy protection, so IV climbs and every premium inflates.
* **Peak (the eve):** IV reaches its maximum the day before the event, when uncertainty is greatest.
* **Crush (immediately after):** the moment the outcome is known, uncertainty collapses, IV crashes, and premiums deflate — the "IV crush" (Chapter 11).
* **Normalise (3–5 days after):** IV drifts back to its baseline as the market digests the outcome.

**Why does it happen?** Because implied volatility is the market's forecast of *future* movement (Chapter 13), and a scheduled event is a *known dose of future uncertainty*. As the event approaches, that uncertainty looms larger in the near-term options' remaining life, inflating their IV; once the event passes, the uncertainty is resolved and the IV that priced it evaporates.

**Why should a trader care?** Because the IV cycle, not the direction, determines most event-trade P&L. A trader who ignores it *buys* inflated pre-event premium and loses to the crush; a trader who understands it *sells* the inflation and profits from the crush, or at least avoids paying for volatility that is about to disappear.

**Intuitive explanation.** The pre-event premium is like a **hotel room the night before a festival** — everyone wants it, so the price spikes; the morning after, the price collapses back to normal, regardless of how good the festival was. Buying the room at the peak price and hoping the festival is amazing enough to justify it is the option buyer's event trap.

**Numerical feel.** Table 23.1 shows a NIFTY ATM straddle through a Budget IV cycle.

**Table 23.1 — NIFTY ATM straddle through a Budget IV cycle (illustrative)**

| Timing | India VIX / ATM IV | ATM straddle (₹) | Phase |
| --- | ---: | ---: | --- |
| Budget − 10 days | 13% | 250 | Baseline |
| Budget − 5 days | 15% | 300 | Build-up |
| Budget − 2 days | 18% | 360 | Build-up |
| **Budget eve (−1)** | **20%** | **400** | **Peak** |
| Budget day + 1 | 13% | (deflated) | Crush |
| Budget + 5 days | 12% | (normalised) | Normalise |

The straddle inflates from ₹250 to ₹400 (60%) purely on the IV build-up, then crushes back after the event — the arc the event trader must position for.

**Professional interpretation.** Professionals trade the *cycle*, not the outcome: they sell the inflated pre-event premium (the vol-crush trade, Section 3.6), or use calendars to harvest the differential crush (Section 3.4), treating the direction of the event as a risk to manage, not a bet to make.

**Common mistake.** Buying options into the peak ("the Budget will surely move the market") and losing to the crush even when the move comes — the pre-event Vega trap (Chapter 11).

**Practical takeaway.** **Around a scheduled event, IV builds up, peaks on the eve, and crushes after — trade the volatility cycle, not the outcome; the reliable edge is selling the inflation and capturing the crush, not predicting the direction.**

---

### 3.3 The expected move — the market's own forecast

The single most useful number in event trading is the **expected move**, read straight off the pre-event straddle. As established in Chapters 13 and 18, the **ATM straddle premium ≈ the market's expected move** over the option's life:

```
Expected event move (± points) ≈ Event-eve ATM straddle premium
```

With the Budget-eve straddle at ₹400 (Table 23.1), the market is pricing an expected Budget-day move of about **±400 points (±1.6%)**. This is the market's own, IV-derived forecast of how much the event will move the index — and it is the yardstick for every event trade:

* A **straddle/strangle seller** profits if the actual move is *less* than ±400 (the crush plus contained move outweighs the Gamma loss); loses if it is *more*.
* A **straddle buyer** profits only if the actual move *exceeds* ±400 by enough to overcome the IV crush — a high bar, because the ₹400 already prices a large move.

The expected move reframes every event trade as a single question: **will the actual move be larger or smaller than what the pre-event straddle is pricing?** That is the bet — not the direction.

---

### 3.4 Pre-event strategies

Before a scheduled event, with IV building toward its peak, the strategies split by whether you are buying or selling volatility:

**Long straddle / strangle (buy volatility — rare windows).** Buying volatility *before* IV peaks can work *if* you enter early in the build-up (5–10 days out) when IV is still low, and exit *before* the crush. This is a narrow window: you profit from the IV build-up (long Vega) but must exit before the event resolves and crushes it. Holding a long straddle *through* the event is the classic trap (you pay peak IV and eat the crush). Rarely the right trade, and only with precise timing.

**Debit spreads (buy volatility with limited Vega).** A debit spread (bull call / bear put) expresses a directional view with *less* Vega than a long option, so it suffers *less* from the crush. If you have a directional lean into an event and IV is not yet at its peak, a debit spread is a more crush-resistant way to buy than a naked long option.

**Calendar spreads (sell the near, buy the far — the differential crush).** The pre-event calendar (Chapter 19) — sell the event-week expiry, buy the next — is the elegant event trade: it captures the **differential IV crush**, because the near-term (event-week) IV is *more* inflated and crushes *harder* than the far-term. As shown in Chapter 19's RBI case, selling the near @rich event IV and buying the far @calmer IV, then holding through a *contained* move, profits from the near crushing more than the far. It is long Vega overall but structured to harvest the near-term event premium — the professional's pre-event structure.

The unifying pre-event principle: **sell the inflated near-term premium (via a short straddle/strangle or a calendar) to capture the crush; if you must buy, use a debit spread to limit the Vega you will lose.**

---

### 3.5 Post-event strategies — and the scheduled/surprise distinction

After the event, the environment depends on whether it was *scheduled* (IV crushed) or a *surprise/crisis* (IV spiked):

**After a scheduled event (IV crushed to low levels):**

* **Directional plays on the post-gap move.** Immediately after the event, the index has gapped/moved and IV, while crushing, may still be somewhat elevated before fully normalising. A directional trade (debit or credit spread) on the post-event move can work while some IV elevation remains — but selling premium here collects *less* (IV is now low), so directional structures usually fit better than pure premium-selling.
* **Do not chase the crushed premium.** Selling a straddle *after* a scheduled crush collects thin premium (IV is low) with the risk that IV *rises* again — a poor risk/reward. The premium-selling edge was *before* the event, not after.

**After a surprise/crisis event (IV spiked):**

* **Sell the elevated premium as it mean-reverts.** A surprise shock (a geopolitical crisis, a pandemic) *spikes* IV with no build-up. Here the elevated premium is *post*-event, and selling it (short straddle/strangle or, safer, iron condor) as IV mean-reverts down is the trade — the "sell the spike" of Chapter 13's COVID Phase 4. This is the *opposite* timing to a scheduled event.

The crucial distinction: **for scheduled events, the elevated premium is *before* (sell before the crush); for surprise events, it is *after* (sell after the spike, as it reverts).** Confusing the two — selling thin post-crush premium on a scheduled event, or missing the post-spike opportunity on a surprise — is a common error.

---

### 3.6 The vol-crush trade

The **vol-crush trade** is the purest expression of event trading: a bet that IV will *fall* after a scheduled event, structured to profit from the crush.

**The mechanics.** Sell the inflated pre-event premium (a short straddle, strangle, or iron condor) on the eve, capturing the IV crush the next day. The profit from the crush alone:

```
IV crush profit = Position Vega × (pre-event IV − post-event IV)
```

**Worked example.** Sell the ATM straddle on Budget eve. A short straddle has Position Vega ≈ **−₹32.6/vol point** (two ATM legs, each ~₹16.3, Chapter 11). IV crushes from 20% to 13% (7 vol points):

```
IV crush profit = −32.6 × (13 − 20) = −32.6 × (−7) = +₹228/unit (if NIFTY is unchanged)
```

The seller gains ₹228/unit from the crush *alone*, before any move. But the short straddle is also short Gamma — if NIFTY *moves*, the Gamma loss offsets (or overwhelms) the crush gain. So the vol-crush trade is really a bet that **the crush gain exceeds the move loss** — i.e., that the actual move is *smaller* than the expected move the premium priced (Section 3.3). It is a positive-expectancy trade (the crush is reliable) that loses on the events where the move is large — exactly the probabilistic nature the case study illustrates.

**The defined-risk version.** Because the naked short straddle carries the gap risk (Section 3.7) and unlimited exposure, the *safer* vol-crush trade is a defined-risk structure — an **iron condor** (short vol, capped loss) or a **calendar** (differential crush, defined debit). These capture most of the crush with a bounded downside — the professional's preferred way to trade the crush through an event.

> **Beginner Alert — the vol-crush edge is real but not free.** Selling pre-event premium to capture the crush has genuine positive expected value — the IV crush is one of the market's most reliable phenomena. But "reliable on average" is not "safe on every event." The crush gain is offset by the Gamma loss if the move is large, and a single big-move event can wipe out several successful crush trades. The edge is captured by *repeating* the trade with *consistent, small sizing* and *defined risk* — not by predicting which events will be calm.

---

### 3.7 Overnight gap risk

The defining danger of event trading is the **overnight gap** — and it is why holding naked short options over events can be catastrophic.

**What is it?** The Indian market is closed from 3:30 PM to 9:15 AM. An event that resolves overnight (or a global shock) can *gap* the index far beyond where it closed, and **you cannot hedge or exit during the gap** — the market is shut. You wake to a position already deep in the money against you, with no chance to have reacted.

**The magnitude.** Table 23.2 shows illustrative overnight gap sizes for NIFTY.

**Table 23.2 — NIFTY overnight gap risk (illustrative, ~10-year range)**

| Situation | Typical overnight gap | Notes |
| --- | --- | --- |
| Normal session | ±0.3–0.8% | Routine |
| Scheduled event (Budget/RBI) | ±1–3% | The IV build-up prices this |
| Election result / major event | ±4–6% | e.g., ~−6% intraday, 4 June 2024 |
| Crisis (pandemic, shock) | ±10–13% | e.g., COVID, March 2020 (lower circuit) |

**Why it is lethal for naked shorts.** A short strangle sits calm until a gap blows through its breakeven overnight, when the seller can do *nothing*. Consider the 24,200 PE / 24,800 CE strangle (credit ₹183, breakevens ~24,017 / 24,983). If NIFTY gaps to **23,400** overnight (a −4.9% event gap):

```
Short 24,200 PE now ITM by 800 → loss = 800 − 183 = ₹617/unit = ₹40,105/lot
```

A single overnight gap turns a ₹11,895 maximum profit into a ₹40,105 loss — un-hedgeable, because it happened while the market was closed. This is why **naked short options over an event are among the most dangerous positions in the market**: the one risk you cannot manage (the gap) is exactly the one events create.

---

### 3.8 Position sizing for events

Because of the gap risk, **event position sizing is more conservative than normal** — the rule of thumb is **20–30% of your normal size through events**, or defined-risk only. The method is to work *backward* from the gap risk:

```
Max event risk = X% of capital → work backward to lots
Lots = Max event loss allowed ÷ Loss per lot on the gap scenario
```

**Worked example.** You allow a maximum event loss of **3% of a ₹10 lakh account = ₹30,000**. From Section 3.7, a naked short strangle could lose **₹617/unit = ₹40,105/lot** on a −4.9% gap. Then:

```
Max naked lots = 30,000 ÷ 40,105 = 0.75 → 0 lots (a single lot already breaches the limit)
```

The gap risk means even *one* naked lot exceeds a sensible event risk limit — so you either **do not hold naked shorts over the event** or switch to a **defined-risk structure**. An iron condor with a ₹7,800/lot max loss allows 30,000 ÷ 7,800 = **3 lots** within the same limit, *and* the loss is capped regardless of gap size. This is the core event-sizing lesson: **through events, use defined risk and small size — the gap is the risk you cannot manage, so cap it structurally.**

> **Market Note — the gap is why defined risk wins at events.** A naked strangle and an iron condor may collect similar-ish premium on a calm event, but their behaviour on the *gap* is worlds apart: the naked strangle's loss is unbounded and un-hedgeable, while the condor's is capped at its wing width no matter how far the index gaps. Since events are precisely when gaps occur, defined-risk structures are not merely "safer" for event trading — they are the *only* structures whose worst case you actually know in advance.

---

## 4. Examples (Real-World)

**Example 1 — The pre-event premium spike.** In the ten days before the Budget, with NIFTY flat, the ATM straddle inflates from ₹250 to ₹400 (Table 23.1) purely on the IV build-up. A trader who bought the straddle early (at ₹250) and sold it on the eve (at ₹400) profited from the build-up alone — but one who bought at the ₹400 peak and held through faced the crush.

**Example 2 — The differential-crush calendar.** Before an RBI policy, a trader sells the event-week option (rich event IV) and buys the next-month (calmer IV), a calendar. After a contained policy, the near-term IV crushes far more than the far-term's, and the calendar profits from the differential (Chapter 19's RBI case).

**Example 3 — The gap that could not be hedged.** A trader holds a naked short strangle over an election result. The result shocks the market, which gaps −6% overnight. The short put is deep ITM at the open, the trader could do nothing while the market was closed, and the loss dwarfs the premium collected — the gap risk realised (Section 3.7).

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65; Budget IV cycle from Table 23.1.

### Numerical Example 1 — The expected move

The Budget-eve ATM straddle is ₹400:

```
Expected Budget-day move ≈ ±₹400 (±1.6%) → range ≈ 24,200 to 25,000
```

A seller profits if NIFTY finishes within ±400; a buyer needs a move *beyond* ±400 to overcome the crush. The straddle price is the market's own forecast — the event bet is "larger or smaller than ±400?", not "up or down?"

### Numerical Example 2 — IV crush profit

Sell the ATM straddle on the eve (Position Vega ≈ −₹32.6/vol point). IV crushes from 20% to 13% (7 points):

```
IV crush profit = −32.6 × (13 − 20) = +₹228/unit (₹14,820/lot), if NIFTY is unchanged
```

The crush alone delivers ₹228/unit. But the position is short Gamma — a move offsets this: the net P&L is the crush gain *minus* the Gamma loss from the actual move, so the trade profits only if the move is contained (smaller than the expected ±400).

### Numerical Example 3 — Gap risk on a naked short

Short strangle 24,200 PE / 24,800 CE, credit ₹183 (₹11,895/lot). NIFTY gaps to 23,400 overnight (−4.9%):

```
Short 24,200 PE ITM by (24,200 − 23,400) = 800 → loss = 800 − 183 = ₹617/unit (₹40,105/lot)
```

A ₹11,895 max-profit trade becomes a ₹40,105 loss on one overnight gap — un-hedgeable, because it happened while the market was closed. The gap risk dwarfs the premium.

### Numerical Example 4 — Event position sizing

Max event loss allowed = 3% of ₹10 lakh = ₹30,000.

```
Naked strangle (gap loss ₹40,105/lot): max lots = 30,000 ÷ 40,105 = 0.75 → 0 (one lot breaches the limit)
Iron condor (max loss ₹7,800/lot): max lots = 30,000 ÷ 7,800 = 3.85 → 3 lots (loss capped at ₹23,400)
```

The gap risk rules out naked shorts within a sensible limit; the defined-risk condor allows a position *and* caps the loss regardless of the gap. Through events, defined risk is the only structure whose worst case you know.

### Numerical Example 5 — The straddle buyer's high bar

You buy the Budget-eve straddle at ₹400 (IV 20%). The Budget moves NIFTY +450 (to 25,050), but IV crushes to 13%:

```
Post-event straddle at 25,050 (IV 13%): call intrinsic 450 + small TV ≈ 480; put ≈ 0 → straddle ≈ 480
Buyer P&L = 480 − 400 = +₹80/unit
```

The buyer needed a +450 move — *more* than the expected ±400 — just to make ₹80, because the crush deflated the premium. A +350 move (within the expected range) would have *lost* money despite being a large, correct-direction move. The buyer's bar is not "a big move" but "a move bigger than the priced-in ±400."

---

## 6. Calculations (the reusable recipes)

**(a) Expected event move**

```
Expected move (± points) ≈ Event-eve ATM straddle premium
```

**(b) IV crush profit**

```
IV crush profit = Position Vega × (pre-event IV − post-event IV) × (per unit; × lot size for rupees)
   (offset by the Gamma loss from the actual move)
```

**(c) Gap risk (max loss on an overnight gap)**

```
Naked short loss = (short strike − gap level) intrinsic − credit  (for a breached put; mirror for a call)
```

**(d) Event position sizing (work backward)**

```
Max lots = (Max event loss allowed) ÷ (Loss per lot on the gap/adverse scenario)
Rule of thumb: 20–30% of normal size through events, and prefer defined risk
```

---

## 7. Practical Insights

* **Trade the IV cycle, not the outcome.** IV builds up, peaks on the eve, and crushes after a scheduled event; the reliable edge is selling the inflation and capturing the crush, not predicting the direction.
* **Read the expected move off the straddle.** The event-eve ATM straddle is the market's forecast; the bet is "larger or smaller than that?" — a buyer needs a move *beyond* it, a seller needs it contained.
* **Distinguish scheduled from surprise events.** Scheduled → sell the elevation *before* (capture the crush); surprise/crisis → sell the elevation *after* (as the spike reverts). The timing is opposite.
* **Never hold naked shorts over an event.** The overnight gap is the one risk you cannot manage — use defined risk and small size, and let the structure cap the worst case.
* **Size backward from the gap.** Set a max event loss, compute the gap-scenario loss per lot, and let that dictate lots — usually pointing to defined-risk structures and 20–30% of normal size.

> **Professional Insight — event trading is probability, not prophecy.** The amateur approaches an event asking "which way will it go?" and bets the direction; the professional asks "is the market over- or under-pricing the move?" and bets the volatility, sized to survive being wrong. The professional's edge is not superior prediction — it is capturing the reliable IV crush across *many* events with consistent, small, defined-risk sizing, accepting that any single event can lose. Over a year of Budgets, RBIs, and results, the disciplined vol-crush seller profits; the direction-predictor is right half the time and blown up on the gap the other half.

---

## 8. Common Mistakes

* **Buying options into the pre-event peak.** Paying inflated IV and losing to the crush even when the move comes — the classic Vega trap (Chapter 11).
* **Confusing "a big move" with "profit" for a buyer.** The buyer needs a move *bigger than the expected move* the premium priced; a large, correct move within the expected range still loses.
* **Holding naked shorts over an event.** The overnight gap is un-hedgeable and can dwarf the premium — the single most dangerous event mistake.
* **Selling thin premium after a scheduled crush.** The premium-selling edge was *before* the event; selling the crushed premium after collects little with the risk of IV rising.
* **Missing the surprise-event timing.** On a crisis spike, the elevated premium to sell is *after* the shock (as it reverts), not before — the opposite of a scheduled event.
* **Sizing events like normal trades.** Event gaps demand 20–30% of normal size and defined risk; full-size naked positions through events are how accounts end.

---

## 9. Case Study — "Budget Day 2024 and 2025: Two Different Outcomes"

**Context.** The Union Budget is the year's most anticipated scheduled event, and its IV cycle is textbook (Table 23.1). This case follows a trader who runs the *same* pre-event strategy — the vol-crush trade, selling the inflated Budget-eve ATM straddle — through *two consecutive Budgets*. The outcomes are opposite, and the reason is not the strategy but the *size of the move relative to what was priced*. Figures are illustrative and representative of the two Budgets' differing reactions; verify actual levels from the archives.

**The strategy (identical both years).** On Budget eve, with NIFTY at 24,600 and IV peaked at ~20%, the trader sells the ATM 24,600 straddle for **₹400** (the expected move is ±400, so breakevens are 24,200 and 25,000). The plan: capture the post-Budget IV crush, profiting if the actual move stays within the expected ±400.

**Budget 2024 — a contained move (the win).** The Budget delivered its news (tax changes that jolted the market intraday), but NIFTY settled only modestly changed — a net move of about **+120 points**, well within the expected ±400. Post-Budget, IV crushed from 20% to ~13%:

```
Post-Budget NIFTY ≈ 24,720 (+120); IV 13%
Straddle now ≈ ₹250 (call intrinsic 120 + deflated TV; put small)
Seller P&L = 400 − 250 = +₹150/unit (+₹9,750/lot)
```

The contained move plus the IV crush delivered a ₹150/unit profit. The strategy worked — because the move was smaller than the ₹400 the market had priced.

**Budget 2025 — a large move (the loss).** The following year, the *same* trade, the *same* ₹400 straddle — but this Budget provoked a larger reaction, moving NIFTY about **+550 points**, *beyond* the expected ±400 and through the upper breakeven (25,000). Even with the IV crush:

```
Post-Budget NIFTY ≈ 25,150 (+550); IV 13%
Straddle now ≈ ₹560 (call intrinsic 550 + small TV; put ~0)
Seller P&L = 400 − 560 = −₹160/unit (−₹10,400/lot)
```

The IV crush still helped, but the move (+550) exceeded the expected (±400) by enough that the Gamma loss overwhelmed the crush gain — a ₹160/unit loss.

**The analysis.** The trader did *nothing different* — same strategy, same structure, same sizing, same IV-crush edge. The outcomes diverged entirely because of **whether the actual move stayed within the priced-in expected move**: in 2024 it did (+120 < ±400 → profit), in 2025 it did not (+550 > ±400 → loss). Crucially, a trader who tried to *predict* the Budget reaction would have been right once and wrong once — no better than a coin flip. But the vol-crush trade had **positive expected value both years**: selling inflated pre-event premium is a reliable edge *on average*, because the IV crush is reliable and the move is contained *more often than not*. The 2025 loss was not a strategy failure; it was the expected, occasional adverse outcome of a positive-EV, probabilistic trade.

**The lesson — probability, not prediction.** Event trading is not about forecasting the Budget's market reaction; it is about *positioning for the volatility cycle* and accepting that any single event can go against you. The trader who repeats the vol-crush trade across many events, sized consistently and small (and ideally defined-risk to cap the 2025-type loss), profits over time — the crush edge compounds while the occasional large-move loss is bounded. The trader who bets the direction, or sizes big on conviction, is one adverse Budget away from ruin. Both years' outcomes were *correct* results of the same sound, probabilistic process.

*(Takeaway: the same event strategy can win or lose depending only on whether the move stays within the priced-in expected move — trade the IV cycle probabilistically, size small and defined-risk, and judge the process over many events, not any single outcome.)*

---

## 10. Chapter Summary

* India's **event calendar** has four tiers — **scheduled** (Budget, RBI, earnings, GST Council), **quasi-scheduled** (elections), **global triggers** (Fed, US data, geopolitics, crude), and **surprises** (SEBI circulars, crises).
* The **IV cycle** around scheduled events is **build-up (5–10 days before) → peak (eve) → crush (after) → normalise (3–5 days)** — a NIFTY Budget straddle inflating from ₹250 to ₹400, then crushing.
* The **expected move** = the event-eve ATM straddle premium (₹400 → ±400); the event bet is "larger or smaller than the priced move?", not the direction.
* **Pre-event:** sell the inflated premium (short straddle/strangle or calendar for the differential crush); if buying, use a debit spread to limit Vega; long straddles work only early in the build-up with precise exit.
* **Scheduled vs surprise timing:** scheduled events → sell the elevation *before* (capture the crush); surprise/crisis events → sell the elevation *after* (as the spike reverts).
* The **vol-crush trade** profits from IV crush (Position Vega × crush = +₹228/unit on a 7-point crush), offset by the Gamma loss if the move is large — positive EV, captured by repetition and defined risk.
* **Overnight gap risk** is the un-hedgeable event danger: a naked short strangle can lose ₹617/unit (₹40,105/lot) on a −4.9% gap — dwarfing the premium.
* **Size events at 20–30% of normal, defined-risk only:** working backward from the gap, a 3%-of-₹10-lakh limit rules out naked shorts and points to iron condors.
* **Budget 2024 vs 2025** — the same vol-crush trade, +₹150 one year and −₹160 the next, decided only by whether the move stayed within the priced ±400 — proves event trading is **probabilistic, not predictive**.

---

## 11. Key Takeaways

* **Trade the IV cycle, not the outcome** — sell the pre-event inflation to capture the reliable crush, and read the expected move off the straddle.
* **Distinguish scheduled (crush) from surprise (spike) events** — the elevated premium to sell is *before* a scheduled event and *after* a surprise.
* **Never hold naked shorts over an event** — the overnight gap is un-hedgeable; use defined risk and 20–30% of normal size, sized backward from the gap.
* **Judge event trading as a probabilistic process over many events** — a positive-EV vol-crush trade will lose on individual big-move events; consistency and defined risk, not prediction, make it pay.

---

## 12. Practice Questions

**Q1 (Calendar).** Name the four tiers of India's event calendar with one example of each.

**Q2 (IV cycle).** Describe the four phases of the IV cycle around a scheduled event.

**Q3 (Expected move).** The Budget-eve ATM straddle is ₹360 with NIFTY at 24,600. What is the expected move, and what must a straddle buyer achieve to profit?

**Q4 (Crush profit).** A short straddle has Position Vega −₹30/vol point. IV crushes from 22% to 14%. Compute the IV crush profit (assume NIFTY unchanged).

**Q5 (Gap risk).** A short 24,300 PE (part of a strangle, total credit ₹150) is held over an event; NIFTY gaps to 23,500. Compute the loss on the put leg per unit.

**Q6 (Sizing).** Your max event loss is ₹40,000. A naked strangle could lose ₹550/unit (₹35,750/lot) on a gap; an iron condor's max loss is ₹8,000/lot. How many lots of each fit your limit?

**Q7 (Scheduled vs surprise).** For a scheduled RBI policy and for a surprise geopolitical shock, when is the elevated premium best sold, and why?

**Q8 (Buyer's bar).** Why can an option buyer be right on direction with a large move at an event and still lose money?

**Q9 (Vol-crush EV).** Explain why the vol-crush trade can have positive expected value yet lose on a given event.

**Q10 (Case judgement).** The same pre-Budget straddle sale made +₹150 in 2024 and −₹160 in 2025. What single factor drove the difference, and what does it teach about event trading?

---

## 13. Detailed Solutions

**A1.** **Scheduled** (Union Budget / RBI policy / earnings / GST Council); **Quasi-scheduled** (general or state elections); **Global triggers** (US Fed / NFP / CPI / geopolitics / crude); **Surprise** (SEBI circulars / crises / pandemics). Any one example per tier suffices.

**A2.** **Build-up** (IV rises 5–10 days before as uncertainty grows) → **Peak** (IV maxes on the eve) → **Crush** (IV collapses immediately after the outcome is known) → **Normalise** (IV drifts back to baseline over 3–5 days).

**A3.** Expected move ≈ ±₹360 (the straddle premium), i.e., ~24,240 to 24,960. A straddle buyer must achieve a move *larger than ±360* — enough to overcome the post-event IV crush — just to profit; a move within ±360 loses despite being real.

**A4.** IV crush profit = Position Vega × (pre − post IV) = −30 × (14 − 22) = −30 × (−8) = **+₹240/unit** (₹15,600/lot), assuming NIFTY unchanged. (A move would offset this via the short Gamma.)

**A5.** Loss = (short strike − gap level) − credit = (24,300 − 23,500) − 150 = 800 − 150 = **₹650/unit** (₹42,250/lot) on the put leg — the un-hedgeable overnight gap loss.

**A6.** Naked strangle: 40,000 ÷ 35,750 = 1.12 → **1 lot** (a second lot would breach the limit — and even that single lot carries un-hedgeable gap risk *beyond* the modelled scenario). Iron condor: 40,000 ÷ 8,000 = 5 → **5 lots** (max loss capped at ₹40,000 regardless of gap size). The defined-risk structure allows five times the size within the same limit, with the worst case known in advance; the naked one barely fits one lot and its true tail is unbounded.

**A7.** **Scheduled RBI policy:** sell the elevated premium **before** the event — IV is inflated pre-event and *crushes* after, so selling beforehand captures the crush. **Surprise geopolitical shock:** sell the elevated premium **after** the shock — a surprise *spikes* IV with no build-up, so the elevation is post-event and you sell it as it mean-reverts down. The timing is opposite because scheduled events crush and surprises spike.

**A8.** Because the pre-event premium already priced a large move (the expected move), and the post-event **IV crush** deflates the option's value. To profit, the buyer needs a move *larger than the priced-in expected move*; a large, correct-direction move that is still *within* the expected range leaves the option worth less after the crush than the inflated price paid — so the buyer loses despite being right.

**A9.** The vol-crush trade sells inflated pre-event premium to capture the reliable IV crush — a positive-expected-value edge *because the crush is reliable and the move is contained more often than not*. On any given event, though, the move can be *large* (exceeding the expected move), and the resulting Gamma loss overwhelms the crush gain, producing a loss. Positive EV means it profits *on average over many events*, not on every one.

**A10.** The single factor: **whether the actual move stayed within the priced-in expected move (±400)**. In 2024 the move (+120) was contained → the crush gain outweighed the Gamma loss → profit; in 2025 the move (+550) exceeded ±400 → the Gamma loss overwhelmed the crush → loss. The lesson: event trading is **probabilistic, not predictive** — the same sound, positive-EV strategy wins or loses on any single event depending on the move size, so judge the process over many events and size small with defined risk.

---

## 14. Mini Glossary

* **Event calendar** — the schedule of market-moving events (Budget, RBI, elections, global triggers, surprises). → this chapter.
* **IV cycle** — the arc of implied volatility around a scheduled event: build-up → peak → crush → normalise. → this chapter.
* **IV build-up** — the pre-event rise in IV as uncertainty grows. → this chapter.
* **IV crush** — the sharp post-event fall in IV as uncertainty resolves. → this chapter.
* **Expected move** — the market's forecast move, read off the event-eve ATM straddle premium. → this chapter.
* **Vol-crush trade** — selling inflated pre-event premium to profit from the post-event IV crush. → this chapter.
* **Pre-event calendar** — selling the event-week expiry and buying the next to harvest the differential crush. → this chapter.
* **Overnight gap risk** — the un-hedgeable risk that the index gaps far beyond its close while the market is shut. → this chapter.
* **Scheduled vs surprise events** — scheduled events crush IV (sell before); surprises spike IV (sell after). → this chapter.
* **Event position sizing** — sizing at 20–30% of normal, worked backward from the gap risk, favouring defined risk. → this chapter.

---

<!-- End of Chapter 23 (Rev 2, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026) — per-unit values unchanged; "/lot" conversions rescaled: gap loss ₹40,105/lot (from ₹46,275), max profit ₹11,895, IV crush ₹14,820/lot, condor max loss ₹7,800/lot, case study +₹9,750/lot (2024) and −₹10,400/lot (2025); A5 gap loss ₹42,250/lot; Q6/A6 rescaled (naked ₹35,750/lot → 1 lot, condor ₹8,000 → 5 lots). IV cycle Table 23.1 (Budget straddle ₹250→₹400 peak→crush) unchanged. Expected move = eve straddle ₹400 = ±400. IV crush = short straddle Vega −32.6 × crush 7 = +₹228/unit. Gap risk Table 23.2; short 24,200 PE gap to 23,400 → −₹617/unit. Sizing: 3%×₹10L=₹30,000 → naked 0 lots, condor 3 lots. Case study Budget 2024 (+120, +₹150/unit) vs 2025 (+550, −₹160/unit): same strategy, opposite outcome → probabilistic not predictive. Scheduled crush (sell before) vs surprise spike (sell after). Events not tied to expiry weekday; gross P&L → Apr-2026 STT not applicable. IV = implied volatility. -->
