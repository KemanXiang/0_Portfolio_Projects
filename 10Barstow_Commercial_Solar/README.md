# Commercial Solar PV + Battery Energy Storage — Barstow, California

## Project Overview

This project evaluates a c**ommercial** behind-the-meter **solar photovoltaic
(PV)** and **battery energy storage system (ESS)** for two utility accounts in
**Barstow, California**. The analysis integrates historical electricity
consumption, time-of-use (TOU) usage, demand-charge exposure, PV
production, battery sizing, scenario comparison, electricity-cost
savings, and long-term financial performance.

The project was developed as an applied **commercial decision-support
workflow**. **Utility billing data** establish the operating baseline;
**technical modeling** translates the load profile into PV and ESS
requirements; **tariff and demand-charge analysis** identifies potential
savings; and **financial modeling** connects the recommended system
configuration to investment outcomes.

## Key Project Results

|Metric|Result|
|---|---|
|Historical annual electricity consumption|709,501 kWh|
|Analyzed utility accounts|2|
|Recommended PV panel count|838|
|PV module rating|485 W|
|Recommended PV capacity|406.43 kW DC|
|Modeled annual PV generation|710,207.5 kWh|
|Annual PV generation coverage|100.10%|
|ESS configuration|2 × 215.04 kWh sizing units|
|Nominal ESS energy|430.08 kWh|
|Estimated AC PCS capacity|200 kW|
|Proposal demand-shave target|100 kW|
|Historical annual electricity bill|\$286,732.11|
|Modeled Year-1 savings|\$106,305.62|
|Modeled new annual electricity bill|\$180,426.49|
|Gross project cost|\$1,074,972.30|
|Modeled net economic cost after tax benefits/incentives|\$392,364.89|
|30-year electricity-bill savings|\$4,694,064|
|IRR|21.5%|
|NPV|\$1,757,719|
|Simple payback|3.9 years|

## Analytical Workflow

The project follows a linked technical and business-analysis process:

1.  **Historical utility analysis** — Analyze 12 billing cycles across
    two utility accounts and establish the annual electricity baseline.
2.  **TOU and demand analysis** — Examine energy-use categories, demand
    indicators, energy charges, demand charges, and other bill
    components.
3.  **PV sizing** — Scale the modeled PV production profile using 485-W
    modules and identify the minimum configuration meeting the
    annual-generation constraint.
4.  **ESS sizing** — Evaluate storage requirements using peak-window
    energy, battery usable-energy assumptions, battery-side power
    capability, and a fixed 100-kW demand-shave target.
5.  **Scenario comparison** — Compare alternative PV/ESS configurations
    on system size, constraint compliance, installed cost, and modeled
    economic performance.
6.  **Electricity-bill analysis** — Estimate PV energy savings,
    demand-charge savings, PV export value, and grid-charging arbitrage.
7.  **Financial analysis** — Evaluate capital cost, modeled incentives
    and tax benefits, long-term cash flows, NPV, IRR, payback, and
    cumulative electricity-bill savings.
8.  **Business recommendation** — Select the minimum-cost configuration
    satisfying the defined project constraints and document the
    assumptions requiring further engineering or commercial
    verification.

## Historical Electricity Profile

The analysis covers **12 billing cycles** ending from October 2023 through
September 2024.

|Account|Annual Load (kWh)|Share of Analyzed Load|
|---|---|---|
|Meter 1|117,058|16.5%|
|Meter 2|592,443|83.5%|
|Combined|709,501|100.0%|

Monthly combined electricity consumption ranges from **40,752 kWh in
April 2024** to **84,369 kWh in September 2024**. July through September
represent the highest-consumption portion of the observed year.

The demand analysis treats account-level demand separately. The site
max-demand indicator is the maximum of the two account-level monthly
maximum demands rather than a coincident sum because timestamped
coincident demand data were not available.

## Solar PV Sizing

PV sizing uses a **485-W module** basis and scales production from the
project's modeled PV production profile. The design requirement is:

> Modeled annual PV generation ≥ historical annual electricity
> consumption.

The minimum integer panel count satisfying this requirement is **838
panels**.

|PV Metric|Recommended Configuration|
|---|---|
|Panel rating|485 W DC|
|Panel count|838|
|PV DC capacity|406.43 kW|
|Modeled annual PV generation|710,207.5 kWh|
|Historical annual load|709,501 kWh|
|Annual generation coverage|100.10%|
|Annual net generation surplus|706.5 kWh|

Annual generation coverage does not imply that the facility is
self-sufficient in every month or hour. Solar production and customer
demand occur at different times, so grid imports can remain during
low-solar periods while surplus generation occurs in other periods.

## Battery Energy Storage Sizing

