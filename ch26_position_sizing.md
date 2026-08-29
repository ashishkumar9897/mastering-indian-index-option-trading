<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapter 25. Target length ~8,500 words. Kelly f*=(pb−q)/b; example win 65%, avg win ₹1,000, avg loss ₹1,600 → b=0.625, f*=9%, half 4.5%, quarter 2.25%. Position size = risk per trade / max loss per lot; ₹10L 2% = ₹20k / ₹7.8k IC = 2 lots. Sizing table ₹5L/10L/25L/50L. Risk of ruin R=((1−edge)/(1+edge))^(capital/risk): edge 10%, risk 2%→0.004%, 5%→1.8%, 10%→13.4%, 20%→36.7%. Kelly maximizes geometric growth; over-betting reduces it. Scaling: +1 lot per ₹2L, −1 lot per ₹1L (asymmetric). Case study: 1%/3%/5% risk over 12 months — 1% +18%/DD8%, 3% +42%/DD22% (best risk-adjusted), 5% +65% peak but 40% DD → stopped. IV = implied volatility. Rev 2 (5 Aug 2026): lot 75→65; NIFTY per-lot max losses rescaled (IC ₹9k→₹7.8k, bull put ₹11.25k→₹9.75k, long debit ₹8k→₹7k, naked stress ₹50k→₹45k) per revised Ch17/Ch18; Table 26.2 recomputed. Kelly/risk-of-ruin/scaling %s lot-independent — unchanged. -->

# Chapter 26 — Position Sizing and Capital Allocation

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Apply position-sizing models appropriate for option trading.
2. Understand why position sizing has more impact on results than strategy selection.
3. Use the Kelly Criterion (modified) for option trade sizing.
4. Manage correlation and concentration risk.
5. Scale positions up and down with account equity.

Chapter 25 gave you the risk framework; this chapter answers its central quantitative question: **how much to bet on each trade.** Position sizing is where the abstract "cap your risk" becomes a precise number of lots — and it is, arguably, the single most powerful lever in trading, more powerful than the strategy itself.

---

## 2. Introduction

Two traders run the *identical* strategy, take the *identical* signals, and are right the *identical* percentage of the time. Over a year, one grows their account 42% with a drawdown they can stomach; the other rides to a 65% gain, suffers a 40% drawdown that breaks their nerve, and quits at breakeven. Same strategy, same signals, same edge — opposite outcomes, determined entirely by **position sizing.**

