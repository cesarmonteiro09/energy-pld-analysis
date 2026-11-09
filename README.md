# What Drives Electricity Prices in the SE/CO Subsystem in Brazil's Free Energy Market? ⚡

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange.svg)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow.svg)](#-key-findings)


## 📋 Business Context

The **PLD (Preço de Liquidação das Diferenças)** is the reference short-term price in Brazil's Free Energy Market (*Mercado Livre de Energia*). Understanding what moves it is critical for energy consumers, traders and anyone who manages energy contracts.

**Scope & focus:** to keep the analysis focused and robust, this study covers only the **Sudeste/Centro-Oeste (SE/CO)** submarket, which concentrates most of the reservoir storage capacity of Brazil's Interconnected National System (SIN). All variables (price, reservoirs, inflows, load and thermal generation) are filtered for SE/CO, so no national or other-region data is mixed into the analysis.

**Period:** January 2017 to September 2025, at monthly frequency (105 months). September 2025 is the last month available in the CCEE historical PLD file, which stopped being updated after the migration to the CCEE Open Data portal.

## ❓ Research Questions

1. Is the PLD in SE/CO significantly different between dry and wet hydrological periods?
2. How much of the PLD variation is explained by reservoir storage (EAR) and natural inflow (ENA), and do thermal dispatch and system load add explanatory power on top of them?
3. Can a simple regression model beat a naive forecast?

## 🗃️ Data Sources

| Variable | Source | Notes |
|---|---|---|
| PLD (target) | [CCEE Open Data](https://dadosabertos.ccee.org.br) | SE/CO submarket, monthly average, in R$/MWh |
| EAR (stored energy) | [ONS Open Data](https://dados.ons.org.br) | Daily, SE/CO subsystem, in MWmês (a stock); also available as % of maximum capacity. Aggregated to monthly mean |
| ENA (natural inflow) | [ONS Open Data](https://dados.ons.org.br) | Daily, SE/CO subsystem, gross inflow in MWmed (a flow). Aggregated to monthly mean |
| System load | [ONS Open Data](https://dados.ons.org.br) | Monthly, SE/CO subsystem, in MWmed |
| Thermal dispatch | [ONS Open Data](https://dados.ons.org.br) | SE/CO subsystem, programmed generation in MWmed, summed across plants. Aggregated to monthly mean |

Data downloaded on: `2026-11-09` 

ONS data is licensed under CC-BY 4.0. Attribution: Operador Nacional do Sistema Elétrico (ONS) and Câmara de Comercialização de Energia Elétrica (CCEE).

## 📁 Project Structure

```
energy-pld-analysis/
├── data/
│   ├── raw/          # Original files from CCEE and ONS (.parquet, .xls), not edited
│   └── processed/    # Cleaned and aligned datasets used in the analysis
├── notebooks/        # Step-by-step Jupyter notebooks (EDA, statistics, baseline model)
├── outputs/          # Exported charts, correlation matrices and evaluation plots
├── src/              # Reusable helper functions
├── requirements.txt
└── README.md
```

## 📊 Key Analytical Steps

1. **Data Engineering & EDA:** handling missing values, filtering SE/CO, aligning the time index of independent ONS and CCEE sources (daily vs. monthly), and outlier detection with Pandas and NumPy.
2. **Statistical Analysis:** hypothesis testing (PLD in dry vs. wet periods), confidence intervals, Spearman correlation, comparison across EAR level bands, and multiple linear regression (`scipy` / `statsmodels`) with multicollinearity check (VIF). The regression is fitted first with EAR and ENA, then with thermal dispatch and load added, to measure the extra explanatory power.
3. **Baseline Forecasting Model:** a simple regression model (lagged EAR and ENA, without thermal dispatch) evaluated with a time-based train/test split against a naive forecast (previous month's PLD).

## 🔎 Key Findings

> 🚧 *In progress. This section will be filled in as the analysis is completed.*

- PLD in SE/CO is **61% higher** in the dry period than in the wet period (p-value = 0.007).


## ⚠️ Limitations

- The PLD has a regulatory **floor and ceiling** that change every year. Months at these limits do not reflect supply and demand (for example, the PLD stays near the floor in 2022-2024), so the price is censored and a linear coefficient understates its relationship with EAR. Months at the limits are flagged and tested separately.
- Part of the data is **daily** (EAR, ENA and thermal dispatch) while the PLD and load are **monthly**, so everything is aligned to monthly frequency, which limits the number of observations.
- Before 2021 the PLD was set weekly by load level; only its monthly average is used here, so the analysis is not valid at finer time granularity.
- Thermal dispatch is a **consequence** of the PLD (it follows the marginal cost of operation), so its association with the price is partly mechanical. It is used as a diagnostic in the explanatory model and left out of the forecasting model.
- Thermal generation uses the **programmed** dispatch, not the verified generation.
- Correlation does not imply causation. The model describes associations in historical data, not a causal mechanism.
- Hydrological series may be revised by ONS; results reflect the data on the download date above.

## 🚀 Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/cesarmonteiro09/energy-pld-analysis.git
   cd energy-pld-analysis
   ```

2. Create and activate a virtual environment (Windows PowerShell):

   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```

3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Download the raw datasets from the sources listed in [Data Sources](#️-data-sources) and place them in `data/raw/`.

5. Run the notebooks in order:

   1. `notebooks/01_exploratory_data_analysis.ipynb`
   2. `statistical_analysis.ipynb`
   3. `baseline_model.ipynb`

## 🗺️ Roadmap

- [x] Data cleaning, alignment and EDA (correlation matrices and time series)
- [ ] Add daily/hourly PLD to increase the number of observations
- [ ] Complete statistical tests and regression
- [ ] Baseline forecasting model vs. naive benchmark
- [ ] Write the final storytelling (article) and publish the key findings
- [ ] Build a Power BI dashboard with the same data (Project 2)

## 📄 License and Attribution

Code: add a license of your choice (for example, MIT).
Data: CCEE and ONS open data (CC-BY 4.0 for ONS), used here for educational and portfolio purposes.