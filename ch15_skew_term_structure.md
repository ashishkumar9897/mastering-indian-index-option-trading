<!-- Difficulty: Level 4/5 (Advanced). Dependency: Chapters 6, 13, 14. Target length ~10,000 words. Closes Part IV. Current as of 4 Aug 2026 (reviewed — no reader-facing changes needed). NOTE: this chapter has NO lot-size-dependent figures (all volatility-surface analytics — IV %, risk reversal, butterfly, term-structure slope, skew-adjusted delta, dispersion; the bull-put ₹68 vs bear-call ₹42 spread credits are per-unit and the teaching point is the R/R ratio), NO transaction-cost figures, and NO expiry-weekday references. So the lot-65 (NSE Jan-2026) and Apr-2026 STT changes do NOT apply here; content is evergreen and verified current. NIFTY skew (IV by strike, spot 24,600): 5%OTM put 17.5% → ATM 13.0% → 5%OTM call 11.0%. Risk reversal (25Δ put 24,300 @14.2% − 25Δ call ~25,050 @11.9%) = +2.3%. Butterfly ≈ +0.05%. Term structure contango: 3d 12.5%, 10d 13.0%, 24d 13.6%, 52d 14.0%; slope ≈ 11.2%/yr. Bull put vs bear call: ₹68 vs ₹42 credit (skew makes puts richer). Edition 2 additions: skew-adjusted (minimum-variance) delta (index puts → more negative than BSM); dispersion/correlation (Professional Insight, awareness-level). IV = implied volatility. -->

# Chapter 15 — Volatility Smile, Skew, and Term Structure

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Explain why different strikes carry different implied volatilities — the smile and the skew.
2. Read and interpret the NIFTY volatility skew.
3. Understand why OTM puts trade at higher IV than OTM calls (the crash premium).
4. Use skew information to build better spreads and assess risk.
5. Read the volatility term structure and its trading implications.
6. Recognise changes in skew and term structure as early-warning signals — and know their limits.

This is the most advanced chapter of Part IV, and it completes your volatility toolkit. Chapter 14 taught you to judge IV *across time* (implied vs realised). This chapter teaches you to read IV *across strikes and expiries* — the full volatility surface — which is where the market hides its deepest information about fear.

---

## 2. Introduction

Chapter 6 exposed a lie in the Black–Scholes model: it assumes one volatility for all strikes, but the market quotes a *different* implied volatility at every strike. Back out the IV from each NIFTY option and you do not get a flat line — you get a downward-sloping curve, with far-out-of-the-money puts priced at IVs several points higher than the at-the-money option, and OTM calls priced lower still. This shape is the **volatility skew**, and it is not an error or an inefficiency. It is the market telling you something Black–Scholes cannot: that a crash is feared more than a melt-up.

That single insight — that the shape of IV across strikes encodes the market's fear — is what this chapter is about. The skew tells you which options are relatively cheap and which are rich, before you even compare them to realised volatility. It makes a bull put spread structurally better-compensated than a bear call spread. It tells you, when it steepens, that institutions are paying up for downside protection. And read alongside the **term structure** — how IV differs across expiries — it reveals whether the market's fear is immediate (backwardation) or long-term (contango).

There is a subtler payoff too, one that most retail traders never reach: because the skew *moves* as the index moves, your true directional exposure is not the Black–Scholes delta on your screen. It is a **skew-adjusted delta**, and for index puts it is systematically larger than the number your platform shows. This chapter builds the full picture — the skew, the term structure, the metrics that quantify them, how to trade on them, and how the skew's own movement changes your hedge. Setting throughout: **NIFTY at 24,600**, with the illustrative surface introduced in Chapter 6.

---

## 3. Core Concepts

### 3.1 The volatility smile and skew — why strikes differ

The skew is the flagship of this chapter.

**What is it?** The **volatility skew** (or **smile**) is the pattern of implied volatility plotted against strike price. If you read the IV off each strike of a NIFTY expiry and plot them, you do not get a flat line (as Black–Scholes assumes) but a sloped curve. For equity indices the curve slopes *downward*: **OTM puts (low strikes) have the highest IV, the ATM sits in the middle, and OTM calls (high strikes) have the lowest.**

**Why does it exist?** Because Black–Scholes wrongly assumes returns are log-normal with constant volatility (Chapter 6), and the market *corrects* for that error through the strike-by-strike IV. Real index returns have **fat tails** — crashes are larger and more frequent than the bell curve predicts (Chapter 6) — and the fear is *asymmetric*: markets crash down far harder and faster than they spike up. The market prices this by charging *extra* implied volatility for the downside protection (OTM puts) that everyone wants, and *less* for the OTM calls that few need. The skew is Black–Scholes's flat-volatility assumption being overwritten by reality.

