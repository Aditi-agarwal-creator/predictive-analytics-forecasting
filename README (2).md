# Predictive Analytics Using Historical Data

Building a predictive model to forecast future revenue trends from historical monthly sales data — built as part of a data-driven forecasting internship task.

## Overview

This project takes 3 years of historical monthly revenue data (with realistic real-world data quality issues — missing months and an outlier), cleans it, and builds **two different forecasting models** to predict the next 6 months of revenue. The models are compared on held-out test data, and the better-performing one is used for the final forecast.

## What's Inside

| File | Description |
|---|---|
| `Predictive_Analytics_Forecasting.ipynb` | Full analysis notebook — cleaning, feature engineering, modeling, evaluation, forecasting |
| `historical_sales.csv` | Raw input dataset (36 months of monthly revenue, Jan 2023–Dec 2025) |
| `forecast_output.csv` | Cleaned historical data + 6-month forecast, combined |
| `model_evaluation_results.csv` | Accuracy metrics (MAE, RMSE, MAPE) for both models |
| `plots/` | All charts generated during the analysis |

## Methodology

1. **Data Cleaning** — missing values filled using time-based linear interpolation; outliers detected via rolling-median deviation and corrected the same way
2. **Feature Engineering** — a time index to capture trend, plus sine/cosine encoding of the calendar month to capture yearly seasonality
3. **Time-Aware Train/Test Split** — the most recent 6 months held out as test data (no random shuffling, since that would leak future information)
4. **Two Models Built & Compared:**
   - **Linear Regression** — trend + cyclical seasonality features
   - **Holt-Winters Exponential Smoothing** — a classical time-series method modeling level, trend, and seasonality directly
5. **Evaluation** — MAE, RMSE, and MAPE calculated on the test period for both models
6. **Forecasting** — the better model (lower MAPE) is refit on the full cleaned dataset and used to forecast the next 6 months

## Results

| Model | MAE (₹) | RMSE (₹) | MAPE |
|---|---|---|---|
| Linear Regression | ~1.36L | ~1.69L | ~12% |
| Holt-Winters (Time Series) | ~0.68L | ~0.81L | ~6% |

Holt-Winters performed better here — expected, since it's purpose-built for data with both trend and seasonality, while linear regression approximates seasonality through fixed sine/cosine features.

## Tools & Libraries

- Python — `pandas`, `numpy`
- `scikit-learn` — `LinearRegression`, evaluation metrics
- `statsmodels` — `ExponentialSmoothing` (Holt-Winters)
- `matplotlib`, `seaborn` — visualization

## How to Run

```bash
pip install pandas numpy scikit-learn statsmodels matplotlib seaborn jupyter
jupyter notebook Predictive_Analytics_Forecasting.ipynb
```

Run all cells top to bottom. To forecast your own data, replace `historical_sales.csv` with your own monthly time series (columns: `Month`, `Revenue`) and re-run.

## Key Learnings

- Cleaning and preprocessing real-world time-series data (missing values, outliers)
- Feature engineering for trend and seasonality (cyclical encoding)
- The difference between regression-based and dedicated time-series forecasting approaches
- Proper time-series evaluation (no random train/test shuffling) and standard accuracy metrics (MAE, RMSE, MAPE)
- Turning a trained model into an actionable future forecast

---
*Built as part of the "Predictive Analytics Using Historical Data" internship task.*
