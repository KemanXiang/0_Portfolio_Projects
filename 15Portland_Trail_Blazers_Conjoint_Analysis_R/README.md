# Portland Trail Blazers: Conjoint Analysis and Economic Decision-Making

**Research-style portfolio project | R · Conjoint Analysis · Willingness-to-Pay · Constrained Optimization · Sensitivity Analysis**

## Overview

How should a sports organization design multigame ticket packages when **consumer preference, willingness-to-pay, fulfillment costs, and commercial objectives do not align**?

This project uses a Portland Trail Blazers case workbook and six linked R Markdown analyses to translate aggregate conjoint part-worth utilities into feasible product alternatives and conditional economic comparisons. The workflow constructs preference scores, examines non-linear price trade-offs, enumerates constrained package designs, compares contribution objectives, identifies Pareto-efficient offers, and stress-tests the resulting decisions.

The contribution is **an integrated decision-analysis workflow**, not a causal evaluation, or forecast of observed ticket sales.

**Companion paper:** *Portland Trail Blazers — Conjoint Analysis and Economic Decision-Making: A Research-Style Portfolio Report* (see the project report PDF).

## Research Questions

1. Which ticket-package attributes and levels contribute most to modeled consumer preference?
2. How do discrete price responses affect willingness-to-pay (WTP) interpretations and attribute trade-offs?
3. Which packages remain feasible under seat-specific pricing policies, and how do consumer utility and contribution objectives conflict?
4. How robust are preferred packages and Pareto-efficient alternatives to utility perturbations and cost assumptions?

## Data and Analytical Scope

The primary input is the case Excel workbook, containing **16 part-worth levels across four attributes** and an associated cost schedule. The original workbook and case materials provide the research setting; the final R Markdown modules define the analytical transformations. CSV exports document intermediate and final results.

|Attribute|Levels|Decision role|
|---|---|---|
|Number of games|3, 6, 10|Package length|
|Ticket price|$15, $25, $35, $60 per seat per game|Consumer price and package revenue|
|Ticket location|300-level behind baskets; 300-level corners; 300-level midcourt; 200-level midcourt|Seat preference and fulfillment cost|
|Promotional item|Playoff priority; hot dog and soda; apparel; restaurant certificate; none|Incremental consumer value and promotional cost|

The full factorial design contains **240 hypothetical combinations**. Seat-specific minimum-price restrictions exclude 60, leaving **180 feasible packages**. These are enumerated design alternatives, **not observed customer purchases**.

## Analytical Workflow

|Module|Focus|Methods and outputs|
|---|---|---|
|01 — Data Input, Validation & EDA|Inspect and validate source assumptions|Input audit, attribute-level exploration, cost and price schedules|
|02 — Conjoint Utility & Importance|Construct modeled preference|Additive part-worth utility, attribute importance, level rankings, feasible-package utilities|
|03 — WTP & Attribute Trade-offs|Translate utility differences into conditional monetary comparisons|Discrete price slopes, local and piecewise WTP, promotion and seat-price trade-offs|
|04 — Package Design & Optimization|Evaluate feasible commercial offers|Full-factorial enumeration, pricing constraints, revenue, two contribution scenarios, Pareto frontiers|
|05 — Model Validation & Sensitivity|Test internal consistency and decision stability|Independent arithmetic checks, utility perturbations, cost stress tests, Pareto persistence|
|06 — Managerial Implications & Conclusions|Synthesize decision evidence|Objective-leader comparison, management shortlist, pilot recommendations, evidence inventory|

The R Markdown notebooks are the methodological record; the companion research report interprets the findings

## Main Findings

### 1. Seat location and price dominate modeled preference

|Attribute|Relative importance|
|---|---|
|Ticket location|39.49%|
|Ticket price|37.58%|
|Number of games|11.78%|
|Promotional item|11.15%|

Together, seat location and ticket price account for **77.07%** of relative attribute importance within the specified attribute levels. This is a *range-dependent conjoint measure*, not a percentage of explained sales or population-wide causal influence.

### 2. Price sensitivity is non-linear

|Price interval|Change in part-worth utility|Utility change per $1|
|---|---|---|
|$15 → $25|−0.43635|−0.043635|
|$25 → $35|−0.09411|−0.009411|
|$35 → $60|−1.12857|−0.045143|

The much smaller utility loss between $25 and $35 shows why a single constant price coefficient would obscure meaningful differences between reference intervals. **WTP calculations are local, model-implied monetary equivalents**, not observed payments or unconditional reservation prices.

### 3. The most preferred package is not the highest-contribution package

|Objective|Package|Configuration|Modeled utility|Conditional contribution|
|---|---|---|---|---|
|Maximum consumer utility|PKG077|6 games; $25/game; 300-level midcourt; hot dog and soda|0.79558|$38.75 (A); $22.50 (B)|
|Maximum contribution per package|PKG012|10 games; $60/game; 300-level behind baskets; playoff priority|−1.88555|$500 (A/B)|
|Exported maximum contribution per game|PKG011|6 games; $60/game; 300-level behind baskets; playoff priority|−1.36532|$50 per game (A/B)|

