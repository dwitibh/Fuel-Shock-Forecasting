# Fuel-Shock-Forecasting


An end-to-end pipeline for detecting and forecasting global energy price shocks — using geopolitical disruption signals, macroeconomic indicators, and supply data to build a deployable forecasting model with an interactive dashboard.

> **Status:** Active development. Problem framing and data pipeline are complete. EDA is in progress.

---

## Why This Problem

Energy price shocks — sudden, sharp disruptions to global oil and gas prices — have historically been driven by a combination of supply constraints, geopolitical events, and demand dynamics. Most forecasting models treat price as a purely financial time series.

This project asks a different question: can integrating geopolitical disruption signals improve our ability to detect shocks *before* they fully materialise?

The framing is practical. A business that imports goods, operates logistics, or manages facilities energy contracts needs to anticipate price moves, not just react to them. Directional accuracy on shock detection matters more than minimising RMSE on a stable series.

---

## Project Phases

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Problem Framing | Complete |
| 2 | Data Pipeline | Complete |
| 3 | Exploratory Data Analysis | In Progress |
| 4 | Feature Engineering | Upcoming |
| 5 | Modelling | Upcoming |
| 6 | Dashboard Deployment | Upcoming |

---

## Data Sources

The pipeline ingests data from four primary sources:

**IEA (International Energy Agency)**
Monthly energy supply, production, and consumption data by country and fuel type. Used as the primary signal for supply-side disruptions.

**World Bank API**
Macroeconomic indicators including GDP growth, inflation, and commodity price indices. Used to contextualise demand-side pressure and country-level economic exposure.

**UN Comtrade**
Bilateral trade flows for energy commodities. Used to map supply chain dependencies between producer-exporter pairs and identify disruption propagation paths.

**Our World in Data / BP Statistical Review**
Long-run historical price series and energy mix data for baseline context and long-term trend modelling.

---

## Approach

### Signal Design

The core hypothesis is that geopolitical disruptions leave detectable footprints in trade flow data (UN Comtrade) and supply figures (IEA) before they fully propagate to consumer prices. The pipeline calculates a set of disruption signals — deviations from rolling baselines across key producer-exporter pairs — to quantify this lead effect.

### Modelling Strategy

The plan is to compare two model classes:

**Baseline:** ARIMA/SARIMA on price series only — establishes how well price history alone predicts future moves.

**Augmented model:** ARIMAX or XGBoost with disruption signals as exogenous features — tests whether geopolitical and supply signals add genuine predictive value beyond price history.

**Evaluation metric:** Directional accuracy on shock detection, not just RMSE. Getting the direction right on a price move matters more than precise magnitude for the target use case.

### Dashboard

The final output will be an interactive Plotly/Dash dashboard showing forecast vs actuals, disruption signal strength over time, and annotated shock events.

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Data wrangling | Python, pandas |
| Statistical modelling | statsmodels (ARIMA/ARIMAX) |
| ML modelling | scikit-learn, XGBoost |
| Data sources | World Bank API, UN Comtrade API |
| Visualisation | Plotly, Dash |
| Notebook environment | Jupyter |

---

## Repository Structure

```
├── data/
│   ├── raw/               # Raw data from APIs and downloads
│   └── processed/         # Cleaned and merged datasets
├── notebooks/
│   ├── 01_data_pipeline.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_modelling.ipynb
│   └── 05_evaluation.ipynb
├── dashboard/
│   └── app.py             # Plotly Dash app
├── requirements.txt
└── README.md
```

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
statsmodels
scikit-learn
xgboost
plotly
dash
wbgapi
```

Install with:

```bash
pip install -r requirements.txt
```

---

## Progress Log

**April 2026**
- Problem framing complete. Core hypothesis defined: geopolitical trade flow deviations as leading indicators of price shocks.
- Data pipeline built. IEA, World Bank, and UN Comtrade sources ingested and merged.
- EDA underway. Initial exploration of price series structure, seasonality, and candidate disruption signal variables.

---

*Author: Dwiti Bhavsar — Senior Data Analyst & Data Scientist*
*Case study write-up: [View project page](energy-forecasting.html)*