**Why should a trader care?** Because the skew tells you which strikes are relatively cheap and which are rich *before any other analysis*. An OTM put at 15% IV and an OTM call at 11% IV are not priced on the same volatility — the put is structurally dearer. This shapes every spread you build (Section 3.6), every hedge you buy, and your read of whether fear is rising (Section 3.4).

**Intuitive explanation.** The skew is the **price list of the market's fears**, strike by strike. Just as flood insurance costs more in a flood-prone area than fire insurance in a fireproof one, downside (put) protection costs more implied volatility than upside (call) speculation — because the market fears the flood (a crash) far more than it fears missing the fire (a rally).

**The shapes.** A symmetric **smile** (IV high on both wings, low at ATM) is typical of *currencies*, where big moves either way are equally feared. Equity indices show a **skew** (also called *reverse* or *negative* skew): high IV on the put side, low on the call side — a downward slope, because equity fear is one-directional.

**Numerical feel.** On our illustrative NIFTY surface (Table 15.1), the 5%-OTM put trades at 17.5% IV while the 5%-OTM call trades at 11.0% — a 6.5-point gap for options equally far from the money. That gap is the crash premium made visible.

**Professional interpretation.** Desks trade the *shape* of the skew, not just its level. They express views on whether the skew is too steep or too flat, whether it will steepen (fear rising) or flatten (complacency), independent of the direction of the index itself. To a professional, the skew is a tradable object in its own right.

**Common mistake.** Assuming all strikes share one IV (the VIX or the ATM IV). Treating a 15% ATM IV as the IV of every strike mis-prices the wings badly — especially the richly-skewed OTM puts.

**Practical takeaway.** **The skew is the market's strike-by-strike price of fear — read it to know which options are cheap and which are rich before you build any position, and never assume one IV fits all strikes.**

---

### 3.2 The NIFTY skew — shape and cause

Table 15.1 shows the illustrative NIFTY skew (IV by strike, spot 24,600, near expiry).

**Table 15.1 — NIFTY volatility skew (illustrative; IV by strike, spot 24,600)**

| Strike | Approx. moneyness | Implied volatility |
| ---: | --- | ---: |
| 23,400 | 5% OTM put | 17.5% |
| 23,700 | 3.7% OTM put | 16.3% |
| 24,000 | 2.4% OTM put | 15.3% |
| 24,300 | 1.2% OTM put | 14.2% |
| **24,600** | **ATM** | **13.0%** |
| 24,900 | 1.2% OTM call | 12.2% |
| 25,200 | 2.4% OTM call | 11.6% |
| 25,500 | 3.7% OTM call | 11.2% |
| 25,800 | 5% OTM call | 11.0% |

The shape is unmistakable: a steady **downward slope from puts to calls**. The three drivers:

* **Crash-risk premium.** Markets fall faster and harder than they rise; the fat left tail (Chapter 6) means OTM puts are more likely to pay off big than a normal distribution implies, so the market charges more IV for them.
* **Demand for put protection.** Institutions, funds, and hedgers are structurally *long* the market and constantly *buy* index puts to insure their holdings (Chapter 1). That persistent demand bids up put IV.
* **Supply–demand imbalance.** Few participants want OTM calls (a leveraged bet on a melt-up), and many willingly sell them (covered-call and overwriting flows), so call IV is pushed down. The mismatch is one-directional, so the skew is one-directional.

> **Beginner Alert — the skew is not a mispricing to exploit.** It is tempting to see "puts cost more IV than calls" and conclude puts are overpriced and should be sold. They are richer *for a reason* — they insure against the crash that actually happens. The skew reflects real, rational risk, not a free edge; selling the rich puts naked is selling the very insurance the market needs, and it carries exactly the tail risk the extra IV is compensating.

---

### 3.3 Skew metrics — risk reversal and butterfly

To *measure* the skew (rather than eyeball it), traders use two standard numbers, quoted in **delta space** (which normalises across expiries and spot levels — Section 3.7).

**Risk reversal** measures the *slope* — how much richer puts are than calls:

```
Risk reversal = IV(25-Delta put) − IV(25-Delta call)                (15.1)
```

A **positive** risk reversal (the equity-index norm) means puts are richer than calls — a put skew. The larger it is, the steeper the skew.

**Butterfly** measures the *convexity* — how much the wings are bid up relative to the ATM (the "smile" component on top of the skew):

```
Butterfly = [IV(25-Delta put) + IV(25-Delta call)] / 2 − IV(ATM)    (15.2)
```

A positive butterfly means both wings sit above the ATM (a genuine smile shape); for equity indices it is usually small — the skew (slope) dominates the butterfly (convexity).

**Worked metrics.** On our surface, the 25-Delta put sits near the 24,300 strike (IV 14.2%) and the 25-Delta call near 25,050 (IV ≈ 11.9%):

