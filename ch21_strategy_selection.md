<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapters 13, 14, 16, 17, 18, 19, 20. Target length ~8,000 words. Current as of 5 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot 65 (NSE Jan-2026 revision). CAPSTONE of Part V. Mostly conceptual (4-factor model, decision matrix, EV, breakeven win rate, Kelly preview, personas, regime table) — all lot-independent, unchanged. Lot-scaled items updated to lot 65: account-size table naked margin ~₹1.5→~₹1.3 lakh/lot; case study condor margin ₹9,000→₹7,800, strangle margin ~₹1.4→~₹1.2 lakh (ballooning to ~₹1.9 lakh in spike), Trader A loss −₹2,600/lot (−₹40/unit), Trader B loss −₹16,250/lot (−₹250/unit), still ~six-fold. Per-unit EV/breakeven figures unchanged (condor RR0.67→60%; butterfly RR12→8%; EV examples +₹10/−₹10/+₹5 per unit). NIFTY only; gross P&L → Apr-2026 STT not applicable. IV = implied volatility. -->

# Chapter 21 — Strategy Selection Framework: Choosing the Right Play

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Build a systematic strategy-selection process from four factors — direction, volatility, time, and risk appetite.
2. Match market conditions to the optimal strategy using a decision matrix.
3. Understand why strategy *selection* matters more than entry *timing*.
4. Develop a personal strategy repertoire — three to five strategies mastered deeply.

This is the capstone of Part V. You now know a dozen strategies (Chapters 16–20); this chapter is the meta-skill that decides *which one to use, when*. It is, for most traders, the single highest-leverage chapter in the book — because the right strategy in the wrong conditions loses, and picking the fit is worth more than any refinement of timing.

---

## 2. Introduction

A trader has spent months mastering strategies. They can construct an iron condor in their sleep, price a calendar, structure a backspread. And still they lose — because they use the *same* strategy in every market. They sell iron condors into a trending market that runs through their strikes; they buy long options into a dead range where Theta grinds them down; they hold short strangles into a volatility spike. Their execution is flawless. Their *selection* is fatal.

This is the lesson of Part V's capstone: **the strategy you choose matters more than how well you time it.** A mediocre entry into the *right* strategy for the conditions beats a perfect entry into the *wrong* one. The market is always in some regime — trending, ranging, or volatile — and some volatility state — IV rich or cheap — and each combination has strategies that thrive and strategies that die. The skill is not knowing twenty strategies; it is having a *system* that maps the current conditions to the two or three strategies that fit, and the discipline to trade only those.

This chapter gives you that system. A **four-factor model** (direction, volatility, time, risk appetite) narrows the whole strategy universe to a handful; a **decision matrix** maps conditions to structures; the **economics** (expected value, risk-reward, breakeven win rate) show why high-win-rate and low-win-rate strategies can both be sound; and the **repertoire** concept — master three to five, not twenty — turns the system into a personal, practiced discipline. We close with the case that proves the thesis: two traders, same view, same market, opposite outcomes, decided entirely by strategy fit. Setting: **NIFTY at 24,600**, drawing on every strategy from Chapters 16–20.

---

## 3. Core Concepts

### 3.1 Why selection beats timing

The flagship idea of this chapter is simple and under-appreciated: **choosing the right strategy for the conditions matters more than timing the entry.**

**What is it?** Strategy selection is the process of matching a *structure* (long call, iron condor, calendar, backspread…) to the *current market conditions* (direction, volatility, time horizon, your risk tolerance) — before worrying about the exact entry moment.

**Why does it matter more than timing?** Because a strategy's *structure* determines how it behaves across a range of outcomes, while timing only shifts the entry point slightly. Sell an iron condor in a trending market and no entry timing saves you — the trend runs through your strikes. Buy a long straddle in a dead range and no timing helps — Theta bleeds it to zero. But pick the *fitting* structure (a directional spread in the trend, a condor in the range) and even a clumsy entry usually works out. The structure is the decision; the timing is the footnote.

**Intuitive explanation.** Selection is choosing the *right vehicle for the terrain*; timing is choosing exactly when to set off. A sports car on a mountain trail fails no matter when you start; a jeep on the same trail succeeds even if you leave an hour late. Traders obsess over the departure time (timing) and neglect the vehicle (strategy) — exactly backwards.

