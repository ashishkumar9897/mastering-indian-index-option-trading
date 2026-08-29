<!-- Difficulty: Level 2.5/5 (Intermediate). Dependency: Chapters 4, 5. Target length ~8,500 words. Current as of 4 Aug 2026. HOUSE BASELINE: NIFTY 24,600, lot size 65 (NSE Jan-2026 revision); NIFTY weekly expiry = Tuesday (since 1 Sep 2025). One internally consistent illustrative NIFTY chain (spot 24,600, F≈24,620) is used throughout for anatomy, OI, PCR, Max Pain, and synthetic future. NOTE: all chain metrics here (PCR 0.91, Max Pain 24,600, synthetic future 24,620) are lot-INDEPENDENT — OI is in lots, PCR is a ratio, Max Pain argmin and synthetic future are unaffected by lot size — so the 75→65 change is cosmetic only. All OI/premium figures are illustrative and flagged. IV = implied volatility. OI figures in thousands of lots. -->

# Chapter 7 — Reading the Option Chain Like a Professional

---

## 1. Learning Objectives

By the end of this chapter, you will be able to:

1. Read and interpret every column on the NSE option chain.
2. Infer the market's directional bias from the chain.
3. Use Open Interest to locate likely support and resistance.
4. Spot unusual activity that hints at institutional positioning.
5. Compute and interpret the Put–Call Ratio (PCR).
6. Calculate Max Pain — and know its real limitations.

The option chain is the single screen you will look at more than any other. This chapter turns it from a wall of numbers into a readable map of what the market is doing with its money.

---

## 2. Introduction

The cash market shows you one number per stock: the price. The option chain shows you *hundreds* of numbers for a single index — a call and a put at every strike, each with its price, its volume, its open interest, and its implied volatility. Buried in that grid is something the price alone can never tell you: **where the market has placed its bets, and how strongly.**

A professional does not read the chain to find "the price." They read it to answer questions the price cannot: Where are the big option writers defending? Which strikes are acting as walls? Is fresh money betting up or down? Is the crowd leaning so far one way that the smart move is to fade it? Where is the market likely to be pinned at expiry?

None of these signals is a crystal ball. Open Interest, PCR, and Max Pain are *context*, not commands — probabilistic tilts that occasionally scream and often merely whisper. Used well, they sharpen a view you already hold. Used naively, they become superstition. This chapter teaches the difference.

We work throughout from a single illustrative NIFTY chain: **spot 24,600, a near weekly expiry, lot size 65**, with the near-month future around **24,620**. Every OI and premium figure is illustrative but internally consistent, so you can follow the arithmetic end to end. Open Interest is quoted in **thousands of lots**.

---

## 3. Core Concepts

### 3.1 Anatomy of the option chain

The NSE chain is laid out symmetrically: **calls on the left, puts on the right, strikes down the middle.** Each side shows the same columns. Table 7.1 is our working chain.

