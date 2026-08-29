<!-- Difficulty: Level 1/5 (Beginner). Dependency: none (entry point). Target length ~7,000 words. All time-sensitive figures (rates, lot sizes, rules, turnover) are dated and flagged "verify current". HOUSE BASELINE for this chapter: NIFTY 24,600, lot size 65 (current per NSE revision effective Jan 2026). NOTE: Chapters 2-30 still use the older lot size 75 as their baseline and need the same lot-size refresh (65) plus the Sept-2025 expiry-day update in a later pass, for book-wide consistency. -->

# Chapter 1 — The Indian Derivatives Market: Why It Exists and Why It Matters

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Explain why derivative markets exist and the economic work they do — price discovery, risk transfer, and speculation.
2. Trace the history of Indian derivatives from the launch of index futures in 2000 to the reforms of 2024–2026.
3. Describe the scale of the Indian market and why India is the world's largest options market by the number of contracts traded.
4. Distinguish exchange-traded derivatives from over-the-counter (OTC) instruments.
5. Identify the role of SEBI as the regulator and of the clearing corporations as the guarantors that stand behind every trade.

This is a conceptual chapter. There are no pricing formulas to memorise. There is, however, a handful of simple arithmetic every serious participant should be able to do in their head — the difference between *notional* value and the *premium* actually at stake, and how a hedge offsets a loss. We will work those out carefully.

---

## 2. Introduction

On the morning of 24 March 2020, the India VIX — the market's fear gauge — closed near **83.6**, its highest reading on record. Over the previous nine weeks the NIFTY 50 — India's benchmark stock index, a basket of the 50 largest listed companies that serves as the country's market barometer — had fallen from roughly **12,362** in late January to about **7,610**, a decline of nearly **38%**. Portfolios that had compounded quietly for years lost a third of their value in a few sessions.

Two investors held the same basket of Indian shares going into that crash. The first did nothing but watch. The second, weeks earlier, had spent a little over 1% of the portfolio's value buying NIFTY put options. When the market fell, the first investor absorbed the full loss. The second investor's puts rose in value almost exactly as fast as the portfolio fell, so the net damage was limited to the small amount paid for the puts. Same shares, same crash, very different outcomes — and the only difference was a derivative.

That is what this book is about: the instruments that let you transfer risk you do not want, take on risk you are paid for, and express a view with precision. Before we can trade a single NIFTY option intelligently, we need to understand the arena it lives in — what a derivative actually is, why the market exists at all, who stands behind your trade so that a stranger on the other side cannot default on you, and why India, of all places, became the busiest options market on earth.

This chapter builds that mental map. It is deliberately short on jargon and long on plain reasoning. Everything that follows in this book — every Greek, every strategy, every risk rule — assumes you understand the ground you are standing on.

---

## 3. Core Concepts

### 3.1 What a derivative is, and why derivatives exist

**What is it?** A **derivative** is a financial contract whose value is *derived* from something else — an underlying asset, rate, or index. A NIFTY option has no independent worth; its value comes entirely from the level of the NIFTY 50 index. Change the index, and the option's value changes. Remove the index, and the option is a meaningless piece of paper.

**Why does it exist?** Derivatives exist to do three things that the ordinary "cash" market (buying and selling the shares themselves) does poorly:

* **Transfer risk.** A mutual fund holding ₹500 crore of shares cannot sell them overnight without crashing the price. It *can* buy NIFTY futures or options in minutes to neutralise the risk of a market fall, then remove the hedge later. The risk moves to someone willing to bear it, without a single share changing hands.
* **Discover price.** Because derivatives are cheap to trade and highly leveraged, informed opinion flows into them fast. For example, when large participants expect a sharp move around an upcoming policy meeting, the prices of that week's options rise *before* the event — the market is signalling expected turbulence through option prices, a live forecast you can read straight off the screen, often sooner and more honestly than any single analyst's note.
* **Provide leverage and access.** A derivative lets you take a large economic position for a small outlay. That is powerful and dangerous in equal measure, and most of this book is about handling that power without being destroyed by it.

**Why should a trader care?** Because the derivative is the *tool*, and the tool determines what jobs you can do. If your only instrument is buying and selling shares, you can profit only when prices rise (or fall, if you can short). With options you can also profit from a market that stays flat, from a rise in fear, from the mere passage of time. Each of those is a different job, and each needs a different tool. Understanding derivatives is understanding your toolbox.

**Intuitive explanation.** Think of a derivative as *insurance on a price*. When you insure a car, you do not buy or sell the car — you buy a contract whose payout depends on what happens to the car. A NIFTY put option is insurance on the value of the market: you pay a premium, and if the market falls below an agreed level, the contract pays you. A NIFTY call option is the mirror image — a contract that pays if the market rises above an agreed level. The insurance analogy will carry you a surprisingly long way.

