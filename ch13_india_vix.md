<!-- Difficulty: Level 3/5 (Intermediate). Dependency: Chapters 5, 11. Target length ~8,500 words. Current as of 4 Aug 2026. Opens Part IV (Volatility Mastery). NOTE: this chapter has NO lot-size-dependent figures — all maths is VIX→expected move (Index × VIX/√periods), lot-independent; no transaction costs; no expiry weekday specified. So the lot-65 and Apr-2026 STT changes do NOT apply here. VIX→range: daily = Index×VIX/√252, weekly /√52, monthly /√12. VIX 15 → 24,600×0.945% ≈ ₹233 daily. Regimes: low 10-13, normal 13-18, high 18-25, crisis 25+. India VIX methodology = model-free CBOE-style variance from the near+mid-month NIFTY OTM option strip, interpolated to 30 days (full formula in appendix). COVID case anchored to closing peak 83.61 on 24 Mar 2020 (still the record). India VIX futures: launched 2014, DISCONTINUED 2017 (low liquidity) — updated from "illiquid"; added note on NSE's new volatility index pilot (2026). IV = implied volatility. -->

# Chapter 13 — India VIX: The Fear Gauge

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Explain what India VIX measures and, conceptually, how it is calculated.
2. Interpret VIX levels against the history of the Indian market.
3. Use India VIX to select strategies and time entries.
4. Understand the VIX–NIFTY inverse relationship and when it breaks.
5. Trade appropriately across the four volatility regimes — low, normal, high, and crisis.

Welcome to Part IV. In Part III you learned to *measure* your volatility exposure (Vega). Now you learn to *read the market's own volatility forecast* — and India VIX is the single number that summarises it.

---

## 2. Introduction

On 24 March 2020, one number on the NSE screen told the whole story of the market's terror: India VIX closed at **83.61**, by far the highest reading in its history. Two months earlier it had been sitting quietly around 12. In eight weeks, the market's fear gauge had risen almost sevenfold, and every option premium on the exchange had inflated with it.

That single number is what this chapter is about. **India VIX is the market's consensus forecast of how much the NIFTY will move over the next 30 days** — a live, model-free reading of implied volatility distilled from the entire NIFTY option chain into one figure. When VIX is 12, the market expects calm; when it is 30, it expects turbulence; when it is 80, it expects chaos. And because every option premium rises and falls with implied volatility (Chapter 11), VIX tells you, at a glance, whether options are cheap or expensive *right now* — which is the first question any volatility trader asks.

Reading VIX well changes how you trade. It tells you which strategies fit the current environment (buy cheap options in a low-VIX calm; sell rich premium in a high-VIX panic), how big a move to expect, and — crucially — that fear is *mean-reverting*: spikes fade and calms end. A trader who ignores VIX is trading volatility blind; one who reads it has a compass. This chapter builds that compass: what VIX measures, how to turn it into an expected NIFTY range, how to classify the regime you are in, and how the fear gauge behaved in the market's most extreme moment. Setting throughout: **NIFTY at 24,600**.

---

## 3. Core Concepts

### 3.1 What India VIX is, and how it is calculated

India VIX is the flagship of this chapter.

**What is it?** **India VIX** is an index, published live by the NSE, that measures the market's expectation of NIFTY volatility over the **next 30 calendar days**, expressed as an **annualised percentage**. A VIX of 15 means the market expects the NIFTY to have an annualised volatility of about 15% over the coming month.

**Why does it exist?** Because implied volatility — the market's forward-looking volatility estimate (Chapter 6) — is scattered across hundreds of option strikes, each with its own IV (the skew, Chapter 6). Traders needed a *single, standard* number summarising the whole surface. India VIX aggregates the entire near-term NIFTY option chain into one figure, so everyone can speak of "the market's volatility" with a common yardstick.

**Why should a trader care?** Because VIX answers the volatility trader's first question — *are options cheap or expensive right now?* — in one glance. Since premiums scale with IV (Chapter 11), a low VIX means cheap options (favouring buyers) and a high VIX means rich options (favouring sellers). VIX also tells you how big a move the market expects, and thus whether your strategy's assumptions are reasonable.

**Intuitive explanation.** India VIX is the market's **weather forecast**, and premiums are the price of umbrellas. When the forecast calls for storms (high VIX), umbrellas are dear; when it calls for clear skies (low VIX), they are cheap. The gauge does not tell you *whether* it will rain — only how much the crowd is bracing for it.

