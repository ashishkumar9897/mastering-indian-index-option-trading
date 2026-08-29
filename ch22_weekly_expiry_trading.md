<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 9, 10, 11, 18. Target length ~10,500 words. Current as of 5 Aug 2026. OPENS Part VI. HOUSE BASELINE: NIFTY 24,600, lot 65; BANKNIFTY lot 30 (NSE Jan-2026). EXPIRY WEEKDAY: NIFTY = Tuesday, SENSEX = Thursday (SEBI standardisation, 1 Sep 2025) — chapter updated from illustrative "Thursday" to Tuesday; run-up pattern "Wednesday–Thursday"→"Monday–Tuesday". Weekly straddle decay (√T, per-unit, lot-independent): 4d ₹268 → 3d ₹232 → 2d ₹189 → Tue open ₹134 → Tue 2PM ₹66 → close ₹0; last 48h ~71%, expiry day ~50%. Table days relabelled to a Tuesday expiry (Thu/Fri/Mon/Tue, illustrative sessions). Intraday Gamma (expiry-day, per-unit): 9:15 0.00238 → 2PM 0.00487 → ~3PM 0.0107; Delta/100pt 0.24→0.49→1.07. Expiry-day condor /lot at 65: credit ₹2,600, max loss ₹3,900. SEBI expiry-day margin (verified current): 2% additional ELM on shorts within 2 trading days of expiry (since 20 Nov 2024, on contract value) + calendar-spread benefit removed on expiry day (index since 10 Feb 2025, single-stock from May 2026). GEX (Edition 2): long-gamma dealers pin, short-gamma amplify. Case study 1000-pt move (BANKNIFTY lot 30): naked straddle −₹820/unit=₹24,600/lot, condor −₹60, long straddle +₹850. No transaction costs (gross P&L) → Apr-2026 STT change not applicable to numbers. IV = implied volatility. -->

# Chapter 22 — Weekly Expiry Trading: The Indian Edge

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Understand the unique dynamics of weekly expiry options in India.
2. Master Theta acceleration in the final 48 hours before expiry.
3. Trade the expiry-day strategies that define the Indian market.
4. Manage Gamma risk on expiry day.
5. Understand SEBI's post-2024 rules and how they reshape expiry trading.

Welcome to Part VI, where theory meets the chaos of real markets. India's weekly expiries are the busiest option contracts on earth (Chapter 1), and expiry day is where every Greek you have learned collides at once. This chapter is the synthesis of Gamma (Chapter 9), Theta (Chapter 10), and non-directional strategies (Chapter 18) into the specific, high-stakes arena of the Indian weekly expiry.

---

## 2. Introduction

Expiry day is the Indian option market's defining event, repeated every week. It is where the most premium is collected, the most money is lost, and the most dangerous force in options — expiry-day Gamma — is unleashed. A short-straddle seller who has calmly harvested Theta all week can watch a single afternoon move erase a month of gains in an hour. A defined-risk trader beside them, with the same view, survives untouched. And behind it all, largely invisible to retail, sit the dealers whose delta-hedging either *pins* the index quietly to a strike or *amplifies* a move into a rout.

This chapter explains all of it. India's weekly options concentrate the entire life-cycle of an option — build-up, decay, and violent resolution — into a few days, with the final 48 hours holding most of the decay and expiry day holding almost all of the risk. Theta accelerates to its steepest; Gamma explodes toward infinity at the strike; and the market often "pins" near high open-interest strikes — not by magic, but through the mechanical delta-hedging of dealers, whose aggregate **gamma exposure (GEX)** either dampens or amplifies every move. Understanding GEX is understanding *why* expiry days behave as they do — the Edition 2 addition that connects the retail seller to the dealer flow on the other side of their trade.

We build the full picture: the post-2024 weekly landscape, the Monday-to-Tuesday decay pattern, the expiry-day Gamma explosion, the specific expiry-day strategies (the straddle sell, the defined-risk condor and butterfly), the dealer-hedging mechanism behind pinning and violence, SEBI's expiry-day margin rules, and the case that every Indian option seller must internalise — the thousand-point expiry move. Setting: **NIFTY at 24,600, lot 65** (and a historical BANKNIFTY expiry for the case).

---

## 3. Core Concepts

### 3.1 India's weekly expiry landscape

**The post-2024 structure.** After SEBI's November 2024 rationalisation (Chapter 1), each exchange offers weekly-expiring options on only **one** index: **NIFTY on the NSE** and **SENSEX on the BSE**. BANKNIFTY, FINNIFTY, and MIDCPNIFTY are now **monthly only**. So "weekly expiry trading" in India today means, overwhelmingly, **NIFTY weeklies** (and SENSEX for BSE traders).

