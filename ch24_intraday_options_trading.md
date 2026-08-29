<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 8, 10, 16, 22. Target length ~8,500 words. CLOSES Part VI. Intraday expected range = day's expected move × √(hours remaining/6.25) — CORRECTS the architecture's inverted "/√"; VIX 14 → day ±217, decaying 9:15 ±217 → 11:00 ±184 → 12:30 ±150 → 2:00 ±106 → 3:00 ±61. Cost per roundtrip ~₹62.5 (from Ch3, lot 65). 10 RT/day = ₹625/day = ₹1.56L/yr vs 2 RT = ₹31,250/yr. Min edge to cover = ₹62.5/65 ≈ ₹0.96/unit. Daily P&L = trades×[p×win − (1−p)×loss] − costs; 5 trades, 60%, win ₹1,500, loss ₹1,000 → +₹2,188/day. Case study 5-trade day: +₹1,507/lot net; 5th FOMO trade cost ₹1,038 (disciplined 4 = +₹2,545). Square off before 3:30 to avoid overnight gap. IV = implied volatility. Rev 2 (5 Aug 2026): lot 75→65, cost per RT ₹61→₹62.5 and min edge ₹0.81→₹0.96/unit per revised Ch3; case study and all NumEx/Q&A recomputed. -->

# Chapter 24 — Intraday Options Trading: Scalping and Day Trading

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Understand what makes intraday options trading a distinct discipline.
2. Apply intraday technical triggers (ORB, VWAP, pivots) for option entry and exit.
3. Manage the speed of premium decay within a single session.
4. Navigate the gap between the 3:30 PM close and the 9:15 AM open.
5. Recognise and avoid overtrading — the intraday trader's chief enemy.

This chapter closes Part VI. Intraday options trading is the most popular — and most punishing — way retail India trades options, dominated by two forces most traders underestimate: **transaction costs** (Chapter 3) and **overtrading**. It synthesises Delta (Chapter 8), Theta (Chapter 10), directional strategies (Chapter 16), and expiry dynamics (Chapter 22) into the compressed arena of a single trading day.

---

## 2. Introduction

Intraday options trading looks like the easiest way to make money and is, for most, the fastest way to lose it. The appeal is obvious: cheap weekly options, fast-moving premiums, a fresh start every morning, no overnight risk. The reality is that it is a game of small edges relentlessly eroded by two forces beginners barely see — the **transaction costs** that skim every round trip and the **overtrading** compulsion that multiplies those costs while forcing marginal trades. SEBI's data (Chapter 1) shows the great majority of individual F&O traders lose money, and intraday trading is where they lose it fastest, precisely because they take the most trades.

This chapter treats intraday trading as the demanding discipline it is. An intraday trader is not a shrunk-down positional trader; they play a *different game*, where a single point of the bid-ask spread and a single extra "FOMO" trade decide the day. The winning intraday trader is defined less by their entry signals — ORB, VWAP, pivots, all useful — than by their *cost awareness* and *trade discipline*: taking few, high-quality trades; sizing each to a strict risk limit; stopping after a daily loss; and never letting the compulsion to "make it back" spawn the undisciplined trade that turns a good day into a bad one.

We cover the session's rhythm, the technical triggers, intraday selling and scalping, the shrinking intraday expected range, the cost arithmetic that sets the *minimum edge* a scalper needs, the overtrading trap, and intraday sizing. It closes with a realistic day in the life — five trades, the disciplined four that made money and the fifth that gave much of it back — the honest portrait of what intraday profitability requires. Setting: **NIFTY at 24,600, lot 65**, with costs carried from Chapter 3.

---

## 3. Core Concepts

### 3.1 Intraday versus positional — a different game

The flagship idea of this chapter is that intraday options trading is a *distinct discipline*, not a faster version of positional trading.

**What is it?** Intraday options trading means opening and closing option positions *within a single session* — from a few minutes to a few hours — squaring off before the 3:30 PM close. It relies on short-term price triggers, tight risk control, and speed of execution.

**Why is it different?** Because the forces that dominate change entirely at the intraday timescale:

* **Costs dominate.** A positional trader crosses the spread and pays costs a handful of times a month; an intraday scalper does so many times a *day*, so transaction costs (Chapter 3) become the single largest determinant of P&L (Section 3.6).
* **Theta and direction compress.** A move that plays out over days for a positional trader must happen in *hours* intraday; there is no time to be patient, and a stalled trade bleeds cost and opportunity immediately.
* **Discipline is the edge.** With dozens of trades a day, the difference between profit and loss is rarely the strategy — it is whether the trader takes only high-quality setups, sizes consistently, and avoids overtrading (Section 3.7).