```
Risk reversal = 14.2% − 11.9% = +2.3%       (puts richer by 2.3 vol points — a put skew)
Butterfly     = (14.2% + 11.9%)/2 − 13.0% = 13.05% − 13.0% = +0.05%   (minimal convexity)
```

The +2.3% risk reversal quantifies the skew's steepness in a single number you can track over time; the near-zero butterfly confirms the NIFTY surface is a *skew*, not a symmetric smile.

---

### 3.4 How the skew changes — and what it signals

The skew is not static; its steepness *moves*, and the movement is information:

* **Before events, the skew steepens.** As uncertainty builds ahead of a budget, election, or shock, hedgers buy more puts, bidding up put IV faster than call IV — the risk reversal rises. Rising skew = rising demand for downside protection.
* **After a crash, the skew becomes extreme.** In the depths of a sell-off, put IV explodes (everyone wants protection at once), pushing the risk reversal to its widest.
* **In calm rallies, the skew flattens.** As fear ebbs and complacency sets in, put demand fades and the risk reversal narrows.

Table 15.2 shows the risk reversal across these regimes.

**Table 15.2 — NIFTY risk reversal by market regime (illustrative)**

| Regime | Risk reversal (25Δ put − call IV) | What it signals |
| --- | ---: | --- |
| Calm rally / complacency | ~+1.5% | Low demand for protection |
| Normal | ~+2.3% | Baseline crash premium |
| Pre-event / rising fear | ~+4.0% | Hedgers bidding up puts |
| Post-crash / panic | ~+6.5% | Extreme protection demand |

The change matters more than the level: a risk reversal *rising* from +2.3% to +4.0% tells you the market is quietly paying up for downside insurance — a shift in positioning that price alone does not reveal (the basis of the case study in Section 9). A *flattening* skew, conversely, signals complacency.

---

### 3.5 The term structure of volatility

Just as IV varies across strikes (the skew), it varies across *expiries* — the **volatility term structure.** Compare the ATM IV of successive expiries and you get a curve across time:

* **Normal (contango):** longer-dated IV > shorter-dated IV. The market assumes today's calm may not last, so it charges more for volatility further out. This is the usual state.
* **Inverted (backwardation):** shorter-dated IV > longer-dated IV. Immediate fear exceeds the expected long-run level — a stress signal. When the near-dated IV spikes above the far-dated, the market is bracing for something *now*.

**Worked term structure (normal, contango).**

**Table 15.3 — NIFTY ATM IV term structure (illustrative)**

| Expiry | Days to expiry | ATM IV | State |
| --- | ---: | ---: | --- |
| This week | 3 | 12.5% | — |
| Next week | 10 | 13.0% | Contango (rising) |
| Monthly | 24 | 13.6% | Contango |
| Next monthly | 52 | 14.0% | Contango |

The **term-structure slope** quantifies the tilt:

```
Slope = (IV_far − IV_near) / (T_far − T_near)
      = (14.0% − 12.5%) / ((52 − 3)/365 years) = 1.5% / 0.134 ≈ +11.2% per year
```

A positive slope is contango (normal). In stress the whole curve *inverts* — a near-week IV of 24% above a next-monthly IV of 15% (backwardation) — which is itself a fear signal, telling you the market expects turbulence imminently but a return to normal later. Reading the term structure tells you *when* the market expects volatility, complementing the skew's *what-strike* information.

> **Market Note — an inverted term structure is a warning worth heeding.** In calm markets you will almost always see contango (far IV above near). When you see the near-dated IV spike *above* the far-dated — backwardation — the market is pricing immediate danger, often around an event or during a developing sell-off. It is one of the cleaner "the market knows something is coming soon" signals available, precisely because it is unusual.

---

### 3.6 Using the skew — better spreads

The skew's most practical payoff is in **spread construction**: because puts are richer than calls, selling the put side is better-compensated than selling the call side. The classic illustration is the bull put spread versus the bear call spread.

Consider two credit spreads on our surface, each the same distance OTM (~2.4%) and the same width (300 points):

* **Bull put spread** (neutral-to-bullish): sell the 24,000 put (IV 15.3%), buy the 23,700 put (IV 16.3%). Because you sell a richly-skewed put, the net credit is large — illustratively **₹68**.
* **Bear call spread** (neutral-to-bearish): sell the 25,200 call (IV 11.6%), buy the 25,500 call (IV 11.2%). Because you sell a cheaply-skewed call, the net credit is small — illustratively **₹42**.

Same width, same distance — but the bull put spread collects **62% more credit** (₹68 vs ₹42), purely because of the skew:

```
Bull put spread: credit ₹68, max loss 300 − 68 = ₹232 → reward/risk = 68/232 = 0.29
Bear call spread: credit ₹42, max loss 300 − 42 = ₹258 → reward/risk = 42/258 = 0.16
```

The bull put spread offers a materially better reward-to-risk ratio for the same structural distance — a direct, tradable consequence of the put skew. This is why, in most market conditions, **selling put spreads is better-compensated than selling call spreads**, and why premium sellers with a neutral-to-bullish lean gravitate to the put side. The skew is not just information; it is an edge in *which side you sell*.

---

### 3.7 Sticky models and the skew-adjusted delta

Here is where the chapter reaches genuinely professional territory — and closes a loop left open in Chapter 8.

**Two models of how the skew moves with the market.** When the index moves, does the skew move with it? Two idealised models bracket the answer:

* **Sticky strike:** each *strike's* IV stays fixed as spot moves (IV is pinned to the strike level). Under sticky strike, as the index rises toward a higher strike, that strike keeps its (lower, call-side) IV, so the *ATM* IV falls.
* **Sticky delta (sticky moneyness):** each *moneyness/delta's* IV stays fixed as spot moves — the whole skew curve slides sideways with the index. Under sticky delta, the *ATM* IV stays constant as spot moves (the smile rides along).

Reality is usually somewhere between the two — often closer to sticky-strike in quiet ranges and closer to sticky-delta in trends. The point is that **the skew moves as the index moves**, which has a crucial consequence.

**The skew-adjusted (minimum-variance) delta.** The Black–Scholes delta on your screen assumes the option's *own* IV does not change when the spot moves. But it does — because the skew shifts. So your *true* directional exposure is not the BSM delta; it is a **skew-adjusted (minimum-variance) delta** that accounts for the IV change that accompanies a spot move:

```
Effective delta ≈ BSM delta + Vega × (change in the option's IV per unit spot move)
```

**The sign, for index puts — and why it matters.** For an equity index, IV *rises* when spot *falls* (the VIX–NIFTY inverse relationship, Chapter 13; the skew). So for an index **put**: a spot drop delivers both the directional gain (negative BSM delta) *and* an IV rise (positive Vega × rising IV) — the two reinforce, making the put's **effective delta more negative than its BSM delta.** An index **call**, conversely, gains on a rally (positive BSM delta) but the rally *crushes* IV (positive Vega × falling IV works against it), making its **effective delta less positive than BSM.**

The practical implication is concrete and important: **hedging a short-put book to its BSM delta systematically under-hedges the downside**, because the put's real sensitivity to a fall is larger than the screen delta shows. A trader who neutralises to BSM delta carries a residual, *predictable* short-delta-into-a-fall exposure — the position gets longer than expected as the market drops. Professionals hedge to the minimum-variance delta for exactly this reason; retail traders who hedge to the screen delta should at least *know* they are under-hedged on the downside.

> **Beginner Alert — your screen delta is not your true delta.** This is advanced, but the takeaway is simple: because the skew moves with the market, an index put's real exposure to a drop is *larger* than the delta your platform displays, and an index call's exposure to a rally is *smaller*. You do not need the formula, but you must not treat the BSM delta as the whole truth — especially when hedging downside risk, where it flatters you.

---

### 3.8 Dispersion and correlation

One final layer completes the picture of *where index volatility comes from* — and points to a professional edge.

> **Professional Insight — index vol is constituent vol plus correlation.** An index's implied volatility is not a standalone quantity; it is a function of its *constituents'* volatilities **and** the *correlations* between them:
>
> ```
> σ_index²  ≈  Σ wᵢ² σᵢ²  +  Σ (i≠j) wᵢ wⱼ ρᵢⱼ σᵢ σⱼ
> ```
>
> Higher correlation between constituents means the index moves more as a bloc, so — for the same constituent volatilities — **higher correlation produces higher index volatility.** This is why **BANKNIFTY behaves so differently from NIFTY**: BANKNIFTY is a handful of large, highly-correlated banks that tend to move together, so its index volatility runs close to its constituents' and it swings violently; the broad NIFTY 50 blends fifty stocks with lower average correlation, so diversification *dampens* its index volatility relative to its constituents.
>
> This decomposition is the basis of **dispersion trading** — selling index volatility while buying constituent volatility (a bet that correlation will *fall*, i.e., stocks will move more independently), or the reverse. It is a genuine professional edge in Indian markets and a way to trade correlation itself. It is flagged here at awareness level — enough to understand *why* BANKNIFTY and NIFTY volatilities differ and that correlation is a tradable variable — and revisited in the systematic-trading context later in the book. A full dispersion manual is beyond this book's Pareto scope, but the concept explains a great deal about how index vol behaves.

---

## 4. Examples (Real-World)