> **Market Note — the expiry weekday (and verify it).** Under SEBI's standardisation effective **1 September 2025**, NIFTY weeklies (and monthlies) expire on **Tuesday**, and SENSEX on **Thursday**. This chapter therefore uses **Tuesday** as the NIFTY expiry day and refers to the "**Monday–Tuesday**" run-up pattern. The exact weekday is exchange-set and has been changed before, so still **confirm the current day** on the NSE/BSE before planning any expiry trade — the *dynamics* in this chapter (final-48-hour decay, expiry-day Gamma) hold regardless of which weekday expiry falls on.

**Why weeklies dominate globally.** India's weekly options became the world's most traded contracts (Chapter 1) for three reasons: **low premium** (a weekly costs a fraction of a monthly, so accessible to small accounts), **high Theta** (they decay ~2× faster per day than monthlies, Chapter 10, attracting sellers), and **event coverage** (a weekly lets you trade a specific week's news cheaply). The result is enormous volume — and enormous concentration of risk into the expiry day.

---

### 3.2 Theta acceleration — the final 48 hours

A weekly option's time value drains unevenly across its short life, with the bulk concentrated in the last two days. Table 22.1 tracks an ATM NIFTY straddle through a weekly cycle (using the √T decay of Chapter 10).

**Table 22.1 — ATM NIFTY straddle decay through the week (illustrative)**

| Day (DTE) | ATM straddle (₹) | Decay from prior | % of week's decay |
| --- | ---: | ---: | ---: |
| Thursday (prior, 4 DTE) | 268 | — | — |
| Friday (3 DTE) | 232 | 36 | 13% |
| Monday (2 DTE) | 189 | 43 | 16% |
| Tuesday open (1 DTE) | 134 | 55 | 21% |
| Tuesday 2:00 PM (~0.24 DTE) | 66 | 68 | 25% |
| Tuesday close (0 DTE) | 0 | 66 | 25% |

The pattern is decisive: **the last 48 hours (Monday open to Tuesday close) contain ~71% of the week's decay**, and **expiry day alone (Tuesday) holds ~50%** of it. The first half of the week is a slow drip; the back half is a flood. This is the mathematical basis of the **"Monday–Tuesday" pattern** for NIFTY weekly sellers: the rich, harvestable decay concentrates in the final two sessions — but so does the Gamma risk (Section 3.3), so the richest decay and the sharpest danger arrive together. (Days are illustrative sessions to a Tuesday expiry; the weekend's decay is muted/pre-priced, per Chapter 10.)

---

### 3.3 The expiry-day Gamma explosion

This is the flagship concept of the chapter, and the single most important thing to understand about expiry day.

**What is it?** As expiry approaches, an at-the-money option's **Gamma explodes** — its Delta changes faster and faster per point of index movement (Chapter 9). On expiry day, and especially in the final hours, an ATM option flips between behaving like an in-the-money and an out-of-the-money contract on tiny moves.

**Why does it happen?** Gamma ∝ 1/√T (Chapter 9). As T shrinks toward zero on expiry day, Gamma shrinks the denominator toward zero, so Gamma rockets upward — theoretically toward infinity for the ATM option exactly at expiry. The option's Delta, which is a smooth 0.5 at the money with weeks to go, becomes a near-instant switch between 0 and 1 in the final minutes.

