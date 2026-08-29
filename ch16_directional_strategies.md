<!-- Difficulty: Level 2.5/5 (Intermediate). Dependency: Chapters 4, 8, 10. Target length ~10,500 words. Current as of 5 Aug 2026. OPENS Part V (Strategy Playbook) — standard strategy template. HOUSE BASELINE: NIFTY 24,600, lot 65; BANKNIFTY lot 30 (NSE Jan-2026 revision); naked margin ~₹1.25 lakh/lot (Ch3, lot-65). Premiums/Greeks per-unit from σ=13% BSM basis (10 DTE): 24,600 CE ₹212 (Δ0.54), 24,600 PE ₹198 (Δ−0.46) — per-unit values, breakevens, Delta-to-premium ratios, ROI %s lot-independent. Lot-scaled figures recomputed at lot 65/30: capital 13,780/12,870; NE1 +5,720/−13,780; NE5 protective put on ₹15,99,000 notional. No transaction costs shown (gross P&L), so Apr-2026 STT change not applicable. Edition 2 additions: protective put, covered call/overwriting, cash-secured put. Case study BANKNIFTY (lot 30, capital re-set to ₹42,000 = 2 ATM + 8 OTM lots): ATM +24k/−19.2k/+117k vs OTM −20.4k/−31.2k/+234k. IV = implied volatility. -->

# Chapter 16 — Directional Strategies: Trading the Move

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Master the four basic directional strategies — long call, long put, short call, short put.
2. Select the right strike and expiry for a directional trade.
3. Decide when to *buy* options versus *sell* them for a directional view.
4. Apply "paying for Theta" versus "earning Theta" in directional bets.
5. Avoid the classic retail trap of buying cheap out-of-the-money options.
6. Use single-leg options for *non-speculative* purposes — the protective put, the covered call, and the cash-secured put.

Welcome to Part V, the heart of the book. You have the instruments (Parts I–II), the Greeks (Part III), and the volatility toolkit (Part IV). Now you assemble them into *strategies* — starting with the simplest: expressing a directional view with a single option.

---

## 2. Introduction

Every trade in this part answers a question, and the directional strategies answer the most basic one: *"I think the market is going up (or down) — how do I express that with options?"* The naive answer — "buy a call if bullish, a put if bearish" — is only the beginning. The real skill is in the details that decide whether the trade wins: *which* strike, *which* expiry, and — the choice most beginners never even consider — whether to *buy* an option or *sell* one to express the same view.

Consider two traders, both correctly bullish on the NIFTY for a 1% rise. One buys the at-the-money call; the other buys a cheap 2%-out-of-the-money call, reasoning that it is "affordable" and offers more leverage. The market rises exactly 1%, as both predicted. The first trader makes money. The second loses everything — because the move never reached their strike. Same view, same outcome in the market, opposite results, decided entirely by strike selection.

This chapter turns "buy a call" into a disciplined craft. You will learn the four single-leg directional strategies and their opposite risk profiles; a framework for matching the strike to the size of the move you expect (the antidote to the OTM-lottery trap of Chapter 4); how to choose the expiry; and when a directional view is better *sold* than *bought*. Finally — the Edition 2 addition — you will see the same four legs used not to speculate but to *reduce risk and earn income*: the protective put, the covered call, and the cash-secured put. Each strategy is presented in a standard template (Setup → View → Risk/Reward → Greeks → Adjustment → Exit → Indian considerations) that we will use throughout Part V. Setting: **NIFTY at 24,600, lot 65**, with premiums and Greeks from the same basis as Part III.

---

## 3. Core Concepts

### 3.1 The four basic directional strategies

The four single-leg positions from Chapter 4 are the building blocks of everything. Here we treat them as *strategies* — when to use each, and with what risk. Table 16.1 is the standardised trade sheet, using ATM NIFTY options (24,600 CE at ₹212, 24,600 PE at ₹198, 10 DTE).

**Table 16.1 — The four basic directional strategies (ATM NIFTY, illustrative)**

| | **Long Call** | **Long Put** | **Short Call (naked)** | **Short Put (naked)** |
| --- | --- | --- | --- | --- |
| View | Bullish | Bearish | Bearish/neutral | Bullish/neutral |
| Action | Buy 24,600 CE @₹212 | Buy 24,600 PE @₹198 | Sell 24,600 CE @₹212 | Sell 24,600 PE @₹198 |
| Max profit | Unlimited | Large (to zero) | ₹212 (premium) | ₹198 (premium) |
| Max loss | ₹212 (premium) | ₹198 (premium) | **Unlimited** | Large (to zero) |
| Breakeven | 24,812 | 24,402 | 24,812 | 24,402 |
| Net Delta | +0.54 | −0.46 | −0.54 | +0.46 |
| Net Theta | −₹10.6/day | −₹10.6/day | +₹10.6/day | +₹10.6/day |
| Net Vega | +₹16.3 | +₹16.3 | −₹16.3 | −₹16.3 |
| Capital | ₹13,780 (premium) | ₹12,870 (premium) | ~₹1.25 lakh margin | ~₹1.25 lakh margin |

