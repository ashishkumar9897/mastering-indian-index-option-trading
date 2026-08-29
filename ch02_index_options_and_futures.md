<!-- Difficulty: Level 1/5 (Beginner); the futures-basis subsection touches Level 2/5. Dependency: Chapter 1. Target length ~11,000 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision). Lot sizes: NIFTY 65, BANKNIFTY 30, FINNIFTY 60, MIDCPNIFTY 120, SENSEX 20. Expiry days (since 1 Sep 2025): NIFTY Tuesday, SENSEX Thursday; BANKNIFTY/FINNIFTY/MIDCPNIFTY monthly-only (last Tuesday). All time-sensitive figures dated and flagged "verify current". IV is reserved for implied volatility; intrinsic value is always spelled out. -->

# Chapter 2 — Index Options and Their Underlying: The Instrument and Index Futures

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Define what an index option is, mechanically and legally.
2. Identify the five index option products — NIFTY, BANKNIFTY, FINNIFTY, MIDCPNIFTY, and SENSEX — and where each trades.
3. Read a contract's specifications: lot size, tick size, strike interval, expiry cycle, and settlement.
4. Explain European-style exercise and cash settlement, and why they matter in India.
5. Decode an option symbol such as `NIFTY 31JUL 24500 CE` without hesitation.
6. Describe the relationship between an index and its options, and split any premium into intrinsic value and time value.
7. Understand index **futures** as the companion instrument: their mechanics, daily mark-to-market, and why options are priced off the future rather than the spot.
8. Distinguish spot, futures price, and the **basis** — and reconcile why options are *priced* off the future but *settled* to the spot.
9. Read the cross-index **liquidity map** and understand why liquidity, not opinion, decides what you can actually trade.

Most of this chapter is conceptual. The arithmetic you do need — a buyer's and seller's payoff, a breakeven, a futures fair value, and a synthetic future — is simple and is worked out in full in Sections 5 and 6.

---

## 2. Introduction

The first time you open a NIFTY option chain, you meet a wall of numbers: dozens of rows, two mirrored halves, prices that flicker and jump, and a header full of abbreviations. It looks like a cockpit you have no licence to fly. By the end of this chapter it will look like what it is — an orderly menu of standardised contracts, each one precisely defined by the exchange.

In Chapter 1 we established *what a derivative is* and *why the market exists*. Now we get specific. This is the chapter where you learn the instrument itself: exactly what a NIFTY call or put is, what one contract controls, when it expires, how it settles, and how to read its name on the screen.

We also do something most beginner books skip. We introduce the **index future** — the option's close sibling — in the same chapter as the option, because you cannot fully understand one without the other. Options are *priced* off the future, not the spot index. The future is the tool professionals use to neutralise the risk of an option position. And a call and a put together can be assembled into a synthetic future, which is your first glimpse of the deep symmetry running through this whole subject.

Throughout, we use a consistent illustrative setting so the numbers are easy to follow: **NIFTY at 24,600**, a **lot size of 65**, a near weekly expiry with about **10 days** to go, and a risk-free rate of about **6.5%**. Lot sizes and rules are revised periodically by SEBI and the exchanges, so we state them explicitly and flag every time-sensitive figure for you to verify.

---

## 3. Core Concepts

### 3.1 What an index option is — the right, and the obligation

**What is it?** An **index option** is a standardised, exchange-traded contract between two parties, based on a stock index. There are two types:

* A **call option (CE)** gives its *buyer* the right — but not the obligation — to receive the value of the index above a fixed level (the **strike**) at expiry. The *seller* of the call takes on the matching obligation.
* A **put option (PE)** gives its *buyer* the right, not the obligation, to receive the value of the index below the strike at expiry. The *seller* takes the matching obligation.

The buyer pays a **premium** for this right. The seller receives that premium and, in exchange, is bound to pay out if the option finishes in the money.

**Why does it exist?** The option exists to slice risk into an *asymmetric* shape. A share (or a future) rises and falls symmetrically. An option lets the buyer cap the downside at the premium while keeping large upside, and lets the seller earn a certain premium in return for accepting a large, uncertain obligation. That asymmetry is the whole point — it is what makes options useful for both insurance and income.

**Why should a trader care?** Because the buyer and seller live in different worlds, and you must always know which one you are in. As a **buyer**, your maximum loss is the premium you paid — no margin calls, no nasty surprises beyond a known number. As a **seller**, your premium is capped but your loss can be many times larger, and you must post margin and can be called on to add more intraday. The same contract is a limited-risk lottery ticket for one side and an open-ended insurance liability for the other.

**Intuitive explanation.** Return to the insurance analogy from Chapter 1. A put buyer is like a homeowner buying flood insurance: a small, certain premium in exchange for a payout if disaster strikes. The put seller is the insurance company: it collects premiums from many homeowners and profits in calm years, but must pay out when the flood comes. Neither role is "better" — they are opposite ends of the same contract, and each suits a different purpose and temperament.

**Numerical example (preview).** Buy a NIFTY 24,500 call for ₹180 with a lot size of 65. You pay ₹180 × 65 = ₹11,700, and that ₹11,700 is the most you can lose. If NIFTY expires at 24,800, your call is worth (24,800 − 24,500) = 300 points, and you collect 300 × 65 = ₹19,500 — a ₹7,800 gross profit. We work the full set of outcomes in Section 5.

**Mathematical logic.** At expiry, ignoring costs:

```
Call payoff to the buyer  = max(0, Settlement − Strike) × Lot size
Put payoff to the buyer   = max(0, Strike − Settlement) × Lot size
```

The seller's payoff is the mirror image (premium received, minus whatever the buyer collects).

**Professional interpretation.** A desk does not see "a call" or "a put"; it sees a package of exposures. But even the most sophisticated trader never loses sight of the buyer/seller asymmetry in *risk*, because that asymmetry drives margin, capital, and survival — not just profit.

**Common mistake.** Beginners sell options to "collect the premium" because it feels like easy income, without registering that they have taken on the insurance company's role — capped reward, uncapped risk. Selling is a legitimate, often superior approach, but only with eyes open.

