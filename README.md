# Economic and Agricultural Determinants of Renewable Energy Consumption

**Evidence from a global panel of 122 countries, 1995–2020**
Doan Nhat Phong Le · ECN 140 (Econometrics), University of California, Davis · Spring 2026

## Research question
How do economic development and agricultural conditions shape a country's renewable energy consumption, and do these relationships differ between developed and developing economies?

## Key findings
1. **U-shaped income relationship.** Renewable energy's share of consumption first falls, then rises, with GDP per capita; the estimated turning point is roughly **US$8,860–12,000 per person**.
2. **Fossil-fuel dependence.** CO₂ emissions per capita are strongly and negatively associated with renewable consumption in every model (FD: −0.43 percentage points per ton, p < 0.001).
3. **Agriculture cuts both ways.** Agricultural value added predicts higher renewable consumption overall (FD: β = +0.122, p < 0.001), consistent with a biomass channel, but the effect reverses sharply in developed countries (FE: −1.228, p < 0.001).

Full write-up: [`report/ECN140_Report_Final.pdf`](report/ECN140_Report_Final.pdf)

## Data
Unbalanced country-year panel: 122 countries, 1995–2020, **N = 3,083** after cleaning (`data/data_final.xlsx`; the `Codebook` sheet lists every variable, unit, and source).

| Source | Variables |
|---|---|
| World Bank (WDI and related indicators) | Renewable energy consumption share, GDP, FDI, urbanization, trade, land use, agricultural value added, climate, CO₂, population, readiness and adaptive capacity |
| Our World in Data / Ember / Energy Institute | Electricity mix and energy demand indicators |
| Mendeley Data (v1) | Supplementary country-level indicators (see report) |

Cleaning steps (in `project.Rmd`): rename variables, audit missingness by variable, year, and country; drop six countries with severe gaps; classify developed vs. developing countries using average GDP per capita against the World Bank high-income threshold (2015 USD); drop rows missing core variables; set two negative outcome values to missing.

## Methods
| Model | Specification | Purpose |
|---|---|---|
| (1) Pooled OLS | Country-clustered robust SEs | Baseline, including time-invariant geography and climate controls |
| (2) Two-way fixed effects | Country and year FE | Within-country variation, net of global shocks |
| (3) First differences | Year-to-year changes | Robustness to persistent unobservables |
| (4) Subsample FE | Developed vs. developing | Heterogeneity across development levels |
| (5) Interaction FE | Development × income, × agriculture | Formal test of heterogeneous effects |

Joint Wald tests (HC1 robust) check the income quadratic and the agricultural channels.

## Repository structure
```
project.Rmd        # Full pipeline: cleaning → EDA → figures → models → tables
data/              # Analysis dataset with codebook
figures/           # EDA and diagnostic figures (distribution, EKC curve, agricultural channels, correlations, multicollinearity)
results/           # Summary statistics and main regression table (Word)
report/            # Final paper (PDF)
```

## How to run
1. Install R (≥ 4.2) and the packages:
   ```r
   install.packages(c("readxl","dplyr","tidyr","ggplot2","scales","patchwork",
                      "modelsummary","car","sandwich","lmtest","plm"))
   ```
2. Open `project.Rmd` from the repository root and knit it (or run chunks in order). Figures are written to `figures/` and tables to `results/`.

## Tools
R (`plm`, `modelsummary`, `sandwich`, `lmtest`, `ggplot2`), LaTeX/Word for the report and poster.
