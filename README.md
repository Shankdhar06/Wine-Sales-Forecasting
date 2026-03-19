# 🍷 Wine Sales Time Series Forecasting

A comprehensive time series analysis and forecasting project on monthly wine sales data (Rose and Sparkling wines) for **ABC Estate Wines** — covering the period from **1980 to 1995**.

---

## 📌 Problem Statement

As an analyst at ABC Estate Wines, the goal is to analyse historical sales data for two wine types — **Rose** and **Sparkling** — and build the best-fit forecasting model to predict future monthly sales.

---

## 📂 Dataset

- **Rose Wine**: Monthly sales from January 1980 to July 1995 (187 records, 2 missing values imputed)
- **Sparkling Wine**: Monthly sales from January 1980 to July 1995 (187 records, no missing values)
- Both datasets are monthly time series with a **train/test split at January 1991**
  - Training set: 132 records (1980–1990)
  - Test set: 55 records (1991–1995)

---

## 🔍 Exploratory Data Analysis

Key findings from EDA:

- **Rose Wine**: Shows a clear **downward trend** over time. Seasonality becomes more prominent post-1988. December consistently records the highest monthly sales.
- **Sparkling Wine**: Shows a **slight upward trend**. Sales peaked around 1987–1988, driven by the "yuppie culture" era. December is again the highest-sales month; June is the lowest.
- Both datasets were decomposed using **Multiplicative decomposition** (chosen over Additive based on residual analysis).
- Both datasets are **non-stationary** at level; first-order differencing (d=1) makes them stationary — confirmed via the **Augmented Dickey-Fuller (ADF) test** at α = 0.05.

---

## 🤖 Models Built

The following models were built on training data and evaluated on test data using **RMSE**:

| # | Model |
|---|-------|
| 1 | Linear Regression |
| 2 | Naïve Forecast |
| 3 | Simple Average |
| 4 | Moving Average (2, 4, 6, 9-point trailing) |
| 5 | Simple Exponential Smoothing (auto + tuned) |
| 6 | Double Exponential Smoothing — Holt's Method (auto + tuned) |
| 7 | Triple Exponential Smoothing — Holt-Winters' Method (auto + tuned) |
| 8 | ARIMA — Auto (AIC-based parameter selection) |
| 9 | SARIMA — Auto (AIC-based parameter selection) |
| 10 | ARIMA — Manual (ACF/PACF cut-off based) |
| 11 | SARIMA — Manual (ACF/PACF cut-off based) |

---

## 📊 Model Performance (Test RMSE)

### Rose Wine

| Model | Test RMSE |
|-------|-----------|
| Linear Regression | 15.27 |
| Naïve Model | 79.72 |
| Simple Average | 53.46 |
| 2-point Moving Average | 11.53 |
| Simple Exponential Smoothing (α=0.07) | 36.44 |
| Double Exponential Smoothing | 15.27 |
| Triple Exponential Smoothing (auto) | 21.65 |
| **Tuned Triple Exponential Smoothing (α=0.2, β=0.7, γ=0.2)** | **8.70 ✅** |
| ARIMA(0,1,2) — AIC | 15.62 |
| SARIMA(0,1,2)(2,0,2,12) — AIC | 26.93 |
| ARIMA(2,1,2) — Manual | 15.35 |
| SARIMA(2,1,2)(2,1,4,12) — Manual | 16.96 |

### Sparkling Wine

| Model | Test RMSE |
|-------|-----------|
| Linear Regression | 1389.14 |
| Naïve Model | 3864.28 |
| Simple Average | 1275.08 |
| 2-point Moving Average | 813.40 |
| Simple Exponential Smoothing (α=0.02) | 1279.50 |
| Double Exponential Smoothing (α=0.1, β=0.1) | 1778.56 |
| Triple Exponential Smoothing (auto) | 380.38 |
| **Tuned Triple Exponential Smoothing (α=0.4, β=0.1, γ=0.3)** | **326.58 ✅** |
| ARIMA(1,1,1) — AIC | 1461.67 |
| SARIMA(1,1,2)(1,0,2,12) — AIC | 528.60 |
| ARIMA(0,1,0) — Manual | 4779.15 |
| SARIMA(0,1,0)(2,1,4,12) — Manual | 937.45 |

---

## 🏆 Best Model

For both wine types, the **Tuned Triple Exponential Smoothing (Holt-Winters' Method)** with Multiplicative trend and seasonality achieved the lowest RMSE on the test set.

| Wine | Best Model | Parameters | Test RMSE | Full Data RMSE |
|------|-----------|------------|-----------|----------------|
| Rose | Tuned Triple ES | α=0.2, β=0.7, γ=0.2 | 8.70 | 20.68 |
| Sparkling | Tuned Triple ES | α=0.4, β=0.1, γ=0.3 | 326.58 | 391.32 |

---

## 🔮 12-Month Future Forecast

The best-fit models were retrained on the **complete dataset** and used to predict the next 12 months (Aug 1995 – Jul 1996) with **95% confidence intervals**.

- **Rose Wine**: Forecast continues the downward trend, consistent with historical patterns.
- **Sparkling Wine**: Forecast predicts an increase of approximately 800 units, maintaining seasonal peaks in Q4.

---

## 🛠️ Tech Stack

- **Python**
- **Pandas**, **NumPy** — Data manipulation
- **Matplotlib** — Visualisation
- **Statsmodels** — ARIMA, SARIMA, Exponential Smoothing
- **Scikit-learn** — Linear Regression, RMSE evaluation
- **Jupyter Notebook**

---

## 📁 Repository Structure

```
wine-sales-time-series-forecasting/
│
├── wine_sales_forecasting.ipynb     # Main notebook with all models
├── Wine sales forecasting.pdf  # Detailed project report
└── README.md
├── Rose.csv #Rose wine raw data
└── Sparkling.csv #Sparkling wine raw data
```

---

## 📈 Key Insights & Recommendations

### Rose Wine
- Sales have been on a consistent decline since the early 1980s due to poor market perception and competition from other wine varieties.
- December, November, and October are peak months — company should stock up inventory by Q3.
- Focus on brand rehabilitation, quality improvement, and aggressive marketing especially via social media.

### Sparkling Wine
- Sparkling wine had a boom period (1985–1988) driven by the "yuppie culture" — it was seen as a status symbol.
- Sales are holiday-heavy (Q3/Q4), especially around Christmas and New Year's.
- Company should maintain Q4 inventory well in advance and run promotions in Q1/Q2 to even out the seasonal peaks.

---

## 👤 Author

**Vaibhav Shankdhar**  