The contribution calculations **condition on a sale** and exclude demand response, fixed overhead, cannibalization, and seat-capacity opportunity costs. Consequently, maximizing contribution per sold package is not equivalent to maximizing expected profit.

### 4. Promotion economics depend on fulfillment frequency

For *g* games, per-game ticket price *p*, per-game seat cost *c_s*, and promotion cost *c_p*:

- **Revenue:** `g × p`
- **Scenario A — promotion once per package:** `g × (p − c_s) − c_p`
- **Scenario B — promotion once per game:** `g × (p − c_s − c_p)`

The source description of hot dog and soda **with each ticket** makes Scenario B especially relevant for literal fulfillment. Scenario A is retained as an alternative cost convention. Neither convention captures all potential opportunity costs.

### 5. A transparent shortlist is more useful than a single winner

|Package|Games|Price/game|Utility|Contribution A|Contribution B|
|---|---|---|---|---|---|
|PKG077|6|$25|0.79558|$38.75|$22.50|
|PKG029|6|$25|0.74641|$42.00|$42.00|
|PKG080|6|$35|0.70147|$98.75|$82.50|
|PKG032|6|$35|0.65230|$102.00|$102.00|

For example, replacing hot dog and soda with playoff priority in the $25 six-game offer (PKG029 versus PKG077) reduces modeled utility by **0.04917** but increases conditional contribution under both promotional cost conventions. Pareto analysis makes such trade-offs explicit rather than assigning an arbitrary weight to utility and dollars.

### 6. Robustness is conditional on the stress-test design

|Utility perturbation|Simulations|Baseline preference leader retained|
|---|---|---|
|±0.01|1,000|100.0%|
|±0.03|1,000|98.1%|
|±0.05|1,000|85.7%|

The study also evaluates **18 cost scenarios**. PKG012 remains the maximum-contribution-per-package leader in those scenarios, although Pareto-frontier membership changes. The simulation retention percentages are **not purchase probabilities or statistical confidence intervals**.

## Economic and Managerial Interpretation

The project connects **consumer valuation → price-equivalent trade-offs → cost accounting → constrained multiobjective choice**. In economic terms, it illustrates how relative preferences and marginal trade-offs interact with a provider's resource-allocation problem. It does **not** directly estimate consumer surplus, total welfare, market shares, or welfare-optimal allocation.

A defensible next commercial step would be a controlled test of six-game 300-level-midcourt packages, comparing promotional benefits and selected price points while collecting actual conversion, net revenue, fulfillment costs, incremental attendance, and cannibalization outcomes.

## Figures and Research Report

The project includes original figures covering part-worth structure, attribute importance, non-linear price utility, WTP comparisons, pricing feasibility, utility–contribution trade-offs, cost sensitivity, and ranking stability. The companion PDF paper selects and explains the most relevant figures. 

**Figure sequence for the paper:** attribute importance; price-utility curve; seat-price feasibility; utility–contribution Pareto plot; ranking stability; cost-sensitivity comparison.

## Reproducibility

1. Open the **case workbook** and confirm the attribute-level part-worths, seat costs, promotional costs, and pricing rules.
2. Run the **final R Markdown modules 01 through 06 in order**, using paths appropriate to the local repository.
3. Compare generated CSV outputs with the project exports, including feasible package counts, utility identities, objective leaders, and sensitivity summaries.
4. Use the report's evidence-traceability appendix to connect published figures and numerical claims to their primary output files.

An independent arithmetic reconciliation of the 180 feasible profiles found a maximum utility discrepancy of approximately **4.44 × 10⁻¹⁶** (floating-point precision) and zero discrepancy for reconstructed revenue and contribution identities. This supports **internal arithmetic consistency**, not independent validation of the original conjoint estimation or real-world demand.

## Limitations and Future Research

- **Aggregate inputs only:** respondent-level choices and preference heterogeneity are unavailable.
- **No observed market response:** cannot validate sales, conversion, market share, or expected profit.
- **Discrete price schedule:** WTP is sensitive to the reference interval and interpolation assumptions.
- **Simplified economics:** contribution omits overhead, capacity opportunity costs, and cannibalization.
- **Hypothetical sensitivity tests:** perturbation frequencies are not sampling-based uncertainty estimates.

Future work could estimate a respondent-level discrete-choice model with a no-purchase option, model heterogeneous preferences, validate predictions on held-out choices, and connect demand estimates to capacity-constrained revenue management and consumer-surplus analysis.

## Source and Attribution

This is an **independent portfolio analysis of Portland Trail Blazers case materials**. The case workbook and case materials provide the input setting; the R Markdown analyses, derived outputs, interpretations, and companion report document the portfolio workflow. Refer to the companion report for methodological discussion, references, and evidence traceability.

---

**Portfolio focus:** R programming · Marketing/Business Analytics · Conjoint preference modeling · WTP interpretation · Economic trade-offs · Pareto optimization · Reproducible research