**Practical takeaway.** **Before anything else, know whether you are the buyer (limited, known risk) or the seller (limited reward, large risk).** That single fact governs your margin, your worst case, and your peace of mind.

---

### 3.2 European style and cash settlement

Two features define every Indian index option, and both differ from the American stock-option intuition many readers absorb from Western material.

**European-style exercise.** An option's *style* determines *when* it can be exercised. An **American-style** option can be exercised any day up to expiry; a **European-style** option can be exercised only *at* expiry. **All Indian index options are European.** This is not a minor technicality — it means you never have to worry about "early assignment," and it makes the options cleaner to price and to hold. If you buy a NIFTY put, no counterparty can force a settlement on you before the expiry date; you (and they) simply wait for expiry.

> **Beginner Alert — "Exercise" rarely means what beginners think.** You almost never "exercise" an index option by pressing a button. If your option has value at expiry, the exchange settles it automatically in cash. During its life, if you want to realise a profit or cut a loss, you do not exercise — you simply *sell the option back* in the market, exactly as you sell a share. Exercise happens once, at expiry, and it is automatic.

**Cash settlement.** You cannot deliver or receive an index — there is no certificate for "the NIFTY." So index options are **cash-settled**: at expiry the exchange calculates each option's intrinsic value against a specified settlement price and credits or debits your account in rupees. There is no transfer of shares, no delivery obligation, and — importantly — none of the physical-delivery machinery that applies to single-stock derivatives.

> **Market Note — Index vs. stock derivatives.** This book covers *index* products only. Single-stock futures and options in India are **physically settled** (shares actually change hands at expiry for in-the-money positions), which creates delivery and margin complications that index traders never face. Do not carry stock-option settlement intuition into index trading, or vice versa.

---

### 3.3 Reading an option symbol

Every contract has a name that fully specifies it. The house format used throughout this book is:

```
NIFTY               31JUL               24500          CE
  │                    │                  │            │
underlying      expiry date (DDMMM)     strike       right (CE = call, PE = put)
```

* **Underlying** — the index: NIFTY, BANKNIFTY, FINNIFTY, MIDCPNIFTY, or SENSEX.
* **Expiry date** — the day the contract dies, written day-then-month (e.g., `31JUL` = 31 July).
* **Strike** — the fixed level at which the option settles (e.g., 24500).
* **Right** — `CE` for a call, `PE` for a put.

So `NIFTY 31JUL 24500 CE` is "the NIFTY 24,500-strike call expiring on 31 July." Read it aloud that way every time until it is second nature.

> **Market Note — Symbols vary by platform.** Your broker or the exchange may encode the same contract slightly differently — some append the year, weekly and monthly formats differ, and older interfaces use a month-code. The *information* is always the same four fields. When in doubt, confirm the exact contract on your platform's order window before placing a trade.

---

### 3.4 Contract specifications — the five index products

An option is only as precise as its specifications. Table 2.1 summarises the five index option products. **Lot sizes and strike intervals are revised periodically by SEBI and the exchanges; the figures below are current as of the January 2026 lot-size revision and must be verified on the exchange before trading.**

**Table 2.1 — Index option products (current specifications, as of the Jan-2026 revision; verify current)**

| Product | Underlying index | Exchange | Lot size (units) | Near-ATM strike interval (pts) | Settlement | Style |
| --- | --- | --- | ---: | ---: | --- | --- |
| **NIFTY** | Nifty 50 | NSE | 65 | 50 | Cash | European |
| **BANKNIFTY** | Nifty Bank | NSE | 30 | 100 | Cash | European |
| **FINNIFTY** | Nifty Financial Services | NSE | 60 | 50 | Cash | European |
| **MIDCPNIFTY** | Nifty Midcap Select | NSE | 120 | 25 | Cash | European |
| **SENSEX** | BSE Sensex | BSE | 20 | 100 | Cash | European |

*Tick size is ₹0.05 for all (the smallest price step of the premium). The lot sizes above reflect the revision effective from the January 2026 contract series (NIFTY was cut from 75 to 65, BANKNIFTY from 35 to 30, FINNIFTY from 65 to 60, MIDCPNIFTY from 140 to 120; SENSEX stands at 20). Because SEBI re-sets lot sizes whenever an index's level drifts (to hold the contract value within its mandated band), they change without notice — confirm the current lot on the NSE/BSE website before every trade in a product you have not traded recently. Trading on a stale lot size means mis-sizing your position.*

A few features to internalise from the table:

* **Lot size** is the number of index units in one contract. It converts a per-unit premium into rupees: a premium of ₹120 on NIFTY (lot 65) means ₹7,800 per contract.
* **Strike interval** is the gap between adjacent strikes. NIFTY lists strikes every 50 points near the money (24,500 / 24,550 / 24,600 …); BANKNIFTY every 100.
* **Expiry cycle (current).** After SEBI's rationalisation (from 20 November 2024), **weekly** expiries survive on only one index per exchange — **NIFTY on the NSE** and **SENSEX on the BSE**; BANKNIFTY, FINNIFTY, and MIDCPNIFTY are **monthly only**. Since **1 September 2025**, the expiry *weekdays* are fixed by SEBI: **NIFTY expires on Tuesday** (weekly, and the monthly on the last Tuesday), while **SENSEX expires on Thursday** (weekly, and the monthly on the last Thursday). The NSE's monthly contracts for BANKNIFTY, FINNIFTY, and MIDCPNIFTY also settle on the last Tuesday. If an expiry day is a trading holiday, expiry moves to the previous trading day — verify the exact date on the exchange before you plan an expiry trade.

---

### 3.5 Moneyness, and the two parts of a premium

An option's premium is never a single mysterious number. It is always the sum of two parts.

**Intrinsic value** is what the option would be worth if it expired right now:

```
Call intrinsic value = max(0, Spot − Strike)
Put  intrinsic value = max(0, Strike − Spot)
```

**Time value** is everything else — the extra the market charges for the possibility that the option moves further in your favour before expiry:

```
Time value = Premium − Intrinsic value
```

**Worked breakdown.** With NIFTY at 24,620, the `24500 CE` trades at ₹185.