> **Market Note — Two shapes of derivative: an obligation and a right.** The two building blocks you will meet throughout this book are *futures* and *options*. A **future** is a firm two-way commitment: both sides are obliged to settle at expiry, so their gains and losses are symmetric — if the index moves one way the buyer gains what the seller loses, and vice versa. An **option** gives its buyer a *right without obligation*: the buyer can simply walk away and lose only the premium, which makes the payoff *asymmetric*. The insurance analogy above is really an analogy for an *option*; a future is more like a fixed forward deal that neither side can back out of. We build both instruments up properly later in the book — for now, hold the one-line distinction: **futures obligate; options entitle.**

> **Market Note — Index derivatives are cash-settled.** You never take or give delivery of "the NIFTY," because you cannot hold an index in a demat account (the electronic account that holds your shares). Indian *index* options and futures are settled in cash: at expiry, the exchange computes what the contract is worth and debits or credits your account in rupees. (Single-stock derivatives are different — they are physically settled — but this book is about index products only.)

**Numerical example (preview).** We work the full numbers in Sections 5 and 6, but here is the shape of it: one NIFTY call option quoted at ₹120, with a lot size of 65, costs ₹120 × 65 = **₹7,800** to buy — yet it tracks the fate of **₹15,99,000** worth of index. That gap between what you pay and what you control is the essence of a derivative.

**Mathematical logic (no calculus needed).** A derivative's value is a *function of* the underlying. For a call option held to expiry, the payoff is `max(0, Settlement − Strike)`; for a put, `max(0, Strike − Settlement)`. The word "derived" is literal: the payoff is computed *from* the underlying's level. Everything else in options pricing is an elaboration of this single idea.

**Professional interpretation.** Professionals rarely think of a derivative as a bet on direction. They think of it as a bundle of *exposures* — to direction, to volatility, to time — that can be assembled and taken apart. A market maker may hold thousands of options with almost no view on where the NIFTY is going; their edge is in pricing and managing the bundle, not in predicting the index.

**Common mistake.** Beginners treat an option as "a cheap way to buy the market." It is not. It is a *different* instrument with a fixed lifespan and a value that erodes with time. Confusing the two is the root of most first-year losses.

**Practical takeaway.** **A derivative is a contract about a price, not the thing itself.** Learn to see the underlying, the contract, and the link between them as three separate objects.

---

### 3.2 The three reasons anyone trades: hedging, speculation, arbitrage

Every derivative trade, without exception, is placed for one of three reasons. Knowing which one *you* are doing on any given trade is the beginning of discipline.

**Hedging.** You already hold a risk and you want to reduce it. The investor in the introduction who bought NIFTY puts against a share portfolio was hedging. A hedger accepts a small, known cost (the premium) to remove a large, uncertain one (the crash). Hedgers are the reason the market exists at all.

**Speculation.** You do not hold the underlying risk; you take it on deliberately because you have a view and expect to be paid for it. A retail trader who buys a NIFTY call expecting a rally is speculating. There is nothing shameful in the word — speculators provide the liquidity that lets hedgers hedge — but speculation is where almost all retail money is lost, precisely because it is voluntary risk.

**Arbitrage.** You spot the same economic value priced two ways and lock in the difference with little or no risk. If a NIFTY future trades meaningfully above its "fair" value relative to the cash index, an arbitrageur buys the cheaper leg and sells the dearer one and pockets the gap. True arbitrage is largely the domain of well-capitalised, low-cost professional desks; for retail traders it is mostly a concept to understand, not a living to make.

> **Professional Insight — Name your motive before you click.** Desk traders are trained to state, out loud, why a trade is going on: "This is a hedge," or "This is a directional speculation, sized at half a percent of capital." The single most common way retail traders drift into trouble is starting a trade as a "hedge" or a "quick scalp" and quietly letting it become an un-sized directional bet. Decide the motive first; it dictates the size, the stop, and the exit.

---

### 3.3 Derivatives are (nearly) a zero-sum game

Here is an uncomfortable but essential truth. When you buy shares of a growing company, both you and the person who sold them to you can prosper over time, because the underlying business creates value. A derivative creates no value. It is a contract between two parties: for every rupee one side gains, the other side loses the same rupee.

**Before costs, derivatives trading is zero-sum. After costs, it is negative-sum for participants as a group.** Every trade carries brokerage, Securities Transaction Tax (STT), exchange charges, GST, a SEBI turnover fee, and stamp duty. Those costs leave the pool of participants and go to intermediaries and the government. So the average rupee traded by the crowd loses a little to friction, always.

This is not a reason to avoid derivatives — hedgers gladly "lose" to friction the way you gladly pay a premium for car insurance. It *is* the reason to be sober. You are not investing in a rising tide that lifts everyone; you are competing for a pot that shrinks slightly with every transaction, often against faster, cheaper, better-informed counterparties.

> **Market Note — What SEBI's own data shows.** SEBI's study released in January 2023 found that roughly **89% of individual F&O (Futures and Options) traders** lost money in FY2022, with an average net loss of over ₹1 lakh each. A follow-up study in September 2024 found the picture had worsened: **more than 90%** of individual traders lost money over FY2022–FY2024, with aggregate net losses of about **₹1.81 lakh crore** across those three years. (Figures are as reported by SEBI on those dates; consult the latest SEBI study for current numbers.) Treat these as the base rate you are trying to beat, not as a footnote.

---