**How it is calculated (conceptually).** Unlike a single option's IV, India VIX is **model-free** — it does not come from Black–Scholes. It is built, using the CBOE-style variance methodology, from the **live order-book prices of a strip of out-of-the-money NIFTY calls and puts** across the near and next-month expiries, interpolated to a constant 30 days. In simplified form:

```
VIX = 100 × √[ (2/T)·Σ (ΔKᵢ/Kᵢ²)·e^(rT)·Q(Kᵢ) − (1/T)·(F/K₀ − 1)² ]     (13.1)
```

where `Q(Kᵢ)` is the price of each OTM option, `ΔKᵢ` the strike spacing, `F` the forward, and `K₀` the strike just below the forward. You never compute this by hand — the NSE publishes it every few seconds — and the full derivation belongs in the appendix. What matters is the *idea*: VIX is a weighted average of the whole OTM option strip, so it reflects the market's complete volatility view, not one strike's.

**Numerical feel.** A VIX of 15 translates to an expected NIFTY move of about ±0.95% *per day* (Section 3.2) — roughly ±233 points at 24,600. That is the single most useful thing VIX tells a trader: how far the market expects the index to swing.

**Professional interpretation.** Desks treat VIX as the market's *price* of volatility and trade around it — buying volatility when VIX looks cheap relative to what they expect the market to actually realise, selling it when VIX looks rich. To a professional, "VIX is 22" is not a fear reading; it is a *price* to be judged cheap or dear.

**Common mistake.** Reading VIX as a *direction* signal ("VIX is high, so the market will crash"). VIX measures expected *magnitude* of movement, not direction — a high VIX means a big move is expected, up **or** down.

**Practical takeaway.** **India VIX is the market's 30-day volatility forecast in one number — read it first to know whether options are cheap or expensive and how big a move to expect, before choosing any strategy.**

---

### 3.2 Turning VIX into an expected move

VIX's greatest practical use is converting its annualised percentage into an **expected NIFTY range** over a chosen horizon. Because volatility scales with the square root of time, you divide the annualised VIX by the square root of the number of periods in a year:

```
Daily expected move   = Index × (VIX/100) / √252
Weekly expected move  = Index × (VIX/100) / √52
Monthly expected move = Index × (VIX/100) / √12
```

**Worked conversion.** With VIX = 15 and NIFTY at 24,600:

```
Daily   = 24,600 × 0.15 / √252 = 24,600 × 0.15 / 15.87 ≈ ±233 points (±0.95%)
Weekly  = 24,600 × 0.15 / √52  = 24,600 × 0.15 / 7.21  ≈ ±512 points
Monthly = 24,600 × 0.15 / √12  = 24,600 × 0.15 / 3.46  ≈ ±1,065 points
```

**Crucially, this expected move is one standard deviation.** So a VIX of 15 says: the NIFTY has roughly a **68% chance** of staying within ±233 points on a given day, a **~95%** chance of staying within ±466 points (two standard deviations), and only a ~5% chance of a larger move. Table 13.1 gives the daily, weekly, and monthly expected moves across VIX levels.

**Table 13.1 — Expected NIFTY move (±) by VIX level (NIFTY 24,600; 1 standard deviation)**

| VIX | Daily (±pts) | Weekly (±pts) | Monthly (±pts) |
| ---: | ---: | ---: | ---: |
| 10 | 155 | 341 | 710 |
| 12 | 186 | 410 | 852 |
| 15 | 233 | 512 | 1,065 |
| 20 | 310 | 682 | 1,420 |
| 25 | 388 | 853 | 1,776 |
| 30 | 465 | 1,023 | 2,131 |
| 40 | 620 | 1,364 | 2,841 |

This table is a working tool: it tells a seller whether their short strikes are safely outside the expected range, and a buyer whether the move they need is realistic. Remember, though, that markets have **fat tails** (Chapter 6): 2-standard-deviation-plus moves happen more often than the normal-distribution maths implies, so treat the outer ranges as *minimums* for how wrong things can go.

> **Beginner Alert — the expected move is a *range*, not a prediction.** "VIX = 15 → ±233 points" does not mean NIFTY *will* move 233 points, nor that it will stay put. It means about two days in three, the move will be *within* ±233 points, and about one day in three it will be larger. It is a statement about the *distribution* of outcomes, not a forecast of tomorrow's close.