The flagship of the four is the **long call**, so we give it the full treatment; the others follow by symmetry.

**Long Call — the archetypal directional buy.**

* **What is it?** Buying a call to profit from a rise, with risk capped at the premium.
* **Why does it exist / why care?** It gives leveraged, defined-risk upside exposure: a small premium controls a large notional (Chapter 2), and the most you can lose is that premium — no margin calls, no open-ended risk. It is the cleanest way for a bull to bet with a known, limited downside.
* **Intuition.** You are paying for the *right* to the upside, funded by accepting time decay (Theta) as the cost. You have "the right to be wrong": if the market falls, you lose only the premium and walk away.
* **Greeks profile.** Long Delta (profits as the index rises), long Vega (helped by rising IV), and — the cost — negative Theta (bleeds daily). You are *paying* Theta for the optionality and the long Vega.
* **Risk/reward.** Max loss = premium (₹212, or ₹13,780/lot); max profit unlimited; breakeven = strike + premium = 24,812. Risk-reward is asymmetric in your favour on the *magnitude* (unlimited up, limited down) but against you on *probability* (you must clear the premium to profit — Section 3.4).
* **Best when.** You expect a decisive up-move *soon* (to outrun Theta) and IV is *low* (cheap to buy, and room for IV to rise).
* **Adjustment.** If the move stalls, there is little to adjust on a single long option — you exit. Some traders roll up (take profit, buy a higher strike) after a strong move to lock gains and reduce risk.
* **Exit.** Pre-set a target (e.g., premium doubles, or the index hits your objective) and a stop (premium halves, or the index breaks your invalidation level). Because Theta bleeds daily, do not let a long call linger past your thesis's time horizon.
* **Indian considerations.** Prefer liquid NIFTY/BANKNIFTY strikes near the money (Chapter 2); weekly options decay fastest (Chapter 10), so a 5-day view needs a weekly with a little cushion, not a 1-day expiry.
* **Common mistake.** Buying a far-OTM call because it is cheap (Section 3.2, and the case study).
* **Takeaway.** **Buy calls when you expect a real move soon and IV is cheap — and size the strike to the move you actually expect, not to the premium you can afford.**

The **Long Put** is the exact mirror (bearish; profits as the index falls; same limited-loss, large-profit, long-Vega, negative-Theta profile). The **Short Call** and **Short Put** invert everything: the seller *collects* the premium (positive Theta) and is *short* Vega, but takes on the large or unlimited loss and must post ~₹1.25 lakh of margin per lot (Chapter 3). Sellers have "the obligation to be right quickly" — they profit from time and calm but are exposed to the move.

---

### 3.2 Strike selection — matching the strike to the move

The single most important decision in a directional option trade is the **strike**, and the governing principle is: **match the strike to the size of the move you expect.**

* **At-the-money (ATM):** balanced risk/reward. Delta ~0.5, so the option captures about half of each point immediately and rises toward full participation as the move develops. Best for a *moderate, confident* move.
* **Slightly in-the-money (ITM):** higher probability, higher cost. Delta ~0.6–0.7, more intrinsic value, less time value to lose. It behaves more like the future — good when you want a *high-probability* directional bet and are willing to pay for it.
* **Out-of-the-money (OTM):** cheap, leveraged, low probability. Delta ~0.2–0.3 (or less). It costs little and offers huge percentage gains — *but only if the move is large enough to reach and clear the strike*. Best reserved for when you expect a *big, fast* move; a poor choice for a modest one.

The trap, quantified in Section 5 and the case study, is buying OTM for a *modest* expected move: the move can be exactly right in direction and still leave the OTM option worthless because it never reached the strike.

**The Delta-to-premium ratio.** A useful strike-selection tool is Delta ÷ premium — the directional "bang per rupee":

```
Delta-to-premium ratio = Delta / Premium
```

A high ratio (OTM options) means lots of Delta per rupee — *leverage* — but low probability and fast decay. A low ratio (ITM options) means less Delta per rupee but high probability and slow decay. The ratio quantifies the leverage-versus-probability tradeoff: **high ratio = leveraged bet needing a big move; low ratio = conservative bet with high odds.** Match it to your conviction, not to your budget.

