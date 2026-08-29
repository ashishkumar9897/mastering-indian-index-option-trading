<!-- Difficulty: Level 1/5 (Beginner). Dependency: Chapter 2. Target length ~8,000 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision). Cost rates (illustrative, 2026, flagged verify-current, consistent with Ch2): brokerage ₹20/order; STT 0.15% option sale / 0.15% exercise (from 1 Apr 2026); exchange txn ~0.035%; GST 18% on brokerage+txn+SEBI fee; SEBI fee ~0.0001% (now +18% GST); stamp duty 0.003% buy. Sell-side cost model 23.60+0.1244P; buy-side 23.60+0.0289B. Margin illustration ~₹1.25 lakh/lot. IV reserved for implied volatility. All P&L shown net of the six cost components. -->

# Chapter 3 — The Trading Infrastructure: Platforms, Orders, and Costs

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Trace the order flow — what actually happens between clicking "buy" and getting a fill.
2. Choose the right order type (market, limit, SL, SL-M) for a given option and situation.
3. Break down the complete cost of an option trade: brokerage, STT, exchange transaction charges, GST, the SEBI turnover fee, and stamp duty.
4. Navigate a broker platform for option trading — order entry, the order and position book, and the Greeks display.
5. Understand, at a working level, what margin is and why sellers post it while buyers do not.
6. Know the trading hours and the pre-open session, and why the first and last minutes behave differently.

This is a practical, Level 1 chapter, but do not skim it. The difference between a strategy that works on paper and one that works in your account is almost entirely **execution and cost** — the two subjects of this chapter.

---

## 2. Introduction

Two traders take the identical view on NIFTY, choose the identical option, and are both right about the market. One ends the month ahead; the other ends it behind. The market did not separate them — their *plumbing* did. One used limit orders and traded sparingly; the other used market orders in thin strikes and traded fifty times a day, bleeding a rupee of spread and cost on every click.

In Chapters 1 and 2 you learned what the instruments are. This chapter is about the machinery you push them through: the order types, the exchange that matches your trade, the six charges that skim every transaction, the margin the system demands, and the hours the market keeps. None of it is glamorous. All of it decides whether your edge survives contact with reality.

The recurring theme is simple and unforgiving: **every trade costs money to enter and exit, and those costs scale with how often you trade and how carelessly you execute.** A trader who internalises this early will out-survive a cleverer trader who ignores it. We use the same illustrative setting as before — **NIFTY at 24,600, lot size 65** — and we state every cost rate with its date, because rates change and stale numbers are dangerous.

---

## 3. Core Concepts

### 3.1 The order flow — what happens when you click "buy"

When you place an option order, it travels a well-defined path in a fraction of a second:

1. **Your platform → your broker.** The order leaves your app or terminal and reaches your broker's systems.
2. **Risk checks at the broker.** Before anything goes to the exchange, the broker verifies you have the required margin (for a sell or a future) or funds (for a buy), and that the order respects position limits and the exchange's **execution price band** (an "operating range" around the option's current price — an order placed far outside it is rejected to stop fat-finger fills). A failed check means instant rejection — not a market event, just a plumbing one.
3. **Broker → exchange matching engine.** The order is routed to the NSE or BSE, where the **matching engine** pairs buyers and sellers by **price–time priority**: the best price is matched first, and among equal prices, the order that arrived earliest.
4. **Match and confirmation.** When your order meets a matching order, a trade is struck and a confirmation flows back to you.
5. **Clearing and settlement.** The clearing corporation steps in by **novation** (Chapter 1), becoming counterparty to each side and guaranteeing settlement.