---

### 3.3 Historical ranges — the four regimes

India VIX does not wander randomly; it lives in recognisable bands, and each band calls for a different approach. The practical regimes:

| Regime | VIX range | What it signals |
| --- | --- | --- |
| **Low (calm)** | 10–13 | Complacency; cheap options; markets grinding or trending quietly |
| **Normal** | 13–18 | Ordinary two-way risk; fairly priced options |
| **High (elevated)** | 18–25 | Rising fear; rich options; often around events or corrections |
| **Crisis** | 25–40+ | Panic; extremely rich options; sharp, fast moves |

For most of its history India VIX has sat in the **low-to-normal** band (10–18); it visits the **high** band around events and corrections, and reaches **crisis** levels only in genuine shocks — the 2020 COVID crash (peak 83.61), the 2008 global crisis, election shocks, and global sell-offs. The higher the regime, the rarer and shorter-lived it is (Section 3.5). Knowing your regime is the first step in strategy selection (Section 3.7).

---

### 3.4 The VIX–NIFTY inverse relationship — and when it breaks

India VIX and the NIFTY usually move in **opposite** directions, and strongly so (a negative correlation typically around −0.7 to −0.8). The logic is behavioural: when the market falls, fear rises, traders rush to buy puts for protection, and that demand inflates implied volatility — so **VIX rises when NIFTY falls**. When the market rises calmly, fear ebbs, protection is sold off, and VIX drifts down — **VIX falls when NIFTY rises.** This is why VIX is called the "fear gauge": it spikes in panics and sags in complacency.

But the relationship is a tendency, not a law, and it **breaks in instructive ways**:

* **Before known events, VIX can rise even as NIFTY rises.** Ahead of an election result or budget, uncertainty (and thus IV) climbs regardless of which way the index is drifting — the market is bracing for a move, not reacting to one.
* **At extreme lows, VIX gets "sticky."** In deep complacency VIX can sit near its floor (~10–11) even as the market keeps grinding higher; there is only so low fear can go.
* **On sharp up-moves, VIX can rise with the market.** A violent *rally* is still a big move, and "upside volatility" can lift VIX even as NIFTY jumps — volatility measures magnitude, not direction (Section 3.1).

The practical lesson: use the inverse relationship as a *default expectation* (a falling market usually means a rising VIX, so protection gets dearer just as you want it), but watch for the breaks — especially the pre-event rise, which is the setup for the IV-crush trades of Chapter 11.

---

### 3.5 Mean reversion — spikes and crushes both fade

The most important behavioural fact about volatility is that it **mean-reverts.** Unlike a stock price, which can trend indefinitely, VIX is pulled back toward its long-run average: **spikes are temporary, and so are crushes.** A VIX of 40 will not stay at 40; it will subside toward the teens over days or weeks. A VIX of 10 will not stay at 10 forever; some event will lift it. Volatility clusters (calm follows calm, storm follows storm) in the short run but reverts over the medium run.

Two consequences for trading:

* **The higher the spike, the more certain — but not the faster — the reversion.** VIX rarely spends long above 25, less time above 30, and only fleetingly above 40 (COVID being the extreme exception, where it stayed elevated for weeks). But the reversion from a crisis peak is *gradual*, often taking weeks, not hours — so "sell the spike" is a sound instinct with dangerous timing risk (you can be right that VIX will fall and still be crushed by a further spike first).
* **Extreme lows are opportunities to buy cheap protection.** When VIX is near its floor, options are cheap and the eventual reversion upward will inflate them — the great asymmetric trade of buying insurance when no one wants it (the COVID case, Section 9).

> **Market Note — VIX mean-reverts, but on its own schedule.** "VIX always comes back down" is true and dangerous in equal measure. It *will* revert — but a trader who sold volatility at VIX 30 in March 2020 watched it climb to 83 before it fell. Mean reversion tells you the *direction* of the eventual move, never the *timing* or the *path*. Size for the spike that comes before the reversion.

---

### 3.6 VIX term structure and India VIX futures

Just as options have a term structure (Chapter 6), so does volatility: the market's expected volatility differs across horizons. In **normal (contango)** conditions, longer-dated implied volatility sits *above* short-dated — the market assumes today's calm may not last. In **stress (backwardation)**, short-dated IV spikes *above* long-dated — immediate fear exceeds the expected long-run level. An inverted (backwardated) term structure is itself a fear signal.