### 3.4 Exchange-traded versus OTC, and the guarantee behind your trade

Derivatives come in two broad forms.

* **Over-the-counter (OTC)** derivatives are private, bespoke contracts negotiated directly between two parties — say, a bank and a corporate customer arranging a currency forward. They are flexible but carry **counterparty risk**: if the other side goes bankrupt, your contract may be worthless.
* **Exchange-traded** derivatives are *standardised* contracts bought and sold on a public exchange (NSE or BSE in India). Everyone trades the same specifications — same lot size, same strikes, same expiry dates — which concentrates liquidity and makes prices transparent.

Every NIFTY, BANKNIFTY, FINNIFTY, MIDCPNIFTY, and SENSEX option you will ever trade is exchange-traded. And exchange-traded derivatives solve the counterparty problem with a mechanism that is easy to miss but absolutely central:

**What is it?** When your buy order matches someone's sell order, the **clearing corporation** steps into the middle. It becomes the buyer to every seller and the seller to every buyer. This substitution is called **novation**.

**Why should a trader care?** Because it means you are never actually exposed to the stranger on the other side of your trade. You face the clearing corporation, which is heavily capitalised, collects margins from all participants daily, and maintains a settlement guarantee fund. Even if your counterparty defaults, you get paid. This is why you can sell an option to an anonymous account and sleep at night.

In India:

* The **National Stock Exchange (NSE)** is cleared by **NSE Clearing Limited (NCL)**.
* The **Bombay Stock Exchange (BSE)** is cleared by the **Indian Clearing Corporation Limited (ICCL)**.
* Sitting above both, **SEBI (the Securities and Exchange Board of India)** is the regulator — it writes the rules on margins, position limits, product design, and investor protection, and it has reshaped this market repeatedly (Section 3.6).

> **Professional Insight — The guarantee is not free.** The clearing corporation eliminates counterparty risk by demanding *margin* from anyone carrying risk, and by revaluing positions daily (marking to market). That is why an option *seller* must post margin and can face a margin call intraday, while an option *buyer*, whose maximum loss is the premium already paid, does not. The guarantee that protects you is funded by the discipline it imposes on you.

---

### 3.5 The scale of the Indian market — and the notional illusion

India is, by the number of contracts traded, the largest derivatives market in the world. The NSE has ranked as the world's largest derivatives exchange by contract volume for several consecutive years (per the Futures Industry Association's annual data, from around 2019 onward), driven overwhelmingly by equity **index options**. By some measures, India accounts for the majority of all equity index option contracts traded globally.

But raw scale is routinely misreported, and understanding *why* is your first piece of real market literacy.

Newspapers love to print enormous "turnover" numbers for options. Almost always, these are **notional turnover** — the full face value of the index that all the traded contracts *control* — not the money actually put at risk. The money actually changing hands is the **premium turnover**, which is a tiny fraction of the notional. We compute both in Section 5. The gap is roughly two hundred to one. When you read that index options "turned over ₹X lakh crore," you are almost never reading a number about money at stake.

**Why India became number one.** Several forces combined:

* **Low ticket size.** For years, index option premiums were small enough that a trader could take a position for a few thousand rupees — sometimes a few hundred. The barrier to entry was almost zero.
* **Weekly expiries.** From 2016 onward, the introduction of weekly-expiring options (Section 3.6) created a fresh, cheap, fast-decaying lottery every few days, which retail traders found irresistible.
* **The discount-broker and smartphone revolution.** Zero- or flat-fee brokers, instant online account opening, and mobile trading apps brought tens of millions of new participants to the market in a few years.
* **Leverage and the lure of the quick multiple.** Cheap out-of-the-money options — those struck far from the current index level, so they carry no intrinsic value yet and cost very little — can, occasionally, multiply many times over. The rare winner is vivid; the common loser is quiet.

That explosion is also why SEBI intervened.

---

### 3.6 Weekly expiries and the 2024–2026 SEBI reforms

**Expiry** is the date on which an option contract ceases to exist and is settled. For most of the market's history, index options expired **monthly**. That changed in stages:

* **May 2016** — the NSE introduced **weekly options on BANKNIFTY**, the first weekly index options in India.
* **February 2019** — **weekly NIFTY options** were launched.
* By the early 2020s, with weekly contracts on several indices staggered across the week, there was effectively an index option **expiring almost every trading day**. Expiry days concentrate cheap, fast-moving contracts, and volumes ballooned around them.

By 2024, SEBI concluded that the frenzy of daily expiries was fuelling speculative losses among retail participants without a matching benefit. In a circular in **October 2024**, "Measures to Strengthen the Equity Index Derivatives Framework," it introduced a package of changes rolled out over the following months. The headline measures:

* **One weekly expiry per exchange.** From **20 November 2024**, each exchange could offer weekly-expiring options on only **one** benchmark index. The NSE retained weekly expiries on **NIFTY**; the BSE retained them on **SENSEX**. Weekly expiries on BANKNIFTY, FINNIFTY, and MIDCPNIFTY were discontinued, leaving those products with **monthly** expiries only.
* **Standardised expiry days.** In a further step, effective **1 September 2025**, SEBI required every equity-derivative expiry to fall on either a Tuesday or a Thursday. The NSE moved its entire F&O segment — NIFTY's weekly *and* monthly expiries alike — to **Tuesday**, while the BSE moved **SENSEX to Thursday**, ending the market's 25-year association of Thursday with expiry day.
* **Larger contract sizes.** Minimum contract value was raised (to about ₹15 lakh in the first phase), which increased lot sizes across the board — NIFTY's lot size, for instance, was raised from 25 to **75** in that first phase. (Lot sizes are reset periodically to keep each contract's value near the mandated floor: NIFTY's was subsequently revised again to **65**, effective January 2026 — the current figure, and the one used in this chapter's examples.) Bigger contracts mean a bigger minimum outlay, deliberately raising the bar for casual speculation.
* **Upfront collection of option premium** from buyers and **removal of the calendar-spread margin benefit on expiry day**, effective in early 2025, tightening leverage precisely when risk is highest.
* **Higher taxes on the sell side.** Separately, from **1 October 2024**, STT on the sale of options was raised to **0.1% of the premium** (from 0.0625%), and then to **0.15% from 1 April 2026** (with option-*exercise* STT also raised to 0.15% and futures-sale STT to 0.05%) — successive hikes that directly increase the cost of high-frequency option selling.

*(All dates and figures above are as announced for 2024–2026; rules and rates change — always verify the current position with SEBI and your exchange before relying on them.)*

The direction of travel is clear: the regulator is deliberately making index derivatives less of a casino and more of a professional instrument. For a serious trader, that is good news — it thins the crowd of the least prepared and rewards those who treat this as a craft.

> **Case Study — The rise and rationalisation of weekly expiries (2016–2024).**
>
> **Context.** When BANKNIFTY weekly options launched in May 2016, they were a novelty: a way to trade a specific week's move for a fraction of a monthly contract's cost. Traders loved that the premium was small and the payoff, if the move came, could be large.
>
> **What happened.** Success bred imitation. NIFTY weeklies followed in 2019, and over the next few years the exchanges added weekly expiries across their index suite, spacing expiry days through the week. The result was an option expiring on nearly every session. Volumes — especially in cheap, same-day and next-day contracts — grew explosively, and so did the share of trading done by individuals.
>
> **The analysis.** The design that made weeklies attractive also made them dangerous. As an option approaches expiry, its time value collapses and its behaviour becomes violent and unforgiving (a dynamic we treat in depth later in the book). A stream of near-expiry contracts is, in effect, a stream of high-variance bets. SEBI's data showed the predictable result: most individuals lost, and the aggregate losses were very large.
>
> **The lesson.** In 2024 SEBI rationalised the market to one weekly expiry per exchange and made contracts larger and leverage tighter. The episode is a template for how this market evolves: an innovation democratises access, volumes surge, retail losses mount, and the regulator recalibrates. As a trader you must expect the rules to keep changing — and build the habit of checking the current specifications rather than trusting last year's memory.
>
> **Takeaway.** *Market structure is not a fixed backdrop; it is a moving part of your strategy. Verify contract specifications and rules before every new campaign.*

---

## 4. Examples (Real-World)

**Example 1 — Hedging (the COVID crash, 2020).** A domestic institution holding a large, NIFTY-like equity portfolio anticipated turbulence in early 2020 and bought NIFTY put options as insurance. As the index fell roughly 38% into late March 2020 and the India VIX spiked toward 83.6, the puts surged in value, offsetting the bulk of the portfolio's decline. The institution paid a modest premium in calm times and was compensated in the storm. This is hedging in its purest form.

**Example 2 — Speculation (a directional retail trade).** A retail trader believes the NIFTY, trading at 24,600, will rally over the coming week ahead of a policy announcement. Rather than buy shares, they buy one lot of a NIFTY 24,600 call for ₹120 — a ₹7,800 outlay (the mechanics are worked in Numerical Example 1). The *asymmetry* is the whole point: if the index rallies sharply the call can multiply several times over, but if the index merely stalls or drifts down, the entire ₹7,800 can be lost — a 100% loss on the outlay from a market that simply failed to rise far enough, fast enough. The trader has taken on that risk voluntarily in exchange for a leveraged, capped-downside bet. This is speculation — the motive behind the overwhelming majority of retail option activity.

**Example 3 — Arbitrage (cash–futures alignment).** Suppose the NIFTY spot index is at 24,600. The "fair" price of the near-month future is the spot *plus a small cost of carry* — roughly the interest cost of holding the position to expiry, net of dividends — which here works out to about 120 points, implying a fair future near **24,720**. Now suppose the future instead trades at **24,850** — about **130 points above fair value**. A professional desk sells the expensive future and buys the underlying basket (or an equivalent), locking in that ~130-point excess, which must converge to zero by expiry when future and spot meet. The profit is small per unit and requires scale and low costs — which is why arbitrage lives on professional desks, not retail screens. (We develop cost of carry and futures fair value properly later in the book; for now, note only that a future has a *computable* fair value, and arbitrage is the force that keeps it there.)

