# Market Share Dynamics Under Brand Switching

## A Markov-Chain Simulation of Loyalty, Advertising, and Coupon Strategy

**Portfolio Project — MGT239 Simulation for Business**  
**Author:** Keman Xiang  
**Tools:** Microsoft Excel, stochastic simulation, Markov-chain modeling  
**Model Scale:** 10,000 customers | 52-week horizon

## Project Overview

This project examines **how customer loyalty and brand switching shape market share over time** and **how marketing interventions can alter both competitive position and profitability**. The analysis models a stylized regional market in which customers choose between **Coke and Pepsi** each week. Weekly purchase behavior is represented as a **two-state Markov process:** a customer's current brand determines the probability of remaining loyal or switching brands in the following week.

The project combines an analytical steady-state benchmark with two stochastic simulation implementations. A **macro simulation** models aggregate customer flows directly through binomial transitions, while a **micro simulation** generates weekly purchase paths for 10,000 individual customers and aggregates those paths into market shares. The model is then extended to evaluate two managerial interventions—advertising and periodic coupons—by changing transition probabilities and comparing the resulting annual profits.

The central analytical idea is that **market share is an intermediate outcome rather than the final business objective**. A marketing action may improve retention or attract competitor customers, but its value depends on whether the resulting dynamic profit gain exceeds the cost of creating that behavioral change.

## Business Questions

The project addresses four related questions:

1. **Baseline Market Dynamics:** How does Coke's market share evolve over a 52-week horizon under the baseline loyalty and switching probabilities?
2. **Initial-Share Sensitivity:** Do markets beginning at substantially different Coke shares converge toward the same long-run region when transition probabilities remain unchanged?
3. **Advertising Decision:** Does increasing Coke retention from 90% to 95% generate enough incremental profit to justify a $50,000 annual advertising cost?
4. **Coupon Promotion:** Does a periodic $0.25 coupon create sufficient switching toward Coke to compensate for the associated margin reduction?

## Theoretical Framework

The market is represented as a first-order Markov process with two states: Coke and Pepsi. The baseline transition matrix is:

|Current Brand|Next: Coke|Next: Pepsi|
|---|---:|---:|
|Coke|0.90|0.10|
|Pepsi|0.20|0.80|

If \(S_t\) denotes the market-share vector at week \(t\), the expected market evolution follows:
```
S(t+1) = S(t)P
```
A stationary market-share vector satisfies:
```
S* = S*P
```
For Coke, the equilibrium condition is:
```
s = 0.90s + 0.20(1 − s)
```
which gives a theoretical equilibrium Coke share of **66.67%**.

This equilibrium is determined by the transition probabilities rather than by the initial market share. The stochastic simulations add finite-market randomness around this analytical benchmark.

## Model Inputs

|Input|Workbook Value|Role in Model|
|---|---:|---|
|Market size|10,000 customers|Fixed customer population|
|Simulation horizon|52 weeks|One simulated year|
|Baseline Coke retention|90%|Probability a Coke customer remains with Coke|
|Baseline Pepsi retention|80%|Probability a Pepsi customer remains with Pepsi|
|Profit per Coke case|$1.00|Baseline contribution per purchase|
|Advertising Coke retention|95%|Retention after advertising|
|Advertising annual cost|$50,000|Deducted from advertising-strategy profit|
|Coupon discount|$0.25|Margin reduction during coupon weeks|
|Coupon-week Coke retention|95%|Coke loyalty during promotion|
|Coupon-week Pepsi retention|60%|Implies 40% Pepsi-to-Coke switching|

## Simulation Design

### Macro Simulation

The macro model tracks Coke and Pepsi customer counts directly. If \(C_t\) is the number of Coke customers at week \(t\), next week's Coke population is generated from two sources:

- existing Coke customers who remain loyal; and
- Pepsi customers who switch to Coke.

The workbook implements these transitions using stochastic binomial draws with `BINOM.INV()` and `RAND()`. Market share is then calculated by dividing simulated customer counts by the 10,000-customer market size.

