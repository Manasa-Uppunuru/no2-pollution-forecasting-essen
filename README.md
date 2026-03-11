# 🌍 Short-Term NO₂ Pollution Forecasting — Essen, Germany

![Python](https://img.shields.io/badge/Python-3.13-blue) ![XGBoost](https://img.shields.io/badge/XGBoost-ML-green) ![Status](https://img.shields.io/badge/Status-Complete-brightgreen) ![Grade](https://img.shields.io/badge/Academic%20Grade-Top%20of%20Class-gold)

> **Predicting nitrogen dioxide (NO₂) pollution 1–6 hours ahead at a roadside monitoring station in Essen, Germany using Machine Learning.**

---

## 📌 Project Overview

This project builds an end-to-end machine learning pipeline to forecast short-term NO₂ concentrations at the **Essen-Ost Steeler Straße** monitoring station using openly available environmental data from the OpenAQ platform.

Two models were developed and compared:
- **ARIMA** — classical statistical baseline
- **XGBoost** — feature-rich gradient boosting model

**Result: XGBoost halved the forecast error of ARIMA across all horizons (1–6 hours ahead).**

---

## 🏆 Academic Achievement
> ⭐ **Top grade in class** — FOM University of Applied Sciences, Essen (Dec 2025)  
> Module: Analysis of Semi-Structured & Unstructured Data | M.Sc. Big Data & Business Analytics

---

## 📊 Key Results

| Model | MAE (avg) | RMSE (avg) |
|-------|-----------|------------|
| ARIMA | ~0.078 µg/m³ | ~0.097 µg/m³ |
| **XGBoost** | **~0.042 µg/m³** | **~0.052 µg/m³** |

✅ XGBoost outperformed ARIMA at **every single forecast horizon**

---

## 🗂️ Project Structure

```
no2-pollution-forecasting-essen/
│
├── 📓 Raw_to_CSV.ipynb          # Data collection from OpenAQ API → CSV
├── 📓 Measurements_data.ipynb   # Feature engineering
├── 📓 Data_clean_EDA.ipynb      # Data cleaning, EDA, feature engineering
├── 📓 Analysis.ipynb            # Model training & results
├── 📄 no2_essen_2025-08_11_raw.json   # Raw JSON data
├── 📄 no2_essen_cleaned_for_ml.csv    # Cleaned ML dataset
└── 📄 README.md
```

---

## 🔧 Technologies Used

| Category | Tools |
|----------|-------|
| Language | Python 3.13 |
| Data Collection | OpenAQ API, openaq Python client |
| Data Processing | Pandas, NumPy, JSON |
| Machine Learning | XGBoost, statsmodels (ARIMA), Scikit-learn |
| Visualisation | Matplotlib, Seaborn |
| Environment | Jupyter Notebook, Conda |

---

## 📥 Data Source

- **Source:** [OpenAQ Platform](https://openaq.org) — open environmental monitoring data
- **Station:** Essen-Ost Steeler Straße (Sensor ID: 6516)
- **Period:** January 2024 – November 2025
- **Records:** 13,618 hourly NO₂ measurements
- **Format:** Nested JSON → transformed to structured CSV

---

## ⚙️ Methodology

### 1. Data Collection
- Retrieved 13,618 hourly NO₂ measurements via paginated OpenAQ API calls
- Implemented retry logic to handle timeouts and API rate limits
- Exported nested JSON responses to structured CSV format

### 2. Data Preprocessing & EDA
- Handled missing values via linear interpolation for short gaps
- Removed outliers and ensured temporal consistency
- Exploratory analysis revealed:
  - 🌅 **Diurnal pattern:** Morning & evening rush-hour peaks
  - 📅 **Weekly pattern:** Higher NO₂ on weekdays vs weekends
  - ❄️ **Seasonal pattern:** Elevated concentrations in winter months

### 3. Feature Engineering
Created supervised learning features from time-series:
- **Temporal:** Hour of day (0–23), Day of week (0–6), Month (1–12)
- **Lagged NO₂ values:** 1-hour, 6-hour, 24-hour lags
- Final dataset: **13,594 ML-ready samples**

### 4. Models
- **ARIMA:** Orders selected via AIC and autocorrelation diagnostics
- **XGBoost:** Hyperparameter tuning via grid search with time-aware cross-validation

### 5. Evaluation
- Metrics: MAE and RMSE per forecast horizon (1h to 6h ahead)
- Chronological train/test split to prevent data leakage

---

## 🚀 How to Run

### Prerequisites
```bash
pip install openaq pandas numpy xgboost statsmodels matplotlib seaborn jupyter
```

### Steps
1. Clone the repository:
```bash
git clone https://github.com/YOUR_USERNAME/no2-pollution-forecasting-essen.git
cd no2-pollution-forecasting-essen
```

2. Get a free API key from [OpenAQ](https://openaq.org) and add it to `Raw_to_CSV.ipynb`

3. Run notebooks in order:
```
1. Raw_to_CSV.ipynb          → collect & save data
2. Data_clean_EDA.ipynb      → clean & explore data  
3. Measurements_data.ipynb   → train models & evaluate
```

---

## 💡 Key Findings

1. **XGBoost consistently outperforms ARIMA** — particularly at short horizons where it captures non-linear rush-hour dynamics
2. **Temporal + lagged features are powerful** — hour of day and 1h lag are the strongest predictors
3. **Open data is sufficient** — reliable forecasts achievable without expensive proprietary data sources
4. **Practical applications:** Real-time NO₂ warning systems, dynamic traffic management, public health advisories

---

## 🔮 Future Work
- Add meteorological features (wind speed, temperature, boundary-layer height)
- Compare with LSTM and hybrid deep learning models
- Deploy as real-time forecasting web app
- Extend to other monitoring stations across Essen/NRW

---

## 👩‍💻 Author

**Manasa Uppunuru**  
M.Sc. Big Data & Business Analytics — FOM University, Essen  
📧 uppunurumanasareddy@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/manasa-reddy-uppunuru-282447224/)

---

## 📜 License
This project is open source and available under the [MIT License](LICENSE).