> **Beginner Alert — cheap does not mean good (again).** The single most repeated beginner error is choosing the strike by *what is affordable* rather than *what the move requires*. A ₹35 OTM call feels "cheaper" than a ₹212 ATM call — but if your expected move only reaches halfway to the OTM strike, the cheap option is a guaranteed loss and the "expensive" one a winner. Pick the strike your *forecast* justifies, then size the position to your risk limit — never the reverse.

---

### 3.3 Expiry selection

The expiry sets the clock on your trade, and the rule is: **match the expiry to your time horizon, with a cushion.**

* **Weekly expiries** suit short-term views (intraday to a few days). They are cheaper but decay fastest (Chapter 10) — a headwind for buyers, income for sellers. A 5-day view should use a weekly with ~5–7 days left, *not* a 1–2 day expiry where Theta and expiry Gamma (Chapter 9) are brutal.
* **Monthly expiries** suit swing views (one to four weeks). They cost more but decay slowly, giving your thesis room to play out without the time pressure of a weekly.

The core tension is Theta versus time: a shorter expiry is cheaper but bleeds faster; a longer expiry costs more but is patient. For a *buyer*, err toward giving yourself a little more time than you think you need (Theta punishes the impatient). For a *seller*, the sweet spot (~5–15 DTE, Chapter 10) balances rich decay against manageable Gamma.

---

### 3.4 Buyers versus sellers — the fundamental choice

The choice most beginners skip is *whether to buy or sell* to express a directional view. The two are profoundly different:

* **Buyers pay Theta, are long Vega, and have limited, known risk.** A call buyer has "the right to be wrong" — capped loss, unlimited upside — but must be right on *direction, magnitude, and timing*, because Theta charges rent daily and the move must clear the premium. Buyers **win rarely and big** (low probability of profit, large payoff when right).
* **Sellers earn Theta, are short Vega, and have large or unlimited risk.** A put seller (bullish) has "the obligation to be right quickly" — they profit from time and calm even if the market goes nowhere, but a wrong move hurts far more than the premium collected. Sellers **win often and small** (high probability of profit, large loss when wrong), and must post heavy margin.

**Probability of profit.** For a buyer, the probability of profit is *lower* than the option's Delta, because you must not only finish ITM but clear the premium — an ATM long call has maybe a ~40% chance of profit at expiry. For a seller, the probability of profit is *high* (an OTM put seller may win ~70–80% of the time) — but the rare loss is large. This asymmetry, not the direction call, is often what decides whether buying or selling is the right expression.

**The IV lens.** The IV regime (Chapters 13–14) tilts the choice: **buy in low IV** (options cheap, and you are long Vega if IV rises); **sell in high IV** (options rich, and you are short Vega as IV mean-reverts down). A bullish view in cheap IV → buy a call; the same bullish view in rich IV → sell a put (collect the fat premium) or use a spread (Chapter 17).

> **Professional Insight — the direction is the easy part.** Amateurs agonise over "up or down" and ignore the three decisions that actually determine the P&L: strike (matched to the move), expiry (matched to the horizon), and buy-vs-sell (matched to the IV regime and the probability profile you want). A professional with a mediocre directional call but the right strike, expiry, and structure routinely beats an amateur with a brilliant call expressed through a cheap OTM weekly. Get the *expression* right, and a modest edge in direction becomes a profitable trade.

---

### 3.5 Stop-losses and targets for directional trades

A directional option trade needs pre-defined exits, set *before* entry:

* **Stop-loss.** Because a long option can lose 100% of its premium, protect it with a stop — either **premium-based** (exit if the premium falls, say, 40–50%) or **underlying-based** (exit if the index breaks your invalidation level). Underlying-based stops are usually better: they tie the exit to your *thesis* being wrong, not to normal premium noise.
* **Target.** Pre-set where you take profit — the index reaching your objective, or the premium hitting a multiple. Because Theta accelerates near expiry and Gamma makes gains volatile, take profits mechanically rather than hoping for more.
* **Time stop.** A long option has a *deadline*. If your thesis has not played out by a set date, exit — do not let Theta grind the premium to nothing while you wait for a move that may never come ("right on direction, wrong on timing," Chapter 10).

The seller's stops differ: because losses can be large, a seller must have a hard stop (underlying-based or premium-multiple) and the discipline to take it — the "one big loss" (Chapters 10, 12) is what a seller's stop exists to prevent.

---

### 3.6 Single-leg options as hedges and overlays

The same four legs, used with a *different intent* — to reduce risk or earn income rather than speculate — become three of the most useful tools in a serious trader's kit. This is the Edition 2 addition, and the bridge to portfolio hedging later in the book.

**Protective put — insurance.** If you hold a long position (a long index future, an index ETF, or a beta-equivalent equity portfolio), buying a put *insures* it: below the put's strike, the put gains offset the holding's losses. It is exactly the insurance model of Chapter 4, applied deliberately.