* Intrinsic value = 24,620 − 24,500 = **₹120**.
* Time value = 185 − 120 = **₹65**.

So of that ₹185, ₹120 is "real" (already in the money) and ₹65 is the market's price for time and uncertainty.

**Moneyness** classifies an option by where the spot sits relative to the strike:

* **In the money (ITM)** — has intrinsic value (a call with spot above strike; a put with spot below strike).
* **At the money (ATM)** — strike ≈ spot; almost all premium is time value.
* **Out of the money (OTM)** — no intrinsic value; premium is entirely time value (a call with spot below strike; a put with spot above strike).

We will not price time value formally in this chapter — that comes later in the book. For now, hold two facts: every premium splits into intrinsic + time value, and moneyness tells you which part dominates.

---

### 3.6 The underlying: an index futures foundation

You cannot understand index options deeply while treating the underlying as a single number on a ticker. The genuine underlying that options track is not the spot index but the **index future**. This subsection gives you the working knowledge of futures that the rest of the book assumes.

**What is a future?** An **index future** is a standardised contract to settle the difference between an agreed price and the index level at expiry. Unlike an option, a future is an **obligation on both sides** — there is no "right"; both buyer and seller are bound. It is the symmetric-payoff sibling of the option: if you are long one NIFTY future and the index rises 100 points, you gain 100 × lot size; if it falls 100, you lose 100 × lot size. No premium is paid to enter; instead, both sides post margin.

**Mark-to-market (MTM).** Here is the crucial mechanical difference from options. An option buyer pays a one-time premium and is done. A futures position is **marked to market every day**: the exchange settles the day's gain or loss in cash into your account each evening. Hold a future through a 150-point up-day and ₹(150 × lot) is credited that night; through a down-day, it is debited. Your profit or loss accrues daily, not just at exit.

**Spot, future, and the basis.** The futures price is tethered to the spot index by the cost of carrying a position to expiry:

```
Fair futures price:  F = S × e^(rT) − (dividends over the period)
Basis = F − S
```

where `S` is the spot index, `r` the risk-free rate, and `T` the time to expiry in years. The term `e^(rT)` is just the continuous-compounding growth factor — `e ≈ 2.718` is the base of natural growth, and `e^(rT)` is the multiplier for earning rate `r` over time `T`; over 30 days at 6.5% it is about **1.0054**, a whisker above 1. In plain terms: holding the index to expiry costs financing (which pushes the future *above* spot) but earns dividends (which pull it *below* spot). The **basis** is the net gap. Because the future must equal the spot at expiry, **the basis shrinks to zero as expiry approaches** — the two converge.

*(A note for the precise-minded: subtracting the dividends at their face value, as above, is a small approximation — a rigorous treatment discounts them to today, or writes the formula with a continuous dividend yield `q` as `F = S × e^((r − q)T)`. Over a few weeks the difference is negligible, and we use the simpler form throughout this chapter.)*

> **Beginner Alert — Why the future is usually a little above the spot.** Think of the future as "the index, plus the cost of financing it to expiry, minus the dividends you'd collect." For a broad index in a normal-rate environment, financing outweighs dividends, so the future trades slightly *above* the spot — a positive basis, called **contango**. Near a dividend-heavy stretch, dividends can catch up and the basis narrows or even turns negative — the future below the spot — which is called **backwardation**. Either way, it always meets the spot at expiry.

**Why options are priced off the future, not the spot.** Because a call-and-put combination replicates a forward position in the index, an option's fair value depends on where the market can *transact the index forward* — that is, the futures price `F`, which already contains carry and dividends. So option pricing uses `F`, not the raw spot `S`. This is why, later in the book, the pricing inputs are written in terms of the future.

**But settlement references the spot.** At expiry, index options are cash-settled against the **spot** index (a specified average of the spot on expiry day), and the future also converges to that same spot. So there is no contradiction: an option is *priced* off the future while it is alive, and *settled* to the spot at expiry — and since the basis is zero at expiry, the two descriptions meet.

**Futures as the hedging tool.** The future is the professional's instrument for neutralising the directional risk of an option position. If your option book has picked up unwanted directional exposure, you buy or sell futures to offset it, because futures give clean, linear, symmetric exposure to the index. (The precise sizing of such a hedge is developed later in the book; for now, register that *the future is how directional risk is switched on and off*.)

**The synthetic future.** Combining options reproduces a future. Buying a call and selling a put at the same strike and expiry gives a payoff identical to being long a future:

```
Long Call − Short Put (same strike, same expiry) ≈ Long Future
```

This is your first encounter with **put–call parity**, the identity that ties calls, puts, and futures together. We use it in Section 5 to build a synthetic future from real chain prices and check it against the actual future.

**Margin, in one line.** Both futures and short options require **margin** — collateral posted with the clearing corporation, computed under the SEBI **SPAN** framework plus an **exposure** add-on. Option *buyers* pay only the premium; *sellers* and futures traders post margin and can face intraday calls. The full margin machinery is treated later; the point here is that carrying an obligation costs collateral.

> **Market Note — Scope boundary.** Everything in this section is about *index* futures. Single-stock futures behave similarly but settle physically and have their own quirks; they are out of scope. When this book says "the future," it means the index future.

---

### 3.7 The cross-index liquidity map

A contract you cannot exit at a fair price is a trap, however clever your view. **Liquidity — not opinion — decides what you can actually trade**, and it varies enormously across the five products, across strikes, and across the days to expiry.

Two ideas frame it:

* **The tradable universe is narrower than the quoted universe.** The exchange lists hundreds of strikes, but only a band around the money trades with tight spreads and real depth. Far out-of-the-money and far-dated strikes may show a quote that you could never actually transact at in size. (The **bid–ask spread** is the gap between the best available buy price and sell price — in effect, the toll you pay to enter and exit; a wide spread is a guaranteed loss the moment you round-trip a position.)
* **Liquidity concentrates at the money and near expiry.** The ATM and nearby strikes of the current expiry are where volume and open interest cluster; spreads there are tightest. (**Open interest** is the number of contracts currently outstanding at a strike — a gauge of how much live activity is parked there.) Move away from the money, or out to a distant expiry, and spreads widen and depth thins.