**Why should a trader care?** Because it redirects effort to where the payoff is. Most traders pour energy into entry signals and ignore whether the strategy even fits the regime. Flip that: spend your effort classifying the conditions and selecting the fitting structure, and the results follow.

**Common mistake.** The "one-strategy trader" — someone who has found a favourite (usually the iron condor or the long call) and runs it in *every* market, winning when the regime happens to suit it and losing when it does not, never understanding why.

**Practical takeaway.** **Classify the conditions first, then select the structure that fits — the vehicle matters more than the departure time, and the right strategy in the wrong market always loses.**

---

### 3.2 The four-factor selection model

Every strategy choice reduces to four questions. Answer them, and the universe of strategies collapses to a handful.

**Factor 1 — Directional view.** *Bullish / Bearish / Neutral / No view (expecting a big move).* Which way (if any) do you think the market goes?

**Factor 2 — Volatility view.** *IV high (sell premium) / IV low (buy premium) / IV neutral.* Are options rich or cheap (IV Rank, Chapter 14)? This decides whether you are a net *seller* or *buyer* of premium — often the *most* important factor, because it determines your Vega sign.

**Factor 3 — Time horizon.** *Intraday / 1–3 days / 1–2 weeks / 1 month+.* How long until your thesis plays out? This picks the expiry (weekly vs monthly) and governs your Theta/Gamma exposure.

**Factor 4 — Risk appetite.** *Conservative (defined risk only) / Moderate (small naked exposure) / Aggressive (unlimited risk acceptable).* How much risk — and margin — can you carry and stomach? This decides between defined-risk (spreads, condors, butterflies) and undefined-risk (naked strangles, ratio spreads) structures.

The full space is large (4 × 3 × 4 × 3 = 144 combinations), but in practice the **first two factors — direction and volatility — do most of the work**, narrowing the choice to two or three candidates. Time and risk appetite then *refine* the selection (which expiry, defined or naked). Think of it as: *direction and volatility choose the strategy family; time and risk appetite choose the specific version.*

---

### 3.3 The decision matrix

Crossing the two dominant factors — **direction × volatility** — gives the core selection matrix. Table 21.1 maps each cell to the fitting strategies from Chapters 16–20.

**Table 21.1 — Core strategy decision matrix (direction × volatility)**

| Direction ↓ / IV → | **Low IV (buy premium)** | **High IV (sell premium)** |
| --- | --- | --- |
| **Bullish** | Long call; bull call spread (debit) | Bull put spread (credit); cash-secured put |
| **Bearish** | Long put; bear put spread (debit) | Bear call spread (credit) |
| **Neutral** | Long straddle/strangle; **calendar** | **Iron condor**; short strangle; iron butterfly |
| **Big move, no direction** | Long straddle/strangle; **put backspread** | (avoid buying; a ratio spread only for a *moderate* drift) |

The logic is consistent throughout: **volatility decides buy vs sell** (low IV → debit/long structures; high IV → credit/short structures), and **direction decides call vs put vs neutral**. Two refinements from the last two chapters:

* The **calendar** (Chapter 19) is the neutral *low-IV* choice (long Vega — profits as IV rises), while the **iron condor** (Chapter 18) is the neutral *high-IV* choice (short Vega — profits as IV falls). Same neutral view, opposite volatility bet.
* The **put backspread** (Chapter 20) is the *low-IV, big-down-move* choice (cheap long-vol convexity), while the **ratio spread** fits a *high-IV, moderate-drift* view (short-vol, collect the rich extra premium).

**Applying time and risk appetite.** Once the matrix gives you a family:

* **Time horizon** picks the expiry — a few days → weekly (fast Theta); weeks → monthly (patient).
* **Risk appetite** picks the version — conservative → the *defined-risk* form (bull put *spread*, iron *condor*); aggressive → the *naked* form (short put, short strangle). A conservative and an aggressive trader with the *same* direction/volatility view choose different rows of the same family.

---

### 3.4 The economics — why both high and low win-rate strategies work

A recurring confusion is "which is better — high-probability selling or high-payoff buying?" The answer: **neither, inherently** — both can be profitable, and the choice is about the P&L *distribution* you can handle. Three tools make this precise.

**Expected value (EV)** is the only measure of whether a strategy is worth trading:

```
EV = (Win rate × Average win) − (Loss rate × Average loss)
```

