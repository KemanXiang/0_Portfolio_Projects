# Healthcare Infectious Disease Simulation

**A Monte Carlo Analysis of Protection, Population Survival, and Economic Preservation**

This project develops an Excel-based stochastic dynamic simulation to evaluate the **spread of an infectious disease in a closed village** and compare two policy scenarios: **no protection** and **universal use of an infection-protection measure**. The model follows **susceptible, infected, and deceased residents** over 100 periods and uses **1,000 Monte Carlo replications** to estimate population survival, disease extinction, cumulative infection, and economic outcomes.

## Project Overview

A remote village begins with 100 residents: 95 susceptible and 5 infected. Each infected resident has a **10% probability of dying per period** and encounters a particular susceptible with probability **5%**. Conditional on an encounter, infection occurs with probability **50% without protection** and **10% with protection**. Each living resident contributes **$10,000 in tax revenue per period**.

The analysis asks whether reducing transmission changes population survival, disease extinction, cumulative infection, and the economic value associated with preserving the living population.

## Research Questions

1. What is the probability that the entire population dies out by period 100?
2. What is the probability that the disease dies out by period 100?
3. What percentage of the original population has been infected by the end of the simulation?
4. How do these outcomes change under universal protection?
5. How does protection affect cumulative tax revenue over the 100-period horizon?

## Modeling Framework

The model tracks three state variables:

- **Sₜ** — susceptible population in period *t*
- **Iₜ** — infected population in period *t*
- **Dₜ** — cumulative deaths through period *t*

The initial state is **S₁ = 95, I₁ = 5, D₁ = 0**, with:

**Sₜ + Iₜ + Dₜ = 100**

### Transmission Without Protection

For one infected–susceptible pair, the per-period transmission probability is:

**0.05 × 0.50 = 0.025**

With *Iₜ* infected residents, the probability that a particular susceptible avoids infection is: 

**qₜ = (1 − 0.05 × 0.50)^Iₜ = 0.975^Iₜ**

and:

**Sₜ₊₁ ~ Binomial(Sₜ, qₜ)**

### Transmission With Protection

Protection leaves encounter probability unchanged but reduces conditional infection probability from 0.50 to 0.10:

**0.05 × 0.10 = 0.005**

Therefore:

**qₜᴾ = (1 − 0.05 × 0.10)^Iₜ = 0.995^Iₜ**

Each infected resident survives a period with probability **0.90**. The next infected population combines surviving infectives with newly infected residents.

## Simulation Design

The Excel model follows a five-stage workflow:

1. Define the initial state and stochastic parameters.
2. Generate a 100-period sample path without protection.
3. Generate a parallel 100-period sample path with protection.
4. Replicate each stochastic model across **1,000 simulated villages** using Excel Data Tables.
5. Estimate probabilities, means, **95% confidence intervals**, scenario differences, and Monte Carlo convergence.

A single sample path represents only one possible realization. Policy conclusions are therefore based on the distribution across all simulated villages.

## Key Results

|Outcome|No Protection|Protection|Change|
|---|---:|---:|---:|
|Population die-out probability|99.3%|56.0%|−43.3 percentage points|
|Disease die-out probability|99.3%|99.6%|+0.3 percentage points|
|Average cumulative infection rate|100.0%|99.352%|−0.648 percentage points|
|Average cumulative tax revenue|$12.610M|$17.141M|+$4.531M|

### 95% Confidence Intervals

|Outcome|No Protection 95% CI|Protection 95% CI|
|---|---:|---:|
|Population die-out probability|98.783%–99.817%|52.922%–59.078%|
|Disease die-out probability|98.783%–99.817%|99.209%–99.991%|
|Average cumulative infection rate|100.000%–100.000%|99.293%–99.411%|
|Average cumulative tax revenue|$12.549M–$12.670M|$17.054M–$17.228M|

## Results and Interpretation

### Population Survival

Protection produces the largest difference in **complete population die-out**. Without protection, 99.3% of simulated villages experience complete population loss by period 100. Under protection, this probability falls to 56.0%, a reduction of **43.3 percentage points**.

Protection therefore substantially reduces catastrophic population risk, although it does not eliminate it.

### Disease Extinction Is Not the Same as Population Survival

Disease extinction is estimated at 99.3% without protection and 99.6% with protection. Viewed alone, this metric could make the two scenarios appear almost equivalent.

However, disease extinction is a terminal-state measure. A village can reach zero infected residents after relatively limited damage or only after extensive mortality. The large difference in population survival shows why the **path of the stochastic process matters**, not only its terminal disease status.

### Cumulative Infection

Average cumulative infection is **100.0% without protection** and **99.352% with protection**. Infection therefore remains nearly universal over the 100-period horizon.

Within this model, the principal benefit of protection is not complete avoidance of infection. Instead, lower transmission alters the timing and evolution of the epidemic sufficiently to preserve more residents for longer.