The NSE launched **India VIX futures** in 2014 to let traders trade the fear gauge directly, but — after persistently **poor liquidity** — the contracts were **discontinued in 2017**. As of 2026 there is **no way to trade India VIX directly** on the exchange. (The NSE has, however, begun **piloting a new volatility index** with a revised methodology, reportedly with a view to eventually supporting tradable derivatives — but nothing is live yet; verify its status before relying on it.) In practice, Indian traders read the VIX term structure indirectly, through the implied volatilities of near- versus far-dated NIFTY options (the term structure we develop further in Part IV). You trade volatility through *options*, not through the VIX itself.

---

### 3.7 Strategy selection by VIX regime

The single most practical use of VIX is matching your strategy to the regime. Because VIX tells you whether options are cheap or rich, it tells you whether to be a net *buyer* or *seller* of premium. Table 13.2 maps regimes to strategies.

**Table 13.2 — Strategy selection by VIX regime**

| Regime | VIX | Options are… | Favour | Avoid |
| --- | ---: | --- | --- | --- |
| **Low** | 10–13 | Cheap | Buying options; debit spreads; calendars; buying cheap protection | Selling naked premium (poor reward for the risk) |
| **Normal** | 13–18 | Fairly priced | Balanced credit/debit spreads; defined-risk structures | Over-leveraging either direction |
| **High** | 18–25 | Rich | Selling premium; credit spreads; iron condors (defined risk) | Buying options outright (expensive) |
| **Crisis** | 25+ | Extremely rich | Reduced size; defined-risk only; buying protection; waiting for reversion | Naked selling (further-spike risk); large new positions |

The core logic is symmetric: **buy volatility when it is cheap (low VIX), sell it when it is rich (high VIX)** — but always with the caveat that "cheap can get cheaper and rich can get richer," so defined-risk structures and disciplined sizing matter more than the regime call itself. Note the crisis-regime warning: high VIX means rich premium, which *tempts* selling — but selling naked into a crisis exposes you to the further spike that mean reversion does not rule out (the COVID trap). In a crisis, richness is a warning as much as an opportunity.

> **Professional Insight — VIX tells you the price of volatility; your job is to judge it against what will be realised.** A professional does not simply "sell high VIX." They compare the *implied* volatility (VIX) against the volatility they expect the market to *actually realise* over the period. Selling premium is attractive only when implied exceeds likely realised (the variance risk premium, developed in the next chapter). A high VIX before a genuine crisis can be *cheap* if the realised move is even bigger; a moderate VIX in a dull market can be *rich*. The regime is the starting point; the implied-versus-realised judgment is the edge.

---

### 3.8 VIX percentile — is "high" really high?

A VIX of 18 is meaningless in isolation — it is high relative to a year of calm but low relative to a crisis year. The fix is the **VIX percentile**: where the current VIX sits within its own recent history.

```
VIX percentile = (number of past readings below the current VIX ÷ total readings) × 100
```

If VIX is 18 and, over the past year, 78% of daily readings were below 18, then VIX is at its **78th percentile** — genuinely elevated *for this market, this year*. If instead 40% were below, VIX at 18 is only middling. The percentile turns a raw number into context, and it is a far better guide to "cheap or rich" than the absolute level. (We formalise this metric, and its cousin IV Rank, in the next chapter; here it is enough to know that *context beats the raw number*.)

---

## 4. Examples (Real-World)

**Example 1 — Sizing an expiry trade by the expected move.** A seller eyeing a weekly iron condor checks VIX at 14 → weekly expected move ≈ ±480 points at 24,600. They place their short strikes *outside* that one-standard-deviation range, giving the position a cushion. VIX did the position sizing.

**Example 2 — The pre-event VIX rise.** In the week before an election result, NIFTY drifts *up* on optimism, yet VIX climbs from 13 to 22. The inverse relationship has broken — the market is bracing for the event, inflating IV regardless of direction. A trader who buys options here is paying event-rich premium (the Chapter 11 trap); one who understands the setup prepares for the post-event crush.

**Example 3 — The sticky low.** For months VIX hovers near 11 as the market grinds higher. Sellers who kept selling "cheap" premium collected little reward for real risk, while the eventual reversion — when it came — inflated every option they were short. Low VIX is not a green light to sell; it is a warning that premium is thin.

---

## 5. Numerical Examples

