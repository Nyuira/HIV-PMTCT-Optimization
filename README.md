# HIV Positivity Forecasting & PMTCT Resource Optimization in Kenya

Forecasting HIV positivity rates in Maternal and Child Health (MCH) services across Kenyan health facilities, and using those forecasts to guide how Prevention of Mother-to-Child Transmission (PMTCT) resources are allocated. The aim is to support Kenya's target of keeping mother-to-child transmission below 5% by 2030.

**Status: work in progress.** Repository structure and documentation are in place and data preprocessing is under way; modelling, optimisation and deployment follow (see [Roadmap](#roadmap)).

## Questions this project answers

1. Which facilities and counties are likely to see rising HIV positivity in MCH services?
2. How accurately can positivity be forecast from routine MOH 731 reporting? (target: MAE ≤ 2 percentage points)
3. Given a fixed budget, where should ART and testing resources go to reduce projected positives the most?

## Data

- **Source:** MOH 731 reports via KHIS and NSDCC (public, aggregated)
- `mch proportion.csv`: 3,553 facility-level records, 8 features
- `HIV_dataset.csv`: 1,828 aggregated records, 40 features
- **Period:** 2020–2024, Kenyan counties and facilities
- **Privacy:** facility- and county-level aggregates only; no patient-level data

## Approach

| Stage | Methods |
|---|---|
| Preparation | Missing-value interpolation, IQR / z-score outlier checks, positivity rates derived from MOH codes, merge on `organisationunitid` |
| Forecasting | Linear regression baseline, XGBoost with SHAP explanations, Prophet for seasonality; time-series cross-validation |
| Optimisation | Linear programming (PuLP) to allocate resources under budget constraints, driven by forecast positivity |
| Delivery | Streamlit dashboard for MoH planners and a FastAPI endpoint returning predictions |

## Repository structure

```
HIV-PMTCT-Optimization/
├── data/          # raw, processed and synthetic data
├── notebooks/     # 01 preprocessing → 05 evaluation
├── src/           # preprocessing, features, models, optimisation, utils
├── deployment/    # streamlit_app.py, fastapi_app.py
└── requirements.txt
```

## Run it

```bash
git clone https://github.com/Nyuira/HIV-PMTCT-Optimization.git
cd HIV-PMTCT-Optimization
pip install -r requirements.txt
python src/data_preprocessing.py
streamlit run deployment/streamlit_app.py
```

## Roadmap

- [x] Repository structure and documentation
- [ ] Data preprocessing
- [ ] Exploratory analysis (county heatmaps, trends, seasonality)
- [ ] Forecasting models and evaluation
- [ ] Resource-allocation optimisation
- [ ] Streamlit dashboard and FastAPI deployment

## Stack

Python · pandas · scikit-learn · XGBoost · Prophet · SHAP · PuLP · Streamlit · FastAPI

## Author

**Peter Kanyuira** — IT & data professional, MSc Data Science & Analytics (Strathmore University)
[GitHub](https://github.com/Nyuira) · [LinkedIn](https://www.linkedin.com/in/peterkanyuira/)

Data courtesy of the Ministry of Health Kenya (KHIS) and NSDCC. Licensed under MIT.