**Why should a trader care?** Because it makes expiry-day short positions **un-hedgeable in real time.** A "Delta-neutral" short straddle at 9:15 AM can develop a large, runaway Delta within a single move by afternoon, and the move happens faster than you can re-hedge (Chapter 12's lesson, at its most extreme). Expiry-day Gamma is why the same seller who profited all week can be destroyed in one afternoon.

**Intuitive explanation.** Early in an option's life, its Delta is a dimmer switch — it changes smoothly as the index moves. On expiry afternoon, it becomes a **light switch** — a tiny move flips it fully on or off. Trying to hedge a light switch that flips faster than you can react is the expiry-day seller's nightmare.

**Numerical feel.** Table 22.2 shows the ATM NIFTY Gamma escalating through expiry day.

**Table 22.2 — ATM NIFTY Gamma through expiry day (illustrative)**

| Time (approx. DTE) | ATM Gamma | Delta change per 100-pt move |
| --- | ---: | ---: |
| 9:15 AM (1 DTE) | 0.00238 | 0.24 |
| 2:00 PM (~0.24 DTE) | 0.00487 | 0.49 |
| ~3:00 PM (~0.05 DTE) | 0.0107 | 1.07 |

By mid-afternoon, a 100-point move flips the ATM Delta by ~0.5; near the close, a 100-point move flips it by *more than its entire range* — the linear approximation breaks, the option snaps from ATM to fully ITM or OTM. This is the explosion.

**Professional interpretation.** Desks treat expiry-day ATM Gamma as radioactive — they either avoid being short it, size it tiny, or hedge it with the *underlying* (futures) continuously and accept the slippage. No professional holds a large naked short ATM straddle into the expiry close and hopes.

**Common mistake.** Selling an expiry-day straddle for the rich Theta without respecting that the Gamma making that Theta rich is the same Gamma that can destroy the position on one move.

**Practical takeaway.** **Expiry-day Gamma is the most dangerous force in options — it makes short positions un-hedgeable in the final hours; size expiry-day shorts tiny, use defined risk, and never assume a "neutral" position stays neutral.**

---

### 3.4 Expiry-day strategies

Expiry day's extreme Theta and Gamma shape a distinct set of strategies:

**The 0 DTE straddle/strangle sell.** The classic expiry-day play: sell the ATM straddle (or an OTM strangle) at 9:15 AM to harvest the day's entire remaining time value (₹134 on the straddle in Table 22.1). The appeal is the rich, fast decay; the peril is the Gamma explosion. Done naked, it is one of the highest-risk trades in the market — a bet that the index stays near the strike all day, with a catastrophic loss if it does not (the case study, Section 9). Only for large, disciplined accounts with active hedging.

**Defined-risk expiry structures.** The safer expiry-day plays cap the risk:

* **Expiry-day iron condor** — sell tight (e.g., 100-point) wings at 9:15 AM, collecting the day's decay with a *capped* loss (Section 5). It harvests expiry Theta without the naked straddle's open-ended Gamma risk.
* **Buying a butterfly around the expected close** — a cheap, defined-risk bet that the index *pins* a specific strike (often a high-OI strike, Section 3.5). Low cost, high reward-to-risk, and it profits if the pinning the market often exhibits actually occurs.

**The expected-range tool.** The ATM straddle premium at the open *is* the market's expected range for the day (Chapters 13, 18): a Tuesday-open (expiry) straddle of ₹134 implies an expected NIFTY range of about ±134 points. Sellers place short strikes *outside* this range; buyers of butterflies center them *inside* it. The straddle price is the expiry-day position-sizing tool.

---

### 3.5 Pin risk, the expiry effect, and dealer gamma (GEX)

Why does the index so often drift toward, and "pin" near, a high open-interest strike at expiry? And why, on other days, does it instead move violently? The answer is **dealer delta-hedging**, measured by **gamma exposure (GEX)** — the Edition 2 addition that explains the mechanism behind pinning, not just its existence.

**The setup.** Every option a retail trader buys or sells has a **dealer (market maker) on the other side**, and dealers hedge their resulting delta by trading the underlying (futures). Their *aggregate* gamma position — GEX — determines *how* they hedge, and that hedging flow moves the market.

**When dealers are net LONG gamma (positive GEX) → pinning.** If retail has, on net, *sold* options to dealers (common in India, where retail loves selling premium), dealers are net *long* gamma. Their delta-hedging is then **mean-reverting**: as the index *rises*, their delta grows positive, so they **sell** futures (into the rally); as it *falls*, their delta grows negative, so they **buy** futures (into the dip). This "sell rallies, buy dips" flow **dampens moves and pins the index near the high-OI strike** — the calm, range-bound expiry that Max Pain (Chapter 7) describes.

**When dealers are net SHORT gamma (negative GEX) → amplification.** If retail has, on net, *bought* options (e.g., a day of heavy call buying chasing a move), dealers are net *short* gamma. Their hedging is then **trend-amplifying**: as the index *rises*, their (short) delta grows negative, so they **buy** futures (chasing the rally); as it *falls*, they **sell** (into the dip). This "buy rallies, sell dips" flow **amplifies moves into violent, trending expiries** — the mechanism behind the thousand-point move (Section 9).

**GEX as the market-structure lens.** Gamma exposure is the aggregate dealer gamma across all strikes. **Positive GEX → pinning and calm; negative GEX → amplification and violence.** This single idea explains the two faces of expiry day: the quiet pin and the violent rout are the *same mechanism* (dealer delta-hedging) with the *opposite sign* of dealer gamma.

> **Beginner Alert — pinning is not magic; it is hedging flow.** It is tempting to think the index "wants" to pin a strike, or that Max Pain is manipulation. Neither is true. Pinning is the mechanical result of dealers who are long gamma selling every rally and buying every dip to stay hedged — a self-fulfilling dampening. When dealers are instead short gamma, the *same* mechanical hedging *amplifies* moves. There is no intention, only flow — but understanding the flow tells you whether to expect a calm pin or a violent move.

**Reading dealer positioning.** You can *estimate* the sign of dealer gamma from the option chain — heavy OI at strikes and who is likely long/short (retail net selling → dealers long gamma → pinning bias). But treat this as **context, not a precise signal**: it tells you whether the day is more likely to pin or to move, not exactly what will happen. In India, normal expiries often see dealers long gamma (retail net sellers) and thus a pinning tendency — but the days retail piles into buying (chasing a trend or an event) flip dealers short gamma and set up the violent moves.

---

### 3.6 SEBI's expiry-day margin rules

SEBI's post-2024 framework (Chapter 1) makes expiry day *more* capital-intensive for short sellers, precisely when the risk is highest:

* **Additional expiry-day ELM.** Since **20 November 2024**, a **2% additional Extreme Loss Margin** — calculated on the contract value (strike × lot size) — is levied on short option positions expiring **within two trading days**, stacked on top of the usual SPAN + ELM. It raises the capital tied up on the short leg as expiry nears.
* **Removal of the calendar-spread benefit on expiry day.** Since **10 February 2025**, the margin offset a calendar spread normally enjoys is *removed* on the day the near leg expires, so the near-term short is fully margined (the two legs no longer net). (From May 2026 this removal was extended to single-stock derivatives as well.)

The practical effect: **the same short position (or credit spread) requires more margin as expiry approaches — the extra 2% ELM biting within two days of expiry — than it did earlier in the week.** A seller must plan for this: the expiry-day margin increase reduces capital efficiency exactly when Gamma risk peaks, and a trader running tight on margin can be forced to reduce positions on expiry day. This is SEBI deliberately making expiry-day speculation costlier and safer for the system (Chapter 1), and it must be built into any expiry-selling plan.

---

### 3.7 Intraday Theta, Gamma, and the excursion concepts

Expiry-day management requires thinking in *hours and minutes*, not days:

**Intraday Theta.** The day's decay is not uniform — it accelerates toward the close. The Tuesday (expiry) straddle (₹134 at open) decays to ~₹66 by 2 PM (~₹14/hour over the first 4.75 hours) and then to ₹0 by close (~₹44/hour in the final 1.5 hours). **The richest decay is in the last hour** — and so is the sharpest Gamma. Converting daily Theta to an hourly figure (daily ÷ ~6.25 trading hours) *understates* the late-day decay; expiry-day Theta is front-loaded away from the open and back-loaded toward the close.

**Intraday Gamma.** As Table 22.2 shows, Gamma roughly doubles from open to 2 PM and doubles again toward the close — the Delta-change per move escalating through the day. Manage the position on a *tightening* leash as the afternoon progresses.

**MFE and MAE.** Two concepts sharpen expiry-day management: **Maximum Favourable Excursion (MFE)** — the best unrealised profit the position reached — and **Maximum Adverse Excursion (MAE)** — the worst unrealised loss it touched. Tracking MFE/MAE over many expiry-day trades tells you whether you are exiting too early (leaving MFE on the table) or holding too long (letting MAE grow), and helps calibrate expiry-day exits.

---

## 4. Examples (Real-World)

**Example 1 — The Monday-to-Tuesday harvest.** A NIFTY seller opens a position Monday morning to capture the final 48 hours' decay (~71% of the week's, Table 22.1). The rich late-week Theta is the reward; the escalating Gamma is the risk they must manage into Tuesday's close.