**Table 7.1 — Illustrative NIFTY option chain (spot 24,600; OI in '000 lots; premiums illustrative)**

| Call OI | Call Chg OI | Call LTP | **Strike** | Put LTP | Put Chg OI | Put OI |
| ---: | ---: | ---: | :---: | ---: | ---: | ---: |
| 25 | +3 | 438 | **24,200** | 28 | +18 | 95 |
| 30 | +5 | 345 | **24,300** | 42 | +12 | 80 |
| 45 | +8 | 258 | **24,400** | 62 | +9 | 70 |
| 55 | +6 | 188 | **24,500** | 92 | +7 | 65 |
| 70 | +10 | 135 | **24,600** | 115 | +11 | 72 |
| 60 | +9 | 92 | **24,700** | 172 | +4 | 48 |
| 85 | +20 | 66 | **24,800** | 240 | +2 | 32 |
| 50 | +7 | 38 | **24,900** | 318 | +1 | 22 |
| 130 | +35 | 22 | **25,000** | 405 | +1 | 15 |

The columns, defined:

* **LTP (Last Traded Price)** — the premium of the last trade at that strike. (The live screen also shows **bid/ask** around it; the LTP sits inside that spread.)
* **Volume** — the number of contracts *traded today* at that strike (not shown in Table 7.1 for width; on the live screen it sits beside LTP). Volume resets to zero each day.
* **Open Interest (OI)** — the number of contracts *currently outstanding* (open, not yet closed) at that strike. This is the heart of the chain and the subject of Section 3.2.
* **Change in OI (Chg OI)** — how OI moved today: positive means net new contracts were opened, negative means contracts were closed.
* **IV (Implied Volatility)** — the volatility the market is pricing into that strike (Chapter 6). It varies by strike — the skew — and is shown per strike in Table 7.2.

> **Beginner Alert — Volume and Open Interest are not the same thing.** *Volume* is how many contracts changed hands **today**; it resets to zero every morning. *Open Interest* is how many contracts are **still open** right now; it carries over day to day. A strike can have huge volume (lots of trading) but low OI (positions opened and closed the same day), or high OI (large standing positions) with little volume today. Confusing the two is one of the most common beginner errors — OI tells you where money is *parked*, volume tells you where it is *moving today*.

---

### 3.2 Open Interest — the chain's most important number

Open Interest deserves the full treatment, because almost every other signal in this chapter is built on it.

**What is it?** Open Interest is the total number of option contracts at a strike that are **open** — created but not yet closed out or expired. Every contract has a buyer and a seller; OI counts each such open pair once.

**Why does it exist / how does it change?** OI rises when a *new* buyer and a *new* seller create a fresh contract, and falls when an existing buyer and seller both close. It is unchanged when a position merely transfers from one holder to another. So OI measures the **stock of live commitments** at each strike — how much conviction is currently parked there.

**Why should a trader care?** Because price tells you what the last trade cost, but OI tells you *where the market has committed capital*. Big OI at a strike means many participants have a stake in that level — and, crucially, many *writers* (sellers) who will hedge to defend it. That is what turns high-OI strikes into support and resistance (Section 3.4).

**Intuitive explanation.** Think of each strike as a table in a casino. **Volume** is how many chips were bet at that table today; **OI** is how many chips are *still on the table right now*. A table piled high with standing chips (high OI) is one the house — the writers — will fight hardest to protect.

**The buyer/seller ambiguity — and how to resolve it.** OI alone does not tell you whether the new contracts were opened by buyers or sellers (every contract has both). You infer intent by combining **OI change with price change** (the matrix in Section 3.3) and with which side of the chain is building. As a working heuristic in index options: **rising call OI acts as resistance** (call writers cap the upside) and **rising put OI acts as support** (put writers cushion the downside).

**Professional interpretation.** Institutions and large writers leave footprints in OI that they cannot hide. A sudden, large OI build-up at a specific strike — especially with the premium there flat or falling — usually signals **writing** (someone selling that strike in size), which marks a level they expect to hold. Reading these footprints is a core professional skill.

**Common mistake.** Treating a strike's high OI as automatically bullish or bearish without checking the price and OI *change* together. High OI is a wall; only the context tells you which way it leans.

**Practical takeaway.** **Read OI to find where the market's capital is committed, and combine it with price and OI *change* to infer whether that commitment is being built or unwound.** OI is where the money sleeps; the change in OI is where it is moving.

---

### 3.3 The Price + OI matrix — reading build-ups

Combining the direction of **price** with the direction of **OI** gives four classic states. Applied to the underlying (or to a single contract), Table 7.3 decodes them.

**Table 7.3 — The Price + OI interpretation matrix**

| | **OI rising** | **OI falling** |
| --- | --- | --- |
| **Price rising** | **Long build-up** — fresh buyers entering; *bullish* | **Short covering** — sellers buying back; bullish but often *temporary* |
| **Price falling** | **Short build-up** — fresh sellers entering; *bearish* | **Long unwinding** — buyers exiting; *bearish/weakening* |

The distinction that matters most: **fresh positioning (OI rising) is a stronger signal than position-closing (OI falling).** A rally on rising OI (long build-up) has new conviction behind it; a rally on falling OI (short covering) is often just trapped sellers scrambling out, and can fade once they are done.

Applied to the chain itself: if a call strike's OI is *rising* while its price is *falling*, that is **call writing** — fresh sellers, marking resistance. If a put strike's OI is rising while its price is flat or falling, that is **put writing** — fresh sellers, marking support.

---

### 3.4 OI concentration — support and resistance

The strikes with the **largest OI** act as magnets and walls, because the writers there hedge to defend those levels. Reading our chain (Table 7.1):

**Call OI (potential resistance), largest first:**

```
25,000 │████████████████████ 130   ← strongest resistance
24,800 │█████████████ 85
24,600 │███████████ 70
24,700 │█████████ 60
```

**Put OI (potential support), largest first:**

```
24,200 │███████████████ 95         ← strongest support
24,300 │█████████████ 80
24,600 │███████████ 72
24,400 │███████████ 70
```

The picture is immediate: **strong resistance at 25,000** (the largest OI wall on the chain) and **strong support at 24,200**, with the index at 24,600 sitting inside that band. The chain is telling you the market expects, for now, a range roughly between 24,200 and 25,000 — and that a decisive break of either wall would be significant, because it would mean the defending writers there were overrun.

> **Professional Insight — Walls are defended until they aren't.** High-OI strikes hold *because* writers hedge to keep them holding — until a large enough flow forces those writers to unwind, at which point the level can break fast and the hedging that defended it reverses to accelerate the move. The strongest OI wall is both the most reliable level and, when it finally gives way, the most violent. Respect the wall, but never assume it is permanent.

---

### 3.5 Change in OI — the leading edge

The *static* OI shows where capital is parked; the **change in OI** shows where it is moving *today*, which is more forward-looking. In our chain:

* **25,000 call: Chg OI +35** (the largest build-up), with the premium low at ₹22 — heavy **fresh call writing**, hardening the 25,000 resistance.
* **24,800 call: Chg OI +20** — more call writing just below the top wall.
* **24,200 put: Chg OI +18** and **24,300 put: +12** — **fresh put writing**, hardening support at the lower band.

The story the *changes* tell is consistent with the static picture and adds conviction: writers are actively reinforcing both walls today, i.e., positioning for a continued range. Had we instead seen call OI at 25,000 *falling* fast (short covering) while the index pushed up, that would warn the ceiling might be about to give.

---

### 3.6 The Put–Call Ratio (PCR)

The **PCR** compresses the whole chain into one number:

```
PCR(OI)     = Total Put OI     ÷ Total Call OI
PCR(Volume) = Total Put Volume ÷ Total Call Volume
```

**PCR(OI)** reflects standing positioning and moves slowly; **PCR(Volume)** reflects today's activity and is jumpier. Use PCR(OI) for the prevailing structural lean, PCR(Volume) for intraday shifts in sentiment.

**Interpretation — and the contrarian twist.** A PCR around **0.8–1.1** is broadly neutral for NIFTY. The signal lives at the *extremes*, and it is usually read **contrarian**:

* **Very high PCR (say > 1.3)** — puts vastly outnumber calls; the crowd is heavily hedged or bearish. Often a sign of *excessive fear* and a potential bottom (contrarian bullish).
* **Very low PCR (say < 0.7)** — calls dominate; the crowd is complacent or greedy. Often a sign of *excessive optimism* and a potential top (contrarian bearish).

For our chain, PCR(OI) = 499 ÷ 550 = **0.91** (Numerical Example 1) — mildly call-heavy, broadly neutral with a slight cautious tilt. No extreme, so no strong contrarian signal; the *distribution* of OI (the walls in Section 3.4) is more informative here than the single ratio.

> **Market Note — PCR is a blunt instrument.** A single ratio hides everything about *where* the OI sits. Two chains can share the same PCR while telling opposite stories — one with balanced walls, another with all its puts piled at a single crash strike. Always read PCR alongside the OI distribution, never instead of it.

---

### 3.7 Max Pain — where writers hurt least

**What is it?** **Max Pain** is the expiry price at which the *total payout to all option holders is smallest* — equivalently, the strike at which option **writers** (sellers) collectively lose the least. The theory, rooted in the idea that large, well-hedged writers influence where price settles, holds that the index tends to **gravitate toward Max Pain by expiry**.

**How to compute it.** For each candidate settlement price, add up the intrinsic value that would be paid out on every in-the-money call and put; the price with the **smallest total** is Max Pain:

```
Total pain(S*) = Σ (K<S*) CallOI[K]·(S* − K) + Σ (K>S*) PutOI[K]·(K − S*)
Max Pain = the S* that minimises Total pain
```

We compute this fully for our chain in Numerical Example 2; the answer there is **24,600**.

**Utility and limitations — read this carefully.** Max Pain is a *descriptive tendency*, not a law:

* It works best in **quiet, range-bound expiries** with stable OI, and it is most visible in the **final day or two** before expiry.
* It **fails on trending and event days** — a strong directional move or a news shock overwhelms any pinning tendency.
* OI **shifts constantly**, so Max Pain moves during the week; today's number is not destiny.
* Correlation is not causation: the index and Max Pain both cluster where OI is heaviest, so they often coincide without one "pulling" the other.

Treat Max Pain as *one more piece of context* — useful for judging where a quiet expiry might settle, useless as a standalone trade trigger.

---

### 3.8 Implied volatility across the chain — the skew

The chain also lets you read **implied volatility by strike**, and it is not constant (Chapter 6). Table 7.2 shows the IV for our chain.

**Table 7.2 — Implied volatility by strike (our chain)**

| Strike | 24,200 | 24,300 | 24,400 | 24,500 | 24,600 | 24,700 | 24,800 | 24,900 | 25,000 |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| IV | 15.3% | 14.6% | 14.0% | 13.5% | 13.0% | 12.6% | 12.3% | 12.1% | 11.9% |

IV falls as the strike rises — the **skew** — because the market pays up for downside (put) protection relative to upside (call) speculation. Reading the skew from the chain tells you, at a glance, that crash insurance is dear and upside bets are cheap today — information you cannot get from price or OI alone.

---

### 3.9 The synthetic future — parity on the chain

Put–call parity (Chapter 4) lets you back the **future** out of the chain directly:

```
Synthetic future = ATM Call LTP − ATM Put LTP + ATM Strike
```

For our chain at the 24,600 strike: 135 − 115 + 24,600 = **24,620** — matching the near-month future. This is a fast sanity check: if the synthetic future from the chain drifts far from the actual future, either your prices are stale or a genuine dislocation exists. It also reminds you that the chain is priced off the *future* (24,620), not the spot (24,600).

---

## 4. Examples (Real-World)

**Example 1 — The wall that held.** A trader eyeing a breakout sees 130,000 lots of call OI stacked at 25,000, growing daily. Rather than buy a 25,000 call into that wall, they recognise the resistance and wait; the index stalls near 24,950 and reverses, and the far-OTM calls they *didn't* buy expire worthless. The chain warned them where the ceiling was.

**Example 2 — Short covering that faded.** The index jumps 1% and the news feed cheers a "breakout." But the chain shows call OI at the resistance strike *falling* sharply (short covering), not put OI building. The move is trapped writers scrambling out, not fresh bullish conviction — and once they finish, the rally stalls. Price + OI told a different story than price alone.

**Example 3 — PCR at an extreme.** After a sharp fall, PCR(OI) spikes to 1.5 as everyone piles into puts. A contrarian reads the *excess fear*, not the panic, and looks for a bounce — which arrives as the oversold market mean-reverts. The extreme, not the level, was the signal.

---

## 5. Numerical Examples

Using the chain in Table 7.1 (OI in '000 lots).

### Numerical Example 1 — PCR(OI)

```
Total Put OI  = 95+80+70+65+72+48+32+22+15 = 499
Total Call OI = 25+30+45+55+70+60+85+50+130 = 550
PCR(OI) = 499 ÷ 550 = 0.91
```

**Interpretation.** At 0.91 the chain is mildly call-heavy and broadly neutral — no fear/greed extreme. With no contrarian signal from the ratio, the actionable read comes from the OI *distribution* (resistance 25,000, support 24,200), not the PCR.

### Numerical Example 2 — Max Pain (full calculation)

For each candidate settlement price (a listed strike), total pain = payout on all ITM calls + all ITM puts, in units of (thousand-lots × points). Table 7.4 shows the totals.

**Table 7.4 — Total option-writer payout by candidate settlement (Max Pain)**

| Settlement | Call payout | Put payout | **Total pain** |
| ---: | ---: | ---: | ---: |
| 24,200 | 0 | 140,900 | 140,900 |
| 24,300 | 2,500 | 100,500 | 103,000 |
| 24,400 | 8,000 | 68,100 | 76,100 |
| 24,500 | 18,000 | 42,700 | 60,700 |
| **24,600** | 33,500 | 23,800 | **57,300 ← minimum** |
| 24,700 | 56,000 | 12,100 | 68,100 |
| 24,800 | 84,500 | 5,200 | 89,700 |
| 24,900 | 121,500 | 1,500 | 123,000 |
| 25,000 | 163,500 | 0 | 163,500 |

*Worked sample (settlement = 24,600):* calls in the money are 24,200–24,500, paying 25×400 + 30×300 + 45×200 + 55×100 = 33,500; puts in the money are 24,700–25,000, paying 48×100 + 32×200 + 22×300 + 15×400 = 23,800; total = 57,300.

**Max Pain = 24,600** — the settlement that minimises writer payout. Here it coincides with the spot, because OI is fairly balanced around the money; on real chains it often sits at a heavy-OI round strike *away* from spot. Remember the limitations (Section 3.7): this is a tendency for quiet expiries, not a prediction.

### Numerical Example 3 — Synthetic future

```
Synthetic future = ATM Call LTP − ATM Put LTP + ATM Strike
                 = 135 − 115 + 24,600 = 24,620
```

Matching the near-month future (≈24,620), confirming a small positive basis and that the chain is priced off the future, not the spot.

### Numerical Example 4 — Reading an OI change

The 25,000 call shows **Chg OI +35** (the chain's largest) with LTP just ₹22. Rising OI with a low, flat premium points to **fresh call writing** — big sellers reinforcing the 25,000 ceiling. Combined with put writing at 24,200 (Chg OI +18), the day's fresh positioning is **range-reinforcing**: writers are defending both 25,000 and 24,200.

---

## 6. Calculations (the reusable recipes)

**(a) Put–Call Ratio**

```
PCR(OI)     = Total Put OI     ÷ Total Call OI
PCR(Volume) = Total Put Volume ÷ Total Call Volume
```

**(b) Max Pain**

```
Total pain(S*) = Σ(K<S*) CallOI[K]·(S*−K) + Σ(K>S*) PutOI[K]·(K−S*)
Max Pain = argmin over S* of Total pain(S*)
```

**(c) Synthetic future (parity)**

```
Synthetic future = ATM Call LTP − ATM Put LTP + ATM Strike
```

**(d) Price + OI read (heuristic)**

```
Price ↑ & OI ↑ → long build-up (bullish)     Price ↑ & OI ↓ → short covering (bullish, temporary)
Price ↓ & OI ↑ → short build-up (bearish)     Price ↓ & OI ↓ → long unwinding (bearish, weakening)
Rising call OI → resistance;  Rising put OI → support
```

---

## 7. Practical Insights

* **OI is where the money sleeps; change in OI is where it moves.** Read the static OI for the walls (support/resistance) and the OI *change* for today's fresh positioning — the more forward-looking of the two.
* **Combine, never isolate.** Price alone, OI alone, or PCR alone will mislead you. The signal lives in the *combination*: price + OI change tells you build-up vs. covering; OI distribution + PCR tells you structure vs. sentiment.
* **Fade extremes, respect walls.** PCR is useful mainly at its extremes (contrarian), and the biggest OI strikes are the levels most worth marking on your chart.
* **Use Max Pain for quiet expiries only.** It is a settling tendency in range-bound weeks, not a trade trigger, and it evaporates on trending or event days.
* **Sanity-check with the synthetic future.** A quick `ATM CE − ATM PE + strike` confirms your chain is live and reminds you options price off the future.

> **Professional Insight — The chain is a positioning map, not a prediction.** Everything here tells you *where participants are committed and how strongly* — invaluable for judging where a move might stall, accelerate, or pin. None of it tells you *what will happen next*. Professionals use the chain to frame risk and locate levels, then let price action confirm; they never trade OI or PCR as a signal on its own.

---

## 8. Common Mistakes

* **Confusing OI with volume.** OI is standing open positions (carries over); volume is today's trading (resets daily). They answer different questions.
* **Reading OI without price/OI-change context.** High OI is a wall, but only the price and the OI *change* tell you whether it is being built (fresh conviction) or unwound (about to break).
* **Trading PCR as a standalone signal.** A single ratio hides the OI distribution; act on extremes and always cross-check *where* the OI sits.
* **Treating Max Pain as a prediction.** It is a quiet-expiry tendency, easily overrun by trends and events; using it as a target on a trending day is a classic trap.
* **Forgetting the chain prices off the future.** Comparing ATM call and put to the *spot* (rather than the future) makes you misread the small basis-driven asymmetry between them.
* **Chasing a breakout into a giant OI wall.** Buying far-OTM options straight into the largest call-OI strike is buying resistance.

---

## 9. Case Study — "Reading the Chain Before a Major Move"

**Context.** Three trading days before a sharp NIFTY fall (a representative pre-correction setup; figures **illustrative**), the chain was flashing warnings that price alone did not show. The index was drifting quietly near 24,600, and the news flow was calm — but the option chain was repositioning defensively.

**What the chain showed over the three days.**

1. **Put OI rising *with* rising put premiums at 24,500 and 24,400.** This is not put *writing* (which would show flat/falling premiums) — it is **long put build-up**: traders *buying* downside protection in size, willing to pay up for it. Price ↓-bias + put OI ↑ + put LTP ↑ together signal fresh bearish/hedging conviction.
2. **Call OI building at 24,600 and 24,700 with falling call premiums** — **call writing** just overhead, capping the upside and hardening resistance right above spot.
3. **PCR(OI) climbing from ~0.9 toward ~1.25** — the structural lean shifting toward puts, approaching (though not yet at) an extreme.
4. **The skew steepening** — OTM put IV rising faster than call IV, i.e., the market paying increasingly for crash protection. The insurance was getting expensive because demand for it was rising.

**What happened.** On the fourth day NIFTY gapped down and fell through 24,400. The long puts that had been accumulating paid off; the call writers overhead were never threatened; and the steepening skew that had warned of rising fear proved justified.

**The analysis.** No single signal was decisive, but *together* they painted a coherent picture: smart money was buying protection (put build-up), capping the upside (call writing), and bidding up crash insurance (skew) — all while the index sat quietly and the headlines were calm. The chain revealed positioning that price concealed.

**The essential caveat.** This reads cleanly *in hindsight*. In real time, the same signals appear before many moves that never come — protection is bought and never needed, PCR rises and the market grinds higher. These are **probabilistic tilts, not guarantees**, and the danger of case studies like this is hindsight bias: seeing an obvious signal after the fact that was one of several ambiguous readings before it. Use the chain to *raise your alertness and manage risk*, not to predict with false confidence.

*(Takeaway: the chain shows you where conviction is building before price confirms it — but treat those signals as a reason to tighten risk and watch closely, never as a certainty.)*

---

## 10. Chapter Summary

* The chain lays out calls (left) and puts (right) around each strike, with **LTP, volume, OI, change in OI, and IV** — and **OI is its most important column**.
* **Open Interest** is standing open contracts (it carries over); **volume** is today's trading (it resets) — do not confuse them.
* The **Price + OI matrix** decodes build-ups: rising OI with price = *fresh conviction* (long or short build-up); falling OI = *closing* (short covering or long unwinding), a weaker signal.
* **OI concentration** marks support (heavy put OI) and resistance (heavy call OI); in our chain, resistance at **25,000** and support at **24,200**.
* **Change in OI** is the leading edge — it shows today's fresh writing/buying; in our chain, writers reinforced both walls (range-reinforcing).
* **PCR** compresses the chain to one number (Put OI ÷ Call OI = **0.91** here); it is most useful at **extremes**, read contrarian, and must be paired with the OI distribution.
* **Max Pain** is the settlement minimising writer payout (**24,600** here); a *quiet-expiry tendency*, not a prediction — it fails on trends and events.
* The chain also reveals the **skew** (IV by strike) and yields the **synthetic future** (`ATM CE − ATM PE + strike = 24,620`), confirming options price off the future.

---

## 11. Key Takeaways

* **Read OI for the walls and change-in-OI for the flow** — where capital is parked, and where it is moving today.
* **Never isolate a signal.** Combine price, OI, OI change, PCR, skew, and the synthetic future; each alone misleads.
* **Fade PCR extremes, respect the biggest OI walls, and use Max Pain only for quiet expiries.**
* **The chain is a positioning map, not a prophecy** — use it to locate levels and manage risk, then let price confirm.

---

## 12. Practice Questions

**Q1 (Definition).** In one sentence each, distinguish Open Interest from volume.

**Q2 (Multiple choice).** A strike shows OI *rising* and its option's price *falling*. This most likely indicates:
(a) fresh buying; (b) fresh writing (selling); (c) short covering; (d) long unwinding.

**Q3 (Matrix).** Classify each: (a) price up, OI up; (b) price down, OI up; (c) price up, OI down; (d) price down, OI down.

**Q4 (Support/resistance).** From Table 7.1, name the strongest resistance and the strongest support strike, and justify each from the OI.

**Q5 (PCR).** Using Table 7.1, recompute PCR(OI) and state whether it signals an extreme.

**Q6 (Max Pain).** Using the sample calculation method, verify the total writer payout at a settlement of 24,500 for the chain in Table 7.1.

**Q7 (Synthetic future).** The ATM 24,600 call trades at ₹150 and the put at ₹120. Compute the synthetic future and state what the basis implies.

**Q8 (OI change).** The 25,000 call shows Chg OI +35 with LTP ₹22. What positioning does this suggest, and what does it mean for the 25,000 level?

**Q9 (PCR interpretation).** After a sharp market fall, PCR(OI) jumps to 1.5. Give the contrarian reading and one reason to be cautious about acting on it.

**Q10 (Judgement).** A trader sees Max Pain at 24,600 early in the week and shorts a straddle expecting the index to pin there by the Tuesday (NIFTY weekly) expiry. Give two reasons this may be a poor decision.

---

## 13. Detailed Solutions

**A1.** *Open Interest* is the number of option contracts currently open (outstanding), carried over day to day. *Volume* is the number of contracts traded today, which resets to zero each morning.

**A2.** **(b) fresh writing (selling).** Rising OI means new positions are opening; a falling price alongside points to sellers (writers) creating those new contracts — call writing marks resistance, put writing marks support.

**A3.** (a) **long build-up** (bullish); (b) **short build-up** (bearish); (c) **short covering** (bullish, often temporary); (d) **long unwinding** (bearish/weakening).

**A4.** **Strongest resistance = 25,000**, which has the largest call OI on the chain (130,000 lots) — a heavy wall of call writers overhead. **Strongest support = 24,200**, which has the largest put OI (95,000 lots) — a heavy wall of put writers below. The index at 24,600 sits inside this 24,200–25,000 band.

**A5.** PCR(OI) = 499 ÷ 550 = **0.91**. This is within the broadly neutral 0.8–1.1 range — **not an extreme** — so it gives no strong contrarian signal; the OI distribution is the more useful read here.

**A6.** Settlement 24,500: calls ITM are 24,200–24,400 → 25×300 + 30×200 + 45×100 = 7,500 + 6,000 + 4,500 = **18,000**; puts ITM are 24,600–25,000 → 72×100 + 48×200 + 32×300 + 22×400 + 15×500 = 7,200 + 9,600 + 9,600 + 8,800 + 7,500 = **42,700**; total pain = 18,000 + 42,700 = **60,700** (matching Table 7.4).

**A7.** Synthetic future = 150 − 120 + 24,600 = **24,720**. With spot at 24,600, the basis is +120 — a positive (contango) basis, meaning the future (and thus the chain) sits above spot, as expected in a normal-rate environment.

**A8.** Rising OI (+35, the chain's largest) with a low, flat premium indicates **fresh call writing** — large sellers opening positions at 25,000. It **hardens 25,000 as resistance**: those writers will hedge to defend the level, so a push toward it should meet supply.

**A9.** **Contrarian reading:** PCR at 1.5 signals *excessive fear* — the crowd is heavily in puts — which often precedes a bounce, so a contrarian looks to buy. **Caution:** a high PCR can also reflect a genuine, continuing downtrend (fear that is *justified*); PCR is blunt and can stay elevated as the market keeps falling, so it must be confirmed by price action and the OI distribution before acting.

**A10.** Two reasons: (i) **Max Pain is not a prediction** — it is a quiet-expiry tendency that fails on trending or event-driven weeks; shorting a straddle on it assumes a pin that may never form. (ii) **Max Pain shifts as OI changes** through the week, so an early-week 24,600 may migrate by the Tuesday expiry. (Also: a short straddle has large, open-ended risk if the index moves sharply away from the pin — the very scenario Max Pain does not protect against.)

---

## 14. Mini Glossary

* **Option chain** — the grid of all listed calls and puts by strike, with their prices, volume, OI, and IV. → this chapter.
* **LTP (Last Traded Price)** — the premium of the most recent trade at a strike. → this chapter.
* **Volume** — contracts traded today at a strike; resets daily. → this chapter.
* **Open Interest (OI)** — contracts currently open (outstanding) at a strike; carries over day to day. → this chapter.
* **Change in OI** — the day's net change in OI; positive = new positions opened, negative = positions closed. → this chapter.
* **Long build-up / short build-up** — fresh buying (price ↑, OI ↑) / fresh selling (price ↓, OI ↑). → this chapter.
* **Short covering / long unwinding** — sellers closing (price ↑, OI ↓) / buyers closing (price ↓, OI ↓). → this chapter.
* **Call writing / put writing** — selling calls (marks resistance) / selling puts (marks support), seen as rising OI with flat/falling premiums. → this chapter.
* **OI concentration** — the strikes with the largest OI; heavy call OI = resistance, heavy put OI = support. → this chapter.
* **Put–Call Ratio (PCR)** — total put OI (or volume) ÷ total call OI (or volume); most useful at extremes, read contrarian. → this chapter.
* **Max Pain** — the expiry settlement that minimises total payout to option holders (writers lose least); a quiet-expiry tendency, not a prediction. → this chapter.
* **Skew** — the variation of implied volatility across strikes (higher for lower strikes in equity indices). → this chapter.
* **Synthetic future** — the future implied by the chain: ATM call LTP − ATM put LTP + ATM strike. → this chapter.

---

<!-- End of Chapter 7 (Rev 2, current as of 4 Aug 2026). Rev 2 updates: NIFTY lot 75→65 (cosmetic only — all chain metrics are lot-independent); Q10 expiry day Thursday→Tuesday (NIFTY weekly, since 1 Sep 2025). One consistent chain (spot 24,600, F≈24,620) used throughout. PCR(OI)=499/550=0.91 verified. Max Pain full table verified (min 57,300 at 24,600). Synthetic future 135−115+24,600=24,620 verified. Q6 payout at 24,500 = 60,700 matches Table 7.4. No transaction costs, so Apr-2026 STT change not applicable. All OI/premium figures illustrative and flagged. IV = implied volatility. No forward chapter-number references; skew and synthetic future link back to Ch4/Ch6 only. -->
