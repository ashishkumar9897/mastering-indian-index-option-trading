# AUTHOR STYLE GUIDE

## *Mastering Indian Index Option Trading* — Permanent Writing Rules (v1.0)

> **Status:** Binding. Every chapter, appendix, exercise, table, and diagram in this book must comply with this guide. Where a chapter draft conflicts with this guide, the guide wins and the draft is corrected. This document is the single source of truth for *how* the book is written; the `book_architecture.md` (Edition 2) is the single source of truth for *what* the book covers.
>
> **Companion documents:** `book_architecture.md` (structure, chapter scope, dependency map). Read both before writing any chapter.

---

## 0. HOW TO USE THIS GUIDE

1. Before drafting a chapter, read: (a) that chapter's entry in `book_architecture.md`, (b) Sections 1–4 and 7 of this guide.
2. While drafting, keep Section 5 (**The 10-Point Concept Framework**) open — it governs how *every* concept is presented.
3. Before submitting a chapter, run the **Consistency Checklist** (Section 18).
4. When in doubt about a term, number, or symbol, consult the canonical tables in Sections 2 and 3. Do not invent alternatives.

---

## 1. WRITING STYLE

### 1.1 Voice and person

* **Second person, active voice.** Address the reader as "you." Write "you sell the 24500 call," not "the trader sells the 24500 call" or "one sells."
* Use "we" only when walking through a calculation *together* ("Let's decompose this premium"). Never use "we" to mean the author's opinion — attribute opinions to evidence or to "professional traders."
* Present tense for mechanics and rules ("Theta decays faster near expiry"). Past tense only for case studies and history.

### 1.2 Tone

* **Plain, precise, and calm.** This is a teaching book, not a hype channel. Never promise profits. Never use "guaranteed," "sure-shot," "secret," "holy grail," or "get rich."
* Respect the reader's intelligence and their capital. Assume they are risking real money and treat every risk statement as if it were being read the night before a live trade.
* Confidence without arrogance. State what is known, flag what is uncertain, and label opinion as opinion.

### 1.3 Reading level and sentence craft

* Target an educated adult with **no finance background** (Parts I–IV) rising to an informed practitioner (Parts V–VIII).
* Average sentence length ≤ 22 words. Break any sentence over 35 words.
* One idea per paragraph. Paragraphs ≤ 5 sentences.
* Define every technical term on first use **in each chapter** (chapters are read out of order). Link to the Glossary.
* Prefer the concrete over the abstract: "loses ₹4 per day to time decay" beats "suffers temporal value erosion."

### 1.4 Jargon protocol

* Introduce jargon *after* the plain-English idea, never before. Pattern: **plain idea → name it → symbol/abbreviation.**
  * *Correct:* "The option loses value every day just because time passes. This daily bleed is called **Theta** (Θ)."
  * *Incorrect:* "Θ measures the first derivative of the option value with respect to time."
* After introduction, use the standard term consistently (see Section 2). Do not switch synonyms for variety.

### 1.5 Indian-first framing

* Every example, cost, rule, and case study is Indian by default: NSE/BSE, SEBI, SPAN, ₹, IST, Indian tax law, post-2024 reforms.
* Never import a US example (SPX, CBOE, OCC, US tax) except to explicitly contrast — and label it clearly as "in the US market, by contrast."
* Convert all foreign concepts to the Indian instrument before teaching them.

### 1.6 Spiral-learning callbacks

* When a concept was introduced earlier, say so and point back: "Recall the time value curve from Chapter 4." When it will deepen later, forward-reference: "We size this properly in Chapter 26."
* Use the exact chapter numbers from the architecture. Verify cross-references against `book_architecture.md` before submitting.

### 1.7 Inclusive, neutral language

* Use "they/them" for a generic trader whose gender is unspecified. Do not default to "he."
* No regional, gender, or class stereotypes in personas or case studies. Personas are defined by *trading behaviour and capital*, not identity.

### 1.8 Forbidden constructions (quick list)

* Tips/hype: "guaranteed," "secret," "easy money," "can't lose."
* False certainty about the future: "NIFTY will…," "this always works." Use probabilistic language: "tends to," "historically," "in most regimes."
* Undefined acronyms on first use.
* Clean payoffs that ignore costs (see Section 6.4).

---

## 2. TERMINOLOGY STANDARDS

### 2.1 Canonical instrument names (use exactly these)