This implementation provides a computationally compact representation of aggregate market movement.

### Micro Simulation

The micro model represents the same transition process from the individual-customer level. Each of the **10,000 rows represents one customer**, and weekly columns record that customer's brand state:

- `0 = Coke`
- `1 = Pepsi`

The next week's state is generated conditionally from the customer's current state using the appropriate transition probability. Individual paths are then aggregated into weekly Coke and Pepsi market shares.

The macro and micro implementations therefore model the same behavioral mechanism at different levels of granularity and provide an internal consistency check.

## Experimental Design

|Experiment|Question|Model Change|Analytical Purpose|
|---|---|---|---|
|Q1 — Baseline Market Dynamics|How does market share evolve under existing loyalty and switching?|Baseline transition matrix over 52 weeks|Establish the stochastic market-share path and compare it with theoretical equilibrium|
|Q2 — Initial-Share Sensitivity|Does the starting market position determine the long-run outcome?|Coke starts at 50%, 10%, or 90% share|Separate short-run path dependence from long-run convergence|
|Q3 — Advertising Decision|Is improved retention worth its cost?|Coke retention rises from 90% to 95%; $50,000 annual cost|Evaluate market-share improvement together with incremental profitability|
|Q4 — Coupon Promotion|Can periodic promotion profitably attract competitor customers?|$0.25 coupon; coupon-week transition matrix changes|Evaluate the trade-off between stronger switching toward Coke and lower promotional margin|

## Key Results

### 1. Baseline Convergence

The analytical baseline predicts a **66.67% Coke equilibrium share**.

In the final workbook realization:

|Model|Week 52 Coke Share|
|---|---:|
|Theoretical equilibrium|66.67%|
|Macro simulation|66.70%|
|Micro simulation|66.10%|

The two stochastic implementations converge near the theoretical benchmark despite being generated through different computational mechanisms and independent random draws. This provides an internal validation of the transition logic.

### 2. Initial-Share Sensitivity

The model was simulated from three substantially different initial Coke market shares.

|Initial Coke Share|Week 52 Coke Share|Absolute Gap from 66.67% Equilibrium|
|---|---:|---:|
|50%|66.70%|0.033%|
|10%|66.69%|0.023%|
|90%|66.75%|0.083%|

The early trajectories differ considerably, but all three scenarios finish close to the same equilibrium region. This illustrates an important distinction: **initial conditions affect the short-run path, while the transition matrix governs the long-run competitive structure**.

### 3. Advertising Strategy

Advertising changes Coke's retention probability from **90% to 95%**, while Pepsi retention remains at 80%.

The corresponding analytical stationary Coke share becomes:

**80%**

The higher retention probability therefore changes the market's long-run structure rather than simply producing a temporary demand increase.

### 4. Coupon Strategy

The coupon strategy offers a **$0.25 discount** according to the workbook's promotion schedule: **weeks 1, 6, 11, ..., 51**.

During coupon weeks, the transition matrix becomes:

|Current Brand|Next: Coke|Next: Pepsi|
|---|---:|---:|
|Coke|0.95|0.05|
|Pepsi|0.40|0.60|

Unlike advertising, the coupon strategy does not create one permanent transition matrix. Instead, the market alternates between baseline and promotion-week behavior, creating a **time-varying competitive system**.

## Profit Comparison

|Strategy|Annual Profit|Increment vs. Baseline|Increment (%)|
|---|---:|---:|---:|
|Baseline|$341,209.00|—|—|
|Advertising — after annual cost|$354,243.00|$13,034.00|3.82%|
|Coupon|$357,852.75|$16,643.75|4.88%|

In this workbook realization, both interventions generate annual profit above the baseline. Advertising produces an incremental gain of **$13,034**, while the coupon strategy produces an incremental gain of **$16,643.75**.

The comparison demonstrates why market-share lift alone is insufficient for managerial evaluation. Advertising incurs a fixed campaign cost, while coupons reduce contribution margin during promotion weeks. The relevant decision metric is therefore **incremental profit after intervention cost**, not market share in isolation.

## Managerial Interpretation