**Example 1 — The rich put, the cheap call.** A trader wants an OTM hedge and an OTM speculation. The 5%-OTM put costs 17.5% IV; the 5%-OTM call costs 11.0% IV. The protection they *need* is dear; the lottery ticket they *want* is cheap — the skew, priced exactly as the market's fears dictate.

**Example 2 — The steepening warning.** Over two quiet weeks the NIFTY drifts sideways, but the risk reversal climbs from +2.3% to +4.2%. Price says "nothing happening"; the skew says "someone is buying a lot of downside protection." A risk-aware trader tightens up (the case study, Section 9).

**Example 3 — The better side to sell.** Two sellers, both neutral-to-bullish. One sells a bull put spread (collecting the rich put IV); the other sells a bear call spread (collecting the thin call IV). Same distance, same width — the put seller collects 62% more credit, purely from the skew. The skew chose the better trade.

---

## 5. Numerical Examples

Setting: NIFTY 24,600; surface from Table 15.1.

### Numerical Example 1 — Risk reversal and butterfly

Using the 25-Delta put (≈24,300, IV 14.2%) and 25-Delta call (≈25,050, IV 11.9%):

```
Risk reversal = 14.2% − 11.9% = +2.3%   (a put skew; puts richer by 2.3 vol points)
Butterfly     = (14.2% + 11.9%)/2 − 13.0% = +0.05%   (minimal convexity — a skew, not a smile)
```

A single +2.3% risk-reversal number captures the whole skew's steepness — track it over time to see fear rise or fall.

### Numerical Example 2 — Term-structure slope

Using the ATM IV term structure (Table 15.3): near IV 12.5% at 3 DTE, far IV 14.0% at 52 DTE:

```
Slope = (14.0% − 12.5%) / ((52 − 3)/365) = 1.5% / 0.134 ≈ +11.2% per year
```

A positive slope confirms **contango** (normal). Had the near-week IV been 24% and the next-monthly 15%, the slope would be sharply negative — **backwardation**, a stress signal.

### Numerical Example 3 — Bull put spread vs bear call spread

Same width (300) and distance (~2.4% OTM), from the surface:

```
Bull put spread (sell 24,000 PE @15.3%, buy 23,700 PE @16.3%): credit ₹68, max loss ₹232, R/R 0.29
Bear call spread (sell 25,200 CE @11.6%, buy 25,500 CE @11.2%): credit ₹42, max loss ₹258, R/R 0.16
```

The bull put spread collects **62% more credit** for the same structure — the skew makes the put side the better-compensated sale.

### Numerical Example 4 — Reading a skew change

A month ago the risk reversal was +2.3%; today it is +4.0%:

```
Change = +4.0% − 2.3% = +1.7 vol points steeper
```

The skew has **steepened** — the market is paying up for downside protection relative to a month ago. This signals rising fear/hedging demand (a risk-management flag), though it is a noisy predictor of an actual fall (Section 9).

### Numerical Example 5 — The skew-adjusted delta, directionally

An index put shows a BSM delta of −0.30 on the screen. Because a spot drop also lifts the put's IV (the skew), the put gains *extra* value on a fall beyond what −0.30 implies:

```
Effective (minimum-variance) delta ≈ −0.30 + [Vega × (IV rise per point of spot fall)]
→ more negative than −0.30 (e.g., ≈ −0.35)
```

So a short-put position hedged to the BSM −0.30 is **under-hedged on the downside** — as the market falls, the position gets longer than the screen delta predicted. The true hedge ratio is the (more negative) skew-adjusted delta.

---

## 6. Calculations (the reusable recipes)

**(a) Skew metrics (in delta space)**

```
Risk reversal = IV(25Δ put) − IV(25Δ call)      (slope; positive = put skew)
Butterfly     = [IV(25Δ put) + IV(25Δ call)]/2 − IV(ATM)   (convexity)
```

**(b) Term-structure slope**

```
Slope = (IV_far − IV_near) / (T_far − T_near)    (positive = contango; negative = backwardation)
```

**(c) Skew-adjusted (minimum-variance) delta (conceptual)**

```
Effective delta ≈ BSM delta + Vega × (ΔIV of the option per unit spot move)
Index puts → more negative than BSM (spot drop also raises IV)
Index calls → less positive than BSM (spot rise crushes IV)
```

**(d) Index volatility from constituents (reference)**

```
σ_index² ≈ Σ wᵢ²σᵢ² + Σ(i≠j) wᵢwⱼ ρᵢⱼ σᵢσⱼ    (higher correlation → higher index vol)
```

---

## 7. Practical Insights