| Concept | Canonical form | Do NOT write |
| --- | --- | --- |
| Nifty 50 index options | **NIFTY** | Nifty, nifty, NIFTY50, NF |
| Nifty Bank index options | **BANKNIFTY** | Bank Nifty, BankNifty, BNF, BANK NIFTY |
| Nifty Financial Services | **FINNIFTY** | Fin Nifty, FinNifty |
| Nifty Midcap Select | **MIDCPNIFTY** | Midcap Nifty, MidCpNifty |
| BSE Sensex options | **SENSEX** | Sensex30, SnP |
| Volatility index | **India VIX** | VIX (alone), IndiaVIX, india vix |

* On a chapter's *first* mention, you may give the full brand once: "the Nifty 50 index (traded as **NIFTY** options)." Thereafter use the canonical symbol only.

### 2.2 Option identifiers and moneyness

* **Call = CE, Put = PE** (NSE convention). Write "the 24500 CE (call)" on first use in a chapter, then "24500 CE."
* Full contract format: **`NIFTY 25JUL 24500 CE`** — index, expiry (DDMMM, uppercase), strike, right. Use this exact format in every worked example.
* Moneyness abbreviations: **ITM, ATM, OTM** (define once per chapter). Also permitted: "deep ITM," "deep OTM." Never "in-the-money" mid-sentence after first definition.
* Days to expiry: **DTE**. Zero-day: **0 DTE** (not "zero DTE," not "0DTE").

### 2.3 The Greeks (capitalization and naming)

* Capitalize the Greeks when named as risk measures: **Delta, Gamma, Theta, Vega, Rho**. Also **Vanna, Charm, Volga/Vomma**.
* "Vega" is retained as the standard name even though it is not a Greek letter; symbol **ν** (see Section 3).
* "Delta-neutral," "long Gamma," "short Vega," "position Delta" — hyphenate compound adjectives; capitalize the Greek.
* Lowercase only when using the word generically and non-technically (rare; avoid).

### 2.4 Volatility and chain terms

* **IV** = implied volatility, **HV** = historical (realized) volatility, **RV** may be used only if "realized volatility" is defined alongside HV; prefer **HV**.
* **IV Rank** and **IV Percentile** — capitalized as named metrics.
* **VRP** = variance risk premium (spell out first use).
* **OI** = open interest, **PCR** = put-call ratio (specify PCR(OI) or PCR(Volume)).
* **Max Pain** — two words, capitalized.
* **Skew, smile, term structure** — lowercase.

### 2.5 Market, regulatory, tax, and cost terms

* **SEBI, NSE, BSE, NSE Clearing, BSE Clearing** — as written.
* **SPAN margin, Exposure margin, Premium margin, Peak margin** — capitalize the first word as a named component.
* **STT, CTT, GST, SEBI turnover fee, stamp duty, brokerage** — the six cost components; STT is spelled out once ("Securities Transaction Tax (STT)").
* Tax: **F&O income**, **non-speculative business income**, **Section 44AB / 44AD / 44ADA**, **ITR-3**, **advance tax**. Use section numbers exactly.
* **Lot size, tick size, strike interval, contract note** — as written.

### 2.6 Money, numbers, and units (Indian conventions)

* **Currency symbol ₹** immediately before the figure, no space: ₹185, ₹1,20,000.
* **Indian digit grouping** in prose and tables: ₹1,00,000 (one lakh), ₹10,00,000 (ten lakh), ₹1,00,00,000 (one crore).
* Spell magnitudes with **lakh** and **crore** for readability in prose: "a ₹10 lakh account," "₹2,100 crore in turnover." In tables, digits are fine.
* Index **points** are unitless: "NIFTY rose 233 points," "a 200-point spread." Premiums are in ₹ per unit: "the 24500 CE at ₹185."
* Percentages: "12%" (no space). Change in rates: **basis points (bps)**, "a 25 bps cut."
* Dates: **absolute and unambiguous** — "on 1 February 2025," "the June 2024 expiry." Never "last year," "recently," "next week" in body text. In case studies, anchor to the real date.
* Time: 24-hour or "9:15 AM IST" style; always mark **IST** for session times.
* Ranges use en-dash: "10–15," "₹180–₹250." Negatives use a minus sign, not a hyphen: "−₹4.2."

### 2.7 One-term-one-meaning rule