### Retention Creates Dynamic Value

A retention improvement affects more than one transaction. A customer retained this week enters the following week as a Coke customer and is again subject to Coke's retention probability. The effect therefore propagates through subsequent periods. This state dependence explains why relatively small changes in loyalty can produce meaningful long-run changes in market structure.

### Market Share Is an Intermediate Metric

The project distinguishes competitive outcomes from economic outcomes. Higher market share may be desirable, but it does not automatically imply higher profitability. Marketing programs should be evaluated by linking behavioral changes to their full economic consequences.

### Promotions Create Dynamic Trade-offs

Coupons simultaneously affect customer switching and unit margin. Their value depends on whether the customers attracted or retained through promotion create enough additional contribution to compensate for the discount. Because the intervention is periodic, its effect is better understood as a recurring dynamic process rather than as a new permanent equilibrium.

### Simulation Supports Scenario-Based Decision Making

The framework can be used as a transparent scenario engine. Managers can modify retention rates, switching probabilities, promotion timing, discount depth, and intervention cost, then observe how those assumptions propagate through market share and profit.

## Workbook Structure

|Worksheet|Purpose|
|---|---|
|`00_Project_Overview`|Portfolio-facing summary of the business problem, model, simulation design, implications, and limitations|
|`1_MarketShare_Macro`|Aggregate 52-week stochastic simulation, initial-share sensitivity, advertising, and coupon experiments|
|`1_MarketShare_Micro`|10,000-customer individual simulation and aggregation into weekly market shares|
|`01_Results_Interpretation`|Linked KPI summary, convergence results, strategy interpretation, and visual comparisons|

## Reproducibility Note

The workbook uses volatile Excel functions including `RAND()` and `BINOM.INV()`. Recalculating the workbook therefore generates a new stochastic realization.

The numerical values reported in this README correspond to the **final saved workbook realization** used in the accompanying portfolio report. Individual weekly values may change after recalculation, but the analytical focus is on structural patterns such as convergence, changes in equilibrium behavior, intervention effects, and profitability.

A natural extension would run many independent 52-week simulations and summarize the resulting distributions of annual profit and final market share using confidence intervals and downside-risk measures.

## Limitations and Future Extensions

The model intentionally simplifies the competitive environment to make the transition mechanism transparent. Key limitations include homogeneous customer behavior, a closed two-brand market, fixed baseline transition probabilities, assumed rather than empirically estimated intervention effects, and simplified contribution economics.

Future extensions could include:

- repeated Monte Carlo replications and confidence intervals;
- heterogeneous customer segments with different transition matrices;
- empirically estimated transition probabilities from customer-level transaction or panel data;
- seasonality and time-varying baseline behavior;
- competitor reactions and strategic interaction;
- alternative coupon timing and discount-depth optimization; and
- risk-adjusted comparison of marketing strategies rather than comparison of a single simulated realization.

## Project Deliverables

The portfolio project consists of:

- **Excel Simulation Workbook** — full macro and micro simulation models, scenario analysis, results, and charts.
- **Analytical Report** — research-style documentation of the business problem, theoretical framework, methodology, results, interpretation, managerial implications, and limitations.
- **README** — concise project documentation for GitHub and portfolio navigation.

## References

Bielza, C., Müller, P., & Ríos Insua, D. (1999). Decision analysis by augmented probability simulation. *Management Science, 45*(7), 995–1007.

Givon, M., & Horsky, D. (1994). Intertemporal aggregation of heterogeneous consumers. *European Journal of Operational Research, 76*(2), 273–282.

Grover, R., & Dillon, W. R. (1988). Understanding market characteristics from aggregated brand switching data by the method of spectral decomposition. *International Journal of Research in Marketing, 5*(2), 77–89.

Leong, T.-Y. (2007). Monte Carlo spreadsheet simulation using resampling. *INFORMS Transactions on Education, 7*(3), 188–198.

Van Horn, R. L. (1971). Validation of simulation results. *Management Science, 17*(5), 247–258.

---

**Keman Xiang PhD Application Portfolio**