A strategy is worth trading only if EV > 0, regardless of its win rate.

**The breakeven win rate** is the win rate at which EV = 0 — the hurdle a strategy must clear:

```
Breakeven win rate = Average loss / (Average win + Average loss) = 1 / (1 + Reward-to-risk)
```

This formula reveals the fundamental symmetry:

* **High-win-rate strategies (selling: credit spreads, condors)** have *low* reward-to-risk, so they need a *high* breakeven win rate. A condor with RR 0.67 needs to win **60%** of the time just to break even.
* **Low-win-rate strategies (buying: long options, debit spreads, butterflies)** have *high* reward-to-risk, so they clear a *low* breakeven win rate. A butterfly with RR 12 breaks even winning just **8%** of the time.

Neither is "better" — they are the same coin (positive EV) seen from opposite sides. The credit-spread seller wins often and small; the option buyer wins rarely and big. The right choice depends on which distribution fits your temperament, capital, and the conditions — *not* on which has the higher win rate.

**The Kelly Criterion (preview).** Once a strategy has positive EV, *how much* to bet is a separate question, answered by the Kelly Criterion:

```
Optimal fraction f* = (p × b − q) / b       (p = win prob, b = win/loss ratio, q = 1 − p)
```

Kelly maximises long-run growth, but full Kelly is too aggressive for options — most traders use half- or quarter-Kelly. This is a *preview*; position sizing gets its full treatment later in the book. The point here: selection (which strategy) and sizing (how much) are *separate* decisions — get the strategy fit right first, then size it.

> **Beginner Alert — a high win rate is not an edge.** The seductive appeal of credit spreads and iron condors is their high win rate (60–80%). But the breakeven-win-rate formula shows that high win rate comes with *low* reward-to-risk — you must win *most* of the time just to break even, and one un-managed loss erases many wins. Conversely, a "risky-looking" long butterfly that wins only 1 time in 10 can be highly profitable because its rare win is huge. Judge every strategy by **expected value**, never by win rate alone.

---

### 3.5 The strategy repertoire — master a few, deeply

You have learned a dozen strategies. You should *trade* three to five.

**The repertoire concept.** A **strategy repertoire** is the small set of strategies you have mastered deeply — knowing their Greeks, their adjustments, their fit, and their failure modes cold — and trade repeatedly. The alternative, knowing twenty strategies superficially and dabbling in each, is a recipe for mediocre execution and no learning curve.

**The Pareto principle applied.** As the book's philosophy holds (Chapter 1), roughly **80% of a trader's profits come from three to five strategies executed well.** Depth beats breadth: a trader who has run iron condors through fifty expiries — learned every adjustment, every failure — will vastly outperform one who runs a different exotic structure each week. Mastery compounds; dabbling does not.

**Building your deck.** Choose your three to five to *cover the regimes* you expect to trade — for most retail traders, something like: a *directional debit spread* (for trends in cheap IV), a *credit spread or iron condor* (for ranges in rich IV), a *calendar* (for cheap-IV neutral), and perhaps a *long option or backspread* (for expected big moves). Write down, for each, the *exact* entry criteria, strike/expiry rules, adjustment triggers, and exit rules — your "strategy card deck." Then trade only from the deck.

---

### 3.6 Strategy fit by account size

Capital constrains the strategy set — not because bigger is better, but because some structures require margin or size that small accounts cannot deploy safely.

**Table 21.2 — Strategy fit by account size (illustrative)**

| Account size | Suited strategies | Why |
| --- | --- | --- |
| **Small (₹2–5 lakh)** | Debit spreads, long options, buying butterflies | Defined risk, low capital per trade; no naked-margin requirement |
| **Medium (₹5–20 lakh)** | Credit spreads, iron condors, calendars | Can carry defined-risk margin on several positions; income strategies viable |
| **Large (₹20+ lakh)** | Short strangles (with adjustments), ratio spreads, portfolio-Greeks management | Can absorb naked-margin (~₹1.25 lakh/lot) and manage a book of positions |

The principle: **smaller accounts must stay defined-risk** (a single naked-strangle blow-up can end a ₹3 lakh account), while larger accounts *can* deploy naked and ratio structures — but only with the discipline and margin buffer to survive their tails. Account size is a *constraint* on the risk-appetite factor, not a licence to take more risk.

---

### 3.7 Strategy rotation and journaling