Table 2.2 gives a representative picture. Exact spreads change constantly; treat this as a map of *relative* liquidity, not a quote sheet.

**Table 2.2 — Cross-index liquidity map (representative/illustrative; verify live)**

| Product | Overall liquidity | Where spreads are tight | Practical note for a retail account |
| --- | --- | --- | --- |
| **NIFTY** | Highest | ATM and ±a few strikes, all listed expiries | Deepest and friendliest; best place to learn and to size up |
| **SENSEX** | High | ATM near the weekly expiry | Grew rapidly after 2024; good depth around the money |
| **BANKNIFTY** | High (monthly only now) | ATM | Moves fast; tails widen quickly on volatile days |
| **FINNIFTY** | Moderate | ATM near expiry | Thins noticeably away from the money |
| **MIDCPNIFTY** | Lower | ATM only | Far strikes can be hard to exit; keep size small |

**A concrete illustration of spread-widening (illustrative).** On a calm day, a NIFTY ATM option might show a bid–ask spread of well under ₹1; a 2%-OTM strike a rupee or two; a 5%-OTM strike several rupees; and a far MIDCPNIFTY strike may barely trade at all. The wider the spread, the more you lose the instant you enter and exit — a cost that dwarfs brokerage in illiquid strikes.

**Practical rule.** For a beginner or a larger account, **stay in NIFTY (and SENSEX), around the money, in the current expiry.** Let liquidity, not the temptation of a cheap far strike, set your boundaries.

---

### 3.8 Settlement mechanics, and the "let it expire" trap

At expiry, every open index option is resolved by cash settlement. Three things happen:

1. **The settlement price is fixed.** The exchange computes a specified value of the underlying on expiry day — for NIFTY, an average of the spot index over a defined window (not simply the last traded price). This average is the number every option is measured against.
2. **In-the-money options are settled; out-of-the-money options expire worthless.** Every ITM option is automatically exercised against the settlement price and paid out in cash; every OTM option simply lapses.
3. **No shares move.** Because it is cash settlement, only rupees are debited and credited.

There is a cost subtlety here that catches many traders, and it is worth learning now.

**The "let it expire vs. square off" question — a trap that has moved.** Securities Transaction Tax (STT) is charged on a *different base* depending on how you close an ITM option:

* If you **square off** (sell the option in the market before expiry), STT is charged on the **premium** you sell at — the option-*sale* rate, **0.15% of premium** (from 1 April 2026).
* If you **let an ITM option expire** and it is exercised, STT is charged on the **intrinsic (settlement) value** — the *exercise* rate, **0.15% of the settlement value** (from 1 April 2026), levied on the *full in-the-money amount*, not the premium.

For years these two rates *differed* — exercise was taxed at 0.125% while a sale was taxed at just 0.0625%, later 0.1% — so letting a deep-ITM option expire cost meaningfully *more* STT than squaring it off. That was the classic "let-it-expire trap." **From 1 April 2026 the two rates are equal at 0.15%**, and because a deep-ITM option's sale premium is approximately its intrinsic value, the STT is now roughly the *same* whichever way you exit — so the old rate-driven penalty for letting an index option expire has largely disappeared. (In fact, because expiry escapes the exchange, SEBI, GST and brokerage charges that a *sale* attracts, letting it expire can now be marginally *cheaper* on total cost — Section 9.)

Two durable reasons to square off nonetheless remain: you **capture any residual time value** (which is simply forfeited at expiry), and you **control your exit price** rather than accept the expiry *settlement price* (the last-half-hour average, which can be worse than the live market on a volatile expiry day). *(STT rates change; the durable mechanism — sale STT on premium, exercise STT on the full intrinsic value — is the lesson. Verify current rates before relying on the numbers.)*