> **Market Note — India VIX, briefly.** The **India VIX** is an index published by the NSE that estimates the market's expectation of NIFTY volatility over the next 30 days. In calm markets it sits in the low teens; in the March 2020 panic it reached about 83.6. You do not need its formula yet — just recognise it as the market's fear gauge, rising when participants scramble for protection.

---

## 5. Numerical Examples

These use a common **illustrative** setup so the numbers are easy to follow: NIFTY at **24,600**, NIFTY lot size **65** (as revised effective January 2026 — verify the current lot before trading). Figures are **before transaction costs**, which we account for fully when we cost real trades elsewhere in the book.

### Numerical Example 1 — Notional value versus premium at stake

You buy one NIFTY 24,600 call option quoted at a premium of **₹120**.

* **Notional value controlled** = index level × lot size = 24,600 × 65 = **₹15,99,000**.
* **Premium actually paid** = premium × lot size = 120 × 65 = **₹7,800**.
* **Premium as a share of notional** = 7,800 ÷ 15,99,000 = **0.49%**.
* **Notional-to-premium multiple** = 15,99,000 ÷ 7,800 ≈ **205×**.

**Interpretation.** ₹7,800 gives you a contract linked to nearly ₹16 lakh of index. That ~205:1 gap is exactly why "notional turnover" headlines are astronomically large while the money genuinely at risk is far smaller. It is also a first, blunt lesson in leverage: the same multiple that can magnify a gain will magnify a loss.

> **Beginner Alert — "205× leverage" and "true exposure is smaller than notional" are *both* true.** These sound contradictory but describe two different things. The **notional** (₹15,99,000) is the size of the index your contract *references* — the right number for understanding turnover headlines and worst-case scale. Your **actual** short-run gain or loss, however, is *not* 205× the index move, because an option's price moves only a *fraction* of each index point (an at-the-money option, very roughly, half a point per index point; a far out-of-the-money option far less). So notional tells you the *reference size*, not your *immediate* sensitivity. For now, resist two opposite errors: do not assume a 1% index move changes your option by 205% of your outlay (it usually changes it by much less), and do not assume the small premium means small risk (near expiry, an option's sensitivity can swing violently). The precise "fraction per point" is a core topic we develop later in the book.

### Numerical Example 2 — How a hedge offsets a loss (held to expiry)

You hold Indian equities worth **₹15,99,000** that closely track the NIFTY at 24,600. Fearing a fall, you buy one lot of a NIFTY 24,600 **put** at a premium of **₹300**.

* **Cost of the hedge** = 300 × 65 = **₹19,500** (about **1.22%** of the portfolio).
* Suppose the NIFTY falls **10%** to 22,140 by expiry.
  * **Portfolio loss** ≈ 10% × 15,99,000 = **₹1,59,900**.
  * **Put intrinsic value at expiry** = strike − settlement = 24,600 − 22,140 = **2,460 points**.
  * **Put payoff** = 2,460 × 65 = **₹1,59,900**.
  * **Net gain on the put** = payoff − premium = 1,59,900 − 19,500 = **₹1,40,400**.
* **Net portfolio outcome** = −1,59,900 (shares) + 1,40,400 (put) = **−₹19,500**.

**Interpretation.** The put converted an uncertain ₹1,59,900 loss into a known ₹19,500 cost — the premium, which behaves like an insurance deductible. This is the mechanism behind the introduction's second investor. (This clean one-for-one offset assumes the portfolio tracks the index exactly and the position is held to expiry; in reality, transaction costs, imperfect tracking, and any residual time value would alter the figures slightly. The principle stands.)

### Numerical Example 3 — Notional turnover versus premium turnover (why the headlines mislead)

Imagine that on a given day **1 crore** NIFTY option contracts (lots) change hands, at an average premium of **₹110** per unit, with the index around 24,600 and lot size 65.

* **Notional turnover** ≈ contracts × lot size × index level = 1,00,00,000 × 65 × 24,600 ≈ **₹15,99,000 crore** (that is ₹15.99 lakh crore).
* **Premium turnover** ≈ contracts × lot size × average premium = 1,00,00,000 × 65 × 110 ≈ **₹7,150 crore**.
* **Ratio** ≈ 15,99,000 crore ÷ 7,150 crore ≈ **224×**.

**Interpretation.** The notional figure is over two hundred times the premium that actually moved. Both numbers are "turnover," but only the premium figure is close to the money genuinely exchanged. When you compare markets, insist on knowing *which* turnover is being quoted. (Contract count and average premium here are illustrative; compute the real ratio yourself using the exercise in Section 11.)

---

## 6. Calculations (the reusable recipes)

The examples above rely on four small calculations you will use for the rest of your trading life. Commit the recipes, not the specific numbers.

**(a) Notional value of one option contract**

```
Notional value = Underlying level (or Strike) × Lot size
```

Example: 24,600 × 65 = ₹15,99,000. This is the economic size of the position, not its cost.

**(b) Premium value — the money that actually changes hands**

```
Premium value = Option premium (per unit) × Lot size
```

Example: 120 × 65 = ₹7,800. This is what a buyer pays and a seller receives (before costs).