**No strategy wins in every regime** — this is the reason the framework exists. Table 21.3 shows how the main strategy families perform across the three market regimes.

**Table 21.3 — Strategy performance by market regime**

| Strategy | Trending | Ranging | Volatile (rising IV) |
| --- | :---: | :---: | :---: |
| Directional buy (long option / debit spread) | ✓ (if right way) | ✗ (Theta bleed) | ✓ (long Vega) |
| Credit spread / iron condor | ✗ (run over) | ✓✓ | ✗ (short Gamma/Vega) |
| Short strangle | ✗✗ | ✓✓ | ✗✗ |
| Long straddle / strangle / backspread | ~ | ✗ (valley/decay) | ✓✓ |
| Calendar | ~ | ✓ (if IV rising) | ✓ (long Vega) |

The table's lesson is stark: **the iron condor that prints money in a range gets run over in a trend and crushed in a volatility spike.** No single strategy is robust to all conditions. Therefore you must **rotate** — shift your *active* strategy set as the regime changes: sell condors in quiet ranges (rich IV), switch to directional spreads when a trend establishes, and move to long-vol structures (calendars, backspreads) when IV is cheap and a move looms.

**Journaling makes rotation possible.** You cannot rotate intelligently without knowing *which strategies work for you in which conditions.* A **trade journal** — recording each trade's strategy, the conditions (direction, IV Rank, regime), and the outcome — is the data that tells you your real edge per strategy per regime. Over time it reveals which of your repertoire strategies to lean on and when — turning "strategy rotation" from a slogan into a data-driven discipline.

---

## 4. Examples (Real-World) — three personas

The framework produces different repertoires for different traders. Three archetypes:

**Persona 1 — The Conservative Retiree (₹5 lakh, income-focused, low risk).** Wants steady income with strictly defined risk and no margin-call anxiety. Repertoire: **bull put spreads** and **iron condors** (in rich IV), **calendars** (in cheap IV), and — if holding an equity portfolio — **covered calls** (Chapter 16). Never trades naked. Trades few, sizes small, prioritises capital preservation over return.

**Persona 2 — The Moderate Swing Trader (₹10 lakh, directional, 1–2 week horizon).** Takes directional views on NIFTY over one-to-two weeks and expresses them through the IV lens. Repertoire: **debit spreads** (bull call / bear put) when IV is cheap, **credit spreads** (bull put / bear call) when IV is rich, and occasional **long options** for high-conviction moves in low IV. Uses defined-risk throughout; rotates between debit and credit by IV Rank.

**Persona 3 — The Aggressive Professional Scalper (₹25 lakh, intraday/short, active).** Runs high-frequency, actively-managed positions with the capital to carry naked margin. Repertoire: **short strangles and straddles** with disciplined adjustments (Chapter 18), **ratio spreads** to monetise the skew (Chapter 20), **expiry-day** structures, and portfolio-level Greeks management (Chapter 12). Accepts undefined risk *only* with active management and hard stops.

The same market conditions point each persona to a *different* structure within the same family — the retiree to a defined-risk condor, the professional to a naked strangle — because their **risk-appetite and capital constraints** differ, even when direction and volatility views agree.

---

## 5. Numerical Examples

### Numerical Example 1 — Breakeven win rate across strategy types

Using breakeven win rate = 1 / (1 + reward-to-risk):

```
Iron condor (RR 0.67):     1/(1+0.67) = 60%  → must win 60% just to break even
Credit spread (RR 0.50):   1/(1+0.50) = 67%  → must win 67%
Bull call spread (RR 0.87): 1/(1+0.87) = 53% → must win 53%
Long option / debit (RR 2): 1/(1+2)   = 33%  → profits winning just 33%
Long butterfly (RR 12):     1/(1+12)  = 8%   → profits winning just 8%
```

High-win-rate sellers need a *high* hurdle; high-payoff buyers clear a *low* one. Neither is inherently better — both can be positive EV.

### Numerical Example 2 — Expected value decides, not win rate

An iron condor: max profit ₹80, max loss ₹120 (RR 0.67, breakeven win rate 60%):

```
At a 65% win rate: EV = 0.65 × 80 − 0.35 × 120 = 52 − 42 = +₹10/unit (worth trading)
At a 55% win rate: EV = 0.55 × 80 − 0.45 × 120 = 44 − 54 = −₹10/unit (a losing strategy)
```