* Each concept has exactly one canonical term (tables above). Do not rotate synonyms. If a common alternative exists, mention it once ("also called the *fear gauge*") and then use the canonical term only.

---

## 3. MATHEMATICAL NOTATION STANDARDS

### 3.1 Canonical symbols (use exactly; define on first chapter use)

| Symbol | Meaning | Unit / note |
| --- | --- | --- |
| S | Spot index level | points |
| F | Futures price of the index | points; **BSM inputs use F, not S** (see Ch 2, Ch 6) |
| K | Strike price | points |
| T | Time to expiry | **years** (e.g., 10 days = 10/365) |
| t | Elapsed time / calendar day | days where stated |
| σ (sigma) | Volatility (annualized) | decimal in formulas (0.13), shown as 13% in prose |
| r | Risk-free rate (annualized) | decimal; India: link to repo/T-bill |
| q | Dividend yield | decimal; usually small for index |
| C, P | Call price, Put price | ₹ per unit |
| N(·) | Standard normal CDF | — |
| n(·) | Standard normal PDF | — |
| d₁, d₂ | BSM auxiliary terms | dimensionless |
| Δ, Γ, Θ, ν, ρ | Delta, Gamma, Theta, Vega, Rho | see 3.3 |

* Do not use S and F interchangeably. When a formula legitimately uses the future, write F and say so.
* Introduce σ as "volatility (σ)" and always clarify **annualized** and **decimal vs percent** on first use.

### 3.2 Formula presentation rules

* Every formula is displayed on its own line, numbered if referenced later, e.g. **(6.1)**.
* Immediately below every formula, add a **one-line plain-English gloss** and a **units line**.
  * Example:
    * `C = S·N(d₁) − K·e^(−rT)·N(d₂)`   **(6.1)**
    * *In words:* today's fair call price is the expected payoff, discounted, weighted by risk-neutral probabilities.
    * *Units:* C, S, K in ₹/points; d₁, d₂ dimensionless.
* Use `·` for multiplication, `e^(x)` for the exponential, `ln` for natural log, `√` for square root, `Σ` for summation with limits stated.
* Show at least one **numeric substitution** for every formula introduced (see Section 6, and the "Math Made Simple" box in Section 7).
* Never present a formula without also giving its **trading meaning**. A formula the reader cannot act on does not belong in the body (move derivations to Appendix A).

### 3.3 Greek sign and unit conventions (enforce everywhere)

* **Delta (Δ):** calls 0→1, puts −1→0. Per 1-point move in the underlying.
* **Gamma (Γ):** change in Delta per 1-point move. Positive for long options.
* **Theta (Θ):** **per calendar day**, and **negative for long options / positive for short**. Always state the day convention.
* **Vega (ν):** premium change **per 1 percentage-point (1 vol point)** change in IV. Positive for long options.
* **Rho (ρ):** premium change per **1% (100 bps)** change in r.
* **Position Greek** = per-unit Greek × quantity × lot size × direction. Always distinguish "per-unit" from "position" Greeks; label which one a number is.
* Sign discipline: a short option's Theta is written **+₹4.2/day**, a long option's **−₹4.2/day**. Never drop the sign.

### 3.4 Approximation and rigor discipline

* Use ≈ for approximations and state the assumption ("ignoring second-order terms").
* When teaching "Delta ≈ probability of ITM," always add the risk-neutral caveat required by the architecture (Ch 8): it is a *risk-neutral* heuristic, not a real-world probability.
* Round money to the paisa only when it matters; otherwise to the rupee. Round Greeks to 2–4 significant figures and state the precision once.
* No calculus computation is required of the reader (see architecture, Section IX). Derivatives are explained as "rate of change"; full derivations live in Appendix A.

---

## 4. EXAMPLE STANDARDS

### 4.1 Every worked example must

1. Use a **named Indian instrument** and the full contract format (`NIFTY 25JUL 24500 CE`).
2. State the **market context**: spot/future level, IV or India VIX, DTE, and the date (real or clearly labelled "illustrative").
3. Use **realistic premiums and lot sizes** consistent with the stated context. Sanity-check that the premium ≈ intrinsic + plausible time value.
4. **Include all transaction costs** whenever P&L is computed (Section 6.4). A "gross" number may be shown only if the "net after costs" number appears beside it.
5. End with the **trading takeaway**, not just the number.

### 4.2 Real vs illustrative data