Setting: NIFTY 24,600.

### Numerical Example 1 — VIX to expected move

VIX = 20. Expected NIFTY moves (1 standard deviation):

```
Daily   = 24,600 × 0.20 / √252 = 24,600 × 0.20 / 15.87 ≈ ±310 points
Weekly  = 24,600 × 0.20 / √52  ≈ ±682 points
Monthly = 24,600 × 0.20 / √12  ≈ ±1,420 points
```

So with VIX at 20, the market expects the NIFTY to stay within about ±310 points on ~68% of days, and within ±620 points (2 SD) on ~95% of days.

### Numerical Example 2 — Checking the range against reality

VIX is 14, so the daily expected move ≈ 24,600 × 0.14 / 15.87 ≈ **±217 points (±0.88%)**. If, over the past week, the NIFTY's actual daily ranges were 180, 200, 150, 260, and 190 points, then four of five days fell within ±217 — consistent with the ~68% expectation, and one day (260) modestly exceeded it. The VIX-implied range was a good calibration of reality.

### Numerical Example 3 — VIX percentile

VIX today is 21. Over the past 250 trading days, 210 readings were below 21:

```
VIX percentile = 210 ÷ 250 × 100 = 84th percentile
```

VIX is at its 84th percentile — **genuinely elevated for the past year**, suggesting options are rich relative to their recent norm and favouring (defined-risk) premium selling. Had only 120 readings been below, the 48th percentile would say VIX 21 is merely average for this market.

### Numerical Example 4 — Regime-based strategy selection

VIX is 11 (low regime). Two *appropriate* choices: **buy a debit spread** (cheap options, limited cost) or **buy protective puts** (insurance is cheap, and reversion will inflate it). Two *inappropriate* choices: **sell a naked strangle** (thin premium, poor reward for large risk) or **sell an iron condor for income** (the credit collected is small relative to the risk, and a VIX reversion would inflate the shorts). In a low-VIX regime, the odds favour buyers, not sellers.

### Numerical Example 5 — Cushion check for a short strangle

VIX is 16, NIFTY 24,600, weekly expiry. Weekly expected move ≈ 24,600 × 0.16 / √52 ≈ **±546 points** (1 SD). A seller placing short strikes at 25,200 (call, +600) and 24,000 (put, −600) is just *outside* the 1-SD range — roughly the 16-Delta strikes — giving about a two-in-three chance both expire worthless, before adjustments. VIX sized the strikes.

---

## 6. Calculations (the reusable recipes)

**(a) VIX to expected move (1 standard deviation)**

```
Daily   move = Index × (VIX/100) / √252
Weekly  move = Index × (VIX/100) / √52
Monthly move = Index × (VIX/100) / √12
```

**(b) Probability interpretation**

```
~68% of outcomes within ±1 expected move; ~95% within ±2; ~99.7% within ±3
(but fat tails make large moves more frequent than the normal model implies)
```

**(c) VIX percentile**

```
VIX percentile = (readings below current VIX ÷ total readings) × 100
```

**(d) India VIX (model-free, from the option strip — reference only)**

```
VIX = 100 × √[ (2/T)·Σ (ΔKᵢ/Kᵢ²)·e^(rT)·Q(Kᵢ) − (1/T)·(F/K₀ − 1)² ]   (NSE-published; not computed by hand)
```

---

## 7. Practical Insights

* **Read VIX before choosing a strategy.** It tells you in one glance whether options are cheap (buy) or rich (sell) and how big a move to expect — the first input to any volatility decision.
* **Turn VIX into an expected range and use it to place strikes.** Sellers should sit outside the 1-SD move; buyers should ask whether the move they need is realistic. VIX is a position-sizing tool, not just a sentiment reading.
* **Respect mean reversion — but never trust its timing.** Spikes fade and calms end, so fade extremes in *bias*; but size for the further spike that can come first, as March 2020 proved.
* **Use the percentile, not the raw number.** "High VIX" only means something relative to its own history; the percentile turns a number into context.
* **Watch for the inverse relationship breaking** — especially the pre-event VIX rise, which sets up the IV-crush dynamics of the previous chapter.

---

## 8. Common Mistakes