The *same* structure is a winner or a loser depending only on whether you clear its 60% breakeven win rate. A long butterfly (RR 12) with a 10% win rate: EV = 0.10 × 185 − 0.90 × 15 = 18.5 − 13.5 = **+₹5/unit** — profitable despite winning only 1 time in 10. Win rate is not edge; EV is.

### Numerical Example 3 — Applying the matrix

Conditions: **bullish** on NIFTY, **IV Rank 80** (rich), **1-week** horizon, **conservative** risk appetite.

```
Direction (bullish) × IV (high) → Table 21.1 cell: bull put spread (credit) or cash-secured put
Risk appetite (conservative) → choose the DEFINED-RISK version: bull put spread
Time (1 week) → weekly expiry
→ Selection: a weekly NIFTY bull put spread (sell a ~30Δ put, buy a lower wing)
```

The four factors funnel cleanly to one structure. Change risk appetite to *aggressive* and the same cell yields a *naked short put* instead; change IV to *low* and the cell yields a *long call or bull call spread*.

### Numerical Example 4 — Regime rotation

Over a quarter, a trader's active strategy rotates with the regime:

```
Month 1 — quiet range, IV Rank 75 → sell iron condors (short vol, range) → profits
Month 2 — trend establishes → switch to bull call spreads (directional, defined risk) → profits
Month 3 — IV cheap, event looms → buy calendars / put backspreads (long vol) → profits
```

A trader who ran iron condors in *all three* months would have profited in Month 1, been run over by the trend in Month 2, and hurt by the volatility in Month 3. Rotation — matching the active strategy to the regime — is what makes a repertoire pay across conditions.

---

## 6. Calculations (the reusable recipes)

**(a) Expected value**

```
EV = (Win rate × Average win) − (Loss rate × Average loss);  trade only if EV > 0
```

**(b) Breakeven win rate**

```
Breakeven win rate = Average loss / (Average win + Average loss) = 1 / (1 + Reward-to-risk)
```

**(c) Kelly Criterion (preview — sizing, not selection)**

```
f* = (p × b − q) / b   (p = win prob, b = win/loss ratio, q = 1 − p); use half- or quarter-Kelly
```

**(d) The four-factor funnel**

```
Direction + Volatility → strategy family (Table 21.1)
Time horizon → expiry (weekly vs monthly)
Risk appetite + account size → defined-risk vs naked version
```

---

## 7. Practical Insights

* **Classify before you construct.** Answer the four factors — direction, volatility, time, risk appetite — *before* choosing a structure. The conditions choose the strategy; you just read the matrix.
* **Volatility often matters more than direction.** IV Rank decides whether you buy or sell premium (your Vega sign) — frequently the difference between profit and loss even when the direction call is right.
* **Judge strategies by expected value, never win rate.** A 65%-win condor and a 10%-win butterfly can both be profitable; a 55%-win condor is a losing machine. Compute EV, not win rate.
* **Master three to five, and rotate them.** Depth beats breadth (Pareto), and no strategy wins in every regime — shift your active set as the market moves from range to trend to volatility.
* **Let account size constrain risk, and journal everything.** Small accounts stay defined-risk; a trade journal is the data that tells you which of your strategies works in which conditions.

> **Professional Insight — the meta-edge is fit, not cleverness.** Amateurs seek an edge in ever-more-exotic strategies; professionals find it in *fit* — trading a small set of well-understood structures, each only in the conditions that suit it, and sitting out when nothing fits. The professional's advantage over the amateur is rarely a better strategy; it is the discipline to select the right one for the regime and to *not trade* when the matrix points nowhere. Selection — including the selection to stand aside — is the meta-skill that makes all the individual strategies pay.

---

## 8. Common Mistakes

* **The one-strategy trader.** Running a favourite structure in every market, winning when the regime happens to suit it and losing otherwise, never understanding why.
* **Ignoring the volatility factor.** Choosing a strategy by direction alone and buying rich IV (or selling cheap IV) — getting the Vega sign wrong even with the right direction.
* **Chasing win rate.** Preferring high-win-rate credit strategies without noticing their unfavourable reward-to-risk and high breakeven hurdle; mistaking win rate for edge.
* **Dabbling in twenty strategies.** Knowing many superficially instead of mastering a few deeply — poor execution, no learning curve, no adjustment skill.
* **Trading the wrong strategy for the account.** A small account selling naked strangles — a single blow-up ends it; account size must constrain the risk-appetite factor.
* **Never rotating.** Failing to shift the active strategy set as the regime changes, so the range strategy that worked last month gets run over by this month's trend.