* Prefer **real historical data** for case studies and headline examples; cite the date and source ("NSE option chain, 1 Feb 2025").
* Where invented numbers are clearer for teaching, label the block **"Illustrative"** and keep the numbers internally consistent and realistic.
* Never mix a real date with impossible numbers (e.g., a premium that violates put-call parity for that day).

### 4.3 Standard reference scenario (use for continuity where possible)

To reduce cognitive load, reuse a **house baseline** unless a concept needs otherwise:

* NIFTY spot ≈ 24,600; ATM strike 24,600; India VIX ≈ 13; r = 6.5%; a weekly expiry with ~10 DTE; NIFTY lot size as per the current SEBI-notified value (state it explicitly each time, since it changes).
* Always **state the lot size in the example** rather than relying on the reader's memory — lot sizes are revised by SEBI/exchanges.

### 4.4 Consistency of the running numbers

* Within a chapter, keep spot, IV, and DTE constant across examples unless the point is to vary one. If you change a driver, say which one and hold the rest fixed ("holding spot and DTE constant, we raise IV from 13% to 16%").

---

## 5. THE 10-POINT CONCEPT FRAMEWORK (MANDATORY FOR EVERY CONCEPT)

> **This is the core rule of the book.** Every teachable concept — each Greek, each strategy, each volatility idea, each risk rule — is presented using all ten elements below, **in this order**. Minor sub-points may compress steps, but a *primary* concept must show all ten explicitly, each under a clear mini-heading or bolded lead-in.

**The ten elements:**