The ESS analysis uses the **SPT6800 commercial energy-storage
platform**, with a **215.04-kWh battery energy sizing unit**.

The battery sizing logic combines an energy constraint and a power
constraint:

- Energy sizing is based on average daily On-Peak + Mid-Peak energy.
- Power sizing uses the fixed **100-kW proposal demand-shave target**.
- The final number of units is the greater of the energy-based and
  power-based requirements.

|ESS Metric|Result|
|---|---|
|Battery sizing unit|215.04 kWh|
|Units required by energy|2|
|Units required by power|1|
|Required units|2|
|Nominal ESS energy|430.08 kWh|
|Modeled delivered energy|367.72 kWh|
|Estimated AC PCS rating|200 kW|
|Proposal demand-shave target|100 kW|
|Approximate duration at 100-kW target|3.68 hours|

The model uses a **90% usable-energy fraction** and **95% discharge
efficiency** as modeling assumptions. The **100-kW AC PCS per sizing
unit** value is also a modeling assumption based on a comparable-product
benchmark; therefore, the resulting **200-kW AC rating is estimated
rather than manufacturer-verified**.

## Demand-Charge Analysis

Demand charges are evaluated by account rather than by summing
noncoincident meter peaks. Meter 2 is used as the proposal modeling
basis because it carries the dominant demand-charge exposure.

At the **100-kW demand-shave target**, the model estimates:

|Demand-Savings Component|Annual Savings|
|---|---|
|Base-demand savings|\$29,634.80|
|TOU-demand savings|\$9,737.95|
|Total demand-charge savings|\$39,372.75|

The 100-kW value is a proposal base case rather than an optimized
dispatch result. Actual savings depend on battery availability at the
relevant billing peaks.

## Configuration Scenarios

Five PV/ESS configurations were compared.

|Scenario|PV Panels|PV Capacity (kW DC)|ESS Units|ESS Energy (kWh)|Screening Installed Cost|
|---|---|---|---|---|---|
|Minimum|838|406.43|2|430.08|\$1,074,972|
|Balanced A|850|412.25|2|430.08|\$1,086,671|
|Balanced B|875|424.38|3|645.12|\$1,240,066|
|Higher Storage|900|436.50|4|860.16|\$1,393,461|
|Historical PV Scale|1,000|485.00|6|1,290.24|\$1,748,994|

The **Minimum** configuration is recommended because it satisfies the
defined annual PV-coverage and ESS-sizing requirements at the lowest
modeled installed cost.

This recommendation represents minimum-cost feasibility under the
project's screening assumptions rather than a globally optimized
engineering design.

## Electricity-Cost Savings

The historical annual electricity bill across the two analyzed accounts
is **\$286,732.11**.

The model estimates
**$106,305.62 in Year-1 savings**, reducing the modeled annual bill to approximately **$<!-- -->180,426.49**.

|Year-1 Value Stream|Modeled Savings|
|---|---|
|PV energy savings|\$57,593.04|
|Demand-charge savings|\$39,372.75|
|PV export value|\$4,327.20|
|Grid-charging arbitrage|\$5,012.64|
|Total Year-1 savings|\$106,305.62|

The savings structure illustrates why the project is evaluated as a
combined PV + ESS system rather than as an annual solar-energy
calculation alone. PV primarily offsets purchased electricity, while
storage creates additional value through demand management and TOU
energy shifting.

## Grid-Charging Logic

The screening model allows grid charging when PV generation is
insufficient and the TOU price spread supports energy shifting.

- **Summer:** Off-Peak charging → On-Peak discharge.
- **Winter:** Super-Off-Peak charging → Mid-Peak discharge.

The model estimates **20,349 kWh/year of grid-charged delivered
discharge** and approximately **22,610 kWh/year of grid charging
input**.

|Grid-Arbitrage Metric|Annual Result|
|---|---|
|Avoided high-price energy cost|\$7,090.54|
|Grid-charging cost|\$2,077.90|
|Net grid-charging arbitrage value|\$5,012.64|

This is a bill-based screening calculation rather than an interval-level
optimized battery dispatch schedule.

## Financial Evaluation

The proposal model evaluates the recommended system over a 30-year
horizon.

|Financial Item|Proposal Model|
|---|---|
|Gross project cost|\$1,074,972|
|PV cost|\$816,924|
|ESS cost|\$258,048|
|Federal tax credit modeled|\$322,492|
|Federal depreciation tax benefit modeled|\$274,118|
|California depreciation tax benefit modeled|\$85,998|
|Total modeled tax benefits / incentives|\$682,607|
|Net economic cost after modeled benefits|\$392,365|

The long-term model uses a **5% discount rate**, **3% annual electricity
escalation**, and **0.8% annual PV degradation**.