* *Cost of insurance:* the premium, expressible as an annualised drag on the portfolio (e.g., a monthly put costing 1% is ~12% a year if bought continuously).
* *Strike selection (the "deductible"):* a higher strike (closer to spot) gives more protection but costs more; a lower strike is cheaper but you "self-insure" the first part of a fall. Choosing the strike is choosing your deductible.
* *Rolling:* as the put nears expiry or the market moves, you roll it (close and re-open at a new strike/expiry) to maintain the hedge.

**Covered call / call-overwriting — income.** If you hold a long exposure, selling a call against it earns premium income in exchange for capping your upside at the strike. The premium cushions small declines and adds income in flat-to-mildly-up markets; the cost is that you forgo gains above the strike.

* *"Covered" for index products:* an index cannot be held in cash form, so the call is "covered" by a **long index future, an index ETF, or a beta-equivalent portfolio** — not by the cash index itself. This is a crucial distinction from stock covered calls.
* *Use:* a standard income overlay for investors who are neutral-to-mildly-bullish and willing to sell their upside above a level for regular premium ("call overwriting").

**Cash-secured put — disciplined income / acquisition.** Selling a put while *reserving the full notional cash* to settle it reframes the "naked short put" as a fully-funded position. If the market stays up, you keep the premium (income); if it falls to the strike, you are effectively "put into" long exposure at the strike — a level you were willing to buy anyway. The key is that it is *cash-secured*: you are not leveraged, so the position is a disciplined income/acquisition tool, not a gamble.

**The mental shift.** These are the *same* four legs from Table 16.1 — but viewed through a *risk-reduction and income* lens rather than a *speculation* lens. A long put is a bearish bet *or* portfolio insurance; a short call is a bearish bet *or* an income overlay. The leg is identical; the *intent and context* make it speculation or risk management. Full portfolio-level hedging — beta-weighted hedge ratios, collars, and overlay sizing — is developed in the risk-management part of the book; here you have the single-leg building blocks.

---

## 4. Examples (Real-World)

**Example 1 — The strike that mattered.** Two bulls, both right about a 1% NIFTY rise. The ATM-call buyer profits; the 2%-OTM-call buyer loses everything because the move never reached their strike (Numerical Example 2). The direction was identical; the strike decided the outcome.

**Example 2 — Buy or sell the same view.** A trader is bullish on NIFTY in a *high*-IV environment. Rather than buy a call (expensive, long Vega into a likely IV crush), they *sell* an OTM put — collecting rich premium, earning Theta, and profiting if the market rises *or* stays flat. Same bullish view, expressed as a seller because the IV regime favoured it.

**Example 3 — The overlay on a portfolio.** An investor holding a NIFTY-tracking portfolio sells a monthly OTM call against it (call overwriting), collecting ~1% a month in premium in a flat-to-mildly-up market — accepting that a sharp rally above the strike would cap their gains. The same short call that would be a speculative bearish bet is here a disciplined income overlay.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, 10 DTE, lot 65; premiums/Greeks from the Part III basis.

### Numerical Example 1 — Long call P&L, at and before expiry

Buy the 24,600 CE at ₹212 (Δ0.54, Θ−10.6, ν+16.3).

* **At expiry**, if NIFTY = 24,900: intrinsic 300, P&L = (300 − 212) × 65 = **+₹5,720**. If NIFTY ≤ 24,600: lose the full 212 × 65 = **−₹13,780**.
* **Before expiry** (3 days pass, NIFTY +150 to 24,750, IV +1 point), using ΔP ≈ Δ·ΔS + Θ·Δt + ν·Δσ:

```
ΔP ≈ 0.54×150 + (−10.6×3) + 16.3×1 = 81 − 31.8 + 16.3 = +₹65.5/unit
```

The call rises from ₹212 to ~₹277 — the Delta gain (₹81) outweighing the Theta bleed (−₹32), helped by the small Vega gain (+₹16). This is the buyer's daily tug-of-war (Chapter 12) in a single position.

### Numerical Example 2 — ATM vs 2% OTM for a 1% expected move

NIFTY 24,600; you expect a 1% rise to ~24,846. Compare an ATM 24,600 CE (₹212) with a 2%-OTM 25,100 CE (₹35), each held to expiry:

```
At 24,846:
ATM 24,600 CE: intrinsic 246 → P&L = (246 − 212) = +₹34/unit  (barely profitable)
2% OTM 25,100 CE: intrinsic 0 (24,846 < 25,100) → P&L = −₹35/unit (total loss)
```