**Example 2 — The pin that formed.** On a normal expiry with dealers net long gamma, NIFTY drifts toward a heavy-OI strike and pins there into the close — dealers selling every uptick and buying every downtick to stay hedged. A butterfly buyer centered on that strike is rewarded; the pinning was dealer hedging flow, not chance.

**Example 3 — The move that ran.** On a day of heavy retail call buying (dealers net short gamma), a morning rally accelerates as dealers buy futures to hedge, feeding the move. The pin never forms; the index trends hard all day. Same market, opposite GEX sign, opposite outcome (the case study, Section 9).

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65; expiry-day figures from Tables 22.1–22.2.

### Numerical Example 1 — The final-48-hour decay

From Table 22.1, the ATM straddle falls from ₹268 (Thursday, prior week) to ₹0 (Tuesday close). The decay in the **last 48 hours** (Monday open ₹189 → Tuesday close ₹0):

```
Last-48-hour decay = ₹189 of the ₹268 week ≈ 71% of the week's decay
Expiry-day (Tuesday) decay = ₹134 ≈ 50% of the week's decay
```

Half the week's time value evaporates on expiry day alone — the seller's richest harvest and the buyer's steepest headwind, concentrated in one session.

### Numerical Example 2 — The Gamma explosion in numbers

From Table 22.2, a 100-point NIFTY move flips the ATM Delta by:

```
9:15 AM (1 DTE):  0.00238 × 100 = 0.24
2:00 PM (0.24 DTE): 0.00487 × 100 = 0.49
~3:00 PM (0.05 DTE): 0.0107 × 100 = 1.07 (more than the option's entire Delta range)
```

A short straddle that was Delta-neutral at 9:15 develops a ~0.5 Delta swing per 100-point move by 2 PM and a full flip near the close — un-hedgeable in real time. The Gamma quadruples through the day.

### Numerical Example 3 — Expiry-day iron condor

At 9:15 AM (Tuesday, 0 DTE), NIFTY 24,600, sell a tight 100-point iron condor:

```
Sell 24,700 CE / buy 24,800 CE (call spread) + Sell 24,500 PE / buy 24,400 PE (put spread)
Net credit ≈ ₹40 (₹2,600/lot); Max loss = 100 − 40 = ₹60 (₹3,900/lot); margin ≈ ₹3,900
Short strikes at ±100; expected day range = straddle ₹134 → ±134 (WIDER than the shorts)
```

If NIFTY chops around 24,600 all day, the condor decays to the full ₹40 by close (Theta harvested with defined risk). But because the expected range (±134) *exceeds* the short strikes (±100), there is meaningful risk of a breach — and if NIFTY trends to 24,700+, the call spread loses fast (expiry Gamma), capped at ₹60. The defined risk (₹60 max loss) is what makes this survivable versus the naked straddle.

### Numerical Example 4 — Intraday Theta acceleration

The Tuesday (expiry) straddle: ₹134 (open) → ₹66 (2 PM) → ₹0 (close):

```
Open to 2 PM (4.75 hrs): (134 − 66)/4.75 ≈ ₹14/hour
2 PM to close (1.5 hrs): 66/1.5 ≈ ₹44/hour
```

Decay accelerates from ~₹14/hour early to ~₹44/hour in the final 1.5 hours — the richest (and riskiest) decay is in the last hour, exactly where Gamma is most explosive.

### Numerical Example 5 — Expected range and short-strike placement

Tuesday-open (expiry) ATM straddle = ₹134, NIFTY 24,600:

```
Expected day range = ±₹134 (the straddle premium ≈ the market's expected move)
→ 1-standard-deviation range ≈ 24,466 to 24,734
```

A seller wanting short strikes *outside* the expected range should place them beyond ±134 (e.g., 24,750 CE / 24,450 PE), accepting a smaller credit for a higher probability of finishing in the range. Selling *inside* ±134 (e.g., 24,650 CE) is selling within the expected move — high credit, low probability.

---

## 6. Calculations (the reusable recipes)

**(a) Expiry-day expected range**

```
Expected range (± points) ≈ ATM straddle premium at the open
1-standard-deviation band = Spot ± straddle premium
```

**(b) Intraday Theta (accelerating)**

```
Average hourly Theta ≈ Daily Theta ÷ ~6.25 trading hours (but decay is back-loaded to the close)
```

**(c) Intraday Gamma escalation**

```
Gamma ∝ 1/√T → escalates through expiry day; Delta change per move = Gamma × (points moved)
```

**(d) Gamma exposure (GEX) sign → expiry behaviour**

```
Dealers net LONG gamma (positive GEX): sell rallies / buy dips → pinning, calm
Dealers net SHORT gamma (negative GEX): buy rallies / sell dips → amplification, violence
```

**(e) Excursion metrics**

```
MFE = best unrealised profit reached;  MAE = worst unrealised loss reached (for exit calibration)
```

---

## 7. Practical Insights

* **The richest decay and the sharpest risk are the same 48 hours.** The final two days hold ~71% of the week's Theta — and the expiry-day Gamma that can destroy the position collecting it. You cannot have the decay without the danger.
* **Expiry-day Gamma is un-hedgeable — respect it.** A neutral morning position can run away by afternoon faster than you can hedge; size expiry-day shorts tiny, prefer defined risk, and tighten management as the close nears.
* **Use the open straddle as your range and sizing tool.** It is the market's expected move; place short strikes outside it, and center butterflies inside it.
* **Read GEX for context.** Dealers long gamma (retail net sellers) bias toward a pin; dealers short gamma (retail net buyers) bias toward a violent move. It is context, not certainty — but it tells you which kind of day to prepare for.
* **Budget for the expiry-day margin increase.** SEBI's enhanced expiry-day margin and removed calendar benefit mean short positions cost more capital exactly when risk peaks — plan the buffer or be forced to reduce.

> **Professional Insight — you are trading against the dealer's hedge, so know its sign.** The single most useful expiry-day question a professional asks is "which way is the dealer gamma?" When dealers are long gamma, moves are dampened and mean-reverting — a good day to sell premium and expect a pin. When dealers are short gamma, moves are amplified and trending — a day to *not* be short naked options, and perhaps to be long them (or long the move). The retail seller who ignores GEX is trading blind against the very flow that will decide whether the day pins quietly or runs a thousand points.

---

## 8. Common Mistakes

* **Selling the expiry-day straddle for the "free" decay.** The rich Theta exists *because* of the explosive Gamma; naked selling into it is one of the market's highest-risk trades.
* **Assuming a neutral expiry position stays neutral.** Expiry Gamma makes Delta run away by afternoon; "Delta-neutral at 9:15" is not "safe at 2 PM."
* **Ignoring the expected range.** Selling short strikes *inside* the open straddle's implied move (high credit, low probability) and being surprised when the index reaches them.
* **Treating pinning as guaranteed (or as manipulation).** Pinning is dealer hedging flow with a *sign*; when dealers are short gamma, the pin becomes a rout. Do not bet the account on a pin.
* **Forgetting the expiry-day margin increase.** Running tight on margin and being forced to reduce short positions on expiry day (Tuesday), at the worst moment.
* **Holding a naked short into the final hour.** The last hour has the richest decay *and* the most explosive Gamma; it is where naked sellers are destroyed.