**Why should a trader care?** Because a trader who brings positional habits — patience, wide stops, "it'll come back" — to intraday trading is destroyed by the cost and speed. Intraday demands its own skillset: fast execution, ruthless cost awareness, and iron discipline over the *number* of trades.

**Intuitive explanation.** Positional trading is a chess game — you have time to think between moves. Intraday scalping is a boxing match — reactions, conditioning, and not throwing wild punches (overtrading) decide it. The same person can be good at one and terrible at the other.

**Numerical feel.** At ~₹62.5 per round trip (Chapter 3), a trader doing 10 round trips a day pays **₹625/day — about ₹1.56 lakh a year** in costs alone (Section 3.6), before a single rupee of profit. Costs, not signals, are the intraday trader's first opponent.

**Professional interpretation.** Professional intraday traders obsess over execution cost and trade *selectivity* far more than over entry signals. They know a mediocre edge, traded cheaply and selectively, beats a great signal traded expensively and compulsively.

**Common mistake.** Treating intraday like positional — holding a losing scalp hoping it recovers, or trading a hundred times a day chasing every wiggle. Both ignore that intraday is a game of costs and discipline.

**Practical takeaway.** **Intraday options trading is a distinct discipline dominated by transaction costs and trade discipline, not by entry signals — win it by trading few high-quality setups cheaply, not many mediocre ones expensively.**

---

### 3.2 Session dynamics — the rhythm of the day

The Indian trading day (9:15 AM – 3:30 PM IST) has three distinct phases, each with its own character:

* **The opening 30 minutes (9:15–9:45).** High volatility, *wide bid-ask spreads*, and gap digestion as the market absorbs overnight news. The opening range forms here (Section 3.3), and the day's trend often begins — but market orders are dangerous (wide spreads, Chapter 3), and false moves are common. A time to *read*, not to trade recklessly.
* **Mid-session (roughly 10:00 AM – 2:00 PM).** Spreads tighten, trends establish and persist, and technical tools (VWAP, pivots) work best. This is the core *trading* window — the calmest, most tradable part of the day.
* **The closing 30 minutes (3:00–3:30).** Position squaring accelerates, volatility can pick up, and intraday (MIS) positions face auto-square-off. A time to *exit*, not to initiate — late-day trades are often FOMO trades (Section 3.7).

Understanding the rhythm shapes when to act: read the open, trade the middle, exit into the close. Fighting the rhythm — initiating in the volatile open with market orders, or opening new positions in the squaring close — is where intraday traders self-harm.

---

### 3.3 Intraday directional trades and technical triggers

Most intraday option trades are *directional* — buying an ATM or slightly-OTM option for a 30-minute to 2-hour move (high Delta to capture the move, accepting the Theta cost over the short hold). The triggers that time these entries:

* **Opening Range Breakout (ORB).** The high and low of the first 15–30 minutes form the "opening range." A break *above* the range signals intraday bullishness (buy a call); a break *below* signals bearishness (buy a put). ORB captures the day's trend as it establishes after the open.
* **VWAP (Volume Weighted Average Price).** The average price weighted by volume — the day's "fair value." Price *above* VWAP is intraday-bullish, *below* is bearish; VWAP acts as intraday support/resistance and a trend filter (trade long above it, short below). A common exit target for an ORB trade is a move to (or from) VWAP.
* **Support/resistance from OI.** The high open-interest strikes (Chapter 7) mark intraday support (heavy put OI) and resistance (heavy call OI) — levels where intraday moves often stall or reverse.
* **Pivots and CPR (Central Pivot Range).** Classical pivot points and the Central Pivot Range (a band around the pivot) mark intraday levels; a wide CPR suggests a range day, a narrow CPR a trending day — a directional filter for the session.

These tools *time* entries and exits, but — the recurring theme — they are not the edge. An intraday trader with good triggers but poor cost discipline loses; one with mediocre triggers but ruthless cost and trade discipline can win. The triggers are the *when*; discipline and cost control are the *whether-you-survive*.

---

### 3.4 Intraday selling and scalping the spread

Beyond directional buying, two other intraday approaches:

**Intraday selling.** Selling OTM options at the open (with a protective stop) to harvest the day's Theta — especially rich near a weekly expiry (Chapter 22). Sell a far-OTM call, and if the market does not rally, the option decays through the session; a stop-loss caps the risk if it does. It is a short-vol, positive-Theta intraday play, hostage to the same expiry-day Gamma dangers of Chapter 22 near expiry, so it demands a hard stop.