* **Never use one IV for all strikes.** The skew means the ATM IV (or VIX) badly misprices the wings; read each strike's own IV, especially the richly-skewed OTM puts.
* **Track the risk reversal, not just the level of IV.** A steepening skew (rising risk reversal) signals rising demand for protection — a positioning shift price does not show.
* **Sell the skew's rich side.** In most conditions the put side is better-compensated than the call side; a bull put spread beats a bear call spread on reward-to-risk for the same structure.
* **Read the term structure for timing.** Contango is normal; backwardation (near IV above far) warns of imminent, expected turbulence.
* **Respect the skew-adjusted delta on the downside.** For index puts, your true exposure to a fall exceeds the screen delta — hedge short-put risk knowing you are otherwise under-hedged.

> **Professional Insight — the surface is a map of what the market fears, and when.** The skew tells you *which* outcome the market fears (the downside — steeply), and the term structure tells you *when* (soon, if inverted). Together they are a two-dimensional map of market anxiety that price alone cannot draw. Professionals read the whole surface before every significant trade — not to predict, but to know what is already priced, which side is rich, and where their true exposures lie.

---

## 8. Common Mistakes

* **Assuming a single IV across strikes.** Treating the ATM IV or VIX as every strike's IV mis-prices the wings and underestimates rich OTM puts.
* **Reading the skew as a mispricing to sell.** Rich puts are rich *because* they insure real crash risk; selling them naked is underwriting the tail the extra IV is paying for.
* **Selling the cheap side of the skew.** Building bear call spreads (selling low-IV calls) when a bull put spread (selling high-IV puts) would collect far more for the same risk.
* **Ignoring a steepening skew.** Dismissing a rising risk reversal as noise when it flags rising hedging demand — a reason to tighten risk.
* **Trusting the BSM screen delta as the whole truth.** For index puts, the true (skew-adjusted) delta is more negative, so downside hedges built on the screen delta under-hedge.
* **Overreading the skew as a crash timer.** A steepening skew is a *positioning* signal, not a reliable *timing* signal — it precedes many falls that never come (Section 9).

---

## 9. Case Study — "Skew Signals Before the Crash"

**Context.** A recurring claim among sophisticated traders is that the volatility skew "warns" of coming corrections: before a fall, put demand rises, the skew steepens, and an alert trader can see the storm forming in the IV surface while price still looks calm. This case examines a representative episode — the NIFTY put skew steepening in the two-to-three weeks *before* a ~10% correction — and asks the honest question: is skew a reliable early warning, or is it noise? Figures are **illustrative and representative**.

**What the skew did.** In the weeks before the correction, with the NIFTY still drifting sideways-to-up and the news flow calm, the 25-Delta risk reversal climbed steadily:

| Timing | Risk reversal (25Δ put − call) | Term structure |
| --- | ---: | --- |
| ~3 weeks before | +2.4% | Contango (normal) |
| ~2 weeks before | +3.3% | Flattening |
| ~1 week before | +4.5% | Near-flat |
| Days before | +5.5% | Inverting (backwardation) |

While price said "nothing is wrong," the surface was repositioning: the risk reversal more than doubled, and the term structure flattened and began to invert — both classic signs that institutions were **buying downside protection in size** and pricing *imminent* risk. Then the correction came, and the skew went to a post-crash extreme (+7%+).

**The honest analysis — signal or noise?** The temptation is to conclude "the skew predicted the crash." The truth is more nuanced, and more useful:

* **The skew carried real information.** A steepening risk reversal and an inverting term structure genuinely reflect rising demand for protection — a *positioning* shift by informed, hedging-oriented players (funds insuring books). That is real, and price did not show it. In this episode, the surface was ahead of the price.
* **But the skew is a *noisy* predictor.** The skew steepens *many* times without a crash following. Institutions buy protection routinely — around events, at quarter-ends, on mild nervousness — and most of those steepenings resolve with no correction at all. So a steepening skew has a high **false-positive rate**: it fires before crashes *and* before nothing.
* **The hindsight trap.** Reading this case *after* the crash, the steepening looks like an obvious flashing red light. In real time, it was one of several ambiguous signals, indistinguishable from the many steepenings that led nowhere. Selecting the episode where the signal "worked" is exactly the survivorship/hindsight bias this book warns against (Chapter 7).

**The correct use.** The skew is therefore a **risk-management input, not a timing signal.** A steepening skew and an inverting term structure should make you *more cautious* — tighten stops, reduce short-Vega and short-Gamma exposure, buy back some risk, size down — precisely because the *tail* the surface is pricing has become more likely (or at least more feared). But it should not be traded as a prediction ("skew steepened, so short the market"), because it is wrong far more often than it is right about timing. Use it to manage the risk you already carry, not to place a directional bet.

**The lesson.** The volatility surface reveals positioning and fear that price conceals — genuine information. But information about *what is feared* is not a forecast of *what will happen*. Read a steepening skew as the market raising its own guard, and raise yours too; do not read it as a crystal ball.