* **Reading VIX as direction.** VIX measures expected *magnitude*, not direction — a high VIX means a big move is coming, up or down, not that a crash is certain.
* **Selling naked premium just because VIX is high.** A high VIX is rich premium *and* a warning; in a crisis it can spike further, and mean reversion does not guarantee timing. Prefer defined-risk structures.
* **Buying options in a low-VIX regime and expecting them to be "cheap enough."** Cheap options can get cheaper, and thin premium can still decay to zero if the move does not come.
* **Trusting the expected move as a hard ceiling.** It is a 1-SD range; roughly a third of days exceed it, and fat tails make big breaks more common than the normal model says.
* **Ignoring the percentile.** Treating VIX 18 as "high" without checking whether it is high *for this year* — context changes the whole read.
* **Trying to trade VIX directly.** India VIX futures were discontinued in 2017; you express volatility views through NIFTY options, not the VIX itself.

---

## 9. Case Study — "COVID Crash 2020: VIX at 83.61"

**Context.** The 2020 COVID crash is the definitive stress test of the fear gauge. In February 2020, with the market complacent, India VIX sat around **12**. As the pandemic spread and the NIFTY began its ~38% collapse (Chapter 1), VIX exploded, closing at its all-time high of **83.61 on 24 March 2020** — a near-sevenfold rise in weeks. It then decayed *slowly*, taking until roughly May–June 2020 to fall back toward the 30s, and months more to return to the 20s and eventually the teens. Figures are drawn from the historical record; treat exact intraday levels as approximate.

**The four phases, and what worked in each.**

* **Phase 1 — Calm before (Feb 2020, VIX ~12).** Options were cheap and sellers complacent. The asymmetric trade of the decade was hiding in plain sight: **buying protective puts** cost almost nothing, and buyers of that cheap insurance were about to be paid many times over. The lesson of low VIX — *insurance is cheapest exactly when no one wants it* — was never clearer.

* **Phase 2 — The spike (late Feb–24 Mar, VIX 12 → 83).** As VIX rocketed, everyone **long volatility** — long puts, long options, long Vega — profited enormously (Vega and Gamma both exploding in their favour, Chapters 9 and 11). The mirror image was catastrophic: **short-premium sellers** (short strangles, naked options) were destroyed, hit by the twin short-Gamma and short-Vega losses that the Chapter 12 case study describes — now at crisis scale. Many accounts that had "safely" sold premium for years blew up in this phase.

* **Phase 3 — The peak (late Mar, VIX 80+).** Premiums were astronomically rich — a VIX of 83 implied a *daily* expected NIFTY move of just over ±5% (83 ÷ √252 ≈ 5.2%). Selling volatility here was extraordinarily lucrative *if* you could survive further spikes and had the capital, because the eventual mean reversion was enormous. But it was a knife-edge: VIX could still climb, and only the well-capitalised, defined-risk, small-sized seller could play it. For most, the correct action was **reduced size, defined risk, and patience** — not heroics.

* **Phase 4 — The slow decay (Apr–Jun 2020, VIX 83 → 30 → 20s).** As the panic subsided, VIX mean-reverted — but *slowly*, over weeks. This phase rewarded **volatility sellers** who entered *after* the peak, harvesting the grinding IV crush as premiums deflated. The key was that the reversion was gradual: a seller who entered at 60 and held as VIX fell to 30 did well, but had to withstand interim bounces. Mean reversion delivered — on its own schedule.

**The analysis.** COVID 2020 is every lesson of this chapter written large: VIX as the fear gauge (12 → 83); the VIX–NIFTY inverse relationship in its purest form (VIX exploded as NIFTY collapsed); the expected-move conversion (a VIX of 83 correctly implied the ~5% daily swings that followed); mean reversion (the spike faded — but over weeks, not hours); and regime-based strategy (buy cheap protection in the calm, survive the spike, sell the rich premium into the slow reversion). Above all, it showed that **the same VIX level means opposite things at different phases**: a VIX of 30 on the way *up* (Phase 2) was a trap for sellers, while a VIX of 30 on the way *down* (Phase 4) was an opportunity — the level alone did not tell you, but the regime and direction did.

**The lesson.** The fear gauge is not a crystal ball, but it is the most honest single number on the screen. It told you, throughout 2020, exactly how frightened the market was and how big a move it expected — and traders who read it, respected its mean reversion, and *matched their strategy to the phase* navigated the storm, while those who ignored it (or sold blindly into the spike) did not survive it.