**(c) Leverage / notional multiple**

```
Notional multiple = Notional value ÷ Premium value  (= Underlying level ÷ Premium)
```

Example: 15,99,000 ÷ 7,800 ≈ 205× — the same as 24,600 ÷ 120. Higher multiples mean cheaper entry and sharper, faster P&L in both directions. As the Beginner Alert stressed, this is the *reference* leverage; the *true* directional exposure of an option is smaller than its notional, because an option's price moves only a fraction of the index's move — the mechanics of that fraction are developed later in the book.

**(d) Hedge offset at expiry**

```
Net outcome = Change in portfolio value + (Option intrinsic payoff − Premium paid)
Put intrinsic payoff = max(0, Strike − Settlement) × Lot size
Call intrinsic payoff = max(0, Settlement − Strike) × Lot size
```

Example (from Numerical Example 2): −1,59,900 + (1,59,900 − 19,500) = −₹19,500.

**(e) Comparing two "turnover" numbers**

```
Notional turnover ≈ Σ (contracts × lot size × underlying level)
Premium turnover  ≈ Σ (contracts × lot size × option premium)
```

The two answer completely different questions. Notional says how much index was *referenced*; premium says how much money was *spent*. Never compare one market's notional turnover with another market's premium turnover.

---

## 7. Practical Insights

* **Read structure before you read prices.** Before your first trade in any product, know its lot size, expiry cycle, and settlement method. All three are set by the exchange and revised periodically by SEBI. A trader who does not know the lot size does not know their position size — the most basic risk error there is.
* **Distinguish the two turnovers instinctively.** When any scale figure is quoted, ask "notional or premium?" This single habit will keep you from being impressed — or frightened — by numbers that do not mean what they appear to mean.
* **Respect the negative-sum reality.** You are not buying into a growing pie; you are competing for a pot that shrinks with costs. That should shape everything: trade less, size carefully, and only when you have a reason.
* **The guarantee cuts both ways.** The clearing system means no counterparty can stiff you — and also means that if you sell options, you *will* post margin and can be called intraday. Never sell what you cannot fund under stress.
* **Assume the rules will change.** This market has been re-engineered repeatedly — weeklies added, weeklies rationalised, lot sizes and taxes raised. Build the habit of verifying current specifications rather than trusting last year's numbers.

> **Professional Insight — Where the crowd is, the edge usually is not.** The products retail traders flock to — the cheapest, nearest-expiry options — are also the ones professionals are most comfortable *selling* to them. That does not make buying them always wrong, but it should make you ask, every time, "Who is on the other side of this, and why are they happy to take it?"

---

## 8. Common Mistakes

* **Confusing notional with money at risk.** Believing you are "trading ₹16 lakh" when you have spent ₹7,800 — or, worse, being lulled into thinking the small premium means small risk when selling, where the risk is far larger than the premium received.
* **Thinking derivatives are just "leveraged shares."** They are different instruments with a fixed life and a value that decays. The share-market intuition of "buy and hold until it recovers" can be fatal on a contract that expires next Tuesday (the NIFTY weekly expiry day).
* **Ignoring the base rate.** Entering the F&O market without absorbing that the large majority of individual traders lose money — and assuming you are automatically the exception.
* **Assuming your counterparty could default.** New traders sometimes worry about the anonymous seller vanishing. They will not; the clearing corporation guarantees settlement. The real counterparty risk you face is your *own* margin obligation if you are short.
* **Treating structure as static.** Trading on stale assumptions about lot sizes, expiry days, or costs after SEBI has changed them — and being caught out by a larger-than-expected position or a higher-than-expected charge.

---

## 9. Chapter Summary

* A **derivative** is a contract whose value is derived from an underlying; Indian index derivatives are **cash-settled** because you cannot hold an index. The two building blocks are **futures** (a firm commitment, symmetric payoff) and **options** (a right without obligation, asymmetric payoff).
* Derivatives exist to **transfer risk, discover price, and provide access/leverage**, and every trade is placed to **hedge, speculate, or arbitrage** — know which you are doing.
* Derivatives trading is **zero-sum before costs and negative-sum after**; SEBI's own studies show most individual traders lose, which is the base rate you must beat.
* **Exchange-traded** derivatives (all index options) are standardised and centrally cleared; **novation** by the clearing corporation removes counterparty risk, funded by the margin discipline it imposes.
* India is the **world's largest options market by contract count**, driven by low ticket sizes, weekly expiries, and the discount-broker boom — but headline **notional turnover** overstates money at stake by roughly 200×, while an option's *true* exposure is smaller still than its notional.
* India's structure evolved from **monthly** expiries to **weekly** (BANKNIFTY 2016, NIFTY 2019) and was then **rationalised by SEBI from 2024 onward** — one weekly expiry per exchange (NIFTY on the NSE, SENSEX on the BSE), larger contracts, tighter leverage, and, from September 2025, standardised expiry days (NIFTY on **Tuesday**, SENSEX on **Thursday**).
* **SEBI** regulates; **NSE Clearing** and **ICCL** guarantee; the specifications they set change over time and must be verified.

---

## 10. Key Takeaways