*(Takeaway: a steepening skew tells you the market is paying more for downside protection — a real, price-invisible signal to manage risk more conservatively, but a noisy and unreliable predictor of an actual crash.)*

---

## 10. Chapter Summary

* The **volatility skew** is IV plotted against strike; for equity indices it slopes *down* — OTM puts have the highest IV, OTM calls the lowest — because Black–Scholes's flat-vol assumption is overwritten by fat tails and one-directional crash fear.
* The NIFTY skew exists because of the **crash-risk premium, structural demand for put protection, and a supply–demand imbalance** (few want OTM calls); it is rational risk pricing, not a free edge.
* **Skew metrics:** the **risk reversal** (IV 25Δ put − 25Δ call) measures the slope (≈+2.3% on our surface, a put skew); the **butterfly** measures convexity (≈0, so a skew, not a smile).
* The skew **steepens before events and after crashes, and flattens in calm rallies** — a rising risk reversal signals rising demand for protection.
* The **term structure** (ATM IV across expiries) is usually **contango** (far > near); **backwardation** (near > far) is a stress signal of imminent, expected turbulence.
* The skew makes the **put side the better-compensated sale** — a bull put spread collects far more than a bear call spread (₹68 vs ₹42) for the same structure.
* **Sticky-strike vs sticky-delta** models describe how the skew moves with spot; because it *does* move, your true exposure is a **skew-adjusted (minimum-variance) delta** — more negative than BSM for index puts, so downside hedges on the screen delta under-hedge.
* **Index volatility = constituent vols + correlations** — higher correlation means higher index vol (BANKNIFTY vs NIFTY); the basis of dispersion trading, flagged at awareness level.
* A **steepening skew** is a real *positioning* signal but a *noisy* crash predictor — use it to manage risk, not to time trades.

---

## 11. Key Takeaways

* **Read the whole surface, never one IV** — the skew tells you which strikes are rich (OTM puts) and cheap (OTM calls) before any other analysis.
* **Track the risk reversal and the term structure** — a steepening skew and an inverting term structure are the market raising its guard; raise yours.
* **Sell the rich side of the skew** — put spreads beat call spreads on reward-to-risk for the same structure in most conditions.
* **Know that your screen delta under-states downside risk on index puts** (the skew-adjusted delta is more negative), and that index vol is driven by correlation — the reason BANKNIFTY and NIFTY behave so differently.

---

## 12. Practice Questions

**Q1 (Definition).** In one sentence, describe the shape of the equity-index volatility skew and why it slopes that way.

**Q2 (Metric).** The 25-Delta put IV is 15.0% and the 25-Delta call IV is 11.5%. Compute the risk reversal and state what it indicates.

**Q3 (Butterfly).** With the Q2 values and an ATM IV of 12.8%, compute the butterfly and interpret it.

**Q4 (Cause).** Give two reasons OTM puts trade at higher IV than OTM calls on the NIFTY.

**Q5 (Skew change).** The risk reversal was +2.5% a month ago and is +4.2% today. Has the skew steepened or flattened, and what does it signal?

**Q6 (Term structure).** Near-week ATM IV is 21% and next-monthly is 14%. Is the term structure in contango or backwardation, and what does it imply?

**Q7 (Spread choice).** You are neutral-to-bullish and want a credit spread. Using the skew, which is better-compensated — a bull put spread or a bear call spread — and why?

**Q8 (Skew-adjusted delta).** An index put's BSM delta is −0.28. Is its true (skew-adjusted) delta more or less negative, and what does that mean for hedging a short put?

**Q9 (Dispersion).** Why does BANKNIFTY typically show more violent volatility than the broad NIFTY, in terms of correlation?

**Q10 (Judgement).** A trader sees the skew steepen sharply and shorts the NIFTY, expecting a crash. Explain why this is a misuse of the signal.

---

## 13. Detailed Solutions

**A1.** The equity-index skew slopes **downward** — OTM puts have the highest IV, the ATM is in the middle, and OTM calls the lowest — because the market fears a crash (a fast, fat-tailed downside move) far more than a rally, so it charges extra implied volatility for downside protection.

**A2.** Risk reversal = 15.0% − 11.5% = **+3.5%**. A positive risk reversal indicates a **put skew** — puts are richer than calls by 3.5 vol points, a fairly steep skew reflecting elevated demand for downside protection.

**A3.** Butterfly = (15.0% + 11.5%)/2 − 12.8% = 13.25% − 12.8% = **+0.45%**. A small positive butterfly indicates modest convexity — both wings sit slightly above the ATM — but the surface is dominated by the skew (slope), not the smile (convexity).

