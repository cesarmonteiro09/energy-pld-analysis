# Analyzing the Drivers of Electricity Prices in the SE/CO Energy Submarket ⚡

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange.svg)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow.svg)]()

## 📋 Business Context
The **PLD (Preço de Liquidação das Diferenças)** is the reference pricing mechanism in Brazil's Free Energy Market (Mercado Livre de Energia). Understanding and forecasting price volatility is critical for energy consumers and traders. 

**Scope & Focus:** To maintain a robust and focused analysis for this portfolio project, this study centers on the **Sudeste/Centro-Oeste (SE/CO) submarket**—the largest and most critical submarket in Brazil's Interconnected National System (SIN), which largely drives nationwide pricing trends.

This project investigates the macro-level drivers of PLD volatility—specifically analyzing the relationship between reservoir storage levels (EAR), thermal dispatch generation, system load demand, and historical pricing using open data from **CCEE** and **ONS**.

---

## 🗂️ Project Structure
- `data/`: Contains raw public datasets and cleaned processed CSVs.
- `notebooks/`: Step-by-step Jupyter notebooks covering EDA, statistical testing, and baseline modeling.
- `outputs/`: Exported correlation matrices, statistical charts, and evaluation plots.

---

## 📊 Key Analytical Steps
1. **Data Engineering & EDA:** Handling missing values, aligning time-series temporal indices across independent ONS and CCEE sources, and outlier detection using Pandas and NumPy.
2. **Statistical Analysis:** Hypothesis testing (comparing PLD distributions between dry vs. wet hydrological periods), confidence intervals, and multiple linear regression modeling (`scipy` / `statsmodels`).
3. **Baseline Forecasting Model:** Building and evaluating a predictive baseline regression model vs. a Naive forecasting benchmark.

---

## 🚀 Getting Started
1. Clone the repository:
   ```bash
   git clone [https://github.com/cesarmonteiro09/energy-pld-analysis.git](https://github.com/cesarmonteiro09/energy-pld-analysis.git)
   cd energy-pld-analysis