---

## 9. Case Study — "The 1000-Point Expiry Day Move"

**Context.** The thousand-point expiry move is the archetype every Indian option seller must internalise. It is drawn from the BANKNIFTY weekly expiries of the pre-2024 era (BANKNIFTY now trades monthly only, but the mechanism is identical for today's NIFTY weeklies) — a day when the index moved ~1,000 points in a single session, Gamma exploded, and short sellers were routed. Figures are illustrative but representative; BANKNIFTY at 52,000, lot 30 (current), per unit unless noted.

**The setup.** On expiry morning, a retail trader sells the ATM **52,000 straddle** (sell 52,000 CE + 52,000 PE) for a total of **₹200** — the thin remaining time value on expiry day — expecting to harvest the day's decay. The position is Delta-neutral, hugely positive Theta, and *hugely* negative Gamma. Crucially, on this day retail has been *buying* calls heavily (chasing an expected move), so **dealers are net short gamma (negative GEX)** — their hedging will *amplify* any move.

**What happened — minute by minute.**

**Table 22.3 — The 1000-point expiry move (illustrative snapshots)**

| Time | BANKNIFTY | 52,000 straddle | Short-seller P&L/unit | Position Delta |
| --- | ---: | ---: | ---: | ---: |
| 9:15 AM | 52,000 | ₹200 | ₹0 (entry) | ~0 |
| 11:00 AM | 52,300 | ₹380 | −₹180 | ~−0.4 |
| 1:00 PM | 52,600 | ₹650 | −₹450 | ~−0.7 |
| 2:30 PM | 53,000 | ₹1,020 | −₹820 | ~−0.9 |
| Close | 53,050 | ₹1,050 | −₹850 | ~−1.0 |

* **The trigger and the amplification.** A mid-morning cue started a rally. Because dealers were **short gamma**, they had to **buy futures to hedge as BANKNIFTY rose** — and that buying *pushed it higher*, forcing more hedging buying, in a feedback loop. The move that might have been 300 points became 1,000, driven by the dealers' own trend-amplifying hedge (negative GEX in action).
* **The Gamma explosion on the short seller.** At 9:15 the straddle seller's Delta was ~0 and manageable. As BANKNIFTY rose, the short 52,000 call's Delta raced toward −1 (short a deep-ITM call) while the short put's went to 0 — so the **position Delta ran from ~0 to ~−1.0**, leaving the seller *fully short* into a rocketing market. Re-hedging was impossible: the move was too fast, and any attempt to buy futures to hedge only added to the buying pressure.
* **The rout.** By 2:30 PM the straddle the seller had collected ₹200 for was worth ₹1,020 — a loss of **₹820/unit (₹24,600/lot)** on a trade whose maximum possible profit was ₹200. Sellers who had not cut early scrambled to buy back at any price, feeding the move further.

**P&L by strategy type.** The same day, the same move:

| Strategy | Outcome per unit |
| --- | ---: |
| Naked short straddle | **−₹850** (catastrophic — the case above) |
| Defined-risk iron condor (100-wide, ₹40 credit) | **−₹60** (capped — survived) |
| Long straddle buyer (bet on a move) | **+₹850** (the mirror windfall) |
| Butterfly buyer (bet on a pin) | −small debit (the pin never formed) |

**The analysis.** Three forces combined into the rout. First, **expiry-day Gamma** made the naked short un-hedgeable — the Delta ran from 0 to −1 faster than anyone could react (Chapter 9 at its extreme). Second, **negative GEX** (dealers short gamma from retail's call buying) *amplified* the move — the dealers' hedging bought into the rally, turning a modest move into a thousand points. Third, the **short seller's own scramble** to buy back added to the buying, feeding the loop. The defined-risk condor trader, with the *same* neutral view, lost only the capped ₹60 — the defined risk was the difference between a survivable loss and a ruinous one (echoing Chapters 18 and 21). And the long-straddle buyer, positioned for a move on a negative-GEX day, took the windfall.

**The lesson.** Expiry day is where Gamma and dealer hedging combine into the market's most violent force. A naked short straddle collects the richest decay in the market *because* it carries the most explosive, un-hedgeable Gamma — and on a negative-GEX day, that Gamma, amplified by dealer flow, can lose many times the maximum possible profit in a single afternoon. The survivors use **defined risk**, size tiny, read the **GEX sign**, and never hold a large naked short into the expiry close. The thousand-point move is not a freak event to dismiss; it is the risk that is *always present* on expiry day, waiting for the day the dealer gamma turns negative.

*(Takeaway: on expiry day, naked short options carry explosive, un-hedgeable Gamma that dealer short-gamma hedging can amplify into a rout — use defined risk, size tiny, read the GEX sign, and never hold a large naked short into the close.)*

---

## 10. Chapter Summary

* Post-2024, India's **weekly expiries** are **NIFTY (NSE) and SENSEX (BSE)** only (others monthly); the exact expiry *weekday* is exchange-set and revised — verify it. Weeklies dominate globally for low premium, high Theta, and event coverage.
* **Theta accelerates into expiry:** the final 48 hours hold ~71% of the week's decay, expiry day alone ~50% — the "Monday–Tuesday" harvest for sellers (NIFTY expiry is Tuesday).
* **Expiry-day Gamma explodes** (∝ 1/√T): the ATM Delta becomes a light switch, flipping fully on tiny moves near the close, making short positions **un-hedgeable** in real time.
* **Expiry-day strategies:** the 0-DTE straddle/strangle sell (rich decay, explosive risk — defined-risk or tiny only) and defined-risk condors/butterflies; the **open straddle premium is the expected day range** and the sizing tool.
* **Pinning is dealer hedging flow (GEX):** dealers net **long gamma** sell rallies/buy dips → **pin** (calm); net **short gamma** buy rallies/sell dips → **amplify** (violence) — the same mechanism, opposite sign.
* **SEBI's expiry-day rules** — a 2% additional ELM on short options within two days of expiry, plus removal of the calendar-spread benefit on expiry day — raise short-position margin exactly when risk peaks.
* **Manage intraday:** decay and Gamma both accelerate to the close (richest decay ~₹44/hr in the final 1.5 hours); track MFE/MAE to calibrate exits.
* The **thousand-point expiry move** shows Gamma + negative GEX + the seller's scramble routing naked shorts (−₹850) while defined-risk condors survive (−₹60) — the ever-present expiry-day risk.

---

## 11. Key Takeaways

* **The final 48 hours hold most of the decay *and* the danger** — you cannot harvest the rich expiry Theta without accepting the explosive Gamma that comes with it.
* **Expiry-day Gamma is un-hedgeable** — size shorts tiny, use defined risk, tighten management to the close, and never assume a neutral position stays neutral.
* **Read the GEX sign** — dealers long gamma bias toward a pin (sell premium), dealers short gamma bias toward a violent move (don't be naked short).
* **The thousand-point move is always possible on expiry day** — the defined-risk trader survives it; the naked short seller may not.

---

## 12. Practice Questions

**Q1 (Landscape).** Post-November 2024, which indices have weekly expiries in India, and which are monthly only?

**Q2 (Theta).** Using Table 22.1, what fraction of the week's decay occurs in the final 48 hours, and on expiry day alone?

**Q3 (Gamma).** Explain why an ATM option's Gamma "explodes" on expiry day, referencing its relationship to time.

**Q4 (Delta run).** An ATM option has Gamma 0.005 at 2 PM on expiry day. By how much does its Delta change on a 120-point move, and why is this dangerous for a short straddle?

**Q5 (Expected range).** The Tuesday-open (expiry) ATM straddle is ₹150 with NIFTY at 24,600. What is the expected day range, and where would a seller place short strikes?

**Q6 (GEX — pinning).** Explain, in terms of dealer hedging, why the index tends to pin a high-OI strike when dealers are net long gamma.

**Q7 (GEX — amplification).** On a day of heavy retail call buying, are dealers net long or short gamma, and how does their hedging affect a rally?

**Q8 (Margin).** Why does the same NIFTY credit spread require more margin on Tuesday (expiry) than earlier in the week?

**Q9 (Strategy choice).** You want to harvest expiry-day decay but cannot risk a large loss. Which structure fits, and why is it safer than a naked straddle?

**Q10 (Case judgement).** In the thousand-point move, the naked straddle seller lost ₹850/unit while the iron condor trader lost ₹60/unit — same view, same day. Explain the two reasons the condor survived.

---

## 13. Detailed Solutions

**A1.** Weekly expiries: **NIFTY (on the NSE) and SENSEX (on the BSE)**. Monthly only: **BANKNIFTY, FINNIFTY, and MIDCPNIFTY**. (The exact weekly expiry weekday is set by the exchanges and has been revised — verify the current day.)

**A2.** From Table 22.1, the final 48 hours (Monday open ₹189 → Tuesday close ₹0) hold **~71%** of the week's decay, and **expiry day alone (Tuesday, ~₹134) holds ~50%.**

**A3.** Gamma ∝ 1/√T. As expiry approaches, the time to expiry T shrinks toward zero, so 1/√T (and thus Gamma) rockets upward — theoretically toward infinity for the ATM option exactly at expiry. The option's Delta, smooth with weeks to go, becomes a near-instant switch between 0 and 1 in the final minutes.

**A4.** Delta change = Gamma × move = 0.005 × 120 = **0.60** — a 120-point move swings the ATM Delta by 0.6. For a short straddle, this means the position, neutral moments earlier, suddenly carries a large directional Delta *against* the move (short Gamma), and the move happens faster than the seller can re-hedge — the loss accelerates uncontrollably.

**A5.** Expected day range = ± the straddle premium = **±150 points** (≈ 24,450 to 24,750). A seller wanting a high probability of finishing in range would place short strikes *outside* ±150 — e.g., a 24,750 CE / 24,450 PE strangle or condor — accepting a smaller credit for the safer distance.

**A6.** When dealers are net long gamma, staying hedged requires **mean-reverting** trades: as the index rises, their delta grows positive, so they **sell** futures (into the rally); as it falls, they **buy** (into the dip). This "sell rallies, buy dips" flow dampens every move and holds the index near the high-OI strike — a self-fulfilling pin created by the hedging, not by intention.

**A7.** Heavy retail call *buying* means dealers, on the other side, are net **short** gamma (negative GEX). To hedge, they must **buy futures as the index rises** (their short-gamma delta grows negative on a rally) — which *pushes the rally further*, amplifying the move in a feedback loop (trend-amplifying hedging).

**A8.** SEBI's post-2024 framework levies a **2% additional Extreme Loss Margin** (on contract value) on short option positions expiring within two trading days and **removes the calendar-spread margin benefit** on the near leg's expiry day. So the same short credit spread is charged more margin on Tuesday (expiry) than earlier in the week — more capital required exactly when Gamma risk is highest.

**A9.** A **defined-risk iron condor** (tight wings) — it harvests the expiry-day decay like the straddle but **caps the maximum loss** at the wing width minus the credit (e.g., ₹60), with margin equal to that capped loss. Unlike the naked straddle, whose loss is open-ended and un-hedgeable in the Gamma explosion, the condor's worst case is bounded and survivable regardless of how far the index moves.

**A10.** Two reasons: (i) **Defined risk** — the condor's long wings cap the loss at the wing width minus the credit (₹60), so no matter how far BANKNIFTY moved, the loss could not exceed that, whereas the naked straddle's loss was open-ended. (ii) **Stable margin** — the defined-risk condor's margin did not balloon in the move, so the trader was not forced to scramble or liquidate, and could simply hold to the capped loss. The naked seller had neither protection: unlimited loss and a margin that ballooned, forcing a panicked exit into the amplified move.

---

## 14. Mini Glossary

* **Weekly expiry** — options expiring each week; in India, NIFTY (NSE) and SENSEX (BSE) post-2024. → this chapter.
* **Expiry-day Gamma explosion** — the rocketing of ATM Gamma as expiry nears (∝ 1/√T), making Delta flip on tiny moves. → this chapter.
* **0 DTE trading** — trading options on their expiry day (zero days to expiry). → this chapter.
* **Monday–Tuesday pattern** — the concentration of ~71% of a NIFTY weekly's decay in its final 48 hours (expiry Tuesday). → this chapter.
* **Pin risk / the expiry effect** — the tendency of the index to settle near a high open-interest strike at expiry. → this chapter.
* **Gamma exposure (GEX)** — the aggregate dealer gamma position; positive → pinning, negative → amplification. → this chapter.
* **Dealer delta-hedging** — market makers trading the underlying to stay delta-neutral; the mechanism behind pinning and amplification. → this chapter.
* **Expected day range** — the ATM straddle premium at the open, ≈ the market's expected move for the day. → this chapter.
* **Intraday Theta / Gamma** — the within-day acceleration of decay and Delta-change on expiry day. → this chapter.
* **MFE / MAE** — Maximum Favourable / Adverse Excursion; the best/worst unrealised P&L a trade reached, for exit calibration. → this chapter.

---

<!-- End of Chapter 22 (Rev 2, opens Part VI, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65, BANKNIFTY lot 35→30 (NSE Jan-2026); NIFTY expiry Thursday→Tuesday (SEBI 1 Sep 2025), run-up "Wednesday–Thursday"→"Monday–Tuesday" throughout (intro, Market Note, Table 22.1 relabelled Thu/Fri/Mon/Tue, §3.2/3.4, NE1/NE3/NE4/NE5, Example 1, Summary, Q5/Q8/A2/A8, glossary). Per-unit straddle decay values (₹268→₹0) and Gamma table lot-independent — unchanged. Lot-scaled: expiry-day condor credit ₹2,600/lot, max loss ₹3,900/lot; case study 1000-pt move loss ₹820/unit = ₹24,600/lot (lot 30). SEBI expiry-day margin SHARPENED & verified current: 2% additional ELM on shorts within 2 trading days of expiry (since 20 Nov 2024) + calendar-spread benefit removed on expiry day (index since 10 Feb 2025; single-stock from 4 May 2026). GEX (Edition 2) unchanged. Case study (Table 22.3): naked straddle −₹850/unit, condor −₹60, long straddle +₹850. No transaction costs (gross P&L) → Apr-2026 STT change not applicable to numbers. IV = implied volatility. -->