**A4.** Any two: (i) the **crash-risk premium** — fat left tails mean OTM puts pay off big more often than a normal distribution implies; (ii) **structural demand for put protection** from institutions hedging long portfolios; (iii) a **supply–demand imbalance** — few want OTM calls (many sell them via overwriting), pushing call IV down while put IV is bid up.

**A5.** The skew has **steepened** (risk reversal rose from +2.5% to +4.2%). It signals **rising demand for downside protection** — the market is paying up for puts relative to calls, a positioning shift toward caution (a risk-management flag, though a noisy predictor of an actual fall).

**A6.** Near IV (21%) is *above* far IV (14%), so the term structure is **inverted — backwardation.** It implies the market expects **imminent turbulence** (a near-term event or developing stress) but a return toward normal volatility later — a stress signal.

**A7.** The **bull put spread** is better-compensated. Because of the skew, OTM puts carry higher IV than equidistant OTM calls, so selling the put side (bull put spread) collects more credit for the same width and distance than selling the call side (bear call spread) — a better reward-to-risk ratio.

**A8.** Its true delta is **more negative** than −0.28 (e.g., ≈ −0.33), because a spot drop also *raises* the put's IV (the skew), adding to its gain on a fall. For hedging a short put, it means hedging to the BSM −0.28 **under-hedges the downside** — as the market falls, the short put position gets longer than the screen delta predicted, so you should hedge to the (more negative) skew-adjusted delta.

**A9.** BANKNIFTY comprises a few large, **highly-correlated** banks that tend to move together, so the correlation term in index variance is large — index volatility runs close to its constituents' and swings violently. The broad NIFTY 50 blends fifty stocks with **lower average correlation**, so diversification dampens its index volatility relative to its constituents.

**A10.** It misuses the signal because a steepening skew is a **positioning/risk signal, not a timing signal.** The skew steepens far more often than crashes occur (a high false-positive rate) — institutions buy protection routinely without a fall following. Shorting the market on it treats a noisy indicator as a prediction; the correct response is to **manage risk more conservatively** (reduce short-Gamma/short-Vega exposure, tighten stops), not to place a directional bet.

---

## 14. Mini Glossary

* **Volatility skew** — the pattern of IV across strikes; downward-sloping for equity indices (OTM puts richest). → this chapter.
* **Volatility smile** — a symmetric version (both wings high), typical of currencies. → this chapter.
* **Crash-risk premium** — the extra IV charged on OTM puts for fat-tailed downside risk. → this chapter.
* **Risk reversal** — IV(25Δ put) − IV(25Δ call); measures the skew's slope; positive = put skew. → this chapter.
* **Butterfly (skew)** — [IV(25Δ put) + IV(25Δ call)]/2 − IV(ATM); measures the smile's convexity. → this chapter.
* **Term structure (of volatility)** — ATM IV across expiries; contango (far > near, normal) vs backwardation (near > far, stress). → this chapter.
* **Sticky strike** — a model where each strike's IV stays fixed as spot moves. → this chapter.
* **Sticky delta (sticky moneyness)** — a model where each delta's IV stays fixed and the skew slides with spot. → this chapter.
* **Skew-adjusted (minimum-variance) delta** — the true directional exposure accounting for the skew's co-movement; more negative than BSM for index puts. → this chapter.
* **Dispersion trading** — trading index volatility against constituent volatility; a bet on correlation. → this chapter.
* **Correlation (index)** — the co-movement of constituents that, with their vols, determines index volatility. → this chapter.

---

<!-- End of Chapter 15 (Rev 2, closes Part IV, current as of 4 Aug 2026). Rev 2: reviewed for 4-Aug-2026 currency — NO reader-facing changes required. Chapter has no lot-size, transaction-cost, or expiry-weekday dependence (all volatility-surface analytics; spread credits per-unit, teaching point is R/R ratio), so the lot-65 and Apr-2026 STT updates do not apply; all content verified accurate and current. NIFTY skew Table 15.1: 5%OTM put 17.5% → ATM 13.0% → 5%OTM call 11.0%. RR = 14.2−11.9 = +2.3%; butterfly = +0.05%. Term structure contango (Table 15.3): 3d 12.5%, 10d 13.0%, 24d 13.6%, 52d 14.0%; slope +11.2%/yr. Bull put ₹68 (R/R 0.29) vs bear call ₹42 (R/R 0.16) — skew makes puts richer. Edition 2: skew-adjusted delta (index puts more negative than BSM; sign derived via Vega×dIV/dSpot<0); dispersion σ_index²=Σw²σ²+Σww ρσσ (BANKNIFTY high correlation). Case study: skew steepening (RR +2.4→+5.5) before a 10% correction — real positioning signal, noisy predictor, hindsight-bias caveat. IV = implied volatility. Dispersion revisited later without chapter-number forward ref. -->
