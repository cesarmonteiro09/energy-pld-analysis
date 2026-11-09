# What Drives Electricity Prices in the SE/CO Subsystem in Brazil's Free Energy Market? ⚡

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange.svg)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow.svg)](#-key-findings)

## 📋 Business Context

The **PLD (Preço de Liquidação das Diferenças)** is the reference short-term price in Brazil's Free Energy Market (*Mercado Livre de Energia*). Understanding what moves it is critical for energy consumers, traders and anyone who manages energy contracts.

**Scope & focus:** to keep the analysis focused and robust, this study covers only the **Sudeste/Centro-Oeste (SE/CO)** submarket, which concentrates most of the reservoir storage capacity of Brazil's Interconnected National System (SIN). All variables (price, reservoirs, inflows, load and thermal generation) are filtered for SE/CO, so no national or other-region data is mixed into the analysis.

**Period:** January 2021 onward, the hourly-PLD era. Earlier data used a weekly price with three load levels and is not comparable.

## ❓ Research Questions

1. Is the PLD in SE/CO significantly different between dry and wet hydrological periods?
2. How much of the PLD variation is explained by reservoir storage (EAR) and natural inflow (ENA)?
3. Do thermal dispatch and system load add explanatory power on top of EAR and ENA?
4. Can a simple regression model beat a naive forecast?

## 🗃️ Data Sources

| Variable | Source | Notes |
|---|---|---|
| PLD (target) | [CCEE Open Data](https://dadosabertos.ccee.org.br) | SE/CO submarket |
| EAR (stored energy) | [ONS Open Data](https://dados.ons.org.br) | Daily, SE/CO subsystem, as % of maximum capacity |
| ENA (natural inflow) | [ONS Open Data](https://dados.ons.org.br) | Daily, SE/CO subsystem, as % of the long-term average (MLT) |
| System load | [ONS Open Data](https://dados.ons.org.br) | SE/CO subsystem |
| Thermal dispatch | [ONS Open Data](https://dados.ons.org.br) | SE/CO subsystem |

Data downloaded on: `YYYY-MM-DD` *(fill in; ONS revised its hydrological series in October 2026, so keep the download date)*.

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
2. **Statistical Analysis:** hypothesis testing (PLD in dry vs. wet periods), confidence intervals, Spearman correlation, comparison across EAR level bands, and multiple linear regression (`scipy` / `statsmodels`) with multicollinearity check (VIF).
3. **Baseline Forecasting Model:** a simple regression model evaluated against a naive forecast benchmark.

## 🔎 Key Findings

> 🚧 *In progress. This section will be filled in as the analysis is completed.*

- PLD in SE/CO is **XX% higher/lower** in the dry period than in the wet period (p-value = X.XX).
- When EAR is below **XX%**, the average PLD is **R$ XXX/MWh**, versus **R$ XXX/MWh** when EAR is above **XX%**.
- EAR and ENA together explain about **XX%** of the PLD variation (adjusted R²).
- The baseline model improves on the naive forecast by **XX%** (RMSE).

## ⚠️ Limitations

- The PLD has a regulatory **floor and ceiling** that change every year. Days at these limits do not reflect supply and demand, so they are flagged and tested separately.
- Part of the data is **monthly** (PLD average and load) while EAR and ENA are daily, which limits the number of observations when everything is aligned to monthly frequency.
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
   2. *(next notebooks will be added here)*

## 🗺️ Roadmap

- [ ] Add daily/hourly PLD to increase the number of observations
- [ ] Complete statistical tests and regression
- [ ] Baseline forecasting model vs. naive benchmark
- [ ] Write the final storytelling (article) and publish the key findings
- [ ] Build a Power BI dashboard with the same data (Project 2)

## 📄 License and Attribution

Code: add a license of your choice (for example, MIT).
Data: CCEE and ONS open data (CC-BY 4.0 for ONS), used here for educational and portfolio purposes.
