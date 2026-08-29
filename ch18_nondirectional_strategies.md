<!-- Difficulty: Level 3.5/5 (Intermediate-Advanced). Dependency: Chapters 10, 11, 17. Target length ~12,000 words (longest strategy chapter). Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). Uses standard strategy template. Per-unit premiums/credits/debits/breakevens/ranges/probabilities/R-R all lot-independent — unchanged. Lot-scaled rupee/margin figures updated to lot 65: short straddle credit ₹410 (₹26,650/lot), margin ~₹1.3 lakh; short strangle credit ₹183 (₹11,895/lot), margin ~₹1.2 lakh; iron condor credit ₹80 (₹5,200/lot), max loss ₹120 (₹7,800/lot), margin ₹7,800; butterfly debit ₹15 (₹975/lot), max profit ₹185 (₹12,025/lot); iron butterfly credit ₹238 (₹15,470/lot), max loss ₹62 (₹4,030/lot). Case study 4-week WEEKLY NIFTY IC (NIFTY retains weekly Tuesday expiry): per-unit +80/+70/−30/+90 = +₹210/unit (+₹13,650/lot); Wk3 adjustment saved ₹90/unit (₹5,850/lot). No transaction costs shown (gross P&L) → Apr-2026 STT change not applicable. IV = implied volatility. -->

# Chapter 18 — Non-Directional Strategies: Profiting from Time and Range

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Construct and manage straddles and strangles, long and short.
2. Construct and manage iron condors.
3. Construct and manage butterflies and iron butterflies.
4. Choose the right non-directional strategy for the market regime.
5. Master the adjustment rules for non-directional positions.

Chapters 16 and 17 traded *direction*. This chapter trades the *absence* of direction — profiting when the market goes nowhere, or when it moves far more than the premium implies. These are the strategies that harvest the variance risk premium (Chapter 14) directly, and the iron condor is the retail world's favourite income machine.

---

## 2. Introduction

Most traders assume you need a market view to make money in options. You do not. A whole family of strategies profits from the market *not moving much* — from range and time — and another from the market moving *a lot*, in either direction. These are the **non-directional** strategies, and they are where the volatility work of Part IV pays off, because they are, at their core, bets on volatility itself: **short** non-directional positions (short straddle, short strangle, iron condor, butterfly) profit when realised volatility comes in *below* what the premium implied; **long** ones (long straddle, long strangle) profit when it comes in *above*.

The appeal is obvious. A short strangle collects premium from both a call and a put, winning if the index simply stays in a range — no need to predict up or down. But so is the danger: these are the concentrated forms of *short Gamma* and *short Vega* (Chapters 9, 11), so a big move or a volatility spike can hand back weeks of income in a session. The entire craft of non-directional trading is managing that asymmetry — winning often and small, and surviving the occasional large loss.

This chapter builds the family from the ground up: the short straddle (maximum premium, maximum risk); the short strangle (wider, safer, still open-ended); the **iron condor** — the defined-risk strangle that is the practical workhorse; and the butterflies (cheap bets on pinning). You will learn to select among them by volatility regime, and — most importantly — to adjust them when the market tests a side. Setting: **NIFTY at 24,600, lot 65**, with skew-consistent premiums from Part V.

---

## 3. Core Concepts

### 3.1 The non-directional idea

Every non-directional strategy is a bet on **how much the market will move, not which way.** Sell them (short straddle, strangle, condor, butterfly) and you are betting the market moves *less* than the premium implies — you collect Theta, are short Gamma and short Vega, and win in a quiet market. Buy them (long straddle, strangle) and you bet it moves *more* — you pay Theta, are long Gamma and long Vega, and win on a big move or a volatility spike.

The short side is by far the more common (and more dangerous) retail activity, because it harvests the variance risk premium — the structural tendency for implied to exceed realised volatility (Chapter 14). But it does so by selling insurance, which means it carries the insurer's risk: frequent small gains punctuated by occasional large losses. The strategies differ mainly in *how* they bound (or fail to bound) that large loss.

---

### 3.2 The short straddle — maximum premium, maximum risk

**Setup.** Sell an ATM call *and* an ATM put at the same strike. On our surface: sell the 24,600 CE @₹212 and the 24,600 PE @₹198 — total credit **₹410** (₹26,650/lot).

**View.** Strongly neutral: you expect the index to stay very close to the strike, and/or IV to fall.

**Risk/reward.** Max profit = the full ₹410, achieved only if NIFTY expires exactly at 24,600. Breakevens = strike ± total premium = **24,190 and 25,010**. Max loss = **unlimited** (the call side) and large (the put side) — both legs are naked.

**Greeks.** Near-zero Delta (−0.08 here, slightly short — the ATM call's +0.54 delta slightly outweighs the put's −0.46, and shorting both nets −0.08), **maximum negative Gamma** and **maximum positive Theta** of any structure (it sells the two richest, highest-Gamma ATM options), and **strongly negative Vega** (~−₹32.6/vol point, both ATM Vegas). It is the purest, most concentrated short-volatility position.