---

## 9. Case Study — "The Power of Strategy Fit"

**Context.** Two traders, **A** and **B**, have identical inputs: the same **₹10 lakh** capital, the same **neutral** view on NIFTY for the coming month (they both expect it to stay range-bound around 24,600), and the same market data. They differ in one thing only — the *strategy* they choose to express the identical view. **Trader A** sells a defined-risk **iron condor**; **Trader B** sells a **naked short strangle** for the larger premium, reasoning that "more premium is more profit." Figures are illustrative but representative; per unit (lot 65).

**The two positions.**

```
Trader A — Iron condor: sell 24,300 PE / buy 24,100 PE + sell 24,900 CE / buy 25,100 CE
   Credit ₹80, max loss ₹120, margin ₹7,800/lot (defined risk)
Trader B — Naked strangle: sell 24,300 PE @₹100 + sell 24,900 CE @₹72
   Credit ₹172, margin ~₹1.25 lakh/lot, UNLIMITED risk
```

At entry, Trader B looks smarter — collecting ₹172 versus ₹80, more than double the premium, on the same view.

**What happened — a mid-month volatility spike.** Halfway through the month, a global risk event spikes India VIX from 13 to 22, and NIFTY slides toward Trader A and B's short put strike (24,300). The identical view (range-bound) is now under pressure, and the *structures* respond completely differently:

* **Trader B (naked strangle) is hit three ways.** (i) The **margin balloons** — the VIX spike raises the SPAN requirement on the naked position from ~₹1.2 lakh toward ~₹1.9 lakh per lot, and with limited spare capital, Trader B faces a margin call and is *forced to reduce* the position at the worst moment. (ii) The **short put loses** as NIFTY falls (short Gamma) and the **VIX spike inflates it** (short Vega) — a large mark-to-market loss. (iii) The forced, panicked exit locks in a loss. Trader B ends the month down roughly **−₹250/unit (−₹16,250/lot).**
* **Trader A (iron condor) weathers it.** (i) The **margin stays at ₹7,800** — defined-risk margin does not balloon with the VIX spike (Chapter 18), so *no margin call, no forced exit*; Trader A holds calmly. (ii) The loss on the tested put side is **capped** by the long wing, and Trader A can adjust (roll the untested call side down for credit) or simply accept the bounded loss. (iii) NIFTY stabilises near the short strike, and Trader A ends the month down only about **−₹40/unit (−₹2,600/lot)** after managing the tested side.

**The outcome.** Same capital, same view, same market — but **Trader A lost ₹2,600/lot while Trader B lost ₹16,250/lot**, a six-fold difference. Trader B's larger premium was an illusion: it came bundled with unlimited risk and volatile margin that, when the spike came, turned the identical view into a large loss and a forced exit. Trader A's defined-risk structure — less premium, but stable margin and a capped loss — was the *fit* for a month that contained a volatility spike.

**The analysis.** Neither trader's *view* was wrong — NIFTY did stay broadly range-bound. What differed was **strategy fit**. Trader B chose a structure whose weaknesses (unlimited risk, margin that balloons in a spike) were exactly the ones the month exposed; Trader A chose one whose strengths (defined risk, stable margin) matched the conditions. And crucially, *Trader A did not have to predict the spike* — the defined-risk structure was more robust *across* conditions, so it protected against the spike whether or not it came. The lesson is not "condors beat strangles always" (in a dead-quiet month, B's larger premium would have won) — it is that **strategy selection determines how a view survives the conditions it actually meets**, and defined-risk structures are more robust to the conditions you cannot foresee.

**The lesson.** The strategy you choose to express a view matters more than the view itself. Two traders with the identical, *correct* market call can have opposite outcomes because one chose a structure that fit the conditions and the other did not. Select for robustness across the conditions you might meet — not just for the premium you collect on the day.