**Scalping the bid-ask spread.** The fastest intraday game — capturing tiny moves for small, frequent profits. It is *only* viable in **ATM strikes with tight spreads** (Chapter 3); in OTM strikes the wide spread makes scalping a guaranteed loss. Scalping requires **speed** (quick execution) and, above all, extreme cost discipline, because at high frequency the costs are enormous (Section 3.6). The speed-versus-accuracy trade-off is real: a scalper values fast, cheap execution over perfect entries, because the edge per trade is tiny and must be captured before it evaporates.

> **Beginner Alert — scalping OTM options is a guaranteed loss.** The seductive "cheap" OTM option has a *wide* bid-ask spread (Chapter 3) — you might buy at ₹42 (ask) and can only sell at ₹40 (bid), losing ~5% instantly on the spread alone, before any move. Scalping is *only* possible in liquid ATM strikes where the spread is a few paise. Trying to scalp cheap OTM options means the spread eats you alive on every trade.

---

### 3.5 The intraday expected range — how much move is left

A useful intraday tool is the **remaining expected range** — how far the index is likely to move for the *rest* of the day. Because volatility scales with the square root of time (Chapters 5, 10), the remaining expected move shrinks through the day:

```
Remaining expected move ≈ Day's expected move × √(hours remaining / total hours)
```