**Best when.** IV is very rich (high IV Rank) and you have strong conviction the market will be quiet — and you have the capital and discipline to manage open-ended risk.

**Indian considerations.** Requires large margin (~₹1.3 lakh+/lot, both sides naked) and is brutal on expiry day (peak Gamma, Chapter 9). Reserved for large, experienced accounts.

**The trade-off.** The short straddle collects the *most* premium of any non-directional structure (it sells the two most expensive options) but has the *narrowest* profit range and *unlimited* risk. It is the highest-octane, least-forgiving non-directional trade.

---

### 3.3 The short strangle — wider range, still open-ended

**Setup.** Sell an OTM call *and* an OTM put. On our surface (the architecture's example): sell the 24,800 CE @₹105 and the 24,200 PE @₹78 — total credit **₹183** (₹11,895/lot).

**View.** Neutral, expecting the index to stay within a range.

**Risk/reward.** Max profit = ₹183, kept in full if NIFTY finishes *anywhere between* 24,200 and 24,800 at expiry. Breakevens = call strike + total premium and put strike − total premium = **24,983 and 24,017** (a 966-point profit range, wider than the straddle's 820). Max loss = large/unlimited beyond the breakevens.

**Greeks and width.** The strangle trades premium for a wider profit range: it collects less than the straddle (₹183 vs ₹410) but wins over a much broader zone. **Strangle width selection** — how far OTM to sell — is the key choice: closer strikes collect more but narrow the range; further strikes (lower delta) collect less but widen it and raise the probability of profit. A common target is ~15–20 delta short strikes for a high-probability strangle.

**A note on balance.** The 24,800 CE (200 OTM, Δ0.39) and 24,200 PE (400 OTM, Δ0.20) are *not* equidistant, so this strangle is slightly delta-imbalanced (net Delta ≈ −0.19, mildly bearish-leaning). A *balanced* (delta-neutral) strangle uses **equal-delta** strikes, not equal-distance ones — because the skew (Chapter 15) makes puts richer and higher-delta at a given distance. Always balance by delta, not by points.

**Long straddle/strangle — the mirror.** *Buying* a straddle or strangle is the long-volatility bet: pay the premium, profit if the index makes a big move *either way* (beyond the breakevens) or if IV spikes. It is the pre-event trade — long Gamma, long Vega, paying Theta — used when you expect a large move but not its direction. It loses if the market is quiet (the mirror of the short's win).

---

### 3.4 The iron condor — the defined-risk workhorse

The iron condor is the flagship of this chapter and the practical centrepiece of retail income trading.

**What is it?** An **iron condor** is a **bull put spread + a bear call spread** — a short strangle with protective wings on both sides. You sell an OTM put and an OTM call (collecting premium) and buy a further OTM put and call (as insurance), creating a *defined-risk* version of the short strangle.

**Why does it exist?** To fix the short strangle's fatal flaw — its open-ended risk. By buying the wings, the iron condor caps the loss on both sides, transforming an unlimited-risk position into a bounded one with a known maximum loss and a margin equal to that loss (Chapter 17).

**Why should a trader care?** Because it is the **highest-probability, defined-risk, capital-efficient way to sell range and time.** It wins in a quiet market (the common case), caps the loss in a big move (survivable), and requires only the max-loss margin — making it scalable and sleep-at-night in a way the naked strangle never is.

**Intuitive explanation.** An iron condor is **two credit spreads facing each other** — you are selling insurance on both a crash and a melt-up, with reinsurance capping each. You profit if the index stays in the broad middle zone, and your worst case is bounded on both ends.

**Trade sheet (the "standard" NIFTY condor).** Using ~30-delta short strikes and 200-point wings:

**Table 18.1 — NIFTY iron condor (illustrative, 10 DTE)**

| Leg | Action | Premium |
| --- | --- | ---: |
| 24,100 PE | Buy (wing) | ₹60 |
| 24,300 PE | Sell (short) | ₹100 |
| 24,900 CE | Sell (short) | ₹72 |
| 25,100 CE | Buy (wing) | ₹32 |

```
Put spread credit  = 100 − 60 = ₹40
Call spread credit = 72 − 32 = ₹40
Net credit         = ₹80 (₹5,200/lot)
Max profit         = ₹80 (if NIFTY finishes between 24,300 and 24,900)
Max loss           = wing width − net credit = 200 − 80 = ₹120 (₹7,800/lot)
Breakevens         = 24,300 − 80 = 24,220 (lower); 24,900 + 80 = 24,980 (upper)
Margin             ≈ ₹7,800 (= max loss, SEBI defined-risk rules)
Prob. max profit   ≈ 1 − 0.25 (put Δ) − 0.32 (call Δ) ≈ 43%
```

**Greeks.** Near-zero Delta (balanced), **negative Gamma** and **positive Theta** (short range/time), **negative Vega** (short volatility) — the short-strangle profile, but with every risk bounded.

**Wing width and structure.**

* *Wing width:* narrow wings (100 pts) cost less protection and cap loss tighter (lower max loss, lower credit); wide wings (300–500) collect more but risk more — the width tradeoff of Chapter 17.
* *Symmetrical vs skewed:* a symmetrical condor is delta-neutral; a **skewed** condor (short strikes placed asymmetrically) tilts the position bullish or bearish while staying defined-risk.

**Best when.** IV is rich (high IV Rank, Chapter 14) and you expect range-bound trade, ideally selling into elevated IV that will mean-revert down (short Vega benefits).

> **Beginner Alert — the iron condor's win rate hides its math.** A 30-delta condor wins its *max profit* ~43% of the time and *any* profit maybe ~55% — but its reward-to-risk is only 80/120 = 0.67, so a single max loss (₹120) erases 1.5 max profits (₹80 each). Widen the short strikes to ~15-delta and the win rate rises toward 70%+, but the credit shrinks and the loss-to-win ratio worsens further. The iron condor is a real, thin edge (the VRP), *not* an ATM machine — it must be sized so its capped loss is survivable and managed when a side is tested (Section 3.7).

---

### 3.5 Butterflies and iron butterflies

Butterflies are the *cheap, pinning* cousins of the condor — bets that the index finishes near a specific strike.

**Long butterfly.** Buy 1 lower-strike option, sell 2 middle-strike options, buy 1 upper-strike option (equidistant, same type). It is a low-cost bet that the index *pins* the middle strike at expiry. On our surface, the architecture's 24,300/24,500/24,700 call butterfly:

```
Buy 24,300 CE @₹400, Sell 2 × 24,500 CE @₹280, Buy 24,700 CE @₹175
Net debit = 400 + 175 − (2 × 280) = 575 − 560 = ₹15 (₹975/lot)
Max profit = wing width − net debit = 200 − 15 = ₹185 (at 24,500 at expiry)
Max loss = net debit = ₹15 (₹975/lot)
Breakevens = 24,300 + 15 = 24,315 (lower); 24,700 − 15 = 24,685 (upper)
Risk-reward ≈ 185/15 ≈ 12:1
```

The butterfly's signature is its **huge reward-to-risk (12:1) paired with a low probability** of hitting the peak — it pays enormously *if* the index pins the middle strike, and costs almost nothing if it does not. It is a cheap, high-conviction bet on a specific level (or a low-cost way to bet on range), not a high-probability income trade.

**Iron butterfly.** A **short ATM straddle plus protective wings** — the defined-risk version of the short straddle. Sell the 24,600 straddle (₹410), buy the 24,300 PE (₹100) and 24,900 CE (₹72) as wings:

```
Net credit = 410 − 172 = ₹238 (₹15,470/lot); wing width 300
Max profit = ₹238 (at 24,600 exactly); Max loss = 300 − 238 = ₹62 (₹4,030/lot)
Breakevens = 24,600 ± 238 = 24,362 and 24,838
```

The iron butterfly collects *more* credit than an iron condor (it sells the richest ATM options) but has a *narrower* profit peak (it wants the index to pin the ATM strike) — a higher-credit, lower-probability sibling of the condor.

**Broken-wing butterfly.** An *asymmetric* butterfly (unequal wing distances) that skews the risk to one side — often structured to eliminate the risk on one side entirely (financed by accepting more on the other), giving a directional tilt within a defined-risk butterfly. A refinement for traders with a mild directional bias.

---

### 3.6 Choosing among them — the regime selector

With five short and two long non-directional structures, *selection* is the skill. The choice is driven by three inputs — **IV regime, directional lean, and days to expiry** — plus your risk appetite. The decision logic:

```
STRATEGY SELECTOR (non-directional)

Is IV rich (high IV Rank) or cheap (low)?
├─ RICH IV → SELL volatility:
│   ├─ Strong neutral, large account, accept open risk → SHORT STRADDLE (most premium)
│   ├─ Neutral, want defined risk → IRON CONDOR (workhorse) or IRON BUTTERFLY (more credit, tighter)
│   └─ Neutral, large account, want range not pin → SHORT STRANGLE (wider, open risk)
├─ CHEAP IV → BUY volatility (expect a big move / IV rise):
│   ├─ Expect big move either way → LONG STRADDLE / STRANGLE
│   └─ Expect pin at a level, cheap bet → LONG BUTTERFLY
└─ Mild directional lean? → SKEW the condor, or use a BROKEN-WING BUTTERFLY

Days to expiry:
├─ Near expiry (high Gamma) → smaller size, defined-risk only, manage actively
└─ Longer (lower Gamma, more Vega) → more room, but more Vega exposure
```

The governing principle mirrors Chapter 14: **sell non-directional structures when IV is rich, buy them when IV is cheap**, prefer *defined-risk* forms (condor, butterfly, iron butterfly) unless you have the capital and discipline for open risk, and size *down* near expiry where Gamma explodes.

---

### 3.7 Adjustment rules for non-directional positions

The defining skill of non-directional trading is **managing a tested side.** When the index moves toward one of your short strikes, you face a decision, and a rule-based approach beats panic. The core adjustment logic for an iron condor (or strangle):

```
IRON CONDOR ADJUSTMENT FLOWCHART

Is a short strike being tested? (index within ~1 wing of it, or short-strike delta > ~0.40)
├─ NO → hold; let Theta work
└─ YES → choose ONE (per pre-set rule):
    ├─ ROLL THE TESTED SIDE out/away → move the threatened spread further OTM
    │     (buys room; may lock a small loss; collects less)
    ├─ ROLL THE UNTESTED SIDE closer → bring the safe spread nearer the money
    │     (collects extra credit to offset the tested side; adds risk on the safe side)
    ├─ CONVERT / REDUCE → close the tested side, or cut size
    │     (takes a defined partial loss; reduces exposure)
    └─ HOLD TO DEFINED LOSS → if view unchanged and loss is within your limit
          (the condor's capped loss is survivable — sometimes the right choice)
```

Two adjustment principles:

* **Roll the untested side to fund the tested side.** A classic condor adjustment: as the market moves up and tests the call spread, roll the *put* spread up (closer to the money) to collect additional credit, which offsets the loss building on the call side and improves the overall breakeven. (The reverse for a downside test.) This "rolling the safe side in" adds credit but also adds risk on that side — a trade-off, not a free fix.
* **Respect the defined loss.** Because the condor's loss is *capped and known*, sometimes the best "adjustment" is none — take the bounded loss if your view is unchanged and the loss is within your pre-set limit. The rolling trap (Chapter 17) applies here too: do not roll a losing condor indefinitely.

> **Professional Insight — adjust the position, not your feelings.** The urge to adjust usually peaks when the mark-to-market loss *feels* worst — which is precisely when decisions are worst. Professionals adjust on *pre-defined triggers* (a short-strike delta threshold, a distance-to-strike, or a loss limit set at entry), not on the emotion of a losing screen. Write the adjustment rule before you enter, and execute it mechanically. The trader who decides "what to do about my tested condor" in the heat of the move has already half-lost.

---

## 4. Examples (Real-World)

**Example 1 — The quiet-week condor.** In a range-bound week with rich IV, a trader sells a NIFTY iron condor for ₹80. The index chops between the short strikes; all four legs expire worthless; the trader keeps ₹5,200/lot. Range and time, harvested with defined risk.

**Example 2 — The event straddle.** Before a major event, with IV still cheap, a trader *buys* an ATM straddle, betting on a big move either way. The event delivers a 2% gap; the straddle's winning leg more than covers the losing leg and the premium. Long volatility, paid off by the move (and the pre-event IV rise).

**Example 3 — The tested condor.** A condor's call side is threatened as the market rallies. The trader, per a pre-set rule, rolls the *put* spread up to collect extra credit, cushioning the call-side loss. The market stalls; the adjusted condor finishes with a small profit instead of a loss — the adjustment decision was the difference (the case study, Section 9).

---

## 5. Numerical Examples

Setting: NIFTY 24,600, 10 DTE, lot 65.

### Numerical Example 1 — Short strangle P&L across the range

Sell the 24,800 CE @₹105 and 24,200 PE @₹78 (credit ₹183). P&L per unit at expiry:

**Table 18.2 — Short strangle (24,200 PE / 24,800 CE) P&L at expiry**

| NIFTY at expiry | Put payoff (seller) | Call payoff (seller) | Net P&L/unit |
| ---: | ---: | ---: | ---: |
| 23,600 | −600 | 0 | −₹417 |
| 24,000 | −200 | 0 | −₹17 |
| **24,017 (lower BE)** | −183 | 0 | **₹0** |
| 24,200 | 0 | 0 | +₹183 |
| 24,500 | 0 | 0 | +₹183 (max) |
| 24,800 | 0 | 0 | +₹183 |
| **24,983 (upper BE)** | 0 | −183 | **₹0** |
| 25,000 | 0 | −200 | −₹17 |
| 25,400 | 0 | −600 | −₹417 |

The seller keeps the full ₹183 anywhere between 24,200 and 24,800, breaks even at 24,017 / 24,983, and loses beyond — with the loss growing without limit as the index runs. This is the short strangle's profile: a wide plateau of max profit, flanked by open-ended risk.

### Numerical Example 2 — Iron condor, fully worked

The condor from Table 18.1 (24,100/24,300 put spread + 24,900/25,100 call spread):

```
Net credit = ₹80 (₹5,200/lot); Max loss = 200 − 80 = ₹120 (₹7,800/lot)
Breakevens = 24,220 and 24,980; Margin ≈ ₹7,800
Prob. max profit ≈ 43%; Risk-reward = 80/120 = 0.67
```

Compared with the naked short strangle (Numerical Example 1), the condor collects less (₹80 vs ₹183) and has a narrower range — but its loss is *capped at ₹7,800* (vs unlimited) and its margin is only ₹7,800 (vs ~₹1.3 lakh). The wings are the price of survivability.

### Numerical Example 3 — Long butterfly

The 24,300/24,500/24,700 call butterfly:

```
Net debit = 400 + 175 − (2 × 280) = ₹15 (₹975/lot)
Max profit = 200 − 15 = ₹185 (₹12,025/lot) — only if NIFTY pins 24,500 at expiry
Max loss = ₹15 (₹975/lot); Breakevens = 24,315 and 24,685
Risk-reward ≈ 12:1
```

For ₹975, the butterfly offers up to ₹12,025 if the index pins 24,500 — a spectacular reward-to-risk, but with a *low probability* of hitting the peak. It is a cheap, high-conviction bet on a level, not a reliable income trade.

### Numerical Example 4 — Straddle vs strangle vs condor

Comparing the three neutral structures on the same underlying/expiry:

| Structure | Credit | Profit range | Max loss | Margin |
| --- | ---: | --- | --- | ---: |
| Short straddle (24,600) | ₹410 | 24,190–25,010 (820) | Unlimited | ~₹1.3 lakh |
| Short strangle (24,200/24,800) | ₹183 | 24,017–24,983 (966) | Unlimited | ~₹1.2 lakh |
| Iron condor (24,300/24,900, 200 wings) | ₹80 | 24,220–24,980 (760) | ₹120 (₹7,800) | ~₹7,800 |

The straddle collects most but has the narrowest range and open risk; the strangle widens the range for less credit, still open risk; the condor collects least but is the only one with *defined* risk and *small* margin. For most traders, the condor's capital efficiency and survivability make it the right default — you sacrifice premium for the ability to always come back tomorrow.

### Numerical Example 5 — Straddle breakevens and the expected move

The short straddle (credit ₹410) breaks even at 24,600 ± 410 = **24,190 / 25,010** — a ±410-point (±1.67%) range. Recall (Chapter 13) that the ATM straddle premium *is* the market's expected move: ₹410 implies the market expects roughly a ±410-point swing by expiry. So the straddle seller profits only if the index moves *less* than the market's own expectation — the variance-risk-premium bet (Chapter 14) in its purest form.

---

## 6. Calculations (the reusable recipes)

**(a) Straddle and strangle breakevens**

```
Straddle: Strike ± Total premium
Strangle: Call strike + Total premium (upper);  Put strike − Total premium (lower)
```

**(b) Iron condor**

```
Net credit = put-spread credit + call-spread credit
Max profit = Net credit;  Max loss = Wing width − Net credit
Breakevens = Short put strike − Net credit;  Short call strike + Net credit
Prob. max profit ≈ 1 − |short put Δ| − |short call Δ|;  Margin ≈ Max loss
```

**(c) Butterfly**

```
Net debit = (lower + upper premiums) − 2 × middle premium
Max profit = Wing width − Net debit (at the middle strike at expiry)
Max loss = Net debit;  Breakevens = lower strike + debit, upper strike − debit
```

**(d) Iron butterfly**

```
Net credit = ATM straddle credit − wing cost
Max profit = Net credit (at ATM strike);  Max loss = Wing width − Net credit
Breakevens = ATM strike ± Net credit
```

---

## 7. Practical Insights

* **Non-directional trading is volatility trading.** Sell these structures when IV is rich (harvest the VRP), buy them when IV is cheap (bet on a move) — the Chapter 14 edge, expressed structurally.
* **Prefer defined risk.** The iron condor and butterflies cap the loss and slash the margin; the naked straddle/strangle offer more premium but open-ended risk and huge margin. For most accounts, defined risk is the right default.
* **Balance by delta, not distance.** The skew makes puts richer and higher-delta at a given distance; a delta-neutral strangle or condor uses equal-delta strikes, not equal-point strikes.
* **Respect the win-rate illusion.** High probability (43–70%) is offset by unfavourable reward-to-risk; these are thin, real edges that one un-managed loss can erase. Size for the capped loss.
* **Adjust on pre-set triggers, not emotion.** Write the adjustment rule (delta threshold, distance, loss limit) before entry, and — for defined-risk structures — remember that taking the capped loss is sometimes the correct "adjustment."

> **Professional Insight — the condor is a business of small edges and disciplined losses.** A well-run iron condor book makes money the way an insurer does: many small premiums collected, the occasional claim paid. It is profitable *only* if the sizing ensures no single claim (max loss) is catastrophic and the management prevents a tested side from becoming a maximal loss unnecessarily. The edge per trade is thin (the VRP); the profitability comes from *repetition with survival*. Amateurs chase the credit; professionals engineer the survival.

---

## 8. Common Mistakes

* **Selling naked straddles/strangles without the capital or discipline for open-ended risk.** The premium is seductive; the unlimited loss and ballooning margin in a spike are what end accounts.
* **Treating the iron condor's win rate as easy income.** A 43–70% win rate with a sub-1.0 reward-to-risk is a thin VRP edge; one un-managed max loss erases several wins.
* **Balancing a strangle/condor by equal points instead of equal delta.** The skew makes the put side heavier; equal-point strikes leave you delta-imbalanced.
* **Over-sizing near expiry.** Non-directional shorts carry peak Gamma near expiry (Chapter 9); the same size that is fine at 10 DTE is dangerous at 1 DTE.
* **Adjusting on emotion.** Reacting to the worst mark-to-market moment rather than a pre-set trigger, and rolling a loser indefinitely (the rolling trap).
* **Buying butterflies expecting reliable income.** The 12:1 reward-to-risk comes with a low probability of pinning the peak; a butterfly is a cheap bet on a level, not an income machine.

---

## 9. Case Study — "Iron Condor Through an Earnings Season"

**Context.** A trader runs a **weekly NIFTY iron condor** for four consecutive weeks through a period of rising volatility — an earnings-heavy, event-clustered stretch that pushes India VIX from 13 up to 20 and back. The case shows how the condor's defined risk behaves as volatility rises, how one week's adjustment decision determined the month's outcome, and why the margin stability of a defined-risk structure is an underrated advantage. Figures are illustrative but representative; per-unit unless noted (lot 65).

**Week 1 — Calm (VIX 13).** Sell a standard condor (24,300/24,100 put spread + 24,900/25,100 call spread) for **₹80** credit, max loss ₹120, margin ₹7,800. NIFTY chops in a tight range and finishes between the short strikes. All legs expire worthless. **Result: +₹80 (+₹5,200/lot).**

**Week 2 — Rising nervousness (VIX 16).** Richer IV lets the trader collect **₹100** for a similar condor. Mid-week, NIFTY drifts up and tests the short call. Per the pre-set rule, the trader **rolls the untested put spread up** (closer to the money), collecting ₹25 of extra credit to cushion the call side. NIFTY stalls and finishes just below the short call. **Result: +₹70 (+₹4,550/lot)** after the adjustment's cost.

**Week 3 — The event week (VIX spikes to 20).** This is the swing week. The trader sells a condor for a rich **₹110** credit. Then the event lands and NIFTY makes a sharp *downside* move, driving straight toward the short put strike. The decision: adjust or hold?

* *The margin advantage.* As VIX doubled from 13 to 20, the condor's margin **stayed at ~₹7,800** (defined risk = max loss, which does not balloon with volatility). A naked short strangle, by contrast, would have seen its margin *balloon* on the VIX spike — potentially forcing liquidation at the worst moment. The condor let the trader hold through the turbulence without a margin scramble.
* *The adjustment.* Per the rule (short-put delta exceeded the trigger), the trader **rolled the put spread down** and rolled the untested call spread down too (collecting extra credit). NIFTY found support near the adjusted short put and stabilised. The adjusted condor finished with a **small loss of −₹30**.
* *The counterfactual.* Had the trader **held** the original condor, the downside move would have breached the put spread and delivered the **full max loss of −₹120**. The adjustment turned a −₹120 loss into a −₹30 loss — a **₹90/unit (₹5,850/lot) difference.** **Result (adjusted): −₹30 (−₹1,950/lot).**

**Week 4 — The IV crush (VIX subsides to 15).** With the event past, IV crushed, which *helped* the short-Vega condor. Sell a condor for **₹90**; NIFTY trades quietly as volatility normalises; all legs expire worthless. **Result: +₹90 (+₹5,850/lot).**

**The four-week tally.**

| Week | VIX | Result/unit | Note |
| ---: | ---: | ---: | --- |
| 1 | 13 | +₹80 | Calm, full credit kept |
| 2 | 16 | +₹70 | Rolled untested side, small give-up |
| 3 | 20 | −₹30 | Event week; adjustment saved ₹90 vs holding |
| 4 | 15 | +₹90 | IV crush aided the short-Vega position |
| **Total** | | **+₹210 (+₹13,650/lot)** | |

Had Week 3 been *unadjusted*, the total would have been +₹80 + ₹70 − ₹120 + ₹90 = **+₹120 (+₹7,800/lot)** — still positive, but the adjustment added ₹5,850 and was the difference between a mediocre month and a good one.

**The analysis.** Three lessons stand out. First, the **defined risk kept the trader in the game**: the condor's margin did not balloon as VIX doubled, so no forced exit — a decisive advantage over the naked strangle during the vol spike. Second, the **Week 3 adjustment was the swing**: rolling the tested side (per a pre-set trigger) converted a max loss into a small one, turning the month's worst week from −₹120 to −₹30. Third, the **IV cycle helped and hurt in sequence**: rising IV enriched the credits (Weeks 2–3) but threatened the positions, while the post-event IV crush (Week 4) directly aided the short-Vega book — the variance-risk-premium and IV-mean-reversion themes of Part IV, playing out in real trades.

**The lesson.** The iron condor's edge is thin and its wins small, so the month is made or lost on two things: *surviving the bad week* (defined risk + stable margin) and *managing the tested side by rule* (the adjustment that turned −₹120 into −₹30). Chase the credit and you will eventually meet the max loss unprepared; engineer the survival and the small edges compound.

*(Takeaway: an iron condor makes money through repetition and survival — the defined risk keeps you solvent through the vol spike, and a pre-set adjustment on the tested side is what separates a winning month from a losing one.)*

---

## 10. Chapter Summary

* **Non-directional strategies bet on how much the market moves, not which way** — short forms (straddle, strangle, condor, butterfly) win in a quiet market (short Gamma/Vega, positive Theta); long forms win on a big move (long Gamma/Vega, negative Theta).
* **Short straddle** (sell ATM CE+PE): most premium (₹410), narrowest range (24,190–25,010), unlimited risk, biggest Gamma/Vega — the highest-octane short-vol trade.
* **Short strangle** (sell OTM CE+PE): less premium (₹183), wider range (24,017–24,983), still open-ended; **balance by delta, not distance** (the skew).
* **Iron condor** (bull put + bear call spread): the **defined-risk workhorse** — caps loss (₹120), cuts margin to the max loss (₹7,800), and is capital-efficient; a thin VRP edge, not easy income.
* **Butterflies** (buy 1 / sell 2 / buy 1): cheap bets on pinning a strike — huge reward-to-risk (12:1) but low probability; **iron butterfly** is a defined-risk short straddle (more credit, tighter peak).
* **Select by regime:** sell non-directional structures in rich IV, buy in cheap IV, prefer defined-risk forms, and size down near expiry (peak Gamma).
* **Adjust on pre-set triggers:** roll the tested side out or the untested side in (to fund it), or take the defined loss — never adjust on emotion or roll a loser indefinitely.
* The **earnings-season case** shows the condor's defined risk keeps margin stable through a VIX spike, and a rule-based Week-3 adjustment (−₹120 → −₹30) was the difference in the month.

---

## 11. Key Takeaways

* **Trade non-directional structures as volatility bets** — sell in rich IV, buy in cheap IV — and prefer *defined-risk* forms (condor, butterflies) for survivability and capital efficiency.
* **Balance by delta, size for the capped loss, and respect the win-rate illusion** — high probability with poor reward-to-risk is a thin edge that one un-managed loss erases.
* **Adjust the tested side by a pre-set rule** (roll out, or roll the untested side in to fund it), and remember that taking the defined loss is sometimes the right move.
* **The month is made by surviving the bad week and managing the tested side** — defined risk keeps you solvent through vol spikes; disciplined adjustment turns max losses into small ones.

---

## 12. Practice Questions

**Q1 (Breakevens).** You sell a short straddle at 24,600 for a total credit of ₹410. Compute the breakevens and the profit range width.

**Q2 (Strangle).** You sell a 24,200 PE / 24,800 CE strangle for ₹183. Compute the breakevens and state where you keep the full credit.

**Q3 (Iron condor).** For a condor with a ₹90 net credit and 250-point wings, compute the max profit, max loss, and margin.

**Q4 (Butterfly).** Buy 24,400 CE @₹340, sell 2 × 24,600 CE @₹212, buy 24,800 CE @₹105. Compute the net debit, max profit, and breakevens.

**Q5 (Comparison).** Rank short straddle, short strangle, and iron condor by (a) credit collected and (b) max loss, and state which is most capital-efficient.

**Q6 (Delta balance).** Why is a strangle sold at equal *distances* from spot (e.g., 400 points each side) usually not delta-neutral, and how do you fix it?

**Q7 (Probability).** An iron condor has a short put delta of −0.20 and a short call delta of 0.22. Estimate the probability of max profit.

**Q8 (Regime).** IV Rank is 15 (very low) and you expect a big move around an event but don't know the direction. Which non-directional strategy fits, and why?

**Q9 (Adjustment).** Your iron condor's call side is tested by a rally. Describe the "roll the untested side in" adjustment and its trade-off.

**Q10 (Judgement).** A trader sells naked NIFTY strangles for the large premium and ignores iron condors as "collecting too little." Explain the flaw, referencing margin and survivability.

---

## 13. Detailed Solutions

**A1.** Breakevens = 24,600 ± 410 = **24,190 and 25,010**. Profit-range width = 25,010 − 24,190 = **820 points** (you profit if NIFTY finishes within this range at expiry, with max profit only exactly at 24,600).

**A2.** Upper breakeven = 24,800 + 183 = **24,983**; lower = 24,200 − 183 = **24,017**. You keep the **full ₹183 anywhere between 24,200 and 24,800** (both options OTM), with partial profit out to the breakevens.

**A3.** Max profit = net credit = **₹90**. Max loss = wing width − credit = 250 − 90 = **₹160** (₹10,400/lot). Margin ≈ max loss = **₹10,400** (SEBI defined-risk).

**A4.** Net debit = (340 + 105) − (2 × 212) = 445 − 424 = **₹21**. Max profit = wing width − debit = 200 − 21 = **₹179** (at 24,600 at expiry). Breakevens = 24,400 + 21 = **24,421** and 24,800 − 21 = **24,779**.

**A5.** (a) Credit: **short straddle (₹410) > short strangle (₹183) > iron condor (₹80)**. (b) Max loss: **straddle and strangle both unlimited; iron condor capped (₹120)**. The **iron condor is by far the most capital-efficient** — its margin equals its small max loss (₹7,800) versus ~₹1.2–1.3 lakh for the naked structures.

**A6.** Because of the **volatility skew** (Chapter 15), puts are richer and carry higher delta than equidistant calls, so a strangle sold at equal *points* has a larger (more negative) put-side delta contribution and ends up net short delta (bearish-leaning). To fix it, sell **equal-delta strikes** (e.g., ~0.20 delta on each side) rather than equal-distance strikes — the put strike will sit further from spot than the call strike.

**A7.** Probability of max profit ≈ 1 − |short put Δ| − |short call Δ| = 1 − 0.20 − 0.22 = **0.58 (58%)** — the approximate chance the index finishes between the two short strikes.

**A8.** A **long straddle or long strangle** (buying volatility). With very low IV, options are cheap; buying a straddle/strangle costs little, profits from a big move in *either* direction (long Gamma), and benefits if the event spikes IV (long Vega). The non-directional *short* structures would be wrong here — you would be selling cheap premium into a likely big move.

**A9.** As the call side is tested by a rally, you **roll the untested put spread up** — closing it and re-selling it closer to the money — to **collect additional credit**. That extra credit offsets the loss building on the tested call side and improves the position's overall breakeven. The **trade-off:** bringing the put spread closer to the money **adds downside risk** — if the market then reverses sharply down, the newly-aggressive put side can be threatened. It funds the tested side by accepting more risk on the other.

**A10.** The flaw is judging the trade by **premium instead of return on capital and survivability**. The naked strangle collects more (₹183 vs ₹80) but ties up ~₹1.2 lakh of margin, carries **unlimited risk**, and sees its **margin balloon during a volatility spike** — potentially forcing liquidation at the worst moment. The iron condor collects less but has a **defined loss**, a margin of only ~₹7,800 (a far higher return on capital), and **stable margin through vol spikes**, letting the trader survive the bad week. Over many trades, survivability and capital efficiency beat raw premium — the naked strangle's larger credit is worthless if one spike ends the account.

---

## 14. Mini Glossary

* **Non-directional strategy** — a position that profits from the *magnitude* (or lack) of movement, not the direction. → this chapter.
* **Short straddle** — sell an ATM call and put; most premium, narrowest range, unlimited risk. → this chapter.
* **Short strangle** — sell an OTM call and put; wider range, less premium, still open-ended risk. → this chapter.
* **Long straddle / strangle** — buy the call and put; a long-volatility bet on a big move (or IV rise). → this chapter.
* **Iron condor** — a bull put spread plus a bear call spread; a defined-risk short strangle. → this chapter.
* **Wing width** — the distance between the short and long strikes of each spread in a condor; sets the max loss. → this chapter.
* **Skewed iron condor** — a condor with asymmetric short strikes, tilted bullish or bearish. → this chapter.
* **Long butterfly** — buy 1 lower, sell 2 middle, buy 1 upper; a cheap, high-reward bet on pinning the middle strike. → this chapter.
* **Iron butterfly** — a short ATM straddle with protective wings; a defined-risk short straddle. → this chapter.
* **Broken-wing butterfly** — an asymmetric butterfly that skews the risk for a directional bias. → this chapter.
* **Rolling the untested side in** — bringing the safe spread closer to the money to collect credit that funds a tested side. → this chapter.

---

<!-- End of Chapter 18 (Rev 2, longest strategy chapter, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026). Per-unit values (credits/debits/breakevens/ranges/probabilities/R-R, P&L table 18.2) lot-independent — unchanged. Lot-scaled figures recomputed to lot 65: straddle credit ₹26,650/lot, margin ~₹1.3 lakh; strangle credit ₹11,895/lot, margin ~₹1.2 lakh; iron condor credit ₹5,200/lot, max loss ₹7,800/lot, margin ₹7,800 (prob max profit ~43%); butterfly debit ₹975/lot, max profit ₹12,025/lot; iron butterfly credit ₹15,470/lot, max loss ₹4,030/lot. Case study 4-week WEEKLY NIFTY IC (weekly valid — NIFTY Tuesday expiry): +80/+70/−30/+90 = +₹210/unit (+₹13,650/lot); Wk3 adjustment −120→−30 saved ₹90/unit (₹5,850/lot); defined-risk margin stable ~₹7,800 through VIX 13→20. A3 max loss ₹10,400/lot; A4 butterfly debit ₹21 (per-unit, unchanged). No transaction costs (gross P&L) → Apr-2026 STT not applicable. IV = implied volatility. -->