The 2%-OTM call needs the index above its breakeven of **25,135** (+2.2%) just to profit — more than double the move you forecast. **A correct 1% call loses everything if expressed through the 2% OTM strike.** For a modest move, the ATM (or slightly ITM) strike is right; the OTM strike only pays on a big move.

### Numerical Example 3 — Delta-to-premium ratio across strikes

```
ATM 24,600 CE:  0.54 / 212 = 0.00255
2% OTM 25,100 CE: 0.20 / 35 = 0.00571  (highest — most Delta per rupee = most leverage)
Deep ITM 24,000 CE: 0.89 / 640 = 0.00139 (lowest — least leverage, highest probability)
```

The OTM call offers the most directional exposure per rupee (leverage) but the lowest probability; the deep-ITM offers the least leverage but the highest probability. The ratio makes the leverage-versus-probability tradeoff explicit — choose by conviction, not by price.

### Numerical Example 4 — Buy a call vs sell a put (same bullish view)

Bullish on NIFTY; compare buying the ATM call with selling the ATM put:

```
Buy 24,600 CE @₹212: capital ₹13,780/lot. If NIFTY → 24,900 at expiry, call = 300 → profit (300−212)×65 = +₹5,720. ROI on capital = 5,720/13,780 ≈ 42%. Max loss = ₹13,780 (100%).
Sell 24,600 PE @₹198: margin ~₹1,25,000/lot. If NIFTY → 24,900 (or any level ≥ 24,600), put expires worthless → keep 198×65 = +₹12,870. ROI on margin = 12,870/1,25,000 ≈ 10%. Loss if NIFTY falls: large.
```