*(Note: the remaining move scales with √time-remaining — it shrinks as the day progresses. The day's expected move itself comes from India VIX or the ATM straddle, Chapter 13.)*

**Worked example.** With India VIX at 14, the day's expected NIFTY range ≈ 24,600 × 0.14/√252 ≈ ±217 points (Chapter 13). Over a 6.25-hour session, the remaining expected move decays as in Table 24.1.

**Table 24.1 — Remaining intraday expected move (VIX 14, day range ±217)**

| Time | Hours remaining | √(remaining/6.25) | Remaining expected move (±) |
| --- | ---: | ---: | ---: |
| 9:15 AM | 6.25 | 1.00 | ±217 |
| 11:00 AM | 4.50 | 0.85 | ±184 |
| 12:30 PM | 3.00 | 0.69 | ±150 |
| 2:00 PM | 1.50 | 0.49 | ±106 |
| 3:00 PM | 0.50 | 0.28 | ±61 |

The practical use: it tells you **how much move is left to trade.** If the index has already moved ±180 by noon, most of the day's expected range (±150 remaining) is used up — chasing a further breakout is fighting the shrinking range. Late-day directional trades (3:00 PM, ±61 remaining) have little room to work — a key reason late trades are usually poor (Section 3.7).

---

### 3.6 Transaction costs and the minimum edge

This is the arithmetic that governs intraday trading, and the reason most intraday traders lose. From Chapter 3, a NIFTY option round trip costs roughly **₹62.5** (brokerage, STT at the post-April-2026 0.15% sell rate, exchange charges, GST, stamp duty on a ~₹100 premium, lot 65). At intraday frequency, this compounds brutally:

**Table 24.2 — Annual transaction cost by intraday frequency (~₹62.5/round trip)**

| Round trips/day | Cost/day | Cost/year (~250 days) |
| ---: | ---: | ---: |
| 2 | ₹125 | ₹31,250 |
| 5 | ₹312.5 | ₹78,125 |
| 10 | ₹625 | ₹1,56,250 |

The 10-round-trip scalper pays **over ₹1.5 lakh a year in costs alone** — a hurdle their edge must clear before earning a rupee. This sets the **minimum edge** per trade:

```
Minimum edge per round trip = Cost per round trip ÷ Lot size = ₹62.5 ÷ 65 ≈ ₹0.96/unit
```

Every scalp must generate **more than ~₹0.96 of premium movement** just to break even — and a scalper aiming for a few rupees of premium hands a large fraction of every winning trade to costs. This is why **frequency is the enemy**: costs scale with the number of trades, not with skill, so the intraday trader's first job is to *minimise trades*, not maximise them.

> **Professional Insight — the intraday trader's first opponent is not the market, it is the cost.** Before any other trader can take a scalper's money, brokerage, STT, GST, the exchange, and the state each take a slice on *every* round trip — and the bid-ask spread takes more. A professional intraday trader treats cost minimisation (fewer trades, tighter spreads, ATM-only scalps, flat-fee broking) as the *primary* edge, because it is the one variable entirely within their control. The trader who obsesses over signals while ignoring costs is optimising the wrong thing.

---

### 3.7 Overtrading — the number-one P&L killer

**Overtrading** — taking more trades than your edge and discipline justify — is the single biggest destroyer of intraday P&L, for two compounding reasons:

* **It multiplies costs.** Every extra trade is another ₹62.5+ and another spread crossed (Section 3.6). Ten trades cost five times what two cost, for the same market.
* **It forces marginal trades.** The compulsion to trade — boredom, FOMO, revenge after a loss — spawns low-quality trades taken outside any real setup. These marginal trades have negative expectancy, and they cluster exactly when discipline is weakest (after a loss, near the close).

The antidote is *structural discipline*: a **fixed maximum number of trades per day**, taking only **A+ setups**, a **daily loss limit** that stops trading for the day when hit, and a **cooling-off rule** after a loss (Chapter 29 will treat the psychology). The case study (Section 9) shows the pattern precisely: a disciplined four trades made ₹2,545, and the undisciplined fifth (a FOMO trade near the close) gave back ₹1,038 — about 40% of the day's profit, from one avoidable trade.

---

### 3.8 Position sizing, risk per trade, and the overnight gap

**Intraday position sizing** is *smaller than positional* and *fixed per trade*. Because you take many trades, no single one should be large; a consistent, small size per trade lets the edge compound without one trade dominating.

**Risk per trade** is a strict, pre-set limit — a fixed rupee or percentage of trading capital. A common rule: risk **≤1% of daily trading capital per trade**. With ₹1 lakh of trading capital, that is ₹1,000/trade — the position is sized so its stop-loss caps the loss at ₹1,000, and the stop is honoured mechanically. This makes each trade survivable and prevents one bad scalp from wrecking the day.

**Navigating the overnight gap.** The defining choice: *square off before 3:30 PM* (true intraday, no overnight risk) or *carry overnight* (positional risk). Pure intraday traders **exit before the close** to avoid the 3:30 PM–9:15 AM gap (Chapter 23) — the un-hedgeable overnight move that can gap the index far from the close. A trader who lets an intraday position become an accidental overnight hold has taken on a risk (the gap) their intraday sizing and stops never accounted for. The discipline: an intraday trade is *closed intraday* — never "held overnight because it's slightly underwater."

> **Market Note — MIS auto-square-off is not a risk plan.** Brokers auto-square-off intraday (MIS) positions before the close (typically ~3:20 PM). Do not rely on this as your exit: it happens at whatever price the market offers, often in the volatile close, and it is not a substitute for your own timed exit at a chosen level. Manage your own exit; the auto-square-off is a backstop, not a plan.

---

## 4. Examples (Real-World)

**Example 1 — The ORB directional trade.** NIFTY's first 15 minutes range 24,550–24,620. At 9:45 it breaks *above* 24,620 (bullish ORB) — a trader buys the ATM 24,600 CE at ₹95, targeting a move to VWAP-plus. NIFTY rallies to 24,720 by 10:30; the call reaches ₹150; the trader exits for +₹55/unit (Section 5). A clean, disciplined intraday directional trade timed by the ORB.

**Example 2 — Intraday Theta harvest.** At 9:30, expecting a quiet day near a weekly expiry, a trader sells a far-OTM 24,900 CE at ₹40 with a stop. NIFTY drifts sideways; the option decays to ₹22 by 2:00 PM; the trader covers for +₹18/unit — the day's Theta harvested, with the stop protecting against a rally.

**Example 3 — The cost-eaten scalper.** A trader scalps ATM options 12 times in a morning, netting a few points of premium on each — but after ₹62.5 × 12 = ₹750 in costs and the spread on each, the "profitable" morning is flat. The signals worked; the costs ate the edge (Section 3.6). Frequency, not the market, was the enemy.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65; costs ~₹62.5/round trip (Chapter 3).

### Numerical Example 1 — The remaining intraday range

With India VIX at 14, the day's expected move ≈ 24,600 × 0.14/√252 ≈ **±217 points**. The remaining expected move at 2:00 PM (1.5 hours left of 6.25):

```
Remaining move = 217 × √(1.5/6.25) = 217 × 0.49 ≈ ±106 points
```

If NIFTY has already moved +190 by 2:00 PM, most of the day's range is spent — only ~±106 remains — so a fresh breakout trade at 2:00 has little room. The shrinking range tells you when the day's move is largely over.

### Numerical Example 2 — The cost hurdle

```
Cost per round trip ≈ ₹62.5 → minimum edge = 62.5 ÷ 65 ≈ ₹0.96/unit
10 round trips/day: 10 × 62.5 = ₹625/day → ~₹1,56,250/year
2 round trips/day: 2 × 62.5 = ₹125/day → ~₹31,250/year
```

The 10-round-trip scalper must generate over ₹0.96/unit of edge *per trade* and ₹1.56 lakh of gross edge *per year* just to cover costs. The 2-round-trip trader's hurdle is a fifth of that — the case for trading less.

### Numerical Example 3 — Daily P&L target

A trader plans 5 trades/day, a 60% win rate, average win ₹1,500/lot (gross), average loss ₹1,000/lot (gross), costs ₹62.5/round trip:

```
Gross EV = 5 × [0.60 × 1,500 − 0.40 × 1,000] = 5 × [900 − 400] = 5 × 500 = ₹2,500
Total costs = 5 × 62.5 = ₹312.5
Net daily P&L target = 2,500 − 312.5 = +₹2,187.5/day ≈ +₹2,188/day
```

The plan is viable *if* the trader actually achieves a 60% win rate and a 1.5:1 win/loss — and *if* they hold to 5 trades. Add five more marginal trades and the extra ₹312.5 of cost plus their negative expectancy erode the target.

### Numerical Example 4 — The ORB trade, costed

Buy the 24,600 CE at ₹95 on a 9:45 ORB breakout; sell at ₹150 at 10:30:

```
Gross P&L = (150 − 95) × 65 = 55 × 65 = ₹3,575
Net P&L = 3,575 − 62.5 (round-trip cost) = +₹3,512.5/lot ≈ +₹3,513/lot
```

A clean +₹3,513 on a disciplined, single directional trade — the kind of high-quality setup that makes an intraday day, versus the marginal trades that erode it.

### Numerical Example 5 — Minimum win rate to cover costs

A scalper with an average win of ₹500/lot and average loss of ₹500/lot (1:1) faces ₹62.5 cost per trade. The breakeven win rate rises because of the cost:

```
Break even: p × 500 − (1 − p) × 500 − 62.5 = 0 → 1,000p − 500 − 62.5 = 0 → p = 562.5/1,000 = 56.3%
```

Even a symmetric 1:1 scalp needs a **56.3%** win rate to break even after costs (versus 50% with no costs) — and higher still at greater frequency. Costs quietly raise the bar on every scalp.

---

## 6. Calculations (the reusable recipes)

**(a) Remaining intraday expected move**

```
Remaining move ≈ Day's expected move × √(hours remaining / total session hours)
   (day's expected move ≈ Index × VIX/100 ÷ √252, or the ATM straddle)
```

**(b) Transaction cost and minimum edge**

```
Cost per round trip ≈ ₹62.5 (per Ch3, ~₹100 premium, lot 65); Minimum edge = cost ÷ lot size ≈ ₹0.96/unit
Annual cost = round trips/day × cost × ~250 days
```

**(c) Daily P&L target**

```
Net daily P&L = Trades × [Win rate × Avg win − (1 − Win rate) × Avg loss] − Total costs
```

**(d) Risk per trade and position size**

```
Risk per trade ≤ 1% of daily trading capital; size the position so the stop-loss caps the loss at that limit
```

---

## 7. Practical Insights

* **Trade few, not many.** Costs scale with frequency, not skill; the single most reliable intraday improvement is *fewer, higher-quality* trades. Set a hard maximum per day.
* **Scalp only ATM, only when spreads are tight.** Wide OTM spreads guarantee losses; the bid-ask spread is the first cost, and it is largest exactly where beginners are tempted (cheap OTM).
* **Respect the shrinking range and the session rhythm.** Read the open, trade the mid-session, exit into the close; late-day breakout trades have little range left and are usually FOMO.
* **Size small, risk a fixed fraction, and honour the stop.** No single scalp should dominate the day; a strict per-trade risk limit keeps every trade survivable.
* **Square off intraday — never accidentally hold overnight.** The 3:30 PM–9:15 AM gap is un-hedgeable and outside your intraday sizing; an intraday trade is closed intraday.

> **Professional Insight — the daily loss limit is the intraday trader's most important rule.** More intraday accounts are wrecked by revenge trading after a loss than by any signal failure. The professional sets a *daily loss limit* — a rupee amount that, once hit, ends trading for the day, no exceptions — because the trades taken after a painful loss (bigger, wilder, outside any setup) are the account-killers. Knowing when to *stop trading for the day* is a greater intraday skill than knowing when to enter.

---

## 8. Common Mistakes

* **Overtrading.** Taking too many trades — multiplying costs and forcing marginal, negative-expectancy setups; the number-one intraday P&L killer.
* **Ignoring transaction costs.** Celebrating "profitable" scalps that are actually flat after ₹62.5/round trip and the spread; costs are the first opponent.
* **Scalping OTM options.** The wide OTM bid-ask spread turns every scalp into an instant loss; scalp ATM only.
* **Bringing positional habits intraday.** Holding a losing scalp "hoping it comes back," using wide stops, or letting an intraday trade become an overnight hold.
* **Chasing late-day breakouts.** Initiating directional trades near the close, when little of the day's expected range remains and FOMO peaks.
* **Revenge trading after a loss.** Taking bigger, wilder trades to "make it back," outside any setup — the trades that turn a bad day into a disaster. Use a daily loss limit.

---

## 9. Case Study — "A Day in the Life of an Intraday NIFTY Trader"

**Context.** This is a realistic five-trade intraday day on NIFTY — two winners, two losers, and one breakeven — that ends profitable, but only because four of the five trades were disciplined. The fifth, an undisciplined FOMO trade near the close, gives back much of the day's gains — the honest portrait of what separates consistent intraday profitability from the average trader's experience. NIFTY opens at 24,600 (India VIX 14, ~2 days to weekly expiry); lot 65; costs ~₹62.5/round trip; figures illustrative.

**The five trades.**

**Table 24.3 — A five-trade intraday day (illustrative, per lot)**

| # | Time | Setup | Trade | Result | Gross P&L | Net P&L |
| ---: | --- | --- | --- | --- | ---: | ---: |
| 1 | 9:45 | ORB breakout above 24,620 | Buy 24,600 CE @₹95 → sell @₹150 (10:30) | **Win** | +3,575 | +3,513 |
| 2 | 11:15 | Pullback-to-VWAP long | Buy 24,700 CE @₹80 → SL @₹55 | Loss | −1,625 | −1,688 |
| 3 | 12:30 | Range-day Theta sell | Sell 24,900 CE @₹35 → cover @₹22 (2:00) | Win | +845 | +783 |
| 4 | 2:15 | VWAP breakdown short | Buy 24,600 PE @₹70 → exit @₹70 (reversal) | Breakeven | 0 | −63 |
| 5 | 3:00 | Late "FOMO" long | Buy 24,700 CE @₹40 → SL @₹25 | Loss | −975 | −1,038 |
| | | | | **Day total** | **+1,820** | **+₹1,507** |

**Trade-by-trade discipline review.**

* **Trade 1 (the day-maker).** A textbook ORB breakout, entered on a clear signal with an ATM option (high Delta, tight spread), exited at a planned target. **+₹3,513** — the disciplined, high-quality trade that made the day.
* **Trade 2 (a valid trade that lost).** A reasonable pullback-to-VWAP setup that simply did not work; the trader honoured the stop and took the **−₹1,688** loss cleanly. A losing trade, but a *disciplined* one — stops are part of the process.
* **Trade 3 (patient Theta).** Recognising a range developing, the trader sold a far-OTM call and let intraday Theta work, covering for a small **+₹783**. A sound, patient use of the session's decay.
* **Trade 4 (breakeven, managed).** A VWAP-breakdown short that reversed; the trader exited at breakeven rather than hoping, taking only the **−₹63** cost. Disciplined damage control.
* **Trade 5 (the mistake).** At 3:00 PM, with little of the day's range left (Table 24.1: ±61 remaining) and after the breakeven trade 4, the trader took a **FOMO** long on a small uptick — no real setup, driven by the urge to end higher. It failed, costing **−₹1,038.**

**The analysis.** The day ended **+₹1,507/lot** — profitable. But the discipline breakdown is stark: **the four disciplined trades (1–4) made +₹2,545**; the single undisciplined fifth trade *gave back ₹1,038* — about **40% of the day's profit** — for no reason but the compulsion to trade. Had the trader stopped after trade 4 (a natural stopping point: a good day, a breakeven, and the volatile close approaching with little range left), they would have banked ₹2,545. Note too the cost drag: five round trips cost ₹312.5, turning a ₹1,820 gross into ₹1,507 net — and a trader doing fifteen trades would have paid ₹937.5, on likely worse setups.

**The lesson.** Consistent intraday profitability is not about a magic signal — Trade 1's ORB was ordinary, and Trades 2 and 5 used similar reasoning with opposite discipline. It is about *trade selection and stopping*: taking the high-quality setups (Trade 1), honouring stops on the ones that fail (Trades 2, 4), harvesting the patient edges (Trade 3), and — above all — *not taking the marginal trades* (Trade 5). The winning intraday trader is defined by the trades they *do not* take and by knowing when to stop for the day, far more than by their entries.

*(Takeaway: intraday profitability comes from trade discipline and cost control, not signals — take few high-quality setups, honour every stop, and know when to stop for the day; the FOMO trade that gives back the day's gains is the one to eliminate.)*

---

## 10. Chapter Summary

* **Intraday options trading is a distinct discipline** dominated by **transaction costs** and **trade discipline**, not by entry signals — a different game from positional trading.
* The **session has three phases**: the volatile, wide-spread open (read, don't trade recklessly), the tradable mid-session (trends and VWAP work), and the squaring close (exit, don't initiate).
* **Technical triggers** (ORB, VWAP, OI support/resistance, pivots/CPR) *time* entries, but discipline and cost control decide survival.
* **Intraday selling** harvests the day's Theta with a hard stop; **scalping** works *only* in tight-spread ATM strikes — OTM spreads guarantee losses.
* The **remaining expected move** shrinks with √(time remaining): a ±217 day range is ±106 by 2:00 PM and ±61 by 3:00 — late-day trades have little room.
* **Costs dominate:** ~₹62.5/round trip means a minimum edge of ~₹0.96/unit, and 10 round trips/day costs ~₹1.56 lakh/year; **frequency is the enemy**, so trade few.
* **Overtrading is the number-one P&L killer** — it multiplies costs and forces marginal trades; counter it with a max trades/day, A+ setups only, and a **daily loss limit**.
* **Size small and fixed, risk ≤1% per trade, and square off intraday** — never let an intraday trade become an un-hedgeable overnight gap.

---

## 11. Key Takeaways

* **Trade few, high-quality setups — frequency is the enemy** because costs scale with trades, not skill.
* **Scalp ATM only, respect the spread, and mind the shrinking intraday range** — read the open, trade the middle, exit the close.
* **Size small, risk a fixed ≤1% per trade, and honour every stop** — no single scalp should dominate the day.
* **Set a daily loss limit and eliminate the FOMO trade** — the marginal late-day trade that gives back the day's gains is what separates the average intraday trader from the profitable one.

---

## 12. Practice Questions

**Q1 (Concept).** In one or two sentences, why is intraday options trading a *different* discipline from positional trading?

**Q2 (Session).** Describe the character of the three phases of the trading day and what a disciplined trader does in each.

**Q3 (Remaining range).** With a day's expected move of ±200 points, compute the remaining expected move at 12:30 PM (3 hours left of 6.25).

**Q4 (Cost hurdle).** At ₹62.5 per round trip and a lot size of 65, what is the minimum premium move needed to cover costs on one round trip?

**Q5 (Annual cost).** Compare the annual transaction cost of a 3-round-trips/day trader with an 8-round-trips/day trader (~250 days).

**Q6 (Daily P&L).** A trader does 4 trades/day, 55% win rate, avg win ₹2,000/lot, avg loss ₹1,200/lot, cost ₹62.5/round trip. Compute the net daily P&L target.

**Q7 (Breakeven win rate with costs).** A 1:1 scalp (avg win = avg loss = ₹600/lot) faces ₹62.5 cost. Compute the breakeven win rate.

**Q8 (Scalping).** Why can you scalp ATM options but not far-OTM options?

**Q9 (Overtrading).** In the case study, the disciplined four trades made ₹2,545 but the day ended +₹1,507. Explain what happened and the lesson.

**Q10 (Judgement).** A trader is down ₹3,000 by 1:00 PM and starts taking larger, more frequent trades to "make it back." Diagnose the mistake and prescribe the fix.

---

## 13. Detailed Solutions

**A1.** Intraday trading is dominated by **transaction costs** (many round trips a day, so costs become the largest P&L determinant) and **trade discipline** (with dozens of trades, selectivity and stopping matter more than any signal), and moves must play out in hours, not days — so positional habits (patience, wide stops, "it'll come back") fail intraday.

**A2.** **Open (9:15–9:45):** high volatility, wide spreads — *read* the range and gap, don't trade recklessly with market orders. **Mid-session (10:00–2:00):** tighter spreads, trends establish — the core *trading* window (VWAP, pivots work). **Close (3:00–3:30):** position squaring, rising volatility — *exit*, don't initiate.

**A3.** Remaining move = 200 × √(3/6.25) = 200 × √0.48 = 200 × 0.693 ≈ **±139 points**. By 12:30, about ±139 of the ±200 day range remains.

**A4.** Minimum move = cost ÷ lot size = 62.5 ÷ 65 ≈ **₹0.96/unit** of premium — the option must move at least ~₹0.96 just to cover the round-trip cost.

**A5.** 3/day: 3 × 62.5 × 250 = **₹46,875/year**. 8/day: 8 × 62.5 × 250 = **₹1,25,000/year**. The 8-round-trip trader pays about ₹78,125 more per year — the cost of frequency.

**A6.** Gross EV = 4 × [0.55 × 2,000 − 0.45 × 1,200] = 4 × [1,100 − 540] = 4 × 560 = ₹2,240. Costs = 4 × 62.5 = ₹250. **Net daily P&L target = 2,240 − 250 = +₹1,990/day.**

**A7.** Break even: p × 600 − (1 − p) × 600 − 62.5 = 0 → 1,200p − 600 − 62.5 = 0 → 1,200p = 662.5 → p = **55.2%.** Even a symmetric 1:1 scalp needs a 55.2% win rate to break even after the ₹62.5 cost (versus 50% with no cost).

**A8.** Because scalping captures *tiny* moves, and its viability depends on a *tight bid-ask spread*. **ATM options** have tight spreads (a few paise), so the spread does not eat the small edge. **Far-OTM options** have *wide* spreads (Chapter 3) — you might buy at the ask and only sell at the bid, losing several percent instantly on the spread alone, which dwarfs any scalp's edge. Scalping OTM is a guaranteed loss.

**A9.** The four disciplined trades (a clean ORB win, two honoured-stop trades, and a patient Theta harvest) made +₹2,545. But a fifth, undisciplined **FOMO trade near the close** — taken with little of the day's range left and no real setup — lost ₹1,038, dropping the day to +₹1,507. The lesson: **overtrading (the marginal fifth trade) gave back ~40% of the day's profit**; consistent intraday profitability comes from *not taking* the marginal trade and knowing when to stop, not from the entries.

**A10.** The mistake is **revenge trading** — taking bigger, more frequent trades after a loss to recover, outside any real setup. These trades multiply costs and have negative expectancy, and they cluster when discipline is weakest, turning a bad day into a disaster. The fix: a pre-set **daily loss limit** that, once hit (here, arguably already), *ends trading for the day, no exceptions* — plus a cooling-off rule after a loss. Knowing when to stop for the day is the more important skill than knowing when to enter.

---

## 14. Mini Glossary

* **Intraday options trading** — opening and closing option positions within a single session, squared off before the close. → this chapter.
* **Session dynamics** — the three phases of the day: volatile open, tradable mid-session, squaring close. → this chapter.
* **Opening Range Breakout (ORB)** — an entry trigger based on a break of the first 15–30 minutes' high/low. → this chapter.
* **VWAP** — Volume Weighted Average Price; the day's fair-value line, used as an intraday trend filter and support/resistance. → this chapter.
* **CPR (Central Pivot Range)** — a pivot-based band; a wide CPR suggests a range day, a narrow one a trend day. → this chapter.
* **Scalping** — capturing tiny moves for small, frequent profits; viable only in tight-spread ATM strikes. → this chapter.
* **Remaining expected move** — the range likely for the rest of the day; shrinks with √(time remaining). → this chapter.
* **Minimum edge** — the premium move needed to cover the round-trip cost (~₹0.96/unit at ₹62.5/round trip, lot 65). → this chapter.
* **Overtrading** — taking more trades than edge and discipline justify; the number-one intraday P&L killer. → this chapter.
* **Daily loss limit** — a pre-set loss that ends trading for the day; the intraday trader's most important discipline rule. → this chapter.

---

<!-- End of Chapter 24 (CLOSES Part VI). Rev 2 (5 Aug 2026): lot 75→65, cost per RT ₹61→₹62.5, min edge ₹0.81→₹0.96/unit, per revised Ch3. Remaining range = day move × √(hrs remaining/6.25) — corrects architecture's inverted formula. Table 24.1: VIX 14 → day ±217, decaying to ±61 by 3:00 (index points, lot-independent, unchanged). Cost per RT ~₹62.5; min edge ₹0.96/unit; 10 RT/day ₹1.5625L/yr (Table 24.2). Daily P&L = trades×[p·win−(1−p)·loss]−costs; NumEx3 5 trades 60% → +₹2,188. NumEx5 1:1 scalp breakeven 56.3%. Case study 5-trade day (Table 24.3): +₹1,507 net; disciplined 4 = +₹2,545; FOMO trade 5 gave back ₹1,038 (~40%). Square off before 3:30 (overnight gap). Q3 remaining ±139, Q6 +₹1,990, Q7 55.2%. Costs from Ch3. IV = implied volatility. Part VII (risk management) previewed without number. -->
