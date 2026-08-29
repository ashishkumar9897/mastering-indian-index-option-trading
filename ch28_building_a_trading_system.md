<!-- Difficulty: Level 4.5/5 (Advanced-Professional). Dependency: Chapters 18, 21, 22, 25, 26. Target length ~11,000 words. OPENS Part VIII. Backtest (NIFTY weekly IC, 2yr, 100 trades): win 68%, avg win ₹5,000, avg loss ₹8,000 → expectancy +₹840/trade, PF 1.33, total ₹84,000/lot. Cost+slippage ~₹450/trade → net +₹390. Edition 2 rigor: multiple-testing/data-mining bias (30 variants → deflate), deflated Sharpe (raw ~1.3 → ~0.6), option-data quality (LTP vs settlement, stale quotes, point-in-time chains). Metrics: Sharpe=(mean−Rf)/SD, Sortino=(mean−Rf)/downside dev, PF, expectancy, R-multiple, RAROC. Case study 4 stages: hypothesis → backtest (raw +₹840, net +₹390, deflated ~+₹200) → paper (+₹250) → live scaled (+₹180) — each stage reveals thinner true edge. IV = implied volatility. Rev 2 (5 Aug 2026): setting label lot 75→65. Backtest ₹ figures are illustrative empirical outputs (win ₹5,000/loss ₹8,000 plausible at lot 65 ≈ ₹77/₹123 per unit) and all ratios (PF, R-multiples, Sharpe/Sortino) are lot-independent, so kept unchanged. Data-cleanliness passage broadened to the 2024 single-weekly consolidation + 2025 Tuesday-weekday shift + Jan-2026 lot cut that a current 2-yr backtest spans. -->

# Chapter 28 — Building a Trading System

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Design a rule-based trading system for index options.
2. Backtest strategies using historical data — rigorously.
3. Distinguish curve-fitting from genuine edge.
4. Build checklists and standard operating procedures.
5. Implement automation where appropriate.

Welcome to Part VIII, which elevates you from a skilled trader to a professional. This chapter is the synthesis of everything before it: it takes the strategies (Part V), the volatility and event context (Parts IV, VI), and the risk and sizing framework (Part VII), and forges them into a *system* — a codified, tested, repeatable process. The difference between a gambler and a professional is not the trades; it is the *system* behind them.

---

## 2. Introduction

Everything in this book so far has been components — strategies, Greeks, risk rules. A professional does not trade components; they trade a *system*: a complete, written set of rules covering what to trade, when to enter, how much to size, when to adjust, and when to exit — validated by honest testing and executed with the discipline of a standard operating procedure. The system is what turns a collection of good ideas into a repeatable business, and it is what removes the emotion that (as Chapters 24 and 29 show) destroys most traders.

But building a system exposes the hardest truth in trading: **most apparent edges are illusions.** A backtest that looks brilliant is usually brilliant *because* it is over-fitted, mined from too many variants, or built on bad data — and the moment it meets live costs, slippage, and honest scrutiny, the edge shrinks or vanishes. This chapter therefore spends as much effort on *validating* an edge as on *finding* one. The Edition 2 additions — multiple-testing bias, deflated performance metrics, and option-data quality — are the professional's defences against fooling themselves. A backtest showing a +₹840-per-trade edge can become +₹390 after real costs and a mere +₹200 after honest deflation — and the trader who acts on the ₹840 blows up while the one who trades the ₹200 survives.

This chapter builds the system from the ground up: what a system is and why rules beat discretion; the nature of a genuine edge; rigorous backtesting and its many pitfalls; the option-data-quality traps that fabricate fake profits; the performance metrics that measure an edge honestly; the trade playbook and SOPs that operationalise it; and the automation spectrum. It closes with a start-to-finish case — building a systematic NIFTY iron condor machine from hypothesis to scaled live trading — showing how the true edge shrinks, and is revealed, at each stage. Setting: **NIFTY at 24,600, lot 65**, synthesising Parts IV–VII.

---

## 3. Core Concepts

### 3.1 What a trading system is — and why rules beat discretion

The flagship concept: a **trading system** is a *completely codified* process, and for most traders, rules beat discretion.