|Financial Performance Metric|Result|
|---|---|
|30-year electricity-bill savings|\$4,694,064|
|NPV|\$1,757,719|
|IRR|21.5%|
|Simple payback|3.9 years|
|PV-generation LCOE screening proxy|≈ \$0.016/kWh|

These outputs are proposal-case results and inherit the assumptions of
the operating, tariff, equipment-cost, incentive, and tax models.

## Environmental Benefits

The client-facing proposal reports the following 20-year environmental
equivalents:

|Environmental Metric|20-Year Proposal Equivalent|
|---|---|
|CO₂ offset|11,127 tons|
|Vehicle miles equivalent|25,298,775 miles|
|Trees equivalent|166,899 trees|

These values are proposal-level environmental equivalency metrics rather
than directly measured emissions reductions.

## Business Interpretation

The project's economics are generated by several complementary
mechanisms:

- **PV energy offset** reduces electricity purchased from the utility.
- **Demand management** addresses the substantial demand-charge
  component of the commercial bill.
- **TOU shifting** allows storage to move energy between lower- and
  higher-cost periods.
- **PV export value** captures part of the value of generation that
  cannot be consumed on site.
- **System sizing discipline** prevents additional equipment from being
  added when incremental modeled value does not justify incremental
  capital cost.

The scenario analysis demonstrates an important capital-allocation
principle: the largest system is not automatically the best business
decision. Under the defined project constraints, the 838-panel /
two-unit ESS configuration provides the minimum-cost passing solution.

## Project Execution and Contribution

The project combined **data analysis, technical proposal development,
financial modeling**, and **cross-functional coordination**.

**My work included:**

- Retrieving and analyzing customer utility data from customer-provided
  account access.
- Developing the Excel calculations used for preliminary PV and ESS
  sizing.
- Analyzing electricity consumption, TOU patterns, demand charges, and
  system scenarios.
- Building the component-level cost model.
- Performing Aurora modeling.
- Configuring Energy Toolbase project inputs, scenarios, and financial
  assumptions and interpreting the resulting software outputs.
- Preparing and iteratively revising the commercial proposal.
- Scheduling and coordinating the engineering site survey and
  incorporating the resulting findings into proposal revisions.

The engineering team conducted the site survey and authored the
electrical single-line diagram. The EMS was provided at the company
level. Energy Toolbase supplied the calculation engine used with the
configured project inputs.

## Limitations

The analysis is intended for commercial screening and proposal
development rather than final engineering design.

Key limitations include:

- The site max-demand indicator is not a simultaneous sum of the two
  account peaks.
- Meter 1 May 2024 TOU detail is estimated from adjacent billing
  periods.
- The 100-kW AC PCS-per-unit value is a benchmark-based modeling
  assumption rather than a verified manufacturer specification.
- The 100-kW demand-shave target is a proposal base case rather than an
  optimized dispatch result.
- Historical effective tariff rates are bill-derived values rather than
  current utility tariff quotations.
- Equipment cost, export value, incentive eligibility, depreciation
  treatment, and tax benefits require current verification before
  investment.
- Final ESS interconnection topology and account-level demand reduction
  require engineering verification.

## Repository Files

|File|Description|
|---|---|
|`Barstow_PV_ESS_Portfolio_Project.xlsx`|Analytical workbook containing utility data, TOU analysis, PV/ESS sizing, scenario analysis, demand-charge modeling, financial analysis, and proposal-support calculations.|
|`Barstow_Proposal_Portfolio_Project.pdf`|Client-facing commercial solar + storage proposal summarizing the recommended configuration, electricity savings, project economics, cash flow, and environmental benefits.|
|`Barstow_Commercial_Solar_ESS_Techno_Economic_Project_Report.docx`|Detailed project report explaining the project background, analytical methodology, sizing logic, results, interpretation, business implications, and limitations.|

## Tools and Analytical Methods

**Methods:** utility-bill analysis, TOU analysis, PV production scaling,
battery energy/power sizing, demand-charge modeling, scenario analysis,
cash-flow analysis, NPV, IRR, payback analysis, sensitivity analysis.

**Tools:** Microsoft Excel, Aurora Solar, Energy Toolbase.

## Key Takeaway

This project demonstrates an **end-to-end commercial analytics workflow** in
which historical operating data are translated into technical system
requirements and then into business decision metrics. The recommended
configuration combines **406.43 kW DC of solar PV** with **430.08 kWh of
battery storage**, producing modeled **Year-1 electricity savings of
\$106,305.62** and a **3.9-year payback** under the proposal
assumptions.

The central analytical contribution is the connection between **utility
data, system sizing, tariff economics, scenario evaluation**, and
**investment performance** while maintaining clear distinctions among
observed data, product specifications, modeling assumptions, and derived
results.