*(Takeaway: the same view expressed through different strategies produces different outcomes — select the structure whose strengths fit the conditions and whose weaknesses the conditions won't expose; defined-risk structures are the more robust default because they survive the surprises you cannot predict.)*

---

## 10. Chapter Summary

* **Strategy selection matters more than entry timing** — the right structure in the wrong conditions always loses; classify the conditions first, then select.
* The **four-factor model** — direction, volatility, time horizon, risk appetite — narrows the strategy universe; **direction and volatility choose the family**, time and risk appetite choose the version.
* The **decision matrix** (Table 21.1) maps direction × IV to structures: low IV → buy (debit/long/calendar/backspread); high IV → sell (credit/condor/strangle/ratio).
* Judge strategies by **expected value**, never win rate: **breakeven win rate = 1/(1 + reward-to-risk)**, so high-win-rate sellers need a high hurdle and high-payoff buyers a low one — both can be positive EV.
* **Kelly** (preview) sizes a positive-EV strategy; selection and sizing are separate decisions.
* Master a **repertoire of three to five** strategies deeply (Pareto: 80% of profits from a few executed well), not twenty superficially.
* **Account size constrains risk** (small → defined-risk only; large → naked/ratio with discipline), and **no strategy wins in every regime** — **rotate** the active set, guided by a **trade journal**.
* The **strategy-fit case** shows the same neutral view producing a ₹2,600 loss (condor) versus a ₹16,250 loss (naked strangle) — decided entirely by structure, because defined risk was the fit for a month with a volatility spike.

---

## 11. Key Takeaways

* **Classify the conditions, then read the matrix** — direction and volatility choose the strategy family; time and risk appetite choose the version.
* **Judge by expected value, not win rate** — a 10%-win butterfly and a 65%-win condor can both be sound; a 55%-win condor is not.
* **Master three to five strategies and rotate them by regime** — depth beats breadth, and no single strategy survives every market.
* **Select for robustness across the conditions you might meet** — defined-risk structures are the more reliable default because they survive the surprises you cannot foresee.

---

## 12. Practice Questions

**Q1 (Framework).** Name the four factors in the strategy-selection model, and state which two do most of the work.

**Q2 (Matrix).** You are bearish on NIFTY with IV Rank at 20 (cheap). From the decision matrix, which strategy family fits, and name one specific structure.

**Q3 (Matrix).** You are neutral on NIFTY. IV Rank is 25 (cheap) and you expect IV to rise. Calendar or iron condor — and why?

**Q4 (Breakeven win rate).** A credit spread has an average win of ₹40 and an average loss of ₹110. Compute the breakeven win rate.

**Q5 (Expected value).** For the Q4 spread, compute the EV at a 70% win rate and at a 75% win rate. Is it worth trading at each?

**Q6 (Win rate vs edge).** A long butterfly wins 12% of the time with an average win of ₹180 and average loss of ₹20. Compute the EV and comment.

**Q7 (Account fit).** Why should a ₹3 lakh account avoid selling naked strangles, and what should it trade instead?

**Q8 (Rotation).** A trader has sold iron condors profitably for three months in a range. A strong trend now begins. What should they do, and why?

**Q9 (Selection vs timing).** Explain, with an example, why strategy selection matters more than entry timing.

**Q10 (Judgement).** Two traders share the same correct neutral view; one sells a naked strangle, the other an iron condor. A volatility spike hits mid-month. Who is likely to fare better, and why?

---

## 13. Detailed Solutions

**A1.** The four factors are **directional view, volatility view, time horizon, and risk appetite.** **Direction and volatility** do most of the work — they choose the strategy family; time and risk appetite refine the specific version.

**A2.** Bearish + low IV → the **buy-premium, bearish** family: a **long put** or, better, a **bear put spread (debit)**. Low IV favours buying (cheap options, long Vega), and the bearish view points to put structures.

**A3.** A **calendar.** A neutral view with *cheap* IV expected to *rise* calls for a **long-Vega** structure — the calendar profits as IV rises (Chapter 19), while an iron condor is *short* Vega and would lose as IV rose. Same neutral view, opposite volatility bet; the rising-IV expectation is decisive.

**A4.** Breakeven win rate = avg loss / (avg win + avg loss) = 110 / (40 + 110) = 110/150 = **73.3%**. The spread must win over 73% of the time just to break even.

**A5.** At 70%: EV = 0.70 × 40 − 0.30 × 110 = 28 − 33 = **−₹5/unit** (below the 73.3% breakeven → *not* worth trading). At 75%: EV = 0.75 × 40 − 0.25 × 110 = 30 − 27.5 = **+₹2.5/unit** (above breakeven → worth trading, though thin). The strategy hinges entirely on clearing its 73% hurdle.

**A6.** EV = 0.12 × 180 − 0.88 × 20 = 21.6 − 17.6 = **+₹4/unit** — **profitable despite a 12% win rate**, because the rare win (₹180) is nine times the frequent loss (₹20). This proves win rate is not edge; a low-win-rate, high-payoff strategy can have positive expected value.

**A7.** A ₹3 lakh account should avoid naked strangles because a single blow-up (unlimited risk, plus margin that balloons in a volatility spike) can wipe out a large fraction — or all — of such a small account, and one lot's naked margin (~₹1.25 lakh) already consumes over a third of the capital. It should trade **defined-risk structures** — debit spreads, iron condors, butterflies — where the loss is capped and the account can survive any single trade.

**A8.** They should **rotate** — stop selling iron condors (which get *run over* in a trend, Table 21.3) and switch to **directional structures** (debit or credit spreads in the trend's direction). No strategy wins in every regime; the condor's range edge disappears in a trend, so the active strategy set must change with the regime.

**A9.** Because the *structure* determines behaviour across outcomes, while timing only shifts the entry slightly. Example: selling an iron condor in a *trending* market loses no matter how well you time the entry — the trend runs through the strikes; but a directional debit spread in the same trend profits even with a clumsy entry. The vehicle (strategy) matters more than the departure time (timing).

**A10.** The **iron condor trader (defined risk)** is likely to fare better. Both have the correct view, but the naked strangle's margin *balloons* in the volatility spike (risking a forced exit) and its loss is *unlimited*, whereas the iron condor's margin is *stable* (defined risk) and its loss is *capped* — so the condor survives the spike calmly while the strangle is hit by ballooning margin, short-Gamma/short-Vega losses, and a possible forced exit. The structure, not the view, decides the outcome; the defined-risk condor is the more robust fit.

---

## 14. Mini Glossary

* **Strategy selection** — matching a structure to the current market conditions (direction, volatility, time, risk appetite). → this chapter.
* **Four-factor model** — the framework of directional view, volatility view, time horizon, and risk appetite. → this chapter.
* **Decision matrix** — the mapping of direction × volatility to fitting strategies. → this chapter.
* **Expected value (EV)** — probability-weighted average outcome; the true test of whether a strategy is worth trading. → this chapter.
* **Breakeven win rate** — the win rate at which EV = 0; equals 1/(1 + reward-to-risk). → this chapter.
* **Reward-to-risk ratio** — average win ÷ average loss; inversely related to the breakeven win rate. → this chapter.
* **Kelly Criterion (preview)** — the optimal bet fraction for a positive-EV strategy; f* = (pb − q)/b. → this chapter.
* **Strategy repertoire** — the small set (3–5) of strategies mastered deeply and traded repeatedly. → this chapter.
* **Strategy rotation** — shifting the active strategy set as the market regime changes. → this chapter.
* **Strategy fit** — how well a structure's strengths and weaknesses match the market conditions. → this chapter.

---

<!-- End of Chapter 21 (Rev 2, CAPSTONE of Part V, current as of 5 Aug 2026). Rev 2 update: NIFTY lot 75→65 (NSE Jan-2026) — conceptual content (4-factor model, matrix, EV, breakeven win rate, Kelly, personas, regime table) unchanged. Lot-scaled: account-size table naked margin ~₹1.5→~₹1.3 lakh/lot; case study condor margin ₹9,000→₹7,800, strangle margin ~₹1.4→~₹1.2 lakh (→~₹1.9 lakh in spike), Trader A −₹2,600/lot (−₹40/unit), Trader B −₹16,250/lot (−₹250/unit), ~six-fold; summary figures ₹2,600 vs ₹16,250. Breakeven win rate = 1/(1+RR): condor RR0.67→60%, credit RR0.5→67%, bull call RR0.87→53%, debit RR2→33%, butterfly RR12→8% (per-unit, unchanged). EV examples: condor 65%→+₹10, 55%→−₹10; butterfly 10%→+₹5 (per unit). Kelly f*=(pb−q)/b. Q4 BE win rate 73.3%, Q6 butterfly EV +₹4 at 12% win (per unit). NIFTY only; gross P&L → Apr-2026 STT not applicable. IV = implied volatility. -->