**What is it?** A trading system is a written, unambiguous set of rules covering **entry** (exact conditions to enter), **exit** (target, stop, time), **position sizing** (Chapter 26), **adjustments** (Chapter 18's triggers), and **risk limits** (Chapter 25) — such that any competent person following the rules would take the *same* trades you would. If a rule requires judgement in the moment, it is not yet a system.

**Why does it exist?** Because *discretionary* trading — deciding each trade by feel — is vulnerable to the emotions that destroy traders: fear, greed, revenge, FOMO (Chapters 24, 29). A codified system **removes the in-the-moment decision**, so emotion cannot corrupt it. It also makes the approach *testable* (you cannot backtest a feeling) and *consistent* (the same rules every time, so results are attributable to the system, not to mood).

**Why should a trader care?** Because the single most reliable path from "knows strategies" to "profitable professional" is *systematisation*. A trader with a mediocre but *codified and disciplined* system outperforms one with brilliant instincts undermined by inconsistent, emotional execution. Rules are how you make your best thinking — done calmly, in advance — govern your worst moments.

**Intuitive explanation.** A trading system is a **flight checklist.** Pilots do not fly by feel, however experienced; they follow a checklist for every phase, because the checklist — written calmly on the ground — prevents the errors that adrenaline and fatigue cause in the air. Your trading system is that checklist: it makes your calm, considered rules override your in-the-heat impulses.

**Rule-based vs discretionary.** Experienced professionals *can* trade discretionarily, but they earned it through years of pattern recognition, and even they lean on rules for risk. For everyone else — and certainly for retail traders — **rules are not a limitation; they are survival.** The rule removes the decision precisely at the moment (a loss, a streak, a spike) when your judgement is most compromised.

**Common mistake.** Having "a strategy" but not "a system" — knowing *what* to trade but leaving the *when, how much, and when to exit* to in-the-moment judgement, which emotion then corrupts.

**Practical takeaway.** **A trading system is your calm, written rules made to govern your emotional moments — codify entry, exit, sizing, adjustments, and risk so completely that no in-the-moment judgement is required, because the judgement you make under stress is the judgement that ruins you.**

---

### 3.2 Edge — the statistical advantage

A system is only worth trading if it has an **edge** — a genuine, statistical advantage that generates profit over many trades.

**What is it?** An edge is a **positive expected value per trade** (Chapter 21) that persists across a large sample: `expectancy = (win rate × avg win) − (loss rate × avg loss) > 0`, *after all costs*. Without an edge, a system does not "sometimes lose"; it loses *systematically* — the more you trade it, the more you lose.

**Where edges come from in options.** Genuine option edges are usually structural, not predictive: the **variance risk premium** (IV persistently above realised, Chapter 14), the **skew** (Chapter 15), or a disciplined *behavioural* edge (doing what most traders cannot — cutting losses, sizing correctly, sitting out). Edges do *not* come from a clever chart pattern that "worked" in a backtest — those are usually curve-fitting (Section 3.4).

**The edge must survive reality.** A backtested edge must survive **costs** (STT, brokerage, GST — Chapter 3), **slippage** (the bid-ask spread you actually pay — Chapter 3), and **honest validation** (deflation for the number of variants tested, Section 3.4). Many "edges" are positive in a naive backtest and *negative* after these — a fatal distinction. The rest of this chapter is largely about telling a real edge from an illusory one.

---

### 3.3 Backtesting methodology

**Backtesting** — testing a system's rules against historical data — is how you estimate an edge before risking capital. Done well, it is invaluable; done carelessly, it manufactures false confidence.

**Data requirements.** Options backtesting needs **historical option-chain data with IV and Greeks** — not just the underlying. Sources: the **NSE Bhav copy** (official end-of-day data) and commercial providers. The data must be *point-in-time* (what was actually quoted then, not reconstructed with today's assumptions — Section 3.5).

**Frameworks.** From simplest to most powerful: **spreadsheet-based** (fine for simple, low-frequency systems like a weekly iron condor), and **Python/R-based** (for complex or higher-frequency systems, and for proper statistical validation). Retail traders can start with free platform tools (Opstra, Sensibull) for basic backtests.

**Walk-forward analysis.** The gold standard for avoiding overfitting: **optimise the system's parameters on an in-sample period, then test the *fixed* parameters on a separate out-of-sample period.** If the system works out-of-sample (on data it was *not* tuned on), the edge is more likely real; if it only works in-sample, it is curve-fitted. Never judge a system on the data you optimised it on.

**Avoiding overfitting — the cardinal rule.** **Fewer parameters = more robust.** A system with two rules that works is far more trustworthy than one with ten rules perfectly tuned to the past — because the ten-rule system has almost certainly been fitted to *noise*, and noise does not repeat. Every added parameter is another opportunity to curve-fit; the professional ruthlessly *minimises* parameters.

**Costs and slippage — always included.** A backtest without transaction costs and slippage is *fiction*. Include realistic costs (Chapter 3, ~₹450+/trade for a four-legged iron condor) and slippage (you fill worse than mid, especially in the wings). As Section 5 shows, costs alone can turn a "profitable" backtest into a marginal or losing one.

---

### 3.4 Backtesting pitfalls — how backtests lie

Backtests overstate edges in predictable ways. The professional knows every trap:

* **Survivorship bias** — testing only instruments that still exist (less relevant for index options, which don't "delist," but relevant if using constituent data).
* **Look-ahead bias** — using information in the backtest that was not available at the time (e.g., the day's close to decide a morning entry). A subtle, common, fatal error.
* **Overfitting** — tuning the system to past noise (Section 3.3); the single biggest source of false edges.
* **Ignoring liquidity and slippage** — assuming you filled at the mid, or in size, in strikes where you could not (Section 3.5).
* **Forgetting transaction costs (especially STT)** — the STT and cost drag (Chapter 3) that a naive backtest omits and that can erase the edge.
* **Multiple-testing / data-mining bias (Edition 2):** testing 50 strategy variants and reporting the best one is *not* finding an edge — it is **p-hacking**. The more configurations you try, the higher the *best* backtest looks *by luck alone*. If you test 50 random, edgeless strategies, the best of them will show an impressive backtest purely by chance — and it will fail live. Every variant you test inflates the best result; you must *deflate* for the number tried.
* **Deflated / haircut performance metrics (Edition 2):** consequently, a raw backtest Sharpe (or expectancy) must be **discounted** for (a) the number of variants tested, (b) the shortness of the sample, and (c) the non-normality of option returns, *before it is believable*. A raw Sharpe of 1.3 from the best of 30 variants over 2 years might deflate to ~0.6 — still positive, but far less impressive, and possibly not real (Section 5).

> **Beginner Alert — the best backtest of many is usually the luckiest, not the best.** The natural workflow — "test 30 variations, trade the one with the highest return" — is precisely how you fool yourself. The best of 30 random strategies *always* looks good in-sample, purely by chance, and *always* disappoints live. Test *few* variants (ideally derived from a real hypothesis, not a parameter sweep), validate out-of-sample, and *deflate* the result for how many you tried. If you tested many, trust the best one *less*, not more.

---

### 3.5 Option-data quality — the biggest source of fake profits

This Edition 2 addition addresses the single largest cause of fictitious backtest profits in Indian option research: **bad data.** Option data has specific pitfalls that manufacture edges that do not exist:

* **Settlement/closing price vs LTP vs bid-ask mid — which price?** A backtest that fills at the **last traded price (LTP)** or the **mid** overstates results, because you cannot actually transact there — you buy at the *ask* and sell at the *bid* (Chapter 3). Using LTP or mid *inflates every fill*, especially in illiquid strikes. A realistic backtest fills at (or worse than) the *bid/ask you would actually have paid*.
* **Stale quotes in illiquid strikes.** A far-OTM strike may show a "printed" price that has not traded in hours — a stale quote you could *never* have transacted at. A backtest that uses these stale prices books profits (or losses) on trades that were never executable. Filter for liquidity; do not trust a price you could not have hit.
* **Point-in-time chains and correct IV/Greeks reconstruction.** The backtest must use the option chain *as it was* at each historical moment — with the IV and Greeks that prevailed *then*, not recomputed with today's assumptions or models. Reconstructing history with hindsight (e.g., today's IV surface applied to past prices) introduces look-ahead bias and fabricates edges.
* **Corporate-action and expiry-calendar cleanliness.** The data must correctly handle lot-size changes, expiry-day conventions, and — critically for Indian options — the recent wave of structural changes: the **2024 single-weekly-expiry consolidation**, the **2025 expiry-weekday standardisation** (NIFTY weekly to Tuesday, SENSEX to Thursday), and the **January 2026 lot-size cut** (NIFTY 75→65, BANKNIFTY to 30) (Chapter 1). A backtest spanning these with an uncorrected calendar or lot map will mis-map expiries, mis-scale P&L, and produce garbage.

The through-line: **an option backtest is only as good as its data, and option data is treacherous.** More fake edges come from bad data — filling at un-hittable prices, stale quotes, hindsight-reconstructed Greeks — than from any other single cause. Before trusting a backtest, interrogate its data: *could I actually have transacted at these prices, at this size, with the information available then?*

> **Market Note — if the fill looks too good, it is the data, not the edge.** The most common way an Indian option backtest shows a spectacular edge is by filling at the LTP or mid of illiquid strikes — prices no real order would ever have got. When a backtest of an OTM-selling strategy shows a fabulous Sharpe, suspect the fills first: re-run it filling at the *bid/ask* with a liquidity filter, and the fabulous edge usually collapses to a thin (or negative) one. Data quality is not a technicality; it is the difference between a real edge and a fantasy.

---

### 3.6 Performance metrics — measuring an edge honestly

To judge a system, measure it with the right metrics:

* **Expectancy** = (win rate × avg win) − (loss rate × avg loss) — the average profit per trade; must be positive *after costs* (the core edge measure).
* **Profit factor** = gross profit ÷ gross loss — how many rupees earned per rupee lost; >1 is profitable, >1.5 is good, but interpret alongside drawdown.
* **Sharpe ratio** = (mean return − risk-free rate) ÷ standard deviation of returns — return per unit of *total* volatility; the standard risk-adjusted measure.
* **Sortino ratio** = (mean return − risk-free rate) ÷ *downside* deviation — like Sharpe but penalising only *harmful* (downside) volatility; higher than Sharpe, and more relevant for strategies with asymmetric returns.
* **Maximum drawdown and recovery time** — the worst peak-to-trough fall (Chapter 25) and how long it took to recover; the survivability measure.
* **R-multiple** = trade profit ÷ initial risk per trade — expressing each result in units of risk (a trade risking ₹8,000 that made ₹5,000 is +0.625R; a max loss is −1R). Expectancy in R-multiples is a clean, size-independent edge measure.
* **RAROC (risk-adjusted return on capital)** — return relative to the risk capital deployed, for comparing strategies of different risk.
* **Deflated Sharpe (Edition 2)** — the raw Sharpe *discounted* for the number of trials, sample length, and non-normality (Section 3.4) — the *believable* version of the Sharpe.

The professional does not judge a system by its *return* alone; they judge it by its **risk-adjusted, cost-inclusive, deflated** metrics — because a high raw return with a huge drawdown, or a high Sharpe from 50 trials, is not a real edge.

---

### 3.7 The trade playbook and SOPs

A system must be *operationalised* into documents you actually use:

**The trade playbook.** A **standardised one-page card per strategy** (extending the Style Guide's strategy template), specifying: the *hypothesis/edge*, the *market conditions* to deploy it (IV regime, direction, DTE), the *exact entry rules*, *strike/expiry selection*, *position size* (Chapter 26), *adjustment triggers* (Chapter 18), *exit rules* (target/stop/time), and *maximum risk*. The playbook turns "I trade iron condors" into a precise, repeatable specification. You trade *only* from the playbook.

**Standard Operating Procedures (SOPs).** The daily routine that executes the playbook:

* **Pre-market** (before 9:15): check overnight gaps and global cues, note India VIX / IV Rank (Chapter 14), review the event calendar (Chapter 23), review open positions' Greeks (Chapter 12), set levels, and *plan* the day's trades per the playbook.
* **Market hours**: execute per the rules, monitor aggregate Greeks and alerts (Chapter 27), adjust per pre-defined triggers, honour stops, and — critically — take *no impulse trades* outside the playbook.
* **Post-market**: **journal every trade** (strategy, conditions, entry/exit, P&L, R-multiple, and *process notes*), update the equity curve, reconcile Greeks (Chapter 27), and review the *process* (was the rule followed?) separately from the *outcome* (did it win?).

The SOP is the flight checklist in action — it ensures the system is executed *the same way every day*, removing the discretion that emotion exploits.

> **Professional Insight — the journal is where edges are found and lost.** The single most valuable professional habit is a disciplined trade journal that separates *process* from *outcome*. A losing trade with a correct process is a *good* trade (the process will pay over many trades); a winning trade with a broken process is a *bad* trade (the luck will reverse). Amateurs judge trades by outcome and learn the wrong lessons; professionals judge by process and refine the system. Over hundreds of journaled trades, the journal reveals which parts of your system carry the edge and which leak it — data no backtest can give you, because it is *your* execution, live.

---

### 3.8 The automation spectrum and tools

Automation exists on a spectrum, and most retail traders should progress along it carefully:

* **Fully manual** — you watch and execute everything. Prone to screen-staring, fatigue, and impulse (Chapter 24).
* **Alert-based** — the platform *alerts* you when a rule's condition is met, and you execute. This is the recommended starting point: it frees you from screen-staring and reduces impulse trades (you act on the alert, not on boredom).
* **Semi-automated** — orders are pre-staged or auto-placed on triggers, with manual oversight and a "kill switch."
* **Fully automated (algo)** — the system executes end-to-end via a **broker API** (Zerodha Kite Connect, Upstox, etc.), with no manual intervention. Powerful but demanding — requires robust code, monitoring, and risk controls, and a bug can be catastrophic.

**Indian tools:** broker APIs (**Kite Connect, Upstox**) for execution and automation; data sources (**NSE Bhav copy** for official data, **Opstra, Sensibull** for chain analytics and basic backtesting). The right level of automation is the one that *reduces your errors* — for most, that is alert-based, which removes the impulse without the risk of unmonitored full automation.

---

## 4. Examples (Real-World)

**Example 1 — The over-fitted backtest.** A trader sweeps 40 combinations of entry delta, wing width, and profit target, and finds one combination with a stunning backtest (Sharpe 2.5). They trade it live and it loses — because the "edge" was the luckiest of 40 noise-fits, not a real advantage. Deflating for the 40 trials would have shown a true Sharpe near zero.

**Example 2 — The data-quality mirage.** A backtest of selling far-OTM options shows a fabulous edge — until the trader re-runs it filling at the *bid/ask* (not the LTP) with a liquidity filter, and the edge collapses. The "profit" was filling at un-hittable stale prices; the real strategy barely breaks even after realistic fills.

**Example 3 — The journal that fixed the system.** A trader journals every trade and, after 100, notices that their losses cluster on trades taken *without* the IV-Rank->50 filter — impulse trades outside the playbook. Adding the filter as a hard rule (and eliminating the impulse trades) turns a break-even system into a profitable one. The journal, not a backtest, found the leak.

---

## 5. Numerical Examples

Setting: NIFTY weekly iron condor system, lot 65; 2-year backtest, 100 trades.

### Numerical Example 1 — Raw backtest metrics

A NIFTY weekly iron condor system over 2 years (100 trades): win rate 68%, average win ₹5,000, average loss ₹8,000:

```
Expectancy = 0.68 × 5,000 − 0.32 × 8,000 = 3,400 − 2,560 = +₹840/trade
Profit factor = (68 × 5,000) / (32 × 8,000) = 3,40,000 / 2,56,000 = 1.33
Total P&L = 100 × 840 = ₹84,000/lot over 2 years
```

The raw backtest looks solid: positive expectancy, profit factor 1.33. But this is *before* costs, slippage, and deflation (the next examples) — and those transform the picture.

### Numerical Example 2 — After costs and slippage

Apply realistic costs and slippage to the same backtest (a four-legged iron condor incurs ~₹300 in costs plus ~₹150 slippage ≈ ₹450/trade, Chapter 3):

```
Net expectancy = 840 − 450 = +₹390/trade
Net total P&L = 100 × 390 = ₹39,000/lot over 2 years
```

Costs and slippage nearly *halved* the edge (₹840 → ₹390). A backtest that omits them overstates the edge by ~₹450/trade — enough, for many systems, to turn a "winner" into a loser.

### Numerical Example 3 — Deflating for multiple testing

Suppose this system was the *best* of **30 variants** tested (a parameter sweep). The raw expectancy (₹390 net) is inflated by having picked the luckiest of 30. Deflating for the number of trials and the short (2-year) sample:

```
Raw net expectancy: +₹390/trade
Deflated (best-of-30, 2-yr sample): ≈ +₹200/trade (a rough, honest haircut)
```

The *believable* edge is ~₹200/trade — real, but a *quarter* of the ₹840 the naive backtest showed. A trader who sized off the ₹840 (Chapter 26) would be dangerously over-sized against the true ₹200 edge.

### Numerical Example 4 — Sharpe and Sortino

The system's monthly returns (on deployed capital) have a mean of 2%, standard deviation 4%, downside deviation 2.5%, with a risk-free rate of 0.5%/month:

```
Sharpe (monthly) = (2 − 0.5) / 4 = 0.375 → annualised = 0.375 × √12 ≈ 1.30
Sortino (monthly) = (2 − 0.5) / 2.5 = 0.60 → annualised = 0.60 × √12 ≈ 2.08
```

The Sortino (2.08) exceeds the Sharpe (1.30) because it penalises only downside volatility — appropriate for the iron condor's asymmetric returns (many small wins, few large losses). *But* the raw Sharpe of 1.30 must itself be **deflated** for the 30 trials and short sample — a deflated Sharpe of ~0.6 is the believable figure.

### Numerical Example 5 — R-multiple expectancy

Expressing the same system in R-multiples (each trade risks its max loss of ₹8,000 = 1R; a winning trade of ₹5,000 = +0.625R):

```
Expectancy (R) = 0.68 × (+0.625R) − 0.32 × (−1R) = 0.425 − 0.32 = +0.105R/trade
```

A +0.105R expectancy means each trade earns, on average, about a tenth of the amount risked — a *thin* edge (before costs, which reduce it further). This size-independent measure confirms what the rupee figures showed: a real but small edge that demands correct sizing (Chapter 26) and cost control (Chapter 3) to be worth trading.

---

## 6. Calculations (the reusable recipes)

**(a) Edge / expectancy**

```
Expectancy = (win rate × avg win) − (loss rate × avg loss)   [must be > 0 AFTER costs]
Expectancy (R) = (win rate × avg win in R) − (loss rate × avg loss in R)
```

**(b) Risk-adjusted metrics**

```
Sharpe = (mean return − risk-free rate) / standard deviation of returns
Sortino = (mean return − risk-free rate) / downside deviation
Profit factor = gross profit / gross loss
R-multiple = trade profit / initial risk per trade
```

**(c) Deflation (the believable edge)**

```
Deflated metric = raw metric discounted for (number of variants tested, sample length, non-normality)
   → the more variants tested and shorter the sample, the larger the haircut
```

**(d) Realistic backtest P&L**

```
Net expectancy = raw expectancy − (transaction costs + slippage) per trade   [then deflate]
```

---

## 7. Practical Insights

* **Trade a system, not a strategy.** Codify entry, exit, sizing, adjustments, and risk so completely that no in-the-moment judgement is required — because judgement under stress is what ruins traders.
* **Assume your backtest is too optimistic — and prove otherwise.** Include realistic costs and slippage, validate out-of-sample, test *few* variants, and *deflate* for the number tried. The believable edge is usually a fraction of the raw backtest.
* **Interrogate the data before trusting the edge.** Fill at bid/ask (not LTP or mid), filter for liquidity, use point-in-time chains, and correctly handle the 2024–2026 expiry and lot-size changes — bad data fabricates more edges than good analysis finds.
* **Judge trades by process, not outcome — and journal everything.** A losing trade with a correct process is good; a winning trade with a broken process is bad. The journal reveals the edge your backtest cannot.
* **Automate to reduce errors, starting with alerts.** Alert-based execution removes screen-staring and impulse; progress to fuller automation only with robust controls.

> **Professional Insight — the goal of a backtest is to *disprove* your edge, not confirm it.** Amateurs backtest to find reasons to trade a system; professionals backtest to find reasons *not* to. They attack their own backtest — Is this over-fitted? Did I test too many variants? Are the fills realistic? Is the data point-in-time? — and only trade what survives the assault, sized for the *deflated* edge. The mindset flip is everything: a backtest is not a green light you seek, it is a gauntlet your system must survive. The trader who tries to confirm their edge fools themselves; the one who tries to destroy it finds the real one.

---

## 8. Common Mistakes

* **Having a strategy but not a system.** Knowing *what* to trade but leaving *when, how much, and when to exit* to emotional in-the-moment judgement.
* **Trusting an over-fitted or over-mined backtest.** Trading the best of many variants (data-mining) or a ten-parameter system fitted to noise — both fail live.
* **Omitting costs and slippage.** Backtesting at the mid/LTP with no costs, showing an edge that vanishes after the real ~₹450/trade drag.
* **Using bad option data.** Filling at un-hittable stale prices, or reconstructing history with today's IV/Greeks (look-ahead) — the biggest source of fake profits.
* **Sizing off the raw backtest edge.** Sizing to a +₹840 backtest when the deflated, cost-inclusive edge is +₹200 — dangerously over-sized (Chapter 26).
* **Judging trades by outcome, not process.** Learning the wrong lessons from lucky wins and unlucky losses instead of refining the system via a process-focused journal.

---

## 9. Case Study — "Building a Systematic NIFTY Iron Condor Machine"

**Context.** This case follows the *complete* professional process of building a trading system — from hypothesis to scaled live trading — for a weekly NIFTY iron condor. Its purpose is to show how the true edge *shrinks and is revealed* at each stage, and how the systematic process (rigor, paper trading, scaled live, SOP) is what turns a hypothesis into a survivable edge — not the impressive backtest. Figures are illustrative but representative; per lot.

**Stage 1 — Hypothesis.** The trader forms a *reasoned* hypothesis (not a mined pattern): *the variance risk premium (Chapter 14) means NIFTY weekly options are, on average, over-priced, so systematically selling defined-risk iron condors when IV is rich should harvest a positive expectancy.* The initial rules: sell a ~16-delta weekly iron condor with 200-point wings *when IV Rank > 50* (only sell rich IV — Chapter 14), size per the risk framework (Chapter 26), roll the tested side per a fixed trigger (Chapter 18), and exit at 50% profit or the defined max loss.

**Stage 2 — Backtest (with rigor).** The trader backtests 2 years (100 trades):

* *Raw backtest:* win rate 68%, expectancy **+₹840/trade**, profit factor 1.33, raw Sharpe 1.30 — looks excellent.
* *After costs and slippage:* the four-legged condor's ~₹450/trade drag cuts expectancy to **+₹390/trade** (Numerical Example 2).
* *After deflation:* recognising the rules emerged from testing ~30 variants over a short 2-year sample, the trader *deflates* the edge to a believable **~+₹200/trade** and the Sharpe to ~0.6 (Numerical Example 3).
* *Data check:* the trader re-runs the fills at *bid/ask* with a liquidity filter (Section 3.5) — confirming the edge survives realistic fills (it does, thinly).

**Verdict:** a *real but thin* edge (~₹200/trade), the variance risk premium — not the ₹840 the naive backtest showed. The trader will size for the ₹200, not the ₹840.

**Stage 3 — Paper trade.** Before risking capital, the trader paper-trades the system live for 3 months (~12 trades). Live-market frictions the backtest could not fully capture — actual fills, missed entries, adjustment timing — show up:

* *Paper expectancy:* **+₹250/trade** — below the backtest's cost-adjusted ₹390 (revealing residual backtest optimism), but positive and near the deflated ~₹200 estimate. The paper stage *validates* that the edge survives live execution, and surfaces execution issues (e.g., difficulty getting fills on all four legs at good prices) to refine.

**Stage 4 — Live, scaled.** The trader goes live, starting with **1 lot** (Chapter 26's scaling) and a strict SOP (Section 3.7). Over the first months:

* *Live expectancy:* **+₹180/trade** — the true, hard-won edge, close to the deflated backtest estimate. The trader scales up per the equity-curve rules (Chapter 26) only as the live results confirm the edge.
* *Adjustments between backtest and live:* the trader tightens the IV-Rank filter (skipping more low-IV weeks after journaling showed those trades leaked), refines the roll trigger, and enforces the "no trade outside the playbook" rule — improvements the *journal* (not the backtest) revealed.

**The stage-by-stage reality.**

**Table 28.1 — The shrinking edge, stage by stage (per trade, illustrative)**

| Stage | Expectancy/trade | What it revealed |
| --- | ---: | --- |
| Raw backtest | +₹840 | The naive, over-optimistic figure |
| After costs & slippage | +₹390 | Costs nearly halve the edge |
| After deflation (best-of-30) | ~+₹200 | The believable edge |
| Paper trading (3 months) | +₹250 | Survives live execution; surfaces frictions |
| Live, scaled | +₹180 | The true, hard-won edge |

**The analysis.** The naive backtest promised +₹840/trade; the *real* edge was ~+₹180 — barely a fifth. A trader who had trusted and sized off the ₹840 would have over-sized against a fifth of the edge (Chapter 26) and likely blown up in the first drawdown. The *systematic process* — a reasoned hypothesis, a *rigorously deflated* backtest, a paper-trading validation, and a *scaled* live rollout with an SOP and journal — is what revealed the true edge and made it survivable. And the edge that survived was *thin but real* (the variance risk premium), harvested with defined risk, correct sizing, and iron discipline — exactly the professional's combination.

**The lesson.** Building a trading system is not about finding a spectacular backtest; it is about *honestly discovering how thin your real edge is* and building the discipline to harvest it anyway. Each stage — backtest, deflation, paper, scaled live — strips away another layer of illusion, leaving the true edge, which is almost always far smaller than the naive backtest and only worth trading with rigorous costs, sizing, and process. The professional's advantage is not a better backtest; it is the honesty to deflate it and the discipline to trade the small, real edge that remains.

*(Takeaway: the true edge is a fraction of the naive backtest — build a system through a reasoned hypothesis, a rigorously deflated and cost-inclusive backtest, a paper-trading validation, and a scaled live rollout with an SOP and journal; the professional edge is the honesty to find how thin your edge really is and the discipline to harvest it.)*

---

## 10. Chapter Summary

* A **trading system** is a completely codified process (entry, exit, sizing, adjustments, risk) that removes in-the-moment judgement — for most traders, **rules beat discretion** because they govern the emotional moments that ruin execution.
* A system needs a genuine **edge** — positive expectancy *after costs* over many trades — usually structural (the variance risk premium, the skew) or behavioural, not a curve-fitted pattern.
* **Backtest rigorously:** point-in-time data, walk-forward validation (in-sample tune, out-of-sample test), *few* parameters, and *always* realistic costs and slippage.
* **Backtests lie** via survivorship, look-ahead, overfitting, ignored costs, and — critically — **multiple-testing bias** (the best of many variants is the luckiest, not the best) requiring a **deflated** metric.
* **Option-data quality** is the biggest source of fake profits: fill at bid/ask (not LTP/mid), filter for liquidity, use point-in-time chains, and correctly handle the 2024–2026 expiry and lot-size changes.
* **Measure honestly:** expectancy, profit factor, Sharpe, **Sortino**, R-multiple, RAROC, and the **deflated Sharpe** — judge by risk-adjusted, cost-inclusive, deflated metrics, not raw return.
* **Operationalise** via a **trade playbook** (one card per strategy) and **SOPs** (pre-market, market-hours, post-market), and **journal by process, not outcome**.
* **Automate to reduce errors**, starting with alert-based execution (Kite Connect/Upstox APIs; NSE Bhav copy/Opstra/Sensibull data).
* The **iron-condor-machine case** shows the edge shrinking from a naive +₹840 to a real +₹180 across backtest → deflation → paper → live — the process reveals the true, thin edge and makes it survivable.

---

## 11. Key Takeaways

* **Trade a fully codified system, not a strategy** — rules made calmly must govern your emotional moments.
* **Assume your backtest is too optimistic** — include costs and slippage, validate out-of-sample, test few variants, deflate for the number tried, and interrogate the data.
* **Judge by process and journal everything** — a process-focused journal reveals the edge (and the leaks) no backtest can.
* **The true edge is a fraction of the naive backtest** — find how thin it really is, size for *that*, and harvest it with defined risk, discipline, and an SOP.

---

## 12. Practice Questions

**Q1 (System).** In one or two sentences, what distinguishes a "trading system" from "a strategy," and why does it matter?

**Q2 (Edge).** Define an edge, and state the three things a backtested edge must survive to be real.

**Q3 (Expectancy).** A system has a 60% win rate, average win ₹6,000, average loss ₹5,000. Compute the raw expectancy per trade.

**Q4 (Costs).** For the Q3 system, if costs and slippage are ₹500/trade, what is the net expectancy?

**Q5 (Multiple testing).** Explain why trading the best of 40 backtested variants is likely to fail live.

**Q6 (Data quality).** Why does backtesting fills at the LTP (or mid) of illiquid strikes overstate a strategy's edge?

**Q7 (Sharpe/Sortino).** A strategy has monthly mean return 2.5%, SD 5%, downside deviation 3%, risk-free 0.5%/month. Compute the annualised Sharpe and Sortino.

**Q8 (R-multiple).** A trade risks ₹10,000 and makes ₹15,000. What is its R-multiple? A trade that hits its max loss is what R?

**Q9 (Deflation).** Why must a raw backtest Sharpe be deflated, and what three factors drive the size of the haircut?

**Q10 (Case judgement).** In the iron-condor-machine case, the naive backtest showed +₹840/trade but the live edge was +₹180. What would have happened to a trader who sized off the ₹840, and what is the lesson?

---

## 13. Detailed Solutions

**A1.** A **strategy** specifies *what* to trade; a **system** codifies *everything* — entry, exit, position sizing, adjustments, and risk limits — so completely that no in-the-moment judgement is required. It matters because the codified system removes the emotional, in-the-moment decisions (fear, greed, revenge) that corrupt discretionary execution, and it makes the approach testable and consistent.

**A2.** An **edge** is a positive expected value per trade that persists over a large sample (after costs). A backtested edge must survive: (i) **transaction costs** (STT, brokerage, GST); (ii) **slippage** (real fills at bid/ask, not mid); and (iii) **honest validation** (out-of-sample testing and deflation for the number of variants tried).

**A3.** Expectancy = (0.60 × 6,000) − (0.40 × 5,000) = 3,600 − 2,000 = **+₹1,600/trade** (raw, before costs).

**A4.** Net expectancy = 1,600 − 500 = **+₹1,100/trade** — still positive, but costs consumed nearly a third of the raw edge.

**A5.** Because testing 40 variants and picking the best is **data-mining (p-hacking)**: even among 40 *edgeless* strategies, the best will show an impressive backtest *by chance*. The winner is likely the *luckiest* fit to past noise, not a real edge, so it fails live. The more variants tested, the more the best result is inflated by luck; it must be deflated for the number tried.

**A6.** Because you cannot actually *transact* at the LTP or mid in an illiquid strike — you buy at the (higher) ask and sell at the (lower) bid, and the printed LTP may be a *stale* quote from hours ago that no order could have hit. Filling at LTP/mid books profits on fills that were never executable, overstating the edge; realistic backtests fill at (or worse than) the bid/ask with a liquidity filter.

**A7.** Sharpe (monthly) = (2.5 − 0.5)/5 = 0.40 → annualised = 0.40 × √12 ≈ **1.39**. Sortino (monthly) = (2.5 − 0.5)/3 = 0.667 → annualised = 0.667 × √12 ≈ **2.31**. (The Sortino exceeds the Sharpe because it penalises only downside volatility.)

**A8.** R-multiple = profit ÷ initial risk = 15,000 ÷ 10,000 = **+1.5R**. A trade that hits its max loss (loses its full initial risk) is **−1R**.

**A9.** A raw backtest Sharpe must be deflated because it *overstates* the true edge, and the haircut's size is driven by: (i) the **number of variants tested** (more trials → the best is more luck-inflated); (ii) the **sample length** (shorter samples → less reliable, larger haircut); and (iii) the **non-normality of returns** (option returns have fat tails and skew, which the raw Sharpe's normal-distribution assumption ignores). The deflated Sharpe is the believable figure.

**A10.** A trader sizing off the +₹840 backtest would have **over-sized by roughly 4–5×** relative to the true +₹180 edge (Chapter 26) — deploying positions far too large for the real, thin edge. In the first normal drawdown, the over-sized positions would have produced an outsized loss, likely a blow-up (Chapters 25, 26). The lesson: **size for the *deflated, cost-inclusive* edge, not the naive backtest** — the true edge is a fraction of what the raw backtest shows, and over-sizing against the illusion is fatal.

---

## 14. Mini Glossary

* **Trading system** — a completely codified set of rules (entry, exit, sizing, adjustments, risk) that removes in-the-moment judgement. → this chapter.
* **Edge** — a positive expected value per trade, after costs, that persists over many trades. → this chapter.
* **Backtesting** — testing a system's rules against historical data to estimate its edge. → this chapter.
* **Walk-forward analysis** — optimising on an in-sample period and testing on a separate out-of-sample period. → this chapter.
* **Overfitting (curve-fitting)** — tuning a system to past noise, which does not repeat; the biggest source of false edges. → this chapter.
* **Multiple-testing / data-mining bias** — the inflation of the best result when many variants are tested (p-hacking). → this chapter.
* **Deflated Sharpe** — the raw Sharpe discounted for trials, sample length, and non-normality; the believable figure. → this chapter.
* **Option-data quality** — the correctness of backtest data (bid/ask vs LTP, liquidity, point-in-time chains); the biggest source of fake profits. → this chapter.
* **Expectancy** — (win rate × avg win) − (loss rate × avg loss); the core edge measure, positive after costs. → this chapter.
* **Sharpe / Sortino ratio** — return per unit of total / downside volatility. → this chapter.
* **R-multiple** — trade profit divided by the initial risk (a max loss is −1R). → this chapter.
* **Trade playbook / SOP** — the one-card-per-strategy specification and the daily pre/during/post-market routine that operationalise the system. → this chapter.

---

<!-- End of Chapter 28 (OPENS Part VIII). Rev 2 (5 Aug 2026): setting label lot 75→65; illustrative backtest ₹ figures kept (empirical outputs, lot-independent ratios); data-cleanliness note broadened to 2024–2026 expiry/lot changes. Backtest (NIFTY weekly IC, 2yr, 100 trades): win 68%, avg win ₹5,000, avg loss ₹8,000 → expectancy +₹840, PF 1.33, total ₹84,000/lot. After costs/slippage ~₹450 → +₹390. Deflated (best-of-30) → ~+₹200. Sharpe 1.30/Sortino 2.08 (deflated Sharpe ~0.6). R-multiple expectancy +0.105R. Edition 2: multiple-testing bias, deflated Sharpe, option-data quality (LTP vs bid/ask, stale quotes, point-in-time, 2024–2026 expiry/lot transitions). Case study 4 stages (Table 28.1): raw +₹840 → costs +₹390 → deflated +₹200 → paper +₹250 → live +₹180. Q3 +₹1,600, Q4 +₹1,100, Q7 Sharpe 1.39/Sortino 2.31, Q8 +1.5R/−1R. Ties to Ch3 costs, Ch14 VRP, Ch18/21 strategy, Ch25/26 risk/sizing. IV = implied volatility. Psychology previewed for next chapter without number. -->