*(Takeaway: VIX tells you the market's expected magnitude of movement and the price of volatility — read the regime and the phase, buy volatility when it is cheap and abundant-to-come, and never sell it blindly just because it looks rich.)*

---

## 10. Chapter Summary

* **India VIX** is the NSE's model-free measure of expected 30-day NIFTY volatility, annualised — the market's volatility forecast distilled from the whole OTM option strip into one number.
* It tells you whether options are **cheap or rich** (since premiums scale with IV) and how big a move to expect; it measures **magnitude, not direction**.
* **VIX → expected move:** daily = Index × (VIX/100)/√252; a VIX of 15 ≈ ±233 points daily at 24,600 — and that is a **1-standard-deviation** range (~68% of days), with fat tails making bigger breaks common.
* **Regimes:** low (10–13, cheap, favour buying), normal (13–18), high (18–25, rich, favour selling defined-risk), crisis (25+, reduce size, hedge).
* **VIX and NIFTY move inversely** (VIX rises as NIFTY falls), but the relationship *breaks* before events (VIX rises with a rising market), at sticky lows, and on sharp rallies.
* **Volatility mean-reverts** — spikes and crushes both fade — but the *timing* is never guaranteed; size for the further spike that can precede the reversion.
* **India VIX cannot be traded directly** (its futures, launched 2014, were discontinued in 2017; a new NSE volatility index is in pilot as of 2026), so volatility views are expressed through NIFTY options; the **VIX percentile** gives context the raw level cannot.
* **COVID 2020** (VIX 12 → 83.61 → 20s) is every lesson at once: the same VIX level meant opposite things on the way up versus down — regime and phase, not the number alone, dictate strategy.

---

## 11. Key Takeaways

* **Read VIX first** — it tells you whether to buy or sell volatility and how big a move to expect, in one number.
* **Convert VIX to an expected range and place your strikes and sizes against it** — it is a quantitative tool, not just a mood ring.
* **Trust mean reversion's direction, never its timing** — fade extremes in bias but size for the spike that can come first.
* **Match strategy to regime and phase** — buy cheap protection in the calm, sell rich premium (defined-risk) into a fading spike, and never sell blindly into a rising crisis.

---

## 12. Practice Questions

**Q1 (Definition).** In one sentence, state what India VIX measures, and whether it indicates direction or magnitude.

**Q2 (Conversion).** VIX is 18 and NIFTY is 24,600. Compute the daily and weekly expected moves (1 SD).

**Q3 (Probability).** For the Q2 daily figure, what does the "1 standard deviation" range mean in terms of probability?

**Q4 (Regime).** Classify these VIX readings into regimes and state whether options are cheap or rich: (a) 11, (b) 16, (c) 22, (d) 35.

**Q5 (Inverse relationship).** Explain the usual VIX–NIFTY relationship and give one situation in which it breaks.

**Q6 (Mean reversion).** A trader sees VIX at 45 and says, "It always comes back down, so I'll sell a naked strangle now." Identify the flaw in the timing logic.

**Q7 (Percentile).** VIX is 19; over the past 250 days, 175 readings were below 19. Compute the VIX percentile and interpret it.

**Q8 (Strategy selection).** VIX is 12. Name one appropriate and one inappropriate strategy, with a one-line reason each.

**Q9 (Cushion).** VIX is 20, NIFTY 24,600, weekly expiry. Roughly where should a seller place short strikes to sit just outside the 1-SD weekly move?

**Q10 (Judgement).** During a crisis, VIX is 60 and premiums are enormous. Explain why "sell the rich premium" is both tempting and dangerous, and what a disciplined trader does instead.

---

## 13. Detailed Solutions

**A1.** India VIX measures the market's expected annualised volatility of the NIFTY over the next 30 days; it indicates the expected **magnitude** of movement, not the direction.

**A2.** Daily = 24,600 × 0.18 / √252 = 24,600 × 0.18 / 15.87 ≈ **±279 points**. Weekly = 24,600 × 0.18 / √52 ≈ **±614 points**.

**A3.** It means the NIFTY has roughly a **68% chance** of staying within ±279 points on a given day, and about a 32% chance of a larger move (with ~95% within ±558 points, 2 SD) — a statement about the distribution of outcomes, not a prediction of tomorrow.

**A4.** (a) 11 = **low** regime, options **cheap**; (b) 16 = **normal**, fairly priced; (c) 22 = **high**, options **rich**; (d) 35 = **crisis**, options **extremely rich**.

**A5.** Usually VIX and NIFTY move **inversely** — VIX rises when NIFTY falls (fear/demand for puts) and falls when NIFTY rises (complacency). It breaks, for example, **before a known event**, when VIX rises even as the market drifts up because the market is bracing for the outcome (also acceptable: sticky lows, or a sharp rally lifting "upside" volatility).

**A6.** VIX mean-reverts in *direction* but not on a guaranteed *timeline* or *path*. VIX at 45 can climb much higher before it falls (in March 2020 it went from the 40s to 83). Selling a **naked** strangle exposes the trader to that further spike — short Gamma and short Vega both losing — and mean reversion offers no protection against the interim move. "It will come down" is true and irrelevant to surviving the path.

**A7.** VIX percentile = 175 ÷ 250 × 100 = **70th percentile** — VIX is elevated relative to the past year (higher than 70% of recent readings), suggesting options are rich for this market and favouring defined-risk premium selling.

**A8.** Appropriate: **buy a debit spread** (options are cheap, so a limited-cost directional bet has good reward-to-cost). Inappropriate: **sell a naked strangle** (thin premium gives poor reward for the large risk, and a VIX reversion upward would inflate the shorts).

**A9.** Weekly expected move ≈ 24,600 × 0.20 / √52 ≈ **±682 points**, so short strikes around **25,300 (call)** and **23,900 (put)** — roughly ±700 points — sit just outside the 1-SD range (near the 16-Delta strikes), giving about a two-in-three chance of both expiring worthless before adjustments.

**A10.** It is **tempting** because a VIX of 60 means premiums are extraordinarily rich, so the potential income is huge. It is **dangerous** because VIX can spike further before reverting (short Gamma and short Vega both losing on the path), and a naked seller can be wiped out before the reversion arrives. A disciplined trader **reduces size, uses defined-risk structures** (spreads/condors with bought wings), and often waits for the spike to *begin fading* rather than selling blindly into a rising crisis — capturing the reversion without betting the account on its timing.

---

## 14. Mini Glossary

* **India VIX** — the NSE's model-free index of expected 30-day annualised NIFTY volatility; the market's fear gauge. → this chapter.
* **Expected move** — the ±range implied by VIX over a horizon (Index × VIX/100 ÷ √periods); one standard deviation. → this chapter.
* **Volatility regime** — the band VIX occupies: low (10–13), normal (13–18), high (18–25), crisis (25+). → this chapter.
* **VIX–NIFTY inverse relationship** — the tendency of VIX to rise when NIFTY falls and fall when NIFTY rises. → this chapter.
* **Mean reversion (of volatility)** — the tendency of VIX to return toward its long-run average; spikes and crushes both fade. → this chapter.
* **Term structure (of volatility)** — how expected volatility differs across horizons; contango (normal) vs backwardation (stress). → this chapter.
* **Backwardation (VIX)** — short-dated IV above long-dated; a fear signal. → this chapter.
* **India VIX futures** — exchange contracts on VIX; launched 2014 and discontinued in 2017 for lack of liquidity, so India VIX is not directly tradable. → this chapter.
* **VIX percentile** — where the current VIX sits within its own recent distribution (readings below ÷ total). → this chapter.
* **Model-free implied volatility** — volatility derived from a whole strip of option prices rather than a single-option pricing model. → this chapter.

---

<!-- End of Chapter 13 (Rev 2, opens Part IV, current as of 4 Aug 2026). Rev 2 update (VIX-specific facts verified vs NSE/Business Standard): India VIX futures corrected from "illiquid" to "launched 2014, DISCONTINUED 2017 for low liquidity — no direct VIX trading currently"; added note on NSE's new volatility index pilot (2026, revised methodology, possible future derivatives). All numerical content is lot-INDEPENDENT (VIX→expected move) — unchanged; no transaction costs so Apr-2026 STT change not applicable; no expiry weekday specified. VIX→range: daily=Index×(VIX/100)/√252; VIX15→±233, VIX20→±310, VIX18→±279. Table 13.1 verified. VIX percentile examples: 210/250=84th, 175/250=70th. Regimes: low 10-13, normal 13-18, high 18-25, crisis 25+. COVID case anchored to closing peak 83.61 (24 Mar 2020, still the record), four phases with regime-appropriate strategies. Formula (13.1) reference-only, full derivation deferred to appendix. IV = implied volatility. -->