The practical implications matter more than the mechanics. Because matching is price–time, a **limit order** placed early sits ahead of one placed late at the same price. Because professional firms **co-locate** their systems (renting rack space for their servers physically inside the exchange's data centre) and react in microseconds, a retail trader will never win a pure speed race — which is one more reason retail edges come from *selection and discipline*, not from out-clicking the machines.

---

### 3.2 Order types — market, limit, SL, and SL-M

This is the most important operational skill in the chapter, so we treat it in full.

**What is it?** An **order type** tells the exchange *how* to execute your instruction — at any price, at a fixed price, or only after a trigger. The four you need:

* **Market order** — execute immediately at the best available price, whatever it is.
* **Limit order** — execute only at your specified price *or better*; otherwise wait.
* **Stop-loss limit (SL)** — dormant until the price hits your **trigger**, then it becomes a *limit* order at your specified price.
* **Stop-loss market (SL-M)** — dormant until the trigger, then it becomes a *market* order.

**Why do they exist?** Because traders need to balance two competing wants: *certainty of execution* (a market order fills for sure) and *certainty of price* (a limit order never overpays). No single order type gives both, so the exchange offers a menu.

**Why should a trader care?** Because in options, the wrong order type can cost you more than a wrong view. Option spreads are often wide, so a **market order in a thin strike can fill far from the price you saw** — you click expecting ₹40 and get ₹43. A limit order protects your price but may not fill when you need it. Getting this choice right is daily, unglamorous money.

**Intuitive explanation.** A market order is hailing a taxi and saying "go, whatever the fare." A limit order is saying "I'll pay up to ₹200, not a rupee more" and waiting. A stop-loss is a tripwire: "if the price falls to my trigger, get me out."

**Numerical example.** An ATM NIFTY call shows bid ₹199.5 / ask ₹200.5. A market **buy** fills at the ask, ₹200.5. A limit buy at ₹200 waits for a seller to come to your price. In a 5%-OTM strike quoted ₹40 bid / ₹42 ask, a market buy fills at ₹42 — you have paid ₹1 over the ₹41 mid before the market has moved at all. That ₹1 is 2.4% of the option's value, gone on entry.

**When to use each (the practical rule):**

* **Liquid ATM strike, speed matters** → a market order is usually fine; the spread is a few paise.
* **Any OTM or thin strike** → use a **limit order**, always. The spread is your enemy here.
* **Protecting a position** → use a stop-loss. Prefer **SL (limit)** with a trigger set a little ahead of your limit price, so the order arms before it needs to fill.

> **Market Note — SL-M availability in options has changed.** The exchanges have, at times, **restricted stop-loss-market (SL-M) orders in options** (notably from 2021) because a market order triggered in a thin strike could fill at a wild price. Availability and the exact rules have shifted since; confirm on your platform what stop order types are currently permitted for options, and default to SL (limit) with a sensible trigger–limit gap.

**Order validity — a second dimension.** Separately from its *type*, every order carries a *validity*: a **DAY** order rests on the book until it fills or the session ends; an **IOC** (immediate-or-cancel) order fills whatever it can *instantly* and cancels the rest. Most option orders are DAY. IOC is useful when you want a fill *now or not at all* and refuse to leave a resting order exposed — but on a limit-IOC you may get only a partial fill. Match the validity to your intent, not just the price.

**Professional interpretation.** Desks almost never send naked market orders into options. They "work" a limit order near the mid, or slice it, precisely to avoid paying the spread. Treat every market order in an option as a small, deliberate decision to *pay* for immediacy — not a default.

**Common mistake.** Using market orders in OTM strikes "to make sure I get filled," then wondering why the fill was terrible. In a wide market, the fill *is* terrible — that is what the width means.

**Practical takeaway.** **Default to limit orders in options; reserve market orders for liquid ATM strikes when speed genuinely matters.** The order type is a cost decision, every time.

---

### 3.3 The bid–ask spread and impact cost — the hidden charges

Before a single visible charge is levied, the market itself takes a cut through the **bid–ask spread**.

* The **bid** is the highest price a buyer is willing to pay; the **ask** (or offer) is the lowest price a seller will accept. You **buy at the ask and sell at the bid**, so the moment you enter and exit, you cross the spread.
* The **mid** is the average of bid and ask — the "fair" reference price you rarely actually transact at.

**Impact cost** measures how far your execution sits from the ideal (mid) price:

```
Impact cost (%) = (Actual execution price − Mid price) ÷ Mid price × 100
```

Impact cost balloons as you move away from the money, because OTM and far strikes have fewer participants and wider spreads. Table 3.1 illustrates (figures illustrative).

**Table 3.1 — Spread and impact cost widen away from the money (illustrative)**

| Strike | Bid (₹) | Ask (₹) | Mid (₹) | Buy at ask → impact cost |
| --- | ---: | ---: | ---: | ---: |
| ATM | 199.5 | 200.5 | 200.0 | (200.5 − 200) ÷ 200 = **0.25%** |
| 5% OTM | 40.0 | 42.0 | 41.0 | (42 − 41) ÷ 41 = **2.44%** |
| 10% OTM | 8.0 | 10.0 | 9.0 | (10 − 9) ÷ 9 = **11.1%** |

**The lesson:** the cheap-looking 10%-OTM option carries an *invisible* 11% cost just to get in and out. This is the quantitative backbone of the liquidity map from Chapter 2 — the spread is why far strikes are traps.

---

### 3.4 The complete cost structure — the six visible charges

On top of the spread come six explicit charges. Learn them once; they apply to every trade you will ever place. **All rates below are illustrative, as of 2026, and must be verified with your broker and the exchange — they change.**

1. **Brokerage** — your broker's fee. Discount brokers typically charge a **flat fee (e.g., ₹20 per executed order)** regardless of size; full-service brokers may charge a **percentage** of turnover. For active option trading, flat-fee broking is dramatically cheaper.
2. **Securities Transaction Tax (STT)** — a government tax. For options: **0.15% of the premium on the sell side** (raised from 0.1% with effect from 1 April 2026, itself up from 0.0625% before October 2024), nothing on the buy side; and **0.15% of the intrinsic (settlement) value if an in-the-money option is exercised at expiry** (raised from 0.125% on the same date) — the "let it expire" trap from Chapter 2.
3. **Exchange transaction charges** — the exchange's fee, roughly **0.035% of the premium value** on the NSE for options (BSE rates differ). Charged on both legs.
4. **GST** — **18%**, levied on the sum of *brokerage + exchange transaction charges + SEBI turnover fee* (not on STT or stamp duty).
5. **SEBI turnover fee** — a tiny regulator levy, about **0.0001% of premium value** (₹10 per crore); since April 2025 it too attracts 18% GST, which is why it sits inside the GST base above.
6. **Stamp duty** — a state levy on the **buy side only**, about **0.003% of premium value** for options.

**Table 3.2 — Roundtrip cost of one NIFTY ATM CE (buy ₹200, sell ₹250, lot 65; illustrative rates 2026)**

| Charge | Buy leg (premium ₹13,000) | Sell leg (premium ₹16,250) |
| --- | ---: | ---: |
| Brokerage (flat) | 20.00 | 20.00 |
| STT | 0.00 (none on buy) | 24.38 (0.15% × 16,250) |
| Exchange txn (0.035%) | 4.55 | 5.69 |
| SEBI fee (0.0001%) | 0.01 | 0.02 |
| Stamp duty (0.003%) | 0.39 | 0.00 (buy side only) |
| GST (18% of brokerage + txn + SEBI) | 4.42 | 4.63 |
| **Leg total** | **≈ 29.37** | **≈ 54.72** |

* **Total roundtrip cost ≈ ₹29.37 + ₹54.72 = ₹84.09.**
* **Gross P&L** = (250 − 200) × 65 = **₹3,250**. **Net P&L ≈ 3,250 − 84.09 = ₹3,165.91 (≈ ₹3,166).**
* Cost as a share of the total premium traded (₹29,250) ≈ **0.29%**; as a share of gross profit ≈ **2.6%**.

On a profitable, low-frequency trade, ₹84 is a rounding error. The danger is not any single trade — it is *frequency*, which we quantify in the case study.

> **Market Note — The April 2026 STT hike changed the maths for sellers.** With effect from 1 April 2026, the option sell-side STT rose from 0.1% to **0.15%** (and the exercise rate from 0.125% to 0.15%) — a 50% jump in the STT slice, on top of the earlier October 2024 increase from 0.0625% to 0.1%. For a trader who sells options many times a day, each hike is a direct, permanent haircut to the strategy's edge — a reminder that the rules of the game are set by the regulator and can move against you.

---

### 3.5 Margin — a working overview

You do not need the full margin machinery yet, but you need the shape of it, because it determines what you can afford to do.

* **Option buyers** pay only the **premium**, in full, upfront (the **premium margin**). Your maximum loss is that premium, so no further collateral is demanded. Since early 2025, SEBI requires this premium to be collected **upfront**.
* **Option sellers and futures traders** must post **margin** — collateral held by the clearing corporation against their open-ended risk. It has two main parts:
  * **SPAN margin** — computed by the SEBI **SPAN** system, which revalues your position across a grid of adverse scenarios (large up/down moves combined with volatility changes) and charges the **worst-case loss**.
  * **Exposure margin** — an additional buffer on top of SPAN.

**Illustrative margin for selling one lot of NIFTY ATM PE** (NIFTY ≈ 24,600, lot 65): SPAN ≈ **₹95,000** + exposure ≈ **₹30,000** = **≈ ₹1,25,000** blocked. If you sold that put at ₹150, you receive 150 × 65 = ₹9,750 in premium, but roughly ₹1.25 lakh of capital is *tied up* as margin for the life of the trade. The premium is your reward; the margin is the price of admission. *(Figures illustrative; always check your broker's margin calculator, and note that margin can rise intraday if the market moves or volatility spikes.)*

The single practical point for now: **selling options is capital-intensive and can trigger intraday margin calls; buying options is not.** Size accordingly.

---

### 3.6 Multi-leg execution and legging risk

Many strategies (introduced later in the book) have two or four legs. Executing them is a skill in itself, and a source of hidden cost that beginners consistently underestimate.

* **The quoted "net price" is optimistic.** When your platform shows a spread's net credit or debit, it is usually computed off the *mid* of each leg. But you buy at the ask and sell at the bid, so a realistic fill is **worse than the displayed net on every leg**. This gap between the price you expected and the price you actually got is called **slippage**, and across a multi-leg structure it **compounds** — every leg adds its own.
* **Legging risk.** If you enter a multi-leg position one leg at a time ("legging in"), the market can move between fills — you may get the first leg and then find the second has run away, leaving you with an unintended naked position at a worse price.
* **All-together (basket) execution.** A basket or multi-leg order tries to fill all legs *at once* rather than one by one, reducing legging risk, but it still cannot escape the spread on each leg.

**Execution tactics that work:**

* Use **limit orders on the combined structure**, and "work" the order near the net mid rather than paying up immediately.
* **Avoid market orders** on any leg that sits in an illiquid strike.
* Prefer **liquid strikes for the short legs**, where the spread is tightest, since those carry the most risk.

> **Professional Insight — The fill is part of the strategy.** On a desk, the person designing a spread and the person executing it both know that a strategy which looks profitable at mid prices can be a loser after realistic fills. Before you trade any multi-leg structure, estimate its cost using the *bid/ask* you will actually transact at, not the friendly mid the screen shows you.

---

### 3.7 Trading hours and the pre-open session

The Indian equity and derivatives market runs a fixed schedule (IST):

* **Normal market: 9:15 AM – 3:30 PM.** This is when options trade continuously.
* **Pre-open call auction (cash market): 9:00 AM – 9:15 AM.** In this window the *cash* market collects orders and discovers a single opening price for each stock and the index. Options begin trading at **9:15 AM**, and their opening prices reflect the index level that the pre-open auction has just established.

Two behavioural facts follow, and they cost the unwary:

* **The first few minutes are volatile and wide.** At 9:15 the market is digesting overnight news and the fresh opening level; spreads are wider and prices whip around. Fills are poor.
* **The last half hour is about position-squaring.** Intraday positions are closed and volumes surge, which can move option prices sharply near the close.

The practical takeaway is to be *especially* careful with order types in the opening minutes — this is exactly when a careless market order in a thin strike does the most damage.

---

### 3.8 Navigating the platform

Every broker platform, whatever its branding, exposes the same core screens. Learn the fields, not the logos.

* **The order window.** You specify: buy/sell, the contract, **quantity in lots** (the platform multiplies by the lot size), the **order type** (market/limit/SL/SL-M), the **price** (for limits) and **trigger** (for stop orders), and the **product type** — typically an intraday product (auto-squared off before close, sometimes with higher leverage) versus a carry-forward product (held overnight, full margin). Choosing the wrong product type is a common, avoidable error.
* **The order book and trade book.** The order book shows pending/rejected orders; the trade book shows executed fills. Check both after every order — a "placed" order is not a "filled" order.
* **The position book.** Your live positions, quantities, average prices, and running profit or loss (marked to market).
* **The option chain and Greeks display.** Most platforms show the live chain with bid/ask, volume, open interest, and per-option Greeks. You will use these heavily later; for now, know where they live.

> **Beginner Alert — Quantity is in lots, value is in rupees.** When you type "1" in the quantity box, you are trading one *lot* — 65 units for NIFTY — not one unit. A premium of ₹200 therefore commits ₹13,000, and selling commits far more as margin. Always read your position in rupees, not in the small number you typed.

---

## 4. Examples (Real-World)

**Example 1 — The spread decides the strike.** Two traders both want an OTM NIFTY hedge. One buys a strike with a ₹0.50 spread and exits cleanly a week later; the other buys a far strike with a ₹3 spread and loses ~7% to entry-and-exit before the market even moves. Same idea, different plumbing.

**Example 2 — Order type saves a trade.** During a volatile 9:16 AM, a trader wants a NIFTY 5%-OTM call. A market order would have filled ₹1.50 above the mid in the chaos. A limit order at the mid filled thirty seconds later at a fair price — the discipline paid for itself instantly.

**Example 3 — Frequency, not skill, sinks a scalper.** A trader with a genuinely good short-term read still finishes the month down, because fifty roundtrips a day multiplied the ₹60-odd per-trip cost into a mountain that the edge could not clear. We quantify this in Section 9.

---

## 5. Numerical Examples

Illustrative setting: **NIFTY, lot size 65**, cost rates as in Section 3.4 (as of 2026, verify current).

### Numerical Example 1 — Roundtrip cost and net P&L

From Table 3.2: buy a NIFTY ATM CE at ₹200, sell at ₹250.

* Gross P&L = (250 − 200) × 65 = **₹3,250**.
* Total roundtrip cost ≈ **₹84.09**.
* **Net P&L ≈ ₹3,166.** Costs consumed ≈ **2.6%** of the gross profit.

### Numerical Example 2 — Minimum move to break even (option bought at ₹100)

You buy a NIFTY option at ₹100 (premium value 100 × 65 = ₹6,500). Buy-side charges ≈ ₹26.49. You then sell at price P; the sell-side charges come to about **23.60 + 0.1244P** in rupees — where the fixed ₹23.60 is brokerage plus its GST, and the 0.1244P term is everything that scales with the sale value (STT at 0.15% + exchange charge + SEBI fee, plus GST on the last two), expressed per rupee of premium P. Setting gross profit equal to total cost:

```
(P − 100) × 65 = 26.49 + 23.60 + 0.1244P
65P − 6,500   = 50.09 + 0.1244P
64.8756P      = 6,550.09
P             ≈ 100.96
```

**The option must rise about ₹0.96 — roughly 1% of its premium — just to cover costs.** Below ₹100.96 you are still losing money even though the option has "gone up." Every roundtrip starts life in this small hole.

### Numerical Example 3 — Impact cost across moneyness

From Table 3.1: buying at the ask versus the mid costs **0.25%** at the ATM, **2.44%** at 5% OTM, and **11.1%** at 10% OTM. The invisible cost of the spread can dwarf all six visible charges combined in a thin strike.

### Numerical Example 4 — Effective breakeven on a ₹200 option

Buy at ₹200 (buy charges ≈ ₹29.37). Selling at price P incurs ≈ 23.60 + 0.1244P in charges:

```
(P − 200) × 65 = 29.37 + 23.60 + 0.1244P
64.8756P       = 13,052.97
P              ≈ 201.20
```

The option must reach about **₹201.20** to break even — a ₹1.20 move, roughly **0.6%** of premium. Note that the *percentage* hurdle is smaller for a pricier option, which is one reason costs bite hardest on cheap, high-frequency scalps.

### Numerical Example 5 — Margin versus premium on a short option

Sell one lot of NIFTY ATM PE at ₹150: premium received = 150 × 65 = **₹9,750**; margin blocked ≈ **₹1,25,000**. The best-case return on margin over the option's life is 9,750 ÷ 1,25,000 ≈ **7.8%** (before costs, if the entire premium is retained) — and the margin can rise if the market moves against you. Selling is not "free income"; it rents out a large slice of your capital.

---

## 6. Calculations (the reusable recipes)

**(a) Total transaction cost**

```
Total cost = Brokerage + STT + Exchange charges + GST + SEBI fee + Stamp duty
   where GST = 18% × (Brokerage + Exchange charges + SEBI fee)
```

**(b) Net P&L**

```
Net P&L = (Exit premium − Entry premium) × Lot size − Total roundtrip cost
```

**(c) Impact cost**

```
Impact cost (%) = (Actual execution price − Mid price) ÷ Mid price × 100
```

**(d) Effective breakeven (bought option)** — solve for the exit premium P at which net P&L = 0:

```
(P − Entry) × Lot size = Buy-side cost + Sell-side cost(P)
```

Because the sell-side cost depends on P (STT, exchange charge, GST scale with premium), solve the small linear equation as in Numerical Examples 2 and 4.

**(e) Return on margin (short option, gross best case)**

```
Return on margin = Premium received ÷ Margin blocked
```

---

## 7. Practical Insights

* **Cost is a function of frequency.** One well-chosen trade barely notices costs; a hundred trades are crushed by them. Before adopting any high-frequency style, compute the annual cost bill first — it is often larger than most traders' entire target profit.
* **The spread is the biggest hidden cost, and it lives in the strike you choose.** Trading liquid, near-the-money strikes is not just "safer" — it is *cheaper*, by a margin that dwarfs brokerage.
* **Order type is a daily cost decision.** Limit by default; market only when the strike is liquid and speed truly matters. This one habit will save more money over a career than most "strategies."
* **Selling ties up capital.** A short option's premium looks like income until you see the ₹1.25 lakh of margin behind it — and margin can rise intraday. Judge sold options by return *on margin*, not on premium.
* **Rules change; verify.** The April 2026 STT hike, the SL-M restriction, and upfront premium collection all arrived by circular. Re-check current rates and order-type rules before you rely on last year's numbers.

> **Professional Insight — Your first, guaranteed opponent is cost.** Before the market can take your money, brokerage, STT, GST, the exchange, the regulator, and the state each take a slice — and the spread takes the biggest slice of all. A professional treats "beating costs" as the *first* hurdle every trade must clear, not an afterthought at tax time.

---

## 8. Common Mistakes

* **Market orders in thin strikes.** The single most expensive habit for beginners: a triggered or manual market order in an illiquid option fills far from the mid.
* **Judging trades gross, not net.** Celebrating a "₹3,250 profit" without subtracting the ₹84 of costs — trivial once, ruinous across hundreds of trades.
* **Ignoring the spread when picking strikes.** Chasing cheap OTM options whose 5–11% impact cost quietly guarantees a loss on entry and exit.
* **Confusing premium with margin when selling.** Believing a sold option "only" involves the premium, then being surprised by the ₹1.25 lakh margin block or an intraday margin call.
* **Wrong product type.** Placing a carry-forward order intending intraday (or vice versa), and discovering the difference in leverage or auto-square-off at the worst moment.
* **Treating displayed spread net prices as achievable.** Assuming the mid-based net credit on a multi-leg order is what you will actually get.

---

## 9. Case Study — The scalper versus the positional trader

**Context.** Two traders run the *same* NIFTY option approach with equal skill and equal per-trade edge. The only difference is frequency: the **scalper** does 50 roundtrips a day; the **positional trader** does 5 roundtrips a *week*. We hold cost rates at the Section 3.4 values (illustrative, 2026).

**The scalper's cost bill.** Assume each roundtrip is on an ATM option at ₹100 (lot 65), a typical scalp.

* Buy-side charges ≈ ₹26.49; sell-side charges at ₹100 ≈ 23.60 + 0.1244 × 100 ≈ ₹36.04.
* **Cost per roundtrip ≈ ₹62.53** (≈ ₹0.96 per unit — recognise this from Numerical Example 2).
* **Per day** = 50 × 62.53 = **₹3,127**.
* **Per month** (≈ 20 trading days) = **₹62,530**.
* **Per year** (≈ 250 days) = **₹7,81,625 — over ₹7.8 lakh in transaction costs alone.**

Before the scalper earns a single rupee of profit, the strategy must first generate **more than ₹7.8 lakh of gross edge a year** just to cover costs. Since a scalp aims for a few points of premium, and costs eat ~₹0.96 of premium every trip, a large fraction of every winning scalp is handed straight to intermediaries and the government.

**The positional trader's cost bill.** Five roundtrips a week on larger positions (say ₹200 options), each costing ≈ ₹80:

* **Per week** = 5 × 80 = **₹400**.
* **Per year** (≈ 50 weeks) ≈ **₹20,000**.

Because positional trades aim for large premium moves (tens of rupees), the ₹80 cost is a tiny fraction of each trade's target.

**The analysis.** Same skill, same edge — but the scalper's annual cost bill (~₹7.8 lakh) is roughly **39 times** the positional trader's (~₹20,000). The April 2026 STT hike made this worse specifically for the high-frequency seller, raising the sell-side STT slice by 50%. Costs do not scale with your *insight*; they scale with your *activity*.

**The lesson.** High-frequency styles are viable only with an edge large and consistent enough to clear an enormous cost hurdle — which is why they are dominated by low-latency professionals, not retail screens. For most traders, *trading less* is the single most reliable way to improve net returns.

*(Takeaway: your net edge = gross edge − costs, and costs are proportional to frequency. Choose a trading frequency your edge can actually afford.)*

---

## 10. Chapter Summary

* An order travels **you → broker (risk checks) → exchange matching engine (price–time priority) → clearing**; retail cannot win a speed race, so edges come from selection and discipline.
* The four **order types** trade off certainty of execution against certainty of price; **default to limit orders in options**, reserving market orders for liquid ATM strikes.
* The **bid–ask spread** is the biggest hidden cost; **impact cost** rises steeply away from the money (≈0.25% ATM to ~11% at 10% OTM in the illustration).
* Six **visible charges** apply — brokerage, STT (0.15% sell / 0.15% exercise, from 1 April 2026), exchange transaction charges (~0.035%), GST (18% on brokerage+txn+SEBI fee), the SEBI fee, and stamp duty (0.003% buy side) — a NIFTY roundtrip costs on the order of ₹84 in the worked example.
* **Buyers** pay only the premium upfront; **sellers** post **SPAN + exposure margin** (≈₹1.25 lakh for one NIFTY lot in the illustration) and can face intraday calls.
* **Multi-leg fills** are worse than the mid-based net shown on screen; slippage compounds across legs, and legging in creates unintended exposure.
* The market runs **9:15 AM–3:30 PM IST** after a cash-market pre-open; the **first and last minutes** are volatile and wide.
* **Costs scale with frequency:** the scalper's ~₹7.8 lakh annual cost bill versus the positional trader's ~₹20,000 (≈ 39×) shows that trading less is often the surest edge.

---

## 11. Key Takeaways

* **Treat cost as the first opponent every trade must beat** — net edge = gross edge − costs, and the spread is the largest cost of all.
* **Make order type a deliberate choice:** limit by default; market only in liquid ATM strikes when speed matters.
* **Respect margin when selling** — judge short options by return on margin, and keep a buffer against intraday increases.
* **Match your trading frequency to your edge.** For most traders, fewer, better trades beat many cheap ones.

---

## 12. Practice Questions

**Q1 (Concept).** In one sentence each, contrast a market order and a limit order in terms of what each guarantees.

**Q2 (Multiple choice).** In options, a market order is most dangerous when placed in:
(a) a liquid ATM strike; (b) an illiquid far-OTM strike; (c) the last minute of a calm day; (d) a futures contract.

**Q3 (Impact cost).** An option shows bid ₹18 / ask ₹22. Compute the mid and the impact cost of buying at the ask.

**Q4 (Roundtrip cost).** Using the Section 3.4 rates, list the six charge components that apply to (a) the buy leg and (b) the sell leg of an option roundtrip, noting which are zero on each leg.

**Q5 (Numerical — net P&L).** You buy a NIFTY option at ₹150 and sell at ₹180 (lot 65). Estimate the gross P&L, and using an illustrative roundtrip cost of about ₹74, the net P&L.

**Q6 (Numerical — minimum move).** An option is bought at ₹100 (lot 65). Roughly how much must the premium rise, in rupees and as a percentage, to cover costs? (Use the chapter's result.)

**Q7 (Margin).** You sell one lot of NIFTY ATM PE at ₹160, with margin of ₹1,25,000 blocked. Compute the premium received and the gross best-case return on margin.

**Q8 (STT logic).** Why did the April 2026 STT change hurt high-frequency option sellers specifically?

**Q9 (Execution).** You want to enter a two-leg spread. Give two reasons the "net credit" shown on your screen may be better than the credit you actually receive, and one tactic to reduce the gap.

**Q10 (Judgement).** A friend plans to scalp 40 NIFTY option roundtrips a day. Using the case study logic, explain in numbers why this is a high hurdle, and what has to be true for it to work.

---

## 13. Detailed Solutions

**A1.** A **market order** guarantees *execution* (it fills immediately at the best available price) but not the price. A **limit order** guarantees the *price* (your specified level or better) but not that it will fill.

**A2.** **(b) an illiquid far-OTM strike.** Wide spreads there mean a market order can fill far from the mid; in a liquid ATM strike the spread is only a few paise.

**A3.** Mid = (18 + 22) ÷ 2 = **₹20**. Buying at the ask (₹22): impact cost = (22 − 20) ÷ 20 × 100 = **10%**. A tenth of the option's value is lost on entry alone.

**A4.** (a) **Buy leg:** brokerage (₹20), exchange transaction charge, SEBI fee, stamp duty (buy side), GST; **STT is zero** on the buy. (b) **Sell leg:** brokerage, STT (0.15% of premium), exchange transaction charge, SEBI fee, GST; **stamp duty is zero** on the sell.

**A5.** Gross P&L = (180 − 150) × 65 = 30 × 65 = **₹1,950**. Net P&L ≈ 1,950 − 74 = **₹1,876**. Costs ≈ 3.8% of gross profit here.

**A6.** From Numerical Example 2, the option must rise to about **₹100.96** — roughly **₹0.96**, or about **1%** of the ₹100 premium — just to cover costs.

**A7.** Premium received = 160 × 65 = **₹10,400**. Gross best-case return on margin = 10,400 ÷ 1,25,000 ≈ **8.3%** (before costs, if the whole premium is retained; margin can rise intraday).

**A8.** STT for option sellers is levied on the **sell side of the premium**. Raising it from 0.1% to 0.15% (1 April 2026) increased that slice by 50%. A high-frequency seller crosses this cost on **every** trade, so the aggregate impact on their annual edge is large, even though it looks tiny per trade.

**A9.** Two reasons: (i) the displayed net is usually computed from the **mid** of each leg, but you buy at the ask and sell at the bid, so realistic fills are worse; (ii) **slippage compounds across legs**, and if you leg in, the market can move between fills. One tactic: place a **limit order on the combined structure near the net mid** (and use liquid strikes for the legs) rather than sending market orders leg by leg.

**A10.** At ~₹62.5 cost per roundtrip, 40 roundtrips/day ≈ ₹2,501/day ≈ ₹6.25 lakh/year in costs alone (≈ 250 days). The strategy must generate **more than ₹6.25 lakh of gross edge a year just to break even on costs**, on top of overcoming the spread on every trip. For it to work, the trader needs a genuine, repeatable edge of well over ₹0.96 of premium per roundtrip, consistent enough to clear that hurdle — which is why such styles are dominated by low-cost, low-latency professionals. Trading less, or demanding a larger per-trade edge, lowers the hurdle.

---

## 14. Mini Glossary

* **Order flow** — the path an order takes from your platform through the broker to the exchange matching engine and clearing. → this chapter.
* **Matching engine** — the exchange system that pairs orders by price–time priority. → this chapter.
* **Market order** — an instruction to execute immediately at the best available price. → this chapter.
* **Limit order** — an instruction to execute only at a specified price or better. → this chapter.
* **Stop-loss (SL) order** — an order that becomes a limit order once a trigger price is reached. → this chapter.
* **Stop-loss market (SL-M)** — an order that becomes a market order once the trigger is reached (availability in options has been restricted; verify). → this chapter.
* **Bid / Ask** — the highest price a buyer will pay / the lowest a seller will accept; you buy at the ask and sell at the bid. → this chapter.
* **Spread** — the gap between bid and ask; a hidden cost crossed on entry and exit. → this chapter.
* **Mid** — the average of bid and ask; the reference "fair" price. → this chapter.
* **Impact cost** — how far an execution sits from the mid, as a percentage; rises for illiquid strikes. → this chapter.
* **Brokerage** — the broker's fee, typically flat per order for discount brokers. → this chapter.
* **STT (Securities Transaction Tax)** — a government tax; 0.15% of premium on option sale and 0.15% of intrinsic value on exercise (both from 1 April 2026). → this chapter.
* **Exchange transaction charges** — the exchange's fee on premium value (~0.035% NSE options). → this chapter.
* **GST** — 18%, levied on brokerage + exchange charges + SEBI fee. → this chapter.
* **SEBI turnover fee** — a small regulator levy on turnover (~0.0001% of premium). → this chapter.
* **Stamp duty** — a state levy on the buy side (~0.003% of premium for options). → this chapter.
* **SPAN margin** — margin computed from the worst-case loss across a grid of scenarios. → this chapter.
* **Exposure margin** — an additional buffer margin on top of SPAN. → this chapter.
* **Premium margin** — the full premium collected upfront from an option buyer. → this chapter.
* **Slippage** — the difference between the price you expected and the price you actually filled at; it compounds across the legs of a multi-leg trade. → this chapter.
* **Legging risk** — the risk, when entering a multi-leg trade one leg at a time, that the market moves before all legs are filled. → this chapter.
* **Order validity (DAY / IOC)** — how long an order stays live: DAY rests until filled or session end; IOC (immediate-or-cancel) fills instantly what it can and cancels the rest. → this chapter.
* **Execution price band** — the exchange's permitted operating range around an option's current price; orders placed far outside it are rejected. → this chapter.
* **Product type** — the order category (intraday vs. carry-forward) governing leverage and auto-square-off. → this chapter.
* **Pre-open session** — the cash-market call auction (9:00–9:15 AM IST) that discovers the opening price; options trade from 9:15 AM. → this chapter.

---

<!-- End of Chapter 3 (Rev 3, current as of 4 Aug 2026). Rev 3 updates (verified vs NSE/SEBI sources): (1) Lot size 75→65 (NSE Jan-2026 revision) throughout. (2) STT updated to 1-Apr-2026 rates: option sale 0.1%→0.15%, exercise 0.125%→0.15%. All cost math recomputed: sell-side model 0.106P→0.1244P; buy-side 0.0289B. Table 3.2 (buy 200/sell 250, lot 65): buy leg 29.37, sell leg 54.72, roundtrip 84.09, gross 3,250, net 3,166, 2.6% of gross. NE2 breakeven 100.82→100.96 (₹0.96, ~1%). NE4 201.00→201.20 (₹1.20, ~0.6%). NE5 premium 9,750, margin ~1,25,000, 7.8%. Case study: roundtrip 62.53 (₹0.96/unit); day 3,127; year ₹7,81,625 (~₹7.8 lakh); ratio 39×; STT hike now +50%. Q5 (lot 65, cost ₹74, net 1,876); Q6 (₹0.96); Q7 (10,400/1,25,000=8.3%); Q8/A8 (Apr-2026 hike); A10 (₹6.25 lakh). (3) Margin illustration 1.45→1.25 lakh (SPAN 95k+exposure 30k). (4) Market Note & glossary STT updated; SEBI-fee-in-GST-base note added; dates redated to 2026. Rev 2 fixes retained (case-study arithmetic method, slippage/validity/price-band glosses, cost-model derivation, impact-cost wording). Margin figures illustrative. All P&L net. IV reserved for implied volatility. -->