* **See three separate objects every time: the underlying, the contract, and the link between them.** Most beginner errors dissolve once these stop blurring together.
* **Always ask "notional or premium?"** — of every scale figure you read and of your own positions — and remember notional is the *reference* size, not your immediate sensitivity.
* **Name your motive — hedge, speculate, or arbitrage — before you place the trade.** The motive fixes the size, the stop, and the exit.
* **Treat the market as negative-sum and the rules as moving.** Trade selectively, size for the risk you actually carry, and verify current specifications before every campaign.

---

## 11. Practice Questions

**Q1 (Concept).** In one sentence, explain why a NIFTY option is called a "derivative."

**Q2 (Multiple choice).** Indian *index* options are settled by:
(a) physical delivery of the index constituents; (b) cash; (c) delivery of a NIFTY ETF; (d) the buyer's choice.

**Q3 (Multiple choice).** The clearing corporation reduces counterparty risk primarily through:
(a) insurance bought from a private insurer; (b) novation, becoming buyer to every seller and seller to every buyer; (c) a government bailout guarantee; (d) banning defaulting members after the fact.

**Q4 (True/False).** "Notional turnover" and "premium turnover" measure the same thing.

**Q5 (Motive).** Classify each as hedging, speculation, or arbitrage:
(a) A fund holding shares buys NIFTY puts before an election.
(b) A trader with no shares buys a NIFTY call expecting a rally.
(c) A desk sells a NIFTY future trading well above fair value and buys the underlying basket.

**Q6 (Numerical).** NIFTY is at 24,600 and the lot size is 65. You buy one 24,600 call at ₹150. Compute (i) the premium you pay, (ii) the notional value controlled, and (iii) the notional-to-premium multiple.

**Q7 (Numerical / hedge).** You hold ₹15,99,000 of NIFTY-tracking equities and buy one 24,600 put at ₹280 (lot size 65). If the NIFTY falls to 23,100 at expiry, compute (i) the portfolio loss, (ii) the put's intrinsic payoff, (iii) the net gain on the put after premium, and (iv) the net portfolio outcome. Ignore transaction costs.

**Q8 (History).** Put these in chronological order: NIFTY weekly options; BANKNIFTY weekly options; SEBI's single-weekly-expiry rationalisation; the launch of Indian index futures.

**Q9 (Applied research).** Using the live NSE website, find today's total index-options figure and state whether the number you found is a *notional* or a *premium* turnover, and how you can tell.

**Q10 (Judgement).** A friend says, "Options are cheap, so the risk is small." Give two reasons this reasoning is flawed.

---

## 12. Detailed Solutions

**A1.** Its value is *derived* entirely from the level of the NIFTY 50 index — it has no independent worth of its own; change the index and the option's value changes.