The **call buyer** deploys little capital (₹13,780), earns a high ROI *if* the move comes, but can lose 100%. The **put seller** ties up ₹1.25 lakh, earns a lower ROI on capital, but profits on a rise *or* a flat market — winning more often, losing big only on a fall. Same view; opposite risk/capital profiles. (The put seller's *return on the small premium* looks large, but the honest denominator is the margin blocked.)

### Numerical Example 5 — Protective put as insurance

You hold a NIFTY-equivalent long worth ₹15,99,000 (one lot notional at 24,600). Buy a 24,000 PE at ₹90 as insurance (₹5,850/lot, ~0.37% of the holding):

```
If NIFTY falls to 23,400 by expiry: holding loses (24,600−23,400)×65 = −₹78,000
Put payoff: (24,000−23,400)×65 = +₹39,000; net put gain = 39,000 − 5,850 = +₹33,150
Net loss ≈ −78,000 + 33,150 = −₹44,850 (vs −₹78,000 unhedged)
```

The put capped the damage: below 24,000 (the "deductible"), the holding is insured. The first 600 points of loss (24,600 → 24,000) are self-insured; beyond that, the put pays. The ₹5,850 premium was the insurance cost.

---

## 6. Calculations (the reusable recipes)

**(a) P&L at expiry (single legs — review from Chapter 4)**

```
Long Call = max(0, Spot − Strike) − Premium;   Long Put = max(0, Strike − Spot) − Premium
Short Call = Premium − max(0, Spot − Strike);   Short Put = Premium − max(0, Strike − Spot)
```

**(b) Before-expiry P&L (using Greeks)**

```
ΔP ≈ Δ·ΔS + Θ·Δt + ν·Δσ      (per unit; × lot size for rupees)
```

**(c) Breakeven and risk-reward**

```
Call breakeven = Strike + Premium;  Put breakeven = Strike − Premium
Risk-reward ratio = Max Profit / Max Loss
```

**(d) Strike selection: Delta-to-premium ratio**

```
Delta-to-premium = Delta / Premium   (high = leveraged/low-probability; low = conservative/high-probability)
```

**(e) Probability of profit (rough)**

```
Buyer POP ≈ probability of finishing beyond breakeven (< option's Delta — must clear the premium)
Seller POP ≈ 1 − |Delta of the short strike| (higher, but with a large tail loss)
```

---

## 7. Practical Insights

* **The direction is the easy part.** Strike, expiry, and buy-vs-sell decide the P&L. Get the *expression* right and a modest directional edge becomes profitable.
* **Match the strike to the move, not to your budget.** ATM/slightly-ITM for moderate moves; OTM only when you expect a big, fast move. Cheap OTM options are lottery tickets for modest views.
* **Let the IV regime pick buy vs sell.** Buy in cheap IV (long Vega, low cost); sell in rich IV (collect premium, short Vega into mean reversion). The same view can be a call buy or a put sell depending on IV.
* **Give buyers time and set a time stop.** Theta punishes the impatient; a 5-day view needs more than a 1-day expiry, and a long option that has not worked by its deadline should be closed.
* **Reuse the four legs as risk tools.** A protective put insures a holding, a covered call earns income, a cash-secured put is disciplined acquisition — the same legs, a different intent.

> **Professional Insight — "sell the view" more often than you think.** Retail traders reflexively *buy* options to express a view, and so pay Theta and fight low odds. Professionals frequently *sell* to express the same view — a bull sells puts, a bear sells calls — collecting Theta and winning on the high-probability side, especially when IV is rich. Buying is correct when IV is cheap and you expect a fast, large move; selling is correct far more often than beginners realise. Ask, every time: "Is this view better bought or sold?"

---

## 8. Common Mistakes

* **Buying cheap OTM options for a modest move.** The direction can be exactly right and the option still expire worthless because the move never reached the strike (Numerical Example 2, and the case study).
* **Choosing the strike by affordability.** Picking a strike because it is cheap rather than because the expected move justifies it — the OTM-lottery trap.
* **Ignoring the buy-vs-sell choice.** Reflexively buying options and paying Theta when the view (and the IV regime) would have been better sold.
* **Buying too-short an expiry.** Expressing a multi-day view through a 1–2 day option, where Theta and expiry Gamma destroy it.
* **No time stop.** Letting a long option bleed to zero waiting for a move that comes too late — "right on direction, wrong on timing."
* **Selling naked without respecting the risk.** Treating a naked short option's premium as easy income while ignoring the large/unlimited loss and the ₹1.25 lakh margin (Chapters 3, 10, 12).

---

## 9. Case Study — "The OTM Buyer vs. The ATM Buyer"

**Context.** Two traders hold the *same* bullish view on BANKNIFTY, at 52,000, with the same capital of ₹42,000 and a 5-day horizon (lot size 30; figures illustrative). They differ only in strike choice:

* **The ATM buyer** buys the **52,000 CE at ₹700** → 2 lots (₹42,000).
* **The OTM buyer** buys the **3%-OTM 53,500 CE at ₹175** → 8 lots (₹42,000), reasoning that the cheaper option gives more lots and more leverage.

We track both through three outcomes over five days.

**Table 16.2 — ATM vs 3%-OTM BANKNIFTY call buyer, same ₹42,000 capital (illustrative)**

| Outcome (5 days) | ATM 52,000 CE (2 lots) | OTM 53,500 CE (8 lots) |
| --- | ---: | ---: |
| **Moderate up-move** (+2% to 53,040) | premium ~₹1,100 → **+₹24,000** | still OTM, ~₹90 → **−₹20,400** |
| **Flat** (unchanged at 52,000) | decays to ~₹380 → **−₹19,200** | decays to ~₹45 → **−₹31,200** |
| **Big up-move** (+5% to 54,600) | ~₹2,650 → **+₹117,000** | ~₹1,150 → **+₹234,000** |

**The analysis.**

* **On the moderate move (the most likely "I was right" scenario), the ATM buyer wins big (+₹24,000) and the OTM buyer *loses* (−₹20,400)** — even though both were correct that BANKNIFTY would rise. The +2% move (to 53,040) never reached the OTM strike (53,500), so the OTM calls decayed toward worthless while the ATM calls captured the move. This is the OTM trap in its purest form: *right on direction, wrong on strike.*
* **On the flat market, both lose — but the OTM buyer loses more** (−₹31,200 vs −₹19,200). The OTM option's entire premium is time value, which decays fastest in percentage terms (Chapter 10), so the leveraged OTM position bleeds harder when nothing happens.
* **Only on the big move does the OTM buyer's leverage pay** — and then spectacularly (+₹234,000 vs +₹117,000), because 8 lots of a now-ITM cheap call outrun 2 lots of the ATM. This is the OTM's *raison d'être*: it is a bet on a *large, fast* move, not a modest one.

**The lesson.** The OTM buyer's leverage cuts both ways. It wins only when the move is *big enough to clear the strike*, and it loses more than the ATM buyer on moderate or flat outcomes. Since moderate and flat outcomes are far more common than big fast moves, the ATM (or slightly-ITM) strike is the higher-expectancy choice for most directional views. Buy OTM *only* when you have a specific, high-conviction reason to expect a large, rapid move — and even then, size it as the lottery ticket it is. "More lots for the same money" is not an edge; it is leverage that demands a bigger move to justify itself.

*(Takeaway: match the strike to the size of the move you expect — cheap OTM options need a big, fast move just to break even, and being right on direction is worthless if the move never reaches your strike.)*

---

## 10. Chapter Summary

* The **four basic directional strategies** are long call / long put (buyers: limited loss, unlimited/large profit, pay Theta, long Vega) and short call / short put (sellers: limited profit, large/unlimited loss, earn Theta, short Vega, heavy margin).
* **Strike selection matches the strike to the expected move:** ATM (moderate move, balanced), slightly ITM (high probability), OTM (big move only — cheap, leveraged, low probability); the **Delta-to-premium ratio** quantifies the leverage-vs-probability tradeoff.
* **Expiry matches the horizon with a cushion:** weekly for short-term (fast decay), monthly for swings (patient) — buyers should not use too-short expiries.
* **Buy vs sell is the choice beginners skip:** buyers have the "right to be wrong" (limited loss, low probability, win rarely and big); sellers have the "obligation to be right quickly" (large loss, high probability, win often and small). The **IV regime tilts it** — buy cheap IV, sell rich IV.
* **Set stop-losses, targets, and a time stop before entry** — long options can go to zero, and Theta punishes waiting.
* **The same four legs are risk tools:** the **protective put** (insurance, choose your deductible), the **covered call / overwriting** (income, covered by a future/portfolio for index products), and the **cash-secured put** (fully-funded, disciplined income/acquisition).
* The **OTM-vs-ATM case** shows the OTM buyer loses on moderate and flat moves and wins only on big fast moves — match the strike to the move.

---

## 11. Key Takeaways

* **Get the expression right, not just the direction** — strike, expiry, and buy-vs-sell decide the P&L more than the up/down call.
* **Match the strike to the move you expect** — ATM/ITM for moderate, OTM only for big fast moves; never pick a strike by affordability.
* **Let IV choose buy vs sell** — buy cheap IV (long Vega), sell rich IV (earn Theta), and remember sellers win more often than buyers.
* **Reuse the legs defensively** — protective puts insure, covered calls earn income, cash-secured puts acquire on discipline — the same tools that speculate can also protect.

---

## 12. Practice Questions

**Q1 (Strategies).** For each of the four basic directional strategies, state the market view and the maximum loss.

**Q2 (Strike).** You expect a 0.8% NIFTY rise from 24,600 over three days. Would you choose an ATM, a slightly-ITM, or a 2%-OTM call, and why?

**Q3 (Delta-to-premium).** Option A: Delta 0.50, premium ₹200. Option B: Delta 0.25, premium ₹40. Compute each Delta-to-premium ratio and state which is more leveraged.

**Q4 (Before-expiry P&L).** A long call has Δ0.50, Θ−12, ν+15. Over 2 days NIFTY rises 120 points and IV falls 2 points. Estimate the per-unit P&L.

**Q5 (Buy vs sell).** You are bullish on NIFTY and IV is *high* (rich). Which is generally the better expression — buying a call or selling a put — and why?

**Q6 (Breakeven).** You buy a 2%-OTM 25,100 CE at ₹35 (NIFTY 24,600). What index level do you need at expiry to break even, and what percentage move is that?

**Q7 (Probability).** Why does a long ATM call have a *lower* probability of profit than its Delta of ~0.5 suggests?

**Q8 (Protective put).** You hold a NIFTY-equivalent long at 24,600 and buy a 24,000 put at ₹90. How far can the market fall before your hedge starts paying, and what is that first stretch called?

**Q9 (Covered call).** In what sense is a covered call "covered" when the underlying is a cash-settled index, and what do you give up by selling it?

**Q10 (Judgement).** A trader with ₹50,000 and a mildly bullish 5-day view buys far-OTM weekly calls "for the leverage." Explain why this is likely a poor choice.

---

## 13. Detailed Solutions

**A1.** Long call — **bullish**, max loss = premium paid. Long put — **bearish**, max loss = premium paid. Short (naked) call — **bearish/neutral**, max loss = **unlimited**. Short (naked) put — **bullish/neutral**, max loss = large (down to the strike, if the index fell to zero).

**A2.** A **slightly-ITM or ATM** call. A 0.8% move (to ~24,797) is *modest*, so an ATM or slightly-ITM call (higher Delta, captures the move, breaks even close to spot) will profit, whereas a 2%-OTM call (strike ~25,100, breakeven ~25,135) would need a far larger move and would likely expire worthless despite the correct direction.

**A3.** A: 0.50/200 = **0.0025**. B: 0.25/40 = **0.00625**. **Option B is more leveraged** (more Delta per rupee) — but with lower probability and faster decay.

**A4.** ΔP ≈ Δ·ΔS + Θ·Δt + ν·Δσ = 0.50×120 + (−12×2) + 15×(−2) = 60 − 24 − 30 = **+₹6/unit** — the Delta gain (₹60) was nearly eaten by Theta (−₹24) and a Vega loss (−₹30), leaving only ₹6 despite a correct 120-point move. A lesson in how Theta and a falling IV can erase a good directional call.

**A5.** Generally **selling a put** is the better expression. In high (rich) IV, options are expensive and IV is likely to mean-revert *down*; buying a call means paying rich premium and being long Vega into a probable IV crush, while selling a put collects the rich premium, earns Theta, is short Vega (benefiting from the IV fall), and profits if the market rises *or* stays flat. (Buying would be preferred only if IV were cheap and a large fast move expected.)

**A6.** Breakeven = strike + premium = 25,100 + 35 = **25,135**. From 24,600 that is (25,135 − 24,600)/24,600 ≈ **+2.2%** — more than double a 1% move, illustrating why OTM calls need large moves.

**A7.** Because to profit, a buyer must not only finish in the money (roughly the Delta probability, ~50% for an ATM) but also finish *beyond the breakeven* (strike + premium) — i.e., recover the premium paid. Clearing the extra premium lowers the probability of profit below the ~0.5 Delta, to roughly 40% for an ATM long call.

**A8.** The hedge starts paying below the put's strike of **24,000** — so the market can fall the first 600 points (24,600 → 24,000) before the put engages. That first, self-insured stretch is the **"deductible"** (you bear it; the put covers losses beyond it).

**A9.** For a cash-settled index, the call is "covered" not by the cash index (which cannot be held) but by an offsetting **long position** — a long index future, an index ETF, or a beta-equivalent portfolio — whose gains above the strike offset the short call's losses. By selling it you **give up all upside above the strike** in exchange for the premium income.

**A10.** A mildly bullish 5-day view implies a *modest* move, but far-OTM calls only profit on a *large, fast* move that clears the strike — so a correct-but-modest rise will likely leave them worthless (right on direction, wrong on strike). They also decay fastest as a percentage (all time value) and, being weekly, bleed Theta rapidly over the 5 days. The "leverage" is a bet on a big move the trader does not actually expect; an ATM or slightly-ITM call (or, if IV is rich, selling a put) would express the modest bullish view far better.

---

## 14. Mini Glossary

* **Long call / long put** — buying a call (bullish) or put (bearish); limited loss (premium), large/unlimited profit, pays Theta, long Vega. → this chapter.
* **Short (naked) call / put** — selling a call (bearish/neutral) or put (bullish/neutral); limited profit (premium), large/unlimited loss, earns Theta, short Vega, heavy margin. → this chapter.
* **Strike selection** — matching the strike (ATM / ITM / OTM) to the expected size of the move. → this chapter.
* **Delta-to-premium ratio** — Delta ÷ premium; measures directional leverage per rupee (high = leveraged/low-probability). → this chapter.
* **Right to be wrong** — the buyer's limited, known loss (the premium). → this chapter.
* **Obligation to be right quickly** — the seller's exposure to large loss if the move goes against them. → this chapter.
* **Probability of profit (POP)** — the chance a trade finishes profitable; lower than Delta for buyers, higher for sellers (with a large tail loss). → this chapter.
* **Time stop** — exiting a long option by a set date if the thesis has not played out, to avoid Theta bleed. → this chapter.
* **Protective put** — buying a put to insure a long position/portfolio; the strike sets the "deductible." → this chapter.
* **Covered call / call-overwriting** — selling a call against a long exposure for income, capping upside; "covered" by a future/ETF/portfolio for index products. → this chapter.
* **Cash-secured put** — selling a put while reserving the full notional cash; disciplined, unleveraged income/acquisition. → this chapter.

---

<!-- End of Chapter 16 (Rev 2, opens Part V, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65, BANKNIFTY lot 35→30 (NSE Jan-2026); naked margin ~₹1.45→~₹1.25 lakh (Ch3 lot-65). Lot-scaled figures recomputed: Table 16.1 capital 13,780/12,870, margin 1.25 lakh; long-call max loss ₹13,780/lot; NE1 +₹5,720/−₹13,780; NE4 capital ₹13,780 (ROI ~42%), put margin ₹1.25 lakh keep ₹12,870 (ROI ~10%); NE5 protective put on ₹15,99,000 notional, ₹5,850 premium, net loss −₹44,850 vs −₹78,000 unhedged. Per-unit figures unchanged: NumEx2 ATM +₹34 vs 2%OTM −₹35 on a 1% move (OTM BE 25,135); Delta-to-premium ATM 0.00255, 2%OTM 0.00571, deep-ITM 0.00139. Case study BANKNIFTY (lot 30, capital re-set to ₹42,000 = 2 ATM + 8 OTM lots): ATM +24k/−19.2k/+117k vs OTM −20.4k/−31.2k/+234k across moderate/flat/big. No transaction costs shown (gross P&L) → Apr-2026 STT change not applicable; expiry discussion generic (no weekday). Edition 2 overlays: protective put, covered call/overwriting, cash-secured put. IV = implied volatility. -->