### Economic Impact

Average cumulative tax revenue increases from approximately **$12.610 million** without protection to **$17.141 million** with protection.

The difference is approximately **$4.531 million per simulated village**, equivalent to a **35.9% increase** relative to the no-protection scenario.

This economic effect arises because more residents remain alive and contribute tax revenue for more periods. It represents **gross tax-base preservation**, not net economic benefit, because intervention costs are not included.

## Monte Carlo Convergence

Running estimates were evaluated at progressively larger simulation samples.

|Simulated Villages|Population Die-Out: No Protection|Population Die-Out: Protection|Tax: No Protection ($M)|Tax: Protection ($M)|
|---:|---:|---:|---:|---:|
|50|100.0%|58.0%|12.727|16.862|
|100|99.0%|56.0%|12.548|16.965|
|250|98.8%|58.0%|12.586|16.929|
|500|99.0%|55.8%|12.608|17.116|
|750|99.2%|55.6%|12.610|17.112|
|1,000|99.3%|56.0%|12.610|17.141|

The estimates become increasingly stable as the number of simulated villages approaches 1,000. The final scenario differences remain large relative to late-stage Monte Carlo variation.

## Managerial and Analytical Implications

**Evaluate the full path, not only the endpoint.** Disease extinction is nearly identical across scenarios, while population survival and cumulative economic output differ substantially.

**Dynamic feedback can amplify an intervention.** Reducing infection in one period changes the number of future infectives, which changes subsequent transmission risk. Simulation captures this recursive mechanism.

**Connect operational outcomes to decision-relevant measures.** Translating population preservation into cumulative tax revenue illustrates how a health intervention can create indirect economic consequences through preservation of the underlying population.

**Report uncertainty explicitly.** The project combines point estimates with 95% confidence intervals and convergence diagnostics rather than treating stochastic simulation outputs as deterministic values.

**Gross benefit is not net benefit.** A complete policy decision would also require the cost of protection and potentially broader health, productivity, and welfare effects.

## Limitations

This is a stylized stochastic decision model rather than an epidemiological forecast. It assumes homogeneous residents, fixed encounter and transmission probabilities, constant mortality risk, no recovery or immunity state, no births or migration, universal protection, and no behavioral adaptation.

The economic calculation includes gross cumulative tax revenue but excludes intervention cost, healthcare expenditure, productivity loss, income heterogeneity, and discounting.

The confidence intervals quantify **Monte Carlo sampling uncertainty conditional on the specified model inputs**. They do not measure uncertainty about whether those parameter values accurately describe a real population.

## Potential Extensions

- Sensitivity analysis for transmission, encounter, and mortality probabilities
- Partial protection adoption and compliance
- Explicit recovery or immunity states
- Heterogeneous residents or contact networks
- Intervention costs and net-benefit analysis
- Discounting of future economic outcomes
- Time-to-extinction distributions
- Alternative initial infection levels

## Workbook Structure

|Worksheet|Purpose|
|---|---|
|`00_Project_Overview`|Problem, model, simulation design, implications, and limitations|
|`1Healthcare`|Stochastic calculation engine, sample paths, Monte Carlo tables, outputs, and calculation documentation|
|`02_Results_Dashboard`|Scenario comparison, confidence intervals, visualizations, and interpretation|
|`03_Convergence`|Running-estimate diagnostics for Monte Carlo stability|
|`04_Documentation`|Assumptions, variable definitions, economic units, and workbook documentation|

## Skills Demonstrated

- Stochastic dynamic modeling
- Monte Carlo simulation
- Binomial random-variable modeling
- Excel `RAND()` and `BINOM.INV()`
- Excel Data Tables
- Scenario and policy analysis
- 95% confidence intervals
- Simulation convergence analysis
- Dynamic state-transition modeling
- Economic impact interpretation
- Model documentation and reproducibility
- Decision analytics

## Repository Files

|File|Description|
|---|---|
|`Healthcare_Infectious_Disease_Simulation_Portfolio_Formatted.xlsx`|Complete Excel simulation model and portfolio workbook|
|`Healthcare_Infectious_Disease_Simulation_Report.docx`|Research-style report covering methodology, results, visualizations, interpretation, implications, and limitations|

## Reproducibility Note

The simulation uses Excel's **RAND()** function. Recalculating the workbook can therefore generate a new Monte Carlo sample and slightly different numerical estimates.

The results reported here correspond to the final **1,000-village simulation run used in the portfolio workbook and accompanying report**. The model structure, assumptions, and analytical workflow remain unchanged across recalculations.

## Project Context

This project was developed from **MGT239 Simulation for Business** Course and demonstrates an end-to-end simulation workflow: translating a decision problem into state variables and probabilistic transitions, implementing stochastic dynamics in Excel, evaluating repeated Monte Carlo outcomes, quantifying uncertainty, diagnosing convergence, and translating results into managerial and economic interpretation.