1. **What is it?** — A one- to two-sentence definition in plain English. Name it and give its symbol/abbreviation.
2. **Why does it exist?** — The economic or structural reason the concept exists (what problem it solves, what it measures, why the market needs it).
3. **Why should a trader care?** — The direct P&L or risk consequence. Answer "what does this cost me or make me?"
4. **Intuitive explanation** — An analogy or mental model with no math. Must be Indian-context-friendly and memorable.
5. **Real-world example** — A concrete Indian market instance (a named event, a real chain, a dated scenario). Qualitative is fine here.
6. **Numerical example** — A fully worked number using the house baseline or real data, including units and (for P&L) costs.
7. **Mathematical explanation** — The formula(s) with the Section 3 presentation rules: displayed, glossed, units, one substitution.
8. **Professional interpretation** — How a market maker, prop trader, or fund manager actually uses it; the nuance retail misses (this is the "Professional Insight" layer).
9. **Common mistake** — The specific retail error tied to this concept, why it happens, and how to avoid it (ties to the architecture's mistake tables).
10. **Practical takeaway** — One to three imperative sentences the reader can act on tomorrow. Bold the single most important line.

### 5.1 Formatting the framework in the text

* For a **major concept** (e.g., Theta, Iron Condor, IV Rank): render all ten as labelled beats, either as bold run-in headers or a numbered block.
* For a **secondary concept**: you may weave steps 4–7 into flowing prose, but steps 1, 3, 9, and 10 must remain explicit.
* Never reorder. The sequence (definition → purpose → stakes → intuition → real → numeric → math → pro → mistake → takeaway) is deliberate: it moves from "what" to "so what" to "now what."

### 5.2 Worked pattern (abbreviated model — Theta)

> Authors: this is the *shape* to imitate, condensed. A real chapter treatment is longer.

1. **What is it?** Theta (Θ) is the amount an option's premium falls per day, purely because one day has passed.
2. **Why does it exist?** An option is time-limited optionality; as expiry nears, there is less time for a favourable move, so the market pays less for it.
3. **Why should a trader care?** If you *buy* options, Theta is a daily headwind you must overcome; if you *sell*, it is your daily income.
4. **Intuitive explanation** Think of an option as an ice cube. Time is heat. It melts a little every day and melts fastest at the end.
5. **Real-world example** A NIFTY weekly ATM straddle bleeds most of its value from Wednesday to Thursday of expiry week.
6. **Numerical example** NIFTY 24600 CE, 10 DTE, ₹120 premium; Θ = −₹8/day → all else equal, tomorrow ≈ ₹112. (Position Θ for 1 lot = −₹8 × lot size; state the lot size.)
7. **Mathematical explanation** Show the BSM Theta formula per Section 3, gloss and units, one substitution.
8. **Professional interpretation** Sellers harvest Theta but are short Gamma; pros size Theta income against the Gamma risk it carries (the Gamma–Theta seesaw).
9. **Common mistake** "Being right on direction but losing money" — buyers ignore that Theta and IV crush can outrun a slow favourable move.
10. **Practical takeaway** **Never buy short-dated options on a slow thesis; if your edge is time, be the seller — and respect the Gamma you take on.**

---

## 6. NUMERICAL & P&L STANDARDS

### 6.1 Show your work

* Every numeric result shows the substitution, not just the answer: "P&L = (24,800 − 24,500) − 180 = ₹120 per unit; × lot size = …"
* Label per-unit vs per-lot vs position-level explicitly at each step.

### 6.2 Units and labels

* Every number carries its unit (₹, points, %, days, lots). No naked numbers in a P&L line.
* Breakevens, max profit, max loss, and margin are stated as a labelled block for every strategy (see Section 10).

### 6.3 Consistency with the Greeks

* When a P&L is estimated via Greeks, use the architecture's expansion: `ΔP ≈ Δ·ΔS + ½·Γ·(ΔS)² + Θ·Δt + ν·Δσ`, and say which terms you kept or dropped.

### 6.4 The all-in-cost rule (non-negotiable)

* Any P&L presented as a result must be shown **net of all six costs**: brokerage, STT, exchange transaction charges, GST, SEBI turnover fee, stamp duty.
* Because rates change, cost examples cite the **rate used and its as-of date**, and note "verify current rates with your broker." Keep a single costs reference (Ch 3 + Appendix C) and point back to it rather than re-listing rates everywhere.
* The "effective breakeven including costs" is shown at least once per strategy family.

---

## 7. RECURRING FEATURE BOXES (STANDARD SET)

Use only these named boxes (from the architecture, Section XI.A). Each has a fixed purpose, icon-label, and placement rule. Do not invent new box types.

| Box | Purpose | Frequency | Placement |
| --- | --- | --- | --- |
| **Market Note** | An India-specific nuance (SEBI rule, NSE feature, India VIX behaviour) | 2–3 / chapter | Beside the relevant concept |
| **Beginner Alert** | Plain re-explanation for absolute beginners | In chapters rated Level 3+ | Right after a hard passage |
| **Professional Insight** | Advanced nuance / desk practice | In chapters rated Level 2–3 (to add depth) | After the core concept |
| **Math Made Simple** | Step-by-step numeric walkthrough of a formula | Wherever a formula appears | Immediately below the formula |
| **Common Mistake** | A flagged retail error + fix | 1–2 / chapter | At the point of risk |

* **Length:** boxes are 40–120 words. A box that grows beyond 120 words becomes body text.
* **Self-containment:** a box must make sense if read alone (a browsing reader).
* The **Professional Insight** box is the home for the "Point 8" material when it is too deep for the main flow.

---

## 8. TABLE STANDARDS

### 8.1 Structure

* Every table has: a **number and caption** ("Table 10.2 — Theta by DTE for NIFTY ATM CE"), **column headers with units** ("Premium (₹)", "Θ (₹/day)"), and, for real data, a **source/date footnote**.
* Right-align numeric columns; left-align text columns. Currency and Greeks columns carry the unit in the header, not in every cell.
* Keep tables ≤ 7 columns for print legibility. If wider, split or move to an appendix.

### 8.2 Content rules

* Use Indian digit grouping (₹1,00,000) and the minus sign for negatives.
* Round consistently within a column (e.g., premiums to ₹, Greeks to 2 decimals).
* Every strategy chapter includes the **standard metrics table** (max profit, max loss, breakeven(s), net Greeks, margin) — same row order every time (Section 10.3).
* A table must be *referenced and interpreted* in the text ("As Table 10.2 shows, daily decay nearly triples in the last three days"). Never drop a table without discussion.

### 8.3 The sensitivity/decision tables

* Sign tables (e.g., the six-factor sensitivity matrix) use **+ / − / 0** and a legend. Directional-only tables never imply magnitude unless a magnitude column is present.

---

## 9. DIAGRAM STANDARDS

### 9.1 Payoff diagrams (the book's signature visual)

* **Axes:** x-axis = underlying level at expiry (points); y-axis = P&L (₹). Label both with units. Zero-P&L line drawn and labelled.
* Mark and label: **breakeven(s), max profit, max loss, current spot, and short/long strikes.**
* Show the **at-expiry** payoff as a solid line; show a **before-expiry** (T+0/T−n) curve as a dashed line when the concept needs it.
* Shade profit region and loss region distinctly. Costs: state whether the payoff is gross or net; if net, note it in the caption.

### 9.2 Greek and volatility charts

* One idea per chart. Title states the variable and what is held constant ("Gamma vs. DTE, ATM, spot fixed").
* Time-decay and Gamma-explosion charts use real DTE steps (e.g., 30/20/10/5/3/1/0).
* Volatility charts (VIX history, skew, term structure) annotate the **events** that matter (COVID, budget, election), with dates.

### 9.3 Accessibility and consistency

* **Do not rely on colour alone.** Distinguish series by line style/markers *and* colour, and label directly on the line where possible.
* Use one consistent visual system across the whole book: same palette, same line weights, same font in labels. (If a design system/palette is provided later, use it; until then, keep a single documented palette and reuse it.)
* Every figure has a **number, caption, and an in-text reference** ("see Figure 17.3"). Captions state the takeaway, not just the contents.
* Screenshots (option chain, order screens) are **annotated** with callouts and are generic/representative; blur or omit broker-identifying and personal data.

### 9.4 Diagram inventory discipline

* Track figures against the architecture's Visual Elements Budget (Section XI.B). Do not exceed a chapter's fair share without reason; do not under-illustrate a Level 3+ chapter.

---

## 10. CHAPTER STRUCTURE (STANDARD TEMPLATE)

Every chapter follows this fixed skeleton. Section names are consistent across the book so readers build a habit.

1. **Chapter number and title** (exactly as in the architecture).
2. **Opening hook** (150–300 words): a concrete Indian scenario, question, or loss/win that motivates the chapter. No definitions yet.
3. **Learning Objectives** (verbatim from the architecture, lightly editable for tense): "By the end of this chapter, you will be able to…"
4. **Body — concept by concept**, each concept using the **10-Point Framework** (Section 5), sequenced per the architecture's Key Concepts order.
5. **Required Examples** integrated into the body (per architecture) — not bolted on at the end.
6. **Key Formulas** recap block (if the chapter has formulas) — each with a **Math Made Simple** treatment.
7. **Common Mistakes** — at least the ones mapped to this chapter in architecture Section VI.
8. **Case Study** (Section 12 format) — the one(s) named in the architecture.
9. **Chapter Summary** — 5–7 bullet takeaways (mirrors architecture Section XI.A #6).
10. **"Your Turn" Exercises** (Section 11 format).
11. **Chapter Quiz** — 10 MCQs (answers in a consolidated answer key, not inline).
12. **What's Next** — 2–3 sentences bridging to the next chapter (spiral-learning forward link).

### 10.1 Difficulty labelling

* Each chapter opens (in front-matter metadata, not the reader-facing hook) with its **Difficulty Level (1–5)** from the architecture. Level 3+ chapters must contain at least one **Beginner Alert** box; Level 1–2 chapters must contain at least one **Professional Insight** box. This keeps every chapter useful across the skill range.

### 10.2 Dependency honouring

* Do not use a concept the reader has not met per the dependency map. If you need it, either move it or add a brief, flagged primer with a back-reference. Verify against `book_architecture.md` Section III.

### 10.3 Standard strategy template (Part V and any strategy)

Every strategy is taught with this fixed sub-structure (extends the 10-Point Framework):

* **Setup** (legs, with the full contract format for each leg)
* **Entry Criteria** (directional view, IV regime via IV Rank, DTE, account size fit)
* **Greeks Profile** (net Delta/Gamma/Theta/Vega, with signs)
* **Risk/Reward block** (max profit, max loss, breakeven(s), margin, probability-of-profit heuristic)
* **Payoff Diagram** (Section 9.1)
* **Adjustment Rules** (pre-defined triggers)
* **Exit Rules** (profit target, stop, time stop)
* **Indian Market Considerations** (liquidity of the chosen strikes/index, expiry structure, SEBI margin, cost drag)
* **Worked Example** with real/house numbers, net of costs
* **Common Mistake** + **Practical Takeaway**

---

## 11. EXERCISE STRUCTURE ("YOUR TURN")

* Exercises are drawn from / consistent with the architecture's "Practical Exercises" for that chapter.
* Each exercise states: **the task, the data source (live NSE chain, broker tool, spreadsheet), and the deliverable** (a number, a chart, a paper trade log).
* Grade of difficulty tag per exercise: **[Observe] / [Calculate] / [Paper Trade] / [Build]**.
* Every chapter has **at least one hands-on market exercise** (open the real chain / broker tool) and **at least one calculation exercise**.
* Exercises must be **doable with free/retail tools** (NSE website, broker calculator, Opstra/Sensibull free tier, a spreadsheet). If a paid tool helps, mark it **optional**.
* Provide **worked solutions or solution guidance** in a consolidated end-of-book/appendix section, not inline (so readers attempt first). MCQ quiz answers likewise consolidated.
* No exercise may instruct real-money trading before the roadmap stage that permits it (architecture Section IV): live trading only from Stage 5 onward; earlier chapters say "paper trade."

---

## 12. CASE STUDY STRUCTURE

Every case study uses this fixed arc:

1. **Title** (evocative, as in the architecture: e.g., "The Expiry Day Gamma Trap").
2. **Context** — date/event, instrument, market regime (spot, India VIX, DTE). Real and dated where possible.
3. **The Setup** — what position/decision was in play.
4. **What Happened** — the sequence, with **numbers and, where relevant, a timeline or minute-by-minute/premium snapshots**.
5. **The Analysis** — decompose *why* using the Greeks/volatility/risk tools already taught. Attribute P&L to Delta/Gamma/Theta/Vega where possible.
6. **The Lesson** — the rule(s) that would have changed the outcome; link to the relevant Common Mistake and chapter(s).
7. **Takeaway box** — one actionable line.

Rules:
* **Anonymize** individuals ("a Pune-based trader," never a real name). Do not defame identifiable persons or firms.
* Distinguish **real** events (dated, sourced) from **composite/illustrative** ones (label "composite, based on typical outcomes").
* Numbers must be internally consistent and net of costs where P&L is claimed.
* A case study must *teach a concept already introduced* in that chapter or earlier — never introduce brand-new theory inside a case study.

---

## 13. RISK-MANAGEMENT DISCUSSION STANDARDS

Risk is the book's spine (architecture Sections V, VII, X). Apply these rules **everywhere risk appears, in every chapter — not only Part VII.**

1. **Risk before reward.** When a strategy or trade is introduced, state the **maximum loss and how it can occur** before dwelling on the profit. Order: risk → reward.
2. **Name the risk domain.** Tag each risk as trade-level, strategy-level, portfolio-level, tail, operational, or psychological (architecture Section X taxonomy).
3. **Undefined-risk warning.** Any naked/short-unlimited position carries an explicit, boxed warning stating that losses can exceed premium and margin, with the Indian margin/penalty context.
4. **Position sizing is mandatory in P&L examples.** Whenever a trade is sized, tie the size to a risk rule (e.g., "risking ≤ 2% of a ₹10 lakh account"). Never show lots chosen arbitrarily.
5. **Tail and gap risk.** For overnight/event positions, always mention gap risk and the possibility of 3σ–6σ moves; reference the stress-test habit (±5%, ±10%, VIX doubling).
6. **Stop discipline.** State the stop type (premium-, underlying-, Greek-, or time-based) and why mental stops fail.
7. **No survivorship storytelling.** Do not present a winning trade as proof of a method without the base-rate/risk context. Cite the SEBI finding on retail F&O losses where relevant (architecture Ch 30) to keep expectations honest.
8. **Consistent risk vocabulary.** Use max loss, drawdown, VaR/CVaR, portfolio heat, risk of ruin exactly as defined in Ch 25–26; do not coin new terms.

---

## 14. GLOSSARY STANDARDS

* The Glossary is organized by the **nine categories** in the architecture (Section VII); ~170 terms total. Each term lives in exactly one category.
* **Entry format:** **Term** (abbreviation, symbol) — one-sentence plain definition — optional second sentence of nuance/Indian context — cross-reference to the chapter where it is taught ("→ Ch 10").
  * Example: **Theta (Θ)** — the daily fall in an option's premium due to the passage of time; negative for long options, positive for short. → Ch 10.
* Definitions must **match the in-text first-use definition** exactly in meaning (no drift). If a term is redefined, update both places.
* Glossary terms appear in **bold at first use** in each chapter and are the canonical terms from Section 2.
* No circular definitions (a term defined only by another undefined term). Keep entries ≤ 40 words.
* Include the abbreviation/symbol so the Glossary doubles as a notation index; keep it consistent with Section 3.

---

## 15. CROSS-REFERENCING & CONSISTENCY RULES

* Reference chapters by number and short title on first cross-reference in a chapter ("Chapter 14, IV vs. HV"), then by number.
* Verify every cross-reference against `book_architecture.md` before submission. A wrong chapter pointer is a defect.
* Keep the **running numbers** (house baseline, lot sizes, VIX levels) consistent within a chapter and plausible across the book.
* When the architecture and a draft disagree on scope, the architecture wins; when this guide and a draft disagree on style, this guide wins.

---

## 16. REGULATORY, LEGAL & ETHICAL GUARDRAILS

* **No investment advice.** The book educates; it does not recommend specific trades to specific readers. Use "you might consider," "a common approach is," never "you should buy X now."
* **No performance promises.** Never state or imply guaranteed or typical returns.
* **Time-sensitive facts are dated.** Rates (STT, margins), lot sizes, and rules change; every such figure carries an as-of date and a "verify current rules" note, and points to the single reference location.
* **Standard risk disclaimer** appears in the front matter and is referenced (not repeated in full) where naked risk is discussed.
* **Sources.** Real data and studies (e.g., the SEBI retail-loss study) are cited with date. Do not fabricate statistics; if a number is illustrative, say so.
* **Respect privacy and reputation** in case studies (Section 12 anonymization).

---

## 17. FILE, FORMATTING & HOUSE MECHANICS

* Markdown for drafts; one file per chapter, named `ch03_trading_infrastructure.md` (zero-padded number + short slug).
* Headings: `#` chapter title, `##` major sections, `###` concepts. Do not skip levels.
* Bold for **key terms on first use** and for the single **Practical Takeaway** line. Italics for *emphasis* and *labels* ("Illustrative"). Avoid ALL-CAPS except canonical symbols (NIFTY, STT).
* Lists for steps and enumerations; prose for explanation. Don't bullet everything.
* Spelling: **Indian/British English** (organise, colour, behaviour) — but keep proper nouns and NSE terms as branded.
* Oxford comma: use it.
* One space after periods. En-dash for ranges, em-dash — like this — for asides.

---

## 18. PRE-SUBMISSION CONSISTENCY CHECKLIST

Run this on every chapter before it is considered done:

**Scope & structure**
- [ ] Chapter matches its architecture entry (objectives, key concepts, examples, case study, word count band).
- [ ] Standard chapter skeleton present (hook → objectives → body → summary → exercises → quiz → what's next).
- [ ] Difficulty level honoured (Beginner Alert if Level 3+; Professional Insight if Level 1–2).
- [ ] No concept used before its dependency (checked against the dependency map).

**Concept treatment**
- [ ] Every primary concept uses all 10 framework points, in order.
- [ ] Steps 1, 3, 9, 10 explicit even for secondary concepts.

**Terminology & numbers**
- [ ] Canonical instrument, Greek, and cost terms used consistently (Section 2).
- [ ] ₹ symbol, Indian digit grouping, lakh/crore, bps, absolute dates, IST all correct.
- [ ] Lot size stated explicitly in every sized example.

**Math**
- [ ] Symbols per Section 3; formulas displayed, glossed, unit-lined, with one substitution.
- [ ] Greek signs and day/vol-point conventions correct.
- [ ] Risk-neutral caveat present wherever "Delta ≈ probability" appears.

**Examples & P&L**
- [ ] Real/Illustrative labelled; context (spot, IV, DTE, date) stated.
- [ ] All P&L results net of the six costs, with rate as-of date.

**Visuals & tables**
- [ ] Every figure/table numbered, captioned (with takeaway), unit-headed, and discussed in text.
- [ ] Payoff diagrams mark breakeven/max profit/max loss/strikes; not colour-dependent.

**Risk & compliance**
- [ ] Risk stated before reward; undefined-risk warning boxed where relevant.
- [ ] No advice/promise language; disclaimers and dated facts handled per Section 16.
- [ ] Case studies anonymized; real vs composite labelled.

**Polish**
- [ ] Cross-references verified against the architecture.
- [ ] Glossary terms bolded at first use and defined consistently.
- [ ] Spelling (Indian/British), Oxford comma, dashes, forbidden constructions (Section 1.8) checked.

---

*End of Author Style Guide v1.0. Update this document — with a version bump and a dated changelog line — whenever a house standard changes, and re-verify affected chapters against the change.*

### Changelog
* **v1.0** — Initial release, aligned to `book_architecture.md` Edition 2.