> **The bigger trap lives elsewhere.** The genuinely punishing exercise trap is in **physically-settled single-stock** options, where letting an ITM option expire triggers *delivery* and delivery-based STT (0.1%) on the *entire contract value* — often dwarfing the profit. Index options (this book's subject) are **cash-settled**, so that physical-delivery trap does not apply to them. We quantify the index-option case in Section 9.

---

## 4. Examples (Real-World)

**Example 1 — The same view, two instruments.** You are bullish on the NIFTY over the next two weeks. You could buy the near-month **future**, which gives you symmetric exposure with margin and daily MTM (a 100-point fall costs you 100 × lot that night). Or you could buy a **call**, paying a premium that caps your loss at that premium while keeping the upside. Same directional view; two very different risk shapes. Choosing between them *is* the craft.

**Example 2 — Why the future leads the option.** On an ordinary session, watch the NIFTY spot, the near-month future, and an ATM call together. The call's price tracks the *future* tick for tick, not the spot — because the future is what an option seller would use to hedge. When the basis is positive, an ATM call measured against the *spot* can look a shade rich; but it is not — that extra simply reflects the carry already embedded in the future the option is priced off, not a mispricing. Measure the option against the future and the puzzle disappears.

**Example 3 — Liquidity deciding a trade.** Two traders both want a cheap OTM hedge. One buys a NIFTY 5%-OTM put with a tight spread and exits easily a week later. The other buys a MIDCPNIFTY far-OTM put that looked cheaper, then finds no bid when they try to sell — the "cheap" option was cheap because almost no one trades it. The first trader respected the liquidity map; the second paid for ignoring it.

---

## 5. Numerical Examples

Illustrative setting: **NIFTY at 24,600**, **lot size 65** (verify current), figures **before transaction costs** except where stated.

### Numerical Example 1 — Buyer's payoff across three outcomes

You buy `NIFTY 31JUL 24500 CE` at a premium of **₹180**. Premium paid = 180 × 65 = **₹11,700** (your maximum loss).

| Settlement | Intrinsic (pts) | Payoff = intrinsic × 65 | P&L = payoff − ₹11,700 |
| ---: | ---: | ---: | ---: |
| 24,800 | 300 | ₹19,500 | **+₹7,800** |
| 24,500 | 0 | ₹0 | **−₹11,700** |
| 24,300 | 0 | ₹0 | **−₹11,700** |

**Interpretation.** Above the strike, profit grows one-for-one with the index. At or below the strike the call expires worthless and you lose the whole premium — no more, no less. Note how the loss is capped and known from the outset.

### Numerical Example 2 — The seller is the mirror image

You **sell** the same `24500 CE` at ₹180, receiving ₹11,700.

| Settlement | Buyer collects | Your P&L (seller) |
| ---: | ---: | ---: |
| 24,800 | ₹19,500 | 11,700 − 19,500 = **−₹7,800** |
| 24,500 | ₹0 | **+₹11,700** |
| 24,300 | ₹0 | **+₹11,700** |

**Interpretation.** Your best case is the ₹11,700 premium; your loss above the strike is open-ended. This is the buyer/seller asymmetry from Section 3.1 in numbers — and why the seller posts margin while the buyer does not.

### Numerical Example 3 — Breakevens

The **breakeven** is the settlement at which a bought option exactly recovers its premium.

* Call: breakeven = strike + premium. For the `24500 CE` at ₹180 → **24,680**. Above 24,680 the buyer is in profit.
* Put: breakeven = strike − premium. For `BANKNIFTY 52000 PE` at ₹350 → 52,000 − 350 = **51,650**. Below 51,650 the put buyer is in profit.

### Numerical Example 4 — Futures fair value and the basis

NIFTY spot **S = 24,600**, `r = 6.5%`, **T = 30/365** years (≈ 0.0822), expected dividends over the period ≈ 32 points.

```
S × e^(rT) = 24,600 × e^(0.065 × 0.0822) = 24,600 × e^(0.005342) ≈ 24,600 × 1.005356 ≈ 24,731.8
Fair future  F ≈ 24,731.8 − 32 ≈ 24,700
Basis = F − S ≈ 24,700 − 24,600 = +100 points
```

In practice the near-month future trades **very close to this fair value** — a small positive basis, or contango — precisely because arbitrage desks step in and sell it whenever it strays richer, and buy it whenever it strays cheaper. That enforcement is *why* the fair-value formula works. Near a dividend-heavy stretch, larger dividends pull `F` down and can shrink the basis toward zero or even flip it negative (backwardation).

### Numerical Example 5 — Building a synthetic future from the chain

At the 24,600 strike, suppose the call trades at **₹250** and the put at **₹150**.

```
Synthetic future = Strike + (Call − Put) = 24,600 + (250 − 150) = 24,700
```

The actual future also trades near **24,700** — so the synthetic and the real future **match**. That is put–call parity *holding*, and it is the point of the example: a call, a put, and a future are three views of the same underlying, and the market keeps them consistent. In live prices a point or two of bid–ask separates the synthetic from the future; a *large* gap would signal either a data-timing mismatch between the three quotes or a fleeting arbitrage that professional desks close within seconds — never standing free money for a retail trader.

### Numerical Example 6 — Daily mark-to-market on a future

You buy one NIFTY future at **24,700** (lot 65). The next day it settles at **24,850**.

```
MTM credited that evening = (24,850 − 24,700) × 65 = 150 × 65 = +₹9,750
```

Unlike an option premium (paid once), this profit is settled into your account **daily**. Had the future fallen to 24,600, ₹6,500 would have been *debited* that night — the discipline that funds the clearing guarantee.

---

## 6. Calculations (the reusable recipes)

**(a) Option buyer / seller P&L at expiry**

```
Call buyer P&L  = [max(0, Settlement − Strike) − Premium] × Lot size
Put  buyer P&L  = [max(0, Strike − Settlement) − Premium] × Lot size
Seller P&L      = − (Buyer P&L)          (the two sides sum to zero, before costs)
```

**(b) Breakeven**

```
Call breakeven = Strike + Premium
Put  breakeven = Strike − Premium
```

**(c) Premium decomposition**

```
Intrinsic value = max(0, Spot − Strike) for calls;  max(0, Strike − Spot) for puts
Time value      = Premium − Intrinsic value
```

**(d) Futures fair value and basis**

```
F = S × e^(rT) − (dividends over the period)
Basis = F − S     →    0 as expiry approaches
```

*(Dividends are subtracted at face value here for simplicity; a precise version discounts them, or uses a continuous dividend yield: `F = S × e^((r − q)T)`. The difference is negligible over a few weeks.)*

**(e) Futures MTM P&L**

```
Daily MTM = (Today's settle − Yesterday's settle) × Lot size    (symmetric; settled daily)
```

**(f) Synthetic future (put–call parity, practical form)**

```
Synthetic future price = Strike + (Call premium − Put premium)   [same strike, same expiry]
```

**(g) Scaling to lots** — every per-unit figure becomes rupees by multiplying by the lot size, and by the number of lots for a multi-lot position.

---

## 7. Practical Insights

* **The future is the true underlying.** When you watch an option's price, watch the *future*, not the spot. The option tracks the future because that is what a hedger transacts. Understanding this removes the mystery of why an ATM call is not simply "spot minus strike."
* **Know your lot size before your view.** The lot size converts points into rupees and is revised by SEBI without asking you. Confirm it every time you trade a product you have not traded recently; a stale lot size is a sizing error waiting to happen.
* **Cash settlement is a feature, not a footnote.** Because index options are European and cash-settled, there is no early assignment and no delivery — but there *is* the exercise-STT subtlety. Manage the exit deliberately.
* **Trade where the liquidity is.** The cheap far strike that never fills has cost far more traders than any single bad view. Anchor yourself in NIFTY/SENSEX, near the money, current expiry, until you have real reason to roam.
* **Options and futures are one family.** A call, a put, and a future are three expressions of the same underlying, linked by parity. Seeing them as a family — rather than as unrelated products — is the beginning of thinking like a professional.

> **Professional Insight — Why desks quote in futures terms.** Trading desks often express strikes and skew relative to the *future* and think in "future-equals-X" language, precisely because the future is the hedge and the pricing reference. When you eventually read professional commentary that says an option is "priced off the 24,700 future," you will now know exactly what that means and why the spot number is almost beside the point.

---

## 8. Common Mistakes

* **Selling options for "easy premium" without registering the role reversal.** Collecting premium feels like income until the flood arrives. Selling is the insurance company's business — capped reward, large risk, margin, and possible intraday calls.
* **Importing American-style / physical-delivery intuition.** Indian index options are European and cash-settled. There is no early assignment and no share delivery; expecting either leads to confused decisions.
* **Assuming the old "let-it-expire STT trap" still bites index options.** Exercise STT is charged on the *full intrinsic value* and a sale on the *premium*; since 1 April 2026 both are 0.15%, so for a cash-settled index option the two exits cost about the same on STT (and expiry can even be marginally cheaper). Square off to capture residual time value and control your exit price — not to dodge an STT penalty that, for index options, has largely gone. (The real delivery-STT trap is in physically-settled single-stock options.)
* **Trading on a stale lot size.** After the repeated 2024–2026 revisions (NIFTY 25 → 75 → 65, and so on), a position sized on last year's lot is mis-sized. Always confirm the current lot.
* **Chasing cheap, illiquid far strikes.** A wide spread is a guaranteed loss on entry and exit, and a "no bid" at exit turns a small hedge into a stuck position. Cheapness usually reflects low liquidity and low odds, not a bargain.
* **Confusing the two meanings of settlement.** Options are *priced* off the future during their life but *settled* to the spot average at expiry. Mixing these up leads to wrong expectations about the closing value.

---

## 9. Case Study — One complete NIFTY trade, order to settlement, all charges

**Context.** On a Wednesday with NIFTY at **24,600** and the NIFTY weekly expiry the coming Tuesday, you are bullish and buy **one lot** of `NIFTY 24600 CE` at a premium of **₹120** (lot size 65). Your maximum loss is the premium, ₹120 × 65 = **₹7,800**. NIFTY rallies over the next few sessions.

We follow the trade to the end down **two different exits** to compare the "let it expire" and "square off" routes. Charges use **illustrative rates as of 2026** — brokerage ₹20 per order; STT 0.15% on option sale (premium) and 0.15% on exercise (intrinsic), both equalised from 1 April 2026; exchange transaction charge ≈ 0.035% of premium; SEBI fee ≈ 0.0001% of premium; stamp duty 0.003% on the buy side; GST 18% on (brokerage + transaction + SEBI fee). **Verify all current rates before relying on them.**

**The buy leg (common to both exits).** Premium value = 120 × 65 = ₹7,800.

| Charge | Basis | Amount (₹) |
| --- | --- | ---: |
| Brokerage | flat | 20.00 |
| STT (buy) | none on option purchase | 0.00 |
| Exchange txn | 0.035% × 7,800 | 2.73 |
| SEBI fee | 0.0001% × 7,800 | 0.01 |
| Stamp duty | 0.003% × 7,800 | 0.23 |
| GST | 18% × (20 + 2.73 + 0.01) | 4.09 |
| **Buy-side charges** | | **≈ 27.06** |

### Exit A — Square off before expiry

A couple of sessions later NIFTY is at 24,900; you **sell** the call at ₹300. Premium value = 300 × 65 = ₹19,500.

| Charge | Basis | Amount (₹) |
| --- | --- | ---: |
| Brokerage | flat | 20.00 |
| STT (sell) | 0.15% × 19,500 | 29.25 |
| Exchange txn | 0.035% × 19,500 | 6.83 |
| SEBI fee | 0.0001% × 19,500 | 0.02 |
| Stamp duty | none on sell | 0.00 |
| GST | 18% × (20 + 6.83 + 0.02) | 4.83 |
| **Sell-side charges** | | **≈ 60.93** |

* Gross P&L = (300 − 120) × 65 = **₹11,700**.
* Total charges ≈ 27.06 + 60.93 = **₹87.99**.
* **Net P&L ≈ 11,700 − 88 = ₹11,612.**

### Exit B — Let it expire in the money (cash settlement)

You hold to the Tuesday expiry; the settlement price is **24,900**, so intrinsic value = 300 points and intrinsic settlement value = 300 × 65 = ₹19,500. The option is auto-exercised.

* STT on **exercise** = 0.15% × 19,500 = **₹29.25** — the *same* 0.15% a sale would pay, but levied on the intrinsic value.
* Buy-side charges as before ≈ ₹27.06. (An exercised option incurs no brokerage, exchange, SEBI or GST on the settlement leg — only STT.)
* Gross settlement gain = (24,900 − 24,600) × 65 = **₹19,500**; less premium paid ₹7,800 = ₹11,700 gross.
* **Net P&L ≈ 11,700 − 27.06 − 29.25 ≈ ₹11,644.**

**The lesson.** Read the two exits carefully. Since April 2026 the sale and exercise STT rates are *equal* (0.15%), so the STT is about the same either way — and because letting the option expire escapes the exchange, SEBI, GST and brokerage that the sell order in Exit A attracts, **Exit B (letting it expire) actually nets a little *more* — ₹11,644 versus ₹11,612.** This *reverses* the old advice: before April 2026, exercise was taxed at a higher rate (0.125% versus 0.1% on a sale) on the full intrinsic value, so letting a deep-ITM option expire was the expensive route. Now it is marginally the *cheaper* one — and the reversal holds even deep in the money. Imagine the settlement leaves the option 1,500 points in the money (intrinsic value = 1,500 × 65 = ₹97,500): exercise STT is 0.15% × 97,500 = **₹146.25**, essentially the *same* STT a sale would pay on the near-identical premium — but the sale would add exchange, SEBI, GST and brokerage on top (~₹60 more), so squaring off costs *more*, not less. **So the reason to square off a cash-settled index option is no longer STT: it is to capture any residual time value and to control your exit price rather than accept the expiry settlement average.** (The costly exercise trap that still bites is in *physically-settled single-stock* options — delivery STT on the full contract value — not in cash-settled index options.)

*(Takeaway: cost is part of the trade, not an afterthought. The same gross P&L nets out differently by exit route — and a rule that was true under one tax regime can reverse under the next, so always re-check the current rates.)*

---

## 10. Chapter Summary

* An **index option** is a standardised, exchange-traded contract: the **buyer** pays a premium for a right (limited, known risk); the **seller** receives it and takes on an obligation (limited reward, large risk).
* All Indian index options are **European** (exercised only at expiry) and **cash-settled** (no delivery); do not import American-style or physical-delivery intuition.
* A contract is fully defined by its **specifications** — lot size, tick, strike interval, expiry cycle, settlement — which SEBI revises periodically; weekly expiries survive only on **NIFTY (NSE, expiring Tuesday)** and **SENSEX (BSE, expiring Thursday)**, with BANKNIFTY, FINNIFTY, and MIDCPNIFTY monthly-only (last Tuesday on the NSE).
* Every premium splits into **intrinsic value** and **time value**, and **moneyness** (ITM/ATM/OTM) tells you which dominates.
* The true underlying is the **index future**: an obligation on both sides, marked to market daily, tied to spot by the **basis** `F = S·e^(rT) − dividends`, which converges to zero at expiry.
* Options are **priced off the future** (which embeds carry and dividends) but **settled to the spot** at expiry; a **synthetic future** (`Strike + Call − Put`) shows calls, puts, and futures are one family.
* **Liquidity decides what you can trade**: stay in NIFTY/SENSEX, near the money, current expiry, until you have reason to roam.
* Settlement carries a cost subtlety — **sale STT is charged on premium, exercise STT on the full intrinsic value**; since both rates equalised at 0.15% (1 April 2026), the two exits cost about the same for a cash-settled index option, so **square off to capture residual time value and control your exit price**, not to save STT (the punishing exercise/delivery-STT trap now lives in *physically-settled single-stock* options).

---

## 11. Key Takeaways

* **Always know your side.** Buyer = limited, known risk; seller = limited reward, open-ended risk and margin. Everything else follows from this.
* **Read the future, not the spot.** The option tracks the future; the basis explains the gap; both meet the spot at expiry.
* **Confirm the lot size and specifications before every trade.** They are revised without your permission, and a stale lot size is a sizing error.
* **Let liquidity draw your boundaries, and exit deep-ITM options by squaring off.** Trade where you can get filled, and manage the settlement cost deliberately.

---

## 12. Practice Questions

**Q1 (Concept).** In one sentence each, state the essential difference between an option and a future in terms of *rights and obligations*.

**Q2 (Multiple choice).** All Indian index options are:
(a) American-style, physically settled; (b) European-style, cash-settled; (c) American-style, cash-settled; (d) European-style, physically settled.

**Q3 (Symbol reading).** Decode `NIFTY 07AUG 24700 PE`. What is the underlying, expiry, strike, and right?

**Q4 (Premium decomposition).** NIFTY is at 24,680. The `24500 CE` trades at ₹210. Compute the intrinsic value and the time value, and state the option's moneyness.

**Q5 (Numerical — buyer P&L).** You buy `NIFTY 24600 CE` at ₹140 (lot 65). Compute your P&L if NIFTY settles at (a) 24,900, (b) 24,600, (c) 24,400.

**Q6 (Numerical — breakeven).** Find the breakeven for (a) a 24,600 call bought at ₹140 and (b) a 24,600 put bought at ₹160.

**Q7 (Numerical — futures fair value).** With S = 24,600, r = 6.5%, T = 20/365, and dividends ≈ 15 points, estimate the fair futures price and the basis.

**Q8 (Numerical — synthetic future).** At the 24,600 strike, the call is ₹230 and the put is ₹132. Compute the synthetic future price. If the actual future is 24,700, comment on the gap.

**Q9 (Settlement cost).** You hold a deep-ITM `NIFTY 24000 CE` and the settlement price is 25,200 (lot 65). Since 1 April 2026 the sale and exercise STT rates are equal at 0.15%. Explain what that did to the old "square off to save STT" rule, and give the reasons that still favour squaring off a cash-settled index option.

**Q10 (Judgement).** A friend wants to buy a far-OTM MIDCPNIFTY option "because it's the cheapest thing on the screen." Give two liquidity-based reasons to be cautious.

---

## 13. Detailed Solutions

**A1.** A **future** is an obligation on *both* buyer and seller to settle the index difference at expiry (symmetric, no premium). An **option** gives its *buyer* a right (not an obligation) in exchange for a premium, while the *seller* carries the matching obligation (asymmetric).

**A2.** **(b) European-style, cash-settled.** They can be exercised only at expiry and are settled in rupees against a specified spot settlement price.

**A3.** Underlying = **NIFTY**; expiry = **7 August**; strike = **24,700**; right = **PE (put)**. It is "the NIFTY 24,700-strike put expiring 7 August." (Your platform may append the year or use a different encoding — confirm on the order window.)

**A4.** Intrinsic value = 24,680 − 24,500 = **₹180**; time value = 210 − 180 = **₹30**. Spot is above the strike for a call, so it is **in the money (ITM)**.

**A5.** Premium paid = 140 × 65 = ₹9,100.
(a) Intrinsic = 300 → payoff 300 × 65 = ₹19,500; P&L = 19,500 − 9,100 = **+₹10,400**.
(b) Intrinsic = 0 → **−₹9,100**.
(c) Intrinsic = 0 → **−₹9,100**.

**A6.** (a) Call breakeven = 24,600 + 140 = **24,740**. (b) Put breakeven = 24,600 − 160 = **24,440**.

**A7.**
```
S × e^(rT) = 24,600 × e^(0.065 × 20/365) = 24,600 × e^(0.003562) ≈ 24,600 × 1.003568 ≈ 24,687.8
Fair future F ≈ 24,687.8 − 15 ≈ 24,673
Basis = 24,673 − 24,600 = +73 points (approx.)
```
A small positive basis (contango), as expected in a normal-rate environment.

**A8.** Synthetic future = 24,600 + (230 − 132) = **24,698**. The actual future at 24,700 is only ~2 points higher, so **put–call parity essentially holds** — the synthetic and the real future agree. That tiny residual is bid–ask across the three instruments (and the small discounting term the simplified formula omits), not a free arbitrage: any real gap wide enough to trade would be closed by professional desks in seconds.

**A9.** Exercise STT = 0.15% on the **intrinsic settlement value** = (25,200 − 24,000) × 65 = 1,200 × 65 = ₹78,000, i.e., 0.15% × 78,000 = **₹117.00**. A square-off pays 0.15% on the **sale premium**, which for a deep-ITM option ≈ its intrinsic value — so the STT is essentially the *same* either way. Before April 2026 exercise (0.125%) was taxed at a higher rate than a sale (0.1%), which made letting it expire the expensive route; **equalising both rates at 0.15% closed that gap**, and since squaring off *adds* the exchange, SEBI, GST and brokerage that exercise avoids, letting it expire is now marginally *cheaper* on cost. So the STT reason to square off has gone; the reasons that remain are to **capture residual time value** (forfeited at expiry) and to **control your exit price** rather than accept the settlement average. (The large exercise/delivery-STT trap still applies to *physically-settled single-stock* options, not to cash-settled index options.) *(Rates illustrative; verify current STT schedule.)*

**A10.** Two liquidity reasons: (i) Far-OTM MIDCPNIFTY strikes often have **wide bid–ask spreads**, so you lose a large fraction of the premium on entry and exit. (ii) They can have **little or no depth** — you may find *no bid* when you try to sell, leaving you stuck in the position. "Cheapest on the screen" usually signals low liquidity and low odds of paying off, not value.

---

## 14. Mini Glossary

* **Index option** — a standardised, exchange-traded contract based on a stock index; a call (CE) or a put (PE). → this chapter.
* **Call option (CE)** — gives the buyer the right to the index's value above the strike at expiry. → this chapter.
* **Put option (PE)** — gives the buyer the right to the index's value below the strike at expiry. → this chapter.
* **Strike** — the fixed reference level at which an option settles. → this chapter.
* **Premium** — the price of an option per unit; paid by the buyer, received by the seller. → this chapter.
* **Lot size** — the number of index units in one contract; converts per-unit premium into rupees. → this chapter.
* **Tick size** — the smallest permissible price step of the premium (₹0.05 for index options). → this chapter.
* **Strike interval** — the gap between adjacent listed strikes. → this chapter.
* **European-style** — exercisable only at expiry; the style of all Indian index options. → this chapter.
* **Cash settlement** — settling in rupees against a settlement price, with no delivery of the underlying. → this chapter.
* **Intrinsic value** — the in-the-money amount: max(0, Spot − Strike) for calls, max(0, Strike − Spot) for puts. → this chapter.
* **Time value** — premium minus intrinsic value; the market's price for remaining time and uncertainty. → this chapter.
* **Moneyness (ITM/ATM/OTM)** — the strike's position relative to spot. → this chapter.
* **Index future** — an obligation on both sides to settle the index difference at expiry; marked to market daily. → this chapter.
* **Mark-to-market (MTM)** — daily cash settlement of a futures position's gain or loss. → this chapter.
* **Basis** — the gap between the futures price and the spot (F − S); converges to zero at expiry. → this chapter.
* **Cost of carry** — the net of financing cost and dividends that sets the fair futures price. → this chapter.
* **Synthetic future** — a futures-equivalent position built from options: Strike + (Call − Put). → this chapter.
* **Put–call parity** — the identity linking calls, puts, and futures at the same strike and expiry. → this chapter.
* **Settlement price** — the specified value of the underlying at expiry against which options are settled. → this chapter.
* **STT (Securities Transaction Tax)** — a tax on securities transactions; charged on option premium at sale and on intrinsic value at exercise. → this chapter.
* **Liquidity** — the ease of trading a contract at a fair price; concentrated at the money and near expiry. → this chapter.

---

<!-- End of Chapter 2 (Rev 4, book-wide audit 5-7 Aug 2026). Rev 4 (STT overhaul): §3.3 "let-it-expire" subsection, Common Mistake, case study, Q9/A9, and Summary reframed for the 1 Apr 2026 STT equalisation — sale 0.1%→0.15% (premium base), exercise 0.125%→0.15% (intrinsic base). Because both rates are now 0.15% and a deep-ITM sale premium ≈ intrinsic, the old rate-driven "let-it-expire trap" has CLOSED for cash-settled index options; letting expire is now marginally CHEAPER (avoids exchange/SEBI/GST/brokerage), so the case study conclusion REVERSED (Exit A square-off net 11,612 vs Exit B expire net 11,644; deep-ITM 97,500 → exercise STT 146.25 ≈ sale STT, but sale adds ~₹60 more). New durable lesson: square off to capture residual time value + control exit price, not to save STT; the punishing exercise/delivery-STT trap now lives in physically-settled single-stock options. A9 exercise STT 78,000×0.15% = ₹117.00. Verified vs Budget 2026 STT amendment (eff 1 Apr 2026). --- Rev 3 updates (verified vs NSE circular FAOP70616 and SEBI expiry-day reform): (1) Lot sizes updated to Jan-2026 revision — NIFTY 75→65, FINNIFTY 65→60 (BANKNIFTY 30, MIDCPNIFTY 120, SENSEX 20 unchanged); Table 2.1 and all lot-dependent numbers recomputed — preview (180×65=11,700; 300×65=19,500; +7,800), NE1/NE2 (max loss 11,700; +7,800/−11,700), NE6 (150×65=9,750; down 6,500), case study (buy 27.06; Exit A net 11,622; Exit B net 11,649; deep-ITM 97,500 → STT 121.88 vs 97.50), Q5/A5 (9,100; +10,400), Q9/A9 (78,000 → 97.50). NE3-NE5, Q6-Q8 have no lot dependence (unchanged; parity numbers retained). (2) Expiry framework updated: since 1 Sep 2025, NIFTY expires Tuesday (weekly + last-Tuesday monthly), SENSEX Thursday; BANKNIFTY/FINNIFTY/MIDCPNIFTY monthly-only on last Tuesday. §3.4, case-study context, and Summary corrected (case study "Thursday" → "Tuesday"). (3) Table note and headers redated to Jan-2026/2026. Rev 2 fixes retained (NE4/NE5 parity reconciliation, e^(rT) gloss, dividend approximation note, contango/backwardation, OI & bid-ask glosses). STT 0.1% sale / 0.125% exercise; tick ₹0.05. IV reserved for implied volatility; intrinsic value spelled out. Costs net per all-in-cost rule. -->