**A2.** **(b) Cash.** You cannot hold an index in a demat account, so index options are settled in rupees by reference to the index level at expiry. (Single-stock derivatives, outside this book's scope, are physically settled.)

**A3.** **(b) Novation.** The clearing corporation interposes itself between the two sides, becoming the counterparty to each, and backs this with daily margining and a settlement guarantee fund — so an individual counterparty's default does not fall on you.

**A4.** **False.** Notional turnover is the full face value of the index *controlled* by the contracts traded; premium turnover is the *money actually paid*. They differ by a factor of roughly 200×.

**A5.** (a) **Hedging** — reducing risk on shares already held. (b) **Speculation** — voluntary directional risk with no underlying holding. (c) **Arbitrage** — locking in a mispricing between the future and the cash basket.

**A6.**
(i) Premium paid = 150 × 65 = **₹9,750**.
(ii) Notional value = 24,600 × 65 = **₹15,99,000**.
(iii) Multiple = 15,99,000 ÷ 9,750 ≈ **164×** (equivalently, 24,600 ÷ 150 = 164).

**A7.** Fall to 23,100 (a drop of 24,600 − 23,100 = 1,500 points, i.e., about 6.10%).
(i) Portfolio loss ≈ 1,500 × 65 = **₹97,500** (equivalently ~6.10% of ₹15,99,000).
(ii) Put intrinsic payoff = (24,600 − 23,100) × 65 = 1,500 × 65 = **₹97,500**.
(iii) Premium paid = 280 × 65 = ₹18,200, so net gain on the put = 97,500 − 18,200 = **₹79,300**.
(iv) Net outcome = −97,500 + 79,300 = **−₹18,200** — the loss is contained to the premium, the "deductible."

**A8.** (1) Launch of Indian index futures (**2000**) → (2) BANKNIFTY weekly options (**2016**) → (3) NIFTY weekly options (**2019**) → (4) SEBI's single-weekly-expiry rationalisation (**2024**).

**A9.** Guidance: on the NSE market-data pages you will typically find index-option turnover reported as a very large **notional** figure (often in lakh crore). You can tell it is notional rather than premium because it is orders of magnitude larger than the market's total premium traded; a premium-turnover figure would be far smaller. Where both are shown, the premium (or "premium turnover") line is the money actually exchanged. (Exact figures change daily — record the date of your reading.)

**A10.** Two valid reasons: (i) A low premium buys a large *notional* exposure (often ~200×), so the position is highly leveraged and can lose its entire value quickly. (ii) "Cheap" usually means short-dated and out-of-the-money, where time decay is fastest and the probability of the option expiring worthless is highest — so cheapness reflects low odds, not low risk. (A third: if you *sell* options, your risk far exceeds the small premium received.)

---

## 13. Mini Glossary

* **Derivative** — a contract whose value is derived from an underlying asset, rate, or index. → this chapter.
* **Underlying** — the asset or index a derivative is based on (for index options, the NIFTY 50, Nifty Bank, etc.). → this chapter.
* **NIFTY 50** — India's benchmark equity index, tracking the 50 largest, most liquid listed companies; the underlying for NIFTY options. → this chapter.
* **Future** — a standardised, firm commitment to settle the underlying at an agreed price on a set date; gains and losses are symmetric for buyer and seller. → this chapter.
* **Call option / Put option** — a *right* (not an obligation) to buy (call) or to sell (put) the underlying at the strike; the buyer's loss is limited to the premium. → this chapter.
* **F&O (Futures and Options)** — the exchange-traded derivatives segment of the market. → this chapter.
* **Cash settlement** — settling a contract in rupees by reference to the underlying's level at expiry, with no delivery of the asset. → this chapter.
* **Hedging** — reducing an existing risk by taking an offsetting derivative position. → this chapter.
* **Speculation** — taking on risk voluntarily to profit from a view. → this chapter.
* **Arbitrage** — locking in profit from the same value priced two ways, with little or no risk. → this chapter.
* **Cost of carry** — the net cost of holding the underlying to expiry (financing cost minus dividends), which sets a future's fair premium over spot. → this chapter.
* **Zero-sum** — a game in which one side's gain equals the other's loss; derivatives are zero-sum before costs, negative-sum after. → this chapter.
* **Exchange-traded derivative** — a standardised derivative bought and sold on an exchange and centrally cleared. → this chapter.
* **OTC (over-the-counter)** — a private, bespoke derivative negotiated bilaterally, carrying counterparty risk. → this chapter.
* **Novation** — the clearing corporation stepping between buyer and seller to become the counterparty to each. → this chapter.
* **Counterparty risk** — the risk that the other side of a contract fails to meet its obligation. → this chapter.
* **Clearing corporation** — the entity that guarantees settlement (NSE Clearing for the NSE; ICCL for the BSE). → this chapter.
* **Margin** — collateral a risk-carrying participant (notably an option seller) must post against potential losses. → this chapter.
* **Mark to market** — the daily revaluation of open positions, with resulting gains or losses reflected in the account. → this chapter.
* **SEBI** — the Securities and Exchange Board of India, the market regulator. → this chapter.
* **Leverage** — controlling a large notional position with a small outlay; it magnifies both gains and losses. → this chapter.
* **Notional value** — the full face value of the underlying that a contract controls (level × lot size). → this chapter.
* **Premium** — the price of an option per unit; the buyer pays it, the seller receives it. → this chapter.
* **Strike price** — the fixed level at which an option can be exercised (e.g., the 24,600 in a "NIFTY 24,600 call"). → this chapter.
* **Notional turnover** — total face value of contracts traded; **premium turnover** — total premium actually exchanged. → this chapter.
* **Lot size** — the fixed number of units in one contract, set by the exchange and revised by SEBI. → this chapter.
* **Expiry** — the date on which a contract ceases to exist and is settled. → this chapter.
* **Out-of-the-money** — an option whose strike is away from the current index level, so it has no intrinsic value yet (and is therefore cheap). → this chapter.
* **India VIX** — the NSE's index of expected 30-day NIFTY volatility; the market's fear gauge. → this chapter.

---

<!-- End of Chapter 1 (Rev 3). Rev 3 updates (verified against NSE/SEBI sources, Aug 2026): (1) NIFTY lot size 75 -> 65 (NSE revision effective Jan 2026); all dependent figures recomputed — premium ₹120×65=₹7,800; notional 24,600×65=₹15,99,000; NE2 hedge (put ₹300: cost ₹19,500, loss ₹1,59,900, net −₹19,500); NE3 turnover (notional ₹15,99,000 cr, premium ₹7,150 cr, ratio 224×); Calcs examples; Q6 (₹9,750/₹15,99,000/164×) and Q7 (portfolio ₹15,99,000; loss ₹97,500; net −₹18,200). Notional multiple 205× unchanged (=index/premium). (2) Added Sept-2025 expiry-day standardisation (NIFTY Tue / SENSEX Thu) to §3.6 and Summary; Common Mistakes "expires next Thursday" -> "next Tuesday". (3) SEBI loss data updated to >90% losers / ~₹1.81 lakh crore over FY22-24. (4) Date ranges 2024-2025 -> 2024-2026 (LO2, §3.6 heading, caveat). Rev 2 fixes retained (arbitrage example, futures-vs-options note, glosses, Beginner Alert, glossary). CROSS-BOOK NOTE: Ch2-30 still on lot 75 — refresh to 65 + expiry days in a later pass. No forward chapter-number references. -->