This is the counterintuitive truth of this chapter: *how much* you bet matters more than *what* you bet on. A mediocre strategy sized well outlasts a brilliant strategy sized recklessly, because reckless sizing produces the drawdown that ends the game (Chapter 25's recovery asymmetry). Position sizing is the bridge between having an edge and *keeping* it — the mechanism that lets a positive-expectancy strategy compound without the volatility that destroys it. Get it wrong and even a genuine edge blows up; get it right and a modest edge compounds into wealth.

This chapter builds sizing from the ground up: the fixed-rupee and fixed-percentage models; the position-size formula that turns a risk limit into lots; the **Kelly Criterion** — the growth-optimal fraction — and why you must use only a *fraction* of it; the **risk of ruin** that quantifies why small per-trade sizing matters so much; and the *scaling* rules that grow size in success and cut it in drawdown. It closes with the experiment that proves the thesis — the same strategy at 1%, 3%, and 5% risk, and why the moderate sizer won. Setting: **NIFTY at 24,600, lot 65**, building on the risk framework of Chapter 25.

---

## 3. Core Concepts

### 3.1 Why sizing beats strategy

The flagship idea of this chapter: **position sizing is the number-one determinant of long-term survival and growth — more than strategy selection.**

**What is it?** Position sizing is the decision of *how much capital to risk* on each trade — expressed, in Indian options, as *how many lots*. It converts a risk limit (Chapter 25) into a concrete position.

**Why does it matter more than the strategy?** Because sizing controls the *volatility of your equity curve*, and volatility — through the drawdown recovery asymmetry (Chapter 25) — controls survival. Two traders with the same edge but different sizing have completely different drawdowns: the aggressive sizer's larger positions produce larger drawdowns, and beyond a point those drawdowns become unsurvivable (financially or psychologically), ending the game *even though the edge was real*. The strategy sets the *edge*; the sizing determines whether you *survive to compound it*.

**Intuitive explanation.** Sizing is the **throttle** on a car with a fixed engine (the strategy). The same engine, driven with a gentle throttle, gets you there safely; floored, it crashes. The engine (edge) matters, but the throttle (sizing) determines whether you arrive. Most traders tune the engine obsessively and floor the throttle — then wonder why they crash.

**Why should a trader care?** Because a trader can improve their results *more* by fixing their sizing than by finding a better strategy. A positive-edge strategy sized too large loses (drawdown-driven ruin); the *same* strategy sized correctly wins. Sizing is the highest-leverage improvement available to most traders — and the most neglected.

**Numerical feel.** The same 60%-win strategy over 12 months (Section 9): at 1% risk it grows 18% with an 8% drawdown; at 5% risk it *peaks* at +65% but suffers a 40% drawdown that ends the trader's participation. Same strategy — the sizing made the difference between steady growth and a broken account.

**Common mistake.** Believing better returns come from a better strategy, when for most traders the binding constraint is *over-sizing* — a good strategy destroyed by too-large positions.

**Practical takeaway.** **Position sizing is a more powerful lever than strategy selection — it controls the drawdown that determines survival, so size to survive the losing streak your edge guarantees will come, not to maximise the return in the winning one.**

---

### 3.2 The sizing models — fixed rupee and fixed percentage

Two foundational models:

**Fixed rupee risk.** Risk a *constant* rupee amount per trade regardless of account size — e.g., ₹15,000 per trade, always. Simple and stable, but it does not adapt: as the account grows, the fixed risk becomes a *smaller* percentage (under-betting the edge); as it shrinks, a *larger* percentage (over-betting into a drawdown). Suitable for beginners who want a simple, unchanging rule.

**Fixed percentage risk.** Risk a constant *percentage* of *current* equity per trade — e.g., 2% of the account, recomputed as equity changes. This is the superior model for most traders because it **adapts automatically**: as the account grows, the rupee risk rises (compounding the edge); as it draws down, the rupee risk *falls* (automatically de-risking in a losing streak). The fixed-percentage model has a built-in equity-curve throttle — it presses harder when winning and eases when losing, exactly what survival requires.

The fixed-percentage model's auto-de-risking is its key virtue: after a string of losses (a smaller account), each subsequent trade risks fewer rupees, cushioning the drawdown — the opposite of the fixed-rupee model, which keeps risking the same rupees into a shrinking account, deepening the hole. For this reason, **the fixed-percentage model is the recommended default.**

---

### 3.3 The position-size formula

Whatever the model, the mechanical step is the same — convert the risk limit into lots:

```
Position size (lots) = Risk per trade / Maximum loss per lot
```

**For defined-risk strategies** this is straightforward, because the max loss per lot is *known* (Chapter 17). A ₹10 lakh account at 2% risk allows ₹20,000 per trade; a NIFTY iron condor with a ₹7,800 max loss per lot (Chapter 18) gives:

```
Lots = 20,000 / 7,800 = 2.56 → 2 lots (round down)
```

**For undefined-risk strategies** (naked options, strangles) it is harder, because the *theoretical* max loss is enormous (or unlimited). You cannot size off the theoretical max; instead you size off an **expected/stress max loss** — the loss on a plausible adverse scenario (e.g., a 2-standard-deviation move plus a vol spike, Chapter 25's stress test). If a naked strangle could lose ₹45,000 per lot on a realistic stress scenario, then a ₹20,000 risk budget allows *zero* lots — which is precisely why small accounts should not trade naked (Chapter 21). Undefined-risk sizing must use the *stress* loss, not the premium collected, or it dangerously over-sizes.

> **Beginner Alert — never size a naked position off the premium.** The seductive error is "I collected ₹10,000, so my risk is ₹10,000." No — a naked short option's risk is the *loss on a large move*, which can be many times the premium (Chapters 18, 22). Size undefined-risk positions off a *stress-scenario* loss (what a 2-SD move plus a vol spike would cost), not off the credit received. Doing otherwise is how the account in Chapter 25 blew up.

---

### 3.4 The Kelly Criterion — the growth-optimal fraction

The **Kelly Criterion** answers, mathematically, the question "what fraction of capital maximises long-run growth?"

```
Kelly fraction f* = (p × b − q) / b
```

where **p** = win probability, **b** = the win/loss ratio (average win ÷ average loss), and **q** = 1 − p. Kelly gives the fraction of capital that **maximises the geometric (compounding) growth rate** of the account (Section 3.4's note on geometric mean).

**Worked example.** From a trade journal, a credit-spread strategy shows: win rate 65% (p = 0.65, q = 0.35), average win ₹1,000, average loss ₹1,600 (b = 1,000/1,600 = 0.625):

```
f* = (0.65 × 0.625 − 0.35) / 0.625 = (0.406 − 0.35) / 0.625 = 0.056 / 0.625 ≈ 0.09 = 9%
```

Full Kelly says risk 9% of capital per trade. But **full Kelly is far too aggressive for options**, for three reasons:

* **Brutal drawdowns.** Full Kelly maximises *growth* but accepts enormous volatility — full-Kelly betting routinely produces 50%+ drawdowns, beyond what most traders can survive financially or psychologically (Chapter 25).
* **Estimation error.** Kelly requires *accurate* p and b. Traders systematically *overestimate* their edge (recency bias, small samples), and an overestimated edge makes Kelly *over-size* — with severe consequences.
* **The geometric-mean penalty.** Betting *above* Kelly actually *reduces* long-run growth (while raising volatility) — the worst of both worlds.

So practitioners use **fractional Kelly** — **half-Kelly (4.5% here) or quarter-Kelly (2.25%)** — which captures most of the growth with far less volatility, and cushions against overestimating the edge. And crucially, the fractional Kelly must still be **capped by the per-trade risk limit** (Chapter 25): use the *smaller* of the fractional-Kelly fraction and your risk limit. Here, quarter-Kelly (2.25%) sits comfortably within a 2–5% limit; half-Kelly (4.5%) is at the aggressive end.

> **Market Note — Kelly is a ceiling, not a target.** Kelly tells you the *most* you should ever risk to a growth-optimal edge — and even that is too aggressive in practice. Treat the fractional-Kelly number as an upper bound to stay *well below*, especially because your estimated edge is almost certainly too optimistic. When Kelly and your risk limit disagree, use the smaller. Sizing errors are asymmetric: under-betting costs you some growth, but over-betting costs you the account.

---

### 3.5 Risk of ruin — why small sizing matters so much

The **risk of ruin** — the probability of losing enough to be knocked out — quantifies *why* small per-trade sizing is so powerful. A simplified formula:

```
Risk of ruin R = [ (1 − edge) / (1 + edge) ] ^ (capital / risk per trade)
```

where the exponent (capital ÷ risk per trade) is the number of "risk units" you can absorb. The key insight: risk of ruin falls **exponentially** as you risk *less* per trade. Table 26.1 shows this for a strategy with a 10% edge.

**Table 26.1 — Risk of ruin by per-trade risk (10% edge)**

| Risk per trade | Risk units (capital/risk) | Risk of ruin |
| ---: | ---: | ---: |
| 2% | 50 | ~0.004% |
| 5% | 20 | ~1.8% |
| 10% | 10 | ~13.4% |
| 20% | 5 | ~36.7% |

The numbers are dramatic: risking **2%** per trade gives a **0.004%** chance of ruin — effectively zero — while risking **20%** gives a **37%** chance of ruin with the *same edge*. Halving your per-trade risk does not halve your risk of ruin; it slashes it *exponentially*. This is the mathematical heart of "size small": the edge is the same, but the survival probability is transformed. A trader with a real edge who risks 2% per trade is virtually certain to survive to compound it; the same trader risking 20% has a one-in-three chance of ruin *despite the identical edge*.

> **Professional Insight — you cannot compound if you are out of the game.** The entire purpose of small per-trade sizing is to make ruin *effectively impossible*, so that your edge has time to work. Professionals think of it as buying survival cheaply: the small "cost" of under-betting (slightly slower growth) purchases near-certain survival, which is the precondition for *all* future growth. The trader who risks 20% for faster growth is trading a one-in-three chance of ruin for a bigger number they may never live to collect.

---

### 3.6 Scaling up and down

Position size should *change* with the account — growing in success, shrinking in drawdown — through **equity-curve-based scaling.**

**Scaling up.** Add size only as the account grows *and* the system proves consistent. A common rule: **add one lot per ₹2 lakh of profit.** Start with 1 lot on a ₹10 lakh account; at ₹12 lakh, go to 2 lots; at ₹14 lakh, 3 lots. This compounds the edge as capital grows — but *only* after the system has demonstrated it works (don't scale up on a lucky streak with a small sample).

**Scaling down.** Cut size *faster* in a drawdown: **reduce one lot per ₹1 lakh of drawdown.** The asymmetry is deliberate — you *add* size per ₹2 lakh gained but *cut* size per ₹1 lakh lost, so you de-risk twice as fast as you risk up. In a drawdown from ₹14 lakh (3 lots), a ₹1 lakh loss (to ₹13 lakh) cuts to 2 lots, protecting capital before the drawdown deepens. This equity-curve throttle — add slowly, cut quickly — is what keeps a losing streak from becoming a blow-up.

The principle: **let the equity curve size the account.** When you are winning (rising equity), the fixed-percentage model and scaling-up rule increase size, compounding gains; when you are losing (falling equity), both *reduce* size, cushioning the drawdown. This automatic throttle is more reliable than any discretionary "I feel confident" sizing.

---

### 3.7 Concentration, lot granularity, and the "one more lot" temptation

Three practical constraints complete the picture:

**Concentration limits.** No more than a set percentage of capital in a *single expiry or strategy* — because all NIFTY positions are correlated (Chapter 25), over-concentrating in one expiry means one bad expiry can hit everything. Spread size across expiries and strategies (limited as that diversification is), and cap any single one.

**Lot-size granularity.** Indian options trade only in *whole lots*, which creates a **granularity problem** for smaller accounts. A ₹5 lakh account at 2% risk (₹10,000) can afford ~1 iron condor lot (₹7,800 max loss) — so it cannot size *precisely* (it's 1 lot or 2, not 1.1). Small accounts are forced into coarse sizing, which is another reason they should stick to low-max-loss, defined-risk structures where 1 lot fits the risk budget. Larger accounts have finer granularity (more lots) and can size more precisely.

**The "one more lot" temptation.** The pervasive urge to add "just one more lot" — to a winner (greed) or a loser (revenge/averaging down) — almost always hurts. Adding to a *winner* increases size after the easy money is made, raising risk at the worst time; adding to a *loser* (averaging down) throws more capital at a failing thesis, deepening the loss. Disciplined sizing means the position size is set by the *rule* (risk limit, fractional Kelly, scaling), not by the emotion of the moment. "One more lot" is how a rule-based sizer becomes a gambler.

---

## 4. Examples (Real-World)

**Example 1 — The fixed-percentage throttle.** A trader risking 2% of current equity per trade hits a losing streak. As the account shrinks from ₹10 lakh to ₹8.5 lakh, each subsequent trade automatically risks less (2% of a smaller number) — cushioning the drawdown. A fixed-rupee sizer, risking ₹20,000 regardless, would have kept betting the same into the shrinking account, deepening the hole.

**Example 2 — Kelly tempered.** A trader computes a 9% full-Kelly fraction from their journal, recognises it as far too aggressive, and trades quarter-Kelly (2.25%) — within their 3% risk limit. They capture most of the compounding with a fraction of the drawdown, and their over-optimistic edge estimate does not blow them up.

**Example 3 — The "one more lot" that hurt.** After three winning trades, a trader adds an extra lot on the fourth "because I'm on a roll." The fourth loses, and the oversized position turns a small loss into a large one — the greed-driven size increase struck exactly when the streak ended. The rule would have kept the size constant; the emotion did not.

---

## 5. Numerical Examples

Setting: NIFTY 24,600, lot 65.

### Numerical Example 1 — Kelly and fractional Kelly

A credit-spread strategy: win rate 65% (p = 0.65, q = 0.35), average win ₹1,000, average loss ₹1,600 (b = 0.625):

```
f* = (0.65 × 0.625 − 0.35) / 0.625 = 0.056 / 0.625 ≈ 0.09 = 9% (full Kelly)
Half-Kelly = 4.5%;  Quarter-Kelly = 2.25%
```

Full Kelly (9%) is too aggressive for options; quarter-Kelly (2.25%) fits comfortably within a 2–5% per-trade limit. The trader sizes at ~2.25% — capturing most of the growth with far less drawdown, and cushioned against overestimating the 65% win rate.

### Numerical Example 2 — Position size from the risk limit

A ₹10 lakh account, 2% risk (₹20,000/trade), NIFTY iron condor (max loss ₹7,800/lot):

```
Lots = Risk per trade / Max loss per lot = 20,000 / 7,800 = 2.56 → 2 lots (round down)
```

The trader can hold 2 iron condor lots within their risk limit (max loss 2 × ₹7,800 = ₹15,600, under the ₹20,000 budget). For a naked strangle with a *stress* max loss of ₹45,000/lot, the same budget allows 20,000/45,000 = 0.44 → **0 lots** — the account is too small for naked risk.

### Numerical Example 3 — The position-sizing table

At 2% risk across account sizes and strategies (max loss/lot: iron condor ₹7,800; bull put spread ₹9,750; long debit ₹7,000; naked strangle ₹45,000 stress):

**Table 26.2 — Maximum lots by account size (2% risk)**

| Account | 2% risk | Iron condor | Bull put spread | Long debit | Naked strangle |
| ---: | ---: | ---: | ---: | ---: | ---: |
| ₹5 lakh | ₹10,000 | 1 | 1 | 1 | 0 |
| ₹10 lakh | ₹20,000 | 2 | 2 | 2 | 0 |
| ₹25 lakh | ₹50,000 | 6 | 5 | 7 | 1 |
| ₹50 lakh | ₹1,00,000 | 12 | 10 | 14 | 2 |

Small accounts (₹5 lakh) can barely size defined-risk trades (1 lot) and *cannot* trade naked (0 lots) — reinforcing Chapter 21's account-size fit. Larger accounts get finer granularity and can carry naked risk within the limit.

### Numerical Example 4 — Risk of ruin

For a strategy with a 10% edge, risking 2% versus 10% per trade:

```
Risk 2% (50 units): R = (0.9/1.1)^50 = (0.8182)^50 ≈ 0.004%
Risk 10% (10 units): R = (0.8182)^10 ≈ 13.4%
```

The *same edge* gives a 0.004% ruin probability at 2% risk and a 13.4% probability at 10% risk — a 3,000-fold difference from sizing alone. Risking small is not caution; it is what makes the edge *bankable*.

### Numerical Example 5 — The scaling model

Start ₹10 lakh, 1 lot; add 1 lot per ₹2 lakh profit, cut 1 lot per ₹1 lakh drawdown:

```
₹10L → 1 lot;  ₹12L (+₹2L) → 2 lots;  ₹14L (+₹2L) → 3 lots
Drawdown to ₹13L (−₹1L) → 2 lots;  further to ₹12L (−₹1L) → 1 lot
```

Size grows with the account in success and *falls faster* in drawdown (cut per ₹1L, add per ₹2L) — the asymmetric throttle that compounds gains while protecting against a losing streak.

---

## 6. Calculations (the reusable recipes)

**(a) Position size**

```
Position size (lots) = Risk per trade / Max loss per lot
   (defined-risk: use the known max loss; undefined-risk: use a STRESS-scenario loss, not the premium)
```

**(b) Kelly Criterion and fractional Kelly**

```
f* = (p × b − q) / b     (p = win prob, b = avg win/avg loss, q = 1 − p)
Practical size = min( fractional-Kelly (¼ to ½ of f*), per-trade risk limit )
```

**(c) Risk of ruin**

```
R = [ (1 − edge) / (1 + edge) ] ^ (capital / risk per trade)   (falls exponentially as risk per trade shrinks)
```

**(d) Scaling (equity-curve based)**

```
Scale up: +1 lot per fixed profit increment;  Scale down: −1 lot per (smaller) drawdown increment
```

**(e) Correlated total risk**

```
Correlation-adjusted total risk = √(Σσᵢ² + 2ΣΣ ρᵢⱼ σᵢ σⱼ)
   (for NIFTY positions ρ ≈ 1, so risks ADD rather than diversify — Chapter 25)
```

---

## 7. Practical Insights

* **Fix your sizing before your strategy.** For most traders, over-sizing — not a poor strategy — is the binding constraint; correct sizing is the highest-leverage improvement available.
* **Use the fixed-percentage model** — it auto-compounds in gains and auto-de-risks in drawdowns, the throttle survival requires.
* **Treat Kelly as a ceiling and use a fraction of it, capped by your risk limit.** Full Kelly is too aggressive and assumes an edge you have probably overestimated; quarter-to-half Kelly, never above your per-trade limit, is the practical zone.
* **Size undefined-risk off the stress loss, never the premium** — the premium collected is not the risk; a large move is.
* **Let the equity curve scale you** — add slowly in success, cut faster in drawdown — and resist the "one more lot" that greed or revenge demands.

> **Professional Insight — the sizing decision is where discipline lives or dies.** A trader's *strategy* can be mechanical, but the *sizing* decision — made trade by trade, in the moment — is where emotion attacks: greed says "size up, you're winning"; fear and revenge say "size up to make it back." The professional removes the decision by fixing it to a *rule* (a risk percentage, a fractional Kelly, a scaling schedule) computed when calm, and executes that rule mechanically. The single most common way a disciplined trader becomes a gambler is by overriding their sizing rule "just this once." The rule exists precisely for the moments you most want to break it.

---

## 8. Common Mistakes

* **Over-sizing a good strategy.** The most common cause of failure — a real edge destroyed by positions too large to survive the inevitable losing streak.
* **Sizing naked positions off the premium.** Treating the ₹10,000 collected as the risk, when a large move can lose many times that; size off the stress loss.
* **Betting full Kelly (or more).** Accepting brutal drawdowns and blowing up when the (overestimated) edge disappoints; use fractional Kelly, capped by the risk limit.
* **Using fixed-rupee sizing into a drawdown.** Risking the same rupees as the account shrinks, deepening the hole; the fixed-percentage model auto-de-risks.
* **The "one more lot" override.** Adding size to a winner (greed) or a loser (revenge), breaking the rule at the worst moment.
* **Ignoring correlation in sizing.** Sizing each position independently when all are NIFTY-correlated, so the aggregate risk is far larger than the sum of "diversified" pieces suggests.

---

## 9. Case Study — "The Position Sizing Experiment"

**Context.** This case isolates the effect of sizing by holding everything else *identical*: the same strategy, the same entry signals, the same 12-month period, the same 60%-win-rate edge — traded by three sizers who differ *only* in how much they risk per trade: **1% (conservative), 3% (moderate), and 5% (aggressive)**, each on a ₹10 lakh account. The result is the clearest possible demonstration that sizing, not strategy, drives outcomes. Figures are illustrative but representative.

**The three outcomes.**

**Table 26.3 — The same strategy at three risk levels over 12 months (illustrative)**

| Sizer | Risk/trade | Peak return | Max drawdown | Year-end result | Outcome |
| --- | ---: | ---: | ---: | ---: | --- |
| Conservative | 1% | +18% | 8% | **+18%** | Survived, steady |
| Moderate | 3% | +42% | 22% | **+42%** | Survived, best risk-adjusted |
| Aggressive | 5% | +65% | **40%** | **~breakeven** | Stopped trading at the drawdown |

**The analysis.**

* **The conservative sizer (1%)** grew the account 18% with a shallow 8% drawdown — steady, unremarkable, and entirely survivable. They *under-used* their edge (leaving growth on the table) but were never remotely at risk. A fine outcome for a beginner or a risk-averse trader.
* **The moderate sizer (3%)** grew the account 42% with a 22% drawdown — a drawdown that was uncomfortable but *bearable*, and (by the recovery asymmetry, Chapter 25) recoverable with a ~28% gain. This was the **best risk-adjusted outcome**: it captured most of the edge's return with a drawdown the trader could survive both financially and psychologically.
* **The aggressive sizer (5%)** *rode the same edge to a peak of +65%* — the best gross return of the three — but the same 5% sizing that amplified the gains amplified the losses, and a mid-year losing streak produced a **40% drawdown.** A 40% drawdown requires a ~67% gain to recover (Chapter 25), and — critically — it *broke the trader's nerve*. Facing a near-halved account, they lost confidence, deviated from the system, and effectively stopped trading, ending the year at roughly breakeven. **The best strategy, the same edge, ruined by size.**

**The deeper lesson.** All three had the *identical* edge; the *only* variable was sizing, and it produced outcomes ranging from steady growth to a broken account. Two points stand out. First, **return is not the goal — survivable return is.** The aggressive sizer had the highest *peak* return but the worst *actual* outcome, because the 40% drawdown ended their participation before the edge could compound. Second, **the drawdown you can survive caps your usable size.** The moderate sizer found the zone where the return was high *and* the drawdown was survivable — the definition of correct sizing. Beyond that zone (the aggressive sizer), extra size buys extra return only until the drawdown ends the game, at which point all the potential return is forfeit.

**The lesson.** Position sizing, not strategy, determined which of three identical-edge traders prospered and which broke. The correct size is the *largest* one whose worst drawdown you can survive — financially *and* emotionally — because a drawdown that stops you trading forfeits all future compounding. Size to survive the losing streak your edge guarantees, and the winning streak takes care of itself.

*(Takeaway: with the same strategy and edge, sizing alone separates steady growth from a broken account — the correct size is the largest whose worst drawdown you can survive, because return is worthless if the drawdown ends your participation.)*

---

## 10. Chapter Summary

* **Position sizing is the number-one determinant of survival and growth — more than strategy** — because it controls the drawdown that (via the recovery asymmetry) determines whether you survive to compound.
* **Two models:** fixed-rupee (simple, static) and **fixed-percentage** (adaptive — compounds in gains, auto-de-risks in drawdowns; the recommended default).
* **Position size = risk per trade / max loss per lot** — straightforward for defined risk (known max loss), but undefined risk must be sized off a **stress loss, never the premium**.
* **Kelly** (`f* = (pb − q)/b`) gives the growth-optimal fraction (9% in the example), but is **too aggressive** — use **fractional Kelly (¼–½)** capped by the per-trade risk limit, and remember your edge estimate is probably too optimistic.
* **Risk of ruin falls exponentially as per-trade risk shrinks:** the same 10% edge gives ~0.004% ruin at 2% risk but ~13.4% at 10% — sizing small is what makes an edge bankable.
* **Scale with the equity curve** — add slowly in success (+1 lot per ₹2L), cut faster in drawdown (−1 lot per ₹1L) — and mind **concentration limits, lot granularity** (coarse for small accounts), and the **"one more lot" temptation**.
* The **Position Sizing Experiment** — the same edge at 1%/3%/5% risk — shows the aggressive sizer's 40% drawdown ended their trading (breakeven) while the moderate sizer captured the best *risk-adjusted* return; sizing alone drove the outcomes.

---

## 11. Key Takeaways

* **Fix your sizing first — it is a more powerful lever than strategy** — and use the fixed-percentage model so size grows in success and shrinks in drawdown.
* **Treat Kelly as a ceiling; use a fraction of it, capped by your risk limit** — and size undefined-risk off the stress loss, never the premium.
* **Size small — risk of ruin falls exponentially with per-trade risk** — small sizing is what turns a real edge into bankable compounding.
* **The correct size is the largest whose worst drawdown you can survive** — return is worthless if the drawdown ends your participation.

---

## 12. Practice Questions

**Q1 (Thesis).** In one or two sentences, why does position sizing matter more than strategy selection?

**Q2 (Models).** Contrast the fixed-rupee and fixed-percentage sizing models, and state which is preferable in a drawdown and why.

**Q3 (Position size).** A ₹15 lakh account risks 2% per trade. How many NIFTY iron condor lots (max loss ₹7,800/lot) can it hold?

**Q4 (Naked sizing).** A trader collects ₹12,000 selling a naked strangle whose stress-scenario loss is ₹60,000/lot. On a ₹10 lakh account at 2% risk, how many lots should they trade, and why not size off the premium?

**Q5 (Kelly).** A strategy has a 60% win rate, average win ₹800, average loss ₹1,000. Compute the full-Kelly fraction and the quarter-Kelly fraction.

**Q6 (Kelly judgement).** Your quarter-Kelly fraction is 3.5% but your per-trade risk limit is 2%. Which do you use, and why?

**Q7 (Risk of ruin).** Using Table 26.1, compare the risk of ruin at 5% versus 20% per-trade risk (10% edge), and state the lesson.

**Q8 (Scaling).** Under a "+1 lot per ₹2L profit, −1 lot per ₹1L drawdown" rule starting at ₹10L/1 lot, what is the lot size at ₹14L, and then after a drawdown to ₹12.5L?

**Q9 (One more lot).** Explain why adding "one more lot" to a winning streak usually hurts.

**Q10 (Experiment).** In the Position Sizing Experiment, the aggressive (5%) sizer had the highest peak return but the worst outcome. Explain why.

---

## 13. Detailed Solutions

**A1.** Position sizing controls the *volatility of the equity curve* and thus the *drawdown*, which (via the recovery asymmetry) determines survival; the same edge sized too large produces an unsurvivable drawdown while sized correctly it compounds — so sizing determines whether you *keep* an edge, which matters more than the edge itself.

**A2.** **Fixed-rupee** risks a constant amount regardless of account size; **fixed-percentage** risks a constant % of *current* equity, so the rupee risk falls as the account shrinks. In a **drawdown, the fixed-percentage model is preferable** because it *automatically de-risks* (risking less as equity falls), cushioning the drawdown, whereas fixed-rupee keeps risking the same amount into a shrinking account, deepening the hole.

**A3.** Risk per trade = 2% × ₹15,00,000 = ₹30,000. Lots = 30,000 / 7,800 = 3.85 → **3 lots** (round down).

**A4.** Size off the stress loss: lots = (2% × 10,00,000) / 60,000 = 20,000 / 60,000 = 0.33 → **0 lots** — the account is too small for this naked position. You must not size off the ₹12,000 premium because the *risk* is the loss on a large move (₹60,000+), not the credit collected; sizing off the premium would dangerously over-size (implying ~1–2 lots against a risk that could lose ₹60,000–120,000).

**A5.** p = 0.60, q = 0.40, b = 800/1,000 = 0.80. f* = (0.60 × 0.80 − 0.40) / 0.80 = (0.48 − 0.40) / 0.80 = 0.08 / 0.80 = **0.10 = 10% (full Kelly)**. Quarter-Kelly = 10% / 4 = **2.5%**.

**A6.** Use the **2% per-trade risk limit** (the smaller of the two). Kelly assumes your estimated edge is accurate, but edges are usually overestimated, so the risk limit is the binding safety constraint. When fractional Kelly exceeds your risk limit, the risk limit wins — under-betting costs a little growth, over-betting can cost the account.

**A7.** At **5%** risk, risk of ruin ≈ **1.8%**; at **20%** risk, ≈ **36.7%** — a roughly 20-fold higher chance of ruin, with the *same edge*. The lesson: risk of ruin rises steeply (exponentially) with per-trade size, so sizing small is what makes an edge survivable; quadrupling the per-trade risk turns a near-safe strategy into one with a one-in-three chance of ruin.

**A8.** From ₹10L/1 lot: +₹2L (to ₹12L) → 2 lots; +₹2L (to ₹14L) → **3 lots**. Then a drawdown from ₹14L to ₹12.5L is −₹1.5L, which crosses one ₹1L threshold → cut 1 lot → **2 lots** (the next cut would come at ₹11L).

**A9.** Because adding to a winner *increases position size after the easy gains are made* — raising your risk at the point where the winning move may be ending, and doing so out of *greed* rather than by the rule. If the streak then ends (as streaks do), the oversized position turns a normal loss into a large one, giving back the streak's gains. Disciplined size is set by the rule, not by the emotion of a hot hand.

**A10.** The aggressive sizer's 5% risk amplified both gains (to a +65% peak) *and* losses, producing a **40% drawdown** during a mid-year losing streak. A 40% drawdown requires a ~67% gain to recover (recovery asymmetry) and, crucially, **broke the trader's nerve** — they lost confidence, abandoned the system, and effectively stopped trading, ending near breakeven. The highest *peak* return became the worst *actual* outcome because the drawdown ended their participation before the edge could compound. Return is worthless if the drawdown stops you trading.

---

## 14. Mini Glossary

* **Position sizing** — the decision of how much capital (how many lots) to risk per trade; the top determinant of survival. → this chapter.
* **Fixed-rupee model** — risking a constant rupee amount per trade regardless of account size. → this chapter.
* **Fixed-percentage model** — risking a constant % of current equity per trade; auto-compounds and auto-de-risks. → this chapter.
* **Position-size formula** — lots = risk per trade ÷ max loss per lot (stress loss for undefined risk). → this chapter.
* **Kelly Criterion** — the growth-optimal risk fraction, f* = (pb − q)/b; maximises geometric growth. → this chapter.
* **Fractional Kelly** — using a fraction (½ or ¼) of full Kelly to reduce drawdowns and guard against edge overestimation. → this chapter.
* **Risk of ruin** — the probability of being knocked out; falls exponentially as per-trade risk shrinks. → this chapter.
* **Geometric mean return** — the compounding growth rate Kelly maximises; over-betting reduces it. → this chapter.
* **Equity-curve scaling** — adjusting lot size with the account: add in success, cut faster in drawdown. → this chapter.
* **Lot granularity** — the whole-lot constraint that forces coarse sizing on small accounts. → this chapter.
* **The "one more lot" temptation** — the emotional urge to add size to a winner or loser, overriding the sizing rule. → this chapter.

---

<!-- End of Chapter 26. Rev 2 (5 Aug 2026): lot 75→65; NIFTY per-lot max losses rescaled (IC ₹9k→₹7.8k, bull put ₹11.25k→₹9.75k, long debit ₹8k→₹7k, naked stress ₹50k→₹45k) per revised Ch17/Ch18; Table 26.2 recomputed (₹5L 1/1/1/0, ₹10L 2/2/2/0, ₹25L 6/5/7/1, ₹50L 12/10/14/2). Kelly example: win 65%, avg win ₹1,000, avg loss ₹1,600 → b=0.625, f*=9%, half 4.5%, quarter 2.25% (rupee journal averages, lot-independent). Position size = risk/max loss per lot; ₹10L 2% ₹20k / IC ₹7.8k = 2 lots; naked strangle stress ₹45k → 0 lots. Risk of ruin Table 26.1 (edge 10%): 2%→0.004%, 5%→1.8%, 10%→13.4%, 20%→36.7% (lot-independent). Scaling +1 lot/₹2L, −1 lot/₹1L. Case study Table 26.3: 1% +18%/DD8%, 3% +42%/DD22% (best risk-adjusted), 5% +65% peak/DD40% → stopped (breakeven). Q3 3 lots, Q4 0 lots (rupee hypothetical, unchanged), Q5 Kelly 10%/quarter 2.5%, Q7 5%→1.8% vs 20%→36.7%. Recovery asymmetry from Ch25. IV = implied volatility. Margin/portfolio-Greeks previewed for next chapter without number. -->
