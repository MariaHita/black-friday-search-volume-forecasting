# 📈 Modeling and Forecasting Black Friday Search Volume Index

<p align="center">
  <img src="https://img.shields.io/badge/Time%20Series-Forecasting-9B8AC4?style=for-the-badge" alt="Time Series Forecasting"/>
  <img src="https://img.shields.io/badge/Model-Hybrid%20ARIMA-D9A3B5?style=for-the-badge" alt="Hybrid ARIMA"/>
  <img src="https://img.shields.io/badge/Data-Google%20Trends-A7BFA0?style=for-the-badge" alt="Google Trends"/>
</p>

<p align="center">
  <i>Capturing seasonal spikes and calendar effects in Black Friday search interest using time series modeling.</i>
</p>

## 📌 Project Overview

Black Friday is an annual shopping event associated with a sharp increase in online search activity. These recurring spikes create a challenging forecasting problem because the data exhibits strong seasonality, calendar effects, and changing long-term trends.

This project analyzes and forecasts the **Search Volume Index (SVI) for the keyword “Black Friday” in Indonesia** using Google Trends data. Eight time series model specifications are evaluated, ranging from classical Time Series Regression (TSR) to regression models with ARIMA errors and a hybrid TSR model with ARMA errors.

The main objective is to identify a model that captures recurring November search spikes, represents the underlying time series structure, and produces reliable forecasts.

## 📑 Table of Contents

- [Research Objectives](#-research-objectives)
- [Dataset](#-dataset)
- [Methodology](#-methodology)
- [Model Specifications](#-model-specifications)
- [Evaluation Metrics](#-evaluation-metrics)
- [Key Findings](#-key-findings)
- [Model Performance](#-model-performance)
- [Forecasting](#-forecasting)
- [Tools and Techniques](#-tools-and-techniques)
- [Project Structure](#-project-structure)
- [Team Members](#-team-members)
- [Academic Information](#-academic-information)

## 🎯 Research Objectives

This project aims to:

- Explore the trend, seasonal patterns, and calendar effects in Black Friday search interest.
- Compare deterministic and stochastic approaches to time series modeling.
- Evaluate the forecasting performance of eight candidate models.
- Diagnose residual autocorrelation using the Ljung–Box test.
- Select a suitable forecasting model based on test-set accuracy and residual diagnostics.
- Forecast the Black Friday Search Volume Index for January–December 2026.

## 📂 Dataset

The dataset was obtained from **Google Trends** and contains monthly Search Volume Index observations for the keyword “Black Friday” in Indonesia.

| Dataset Characteristic | Description |
|---|---|
| Data source | Google Trends |
| Search keyword | Black Friday |
| Geographic scope | Indonesia |
| Observation frequency | Monthly |
| Observation period | January 2015 – December 2025 |
| Total observations | 132 |
| Training period | January 2015 – December 2024 |
| Testing period | January 2025 – December 2025 |
| Forecast horizon | January 2026 – December 2026 |

Google Trends reports SVI on a relative scale from 0 to 100. A value of 100 represents the highest relative search interest within the specified query and observation period, rather than the absolute number of searches.

### Key Data Characteristics

The exploratory analysis identifies three important characteristics:

- **Strong annual seasonality:** Search interest rises sharply around November, coinciding with Black Friday.
- **Long-term trend changes:** The series shows changes in its general level over the observation period.
- **Calendar effects:** The timing of Black Friday plays an important role in explaining the recurring search spikes.

## 🧪 Methodology

### 1. Exploratory Time Series Analysis

The monthly SVI data is examined to identify long-term movements, annual seasonal patterns, and unusually high values around November.

### 2. Time Series Modeling

Eight model specifications are developed to represent different combinations of trend, seasonality, calendar effects, and stochastic error structures.

### 3. Chronological Train–Test Split

The data is divided chronologically rather than randomly to preserve the temporal order of observations.

- **Training data:** January 2015 – December 2024.
- **Testing data:** January 2025 – December 2025.

### 4. Forecast Accuracy Evaluation

The models are compared using RMSE, MAPE, and sMAPE on the training and testing periods.

### 5. Residual Diagnostics

Residual autocorrelation is assessed using ACF plots and the Ljung–Box test. A p-value greater than 0.05 indicates insufficient evidence to reject the null hypothesis that the residuals have no autocorrelation over the tested lags.

### 6. Model Selection and Forecasting

The final model is selected by considering test-set accuracy and residual diagnostics. The selected model is then used to forecast monthly search interest throughout 2026, together with a 95% prediction interval.

## ⚙️ Model Specifications

Eight candidate models are compared.

| Model | Specification |
|---|---|
| M1 | Deterministic Trend + Fourier Seasonality with ARIMA Errors |
| M2 | Stochastic Trend + Fourier Seasonality with ARIMA Errors |
| M3 | Deterministic Trend + Stochastic Seasonality |
| M4 | Stochastic Trend + Stochastic Seasonality |
| M5 | Time Series Regression with Trend Only |
| M6 | Time Series Regression with Trend + Seasonality |
| M7 | Time Series Regression with Trend + Seasonality + Calendar Variation |
| M8 | Hybrid Time Series Regression with ARMA Errors |

### Why a Hybrid Model?

Classical regression can capture interpretable components such as trend and seasonality, but it may leave autocorrelation in the residuals.

The hybrid approach combines:

1. **Deterministic component:** Regression terms that represent trend, monthly seasonality, and calendar-related patterns.
2. **Stochastic component:** ARMA-type modeling of the remaining error structure.

This combination aims to preserve interpretability while accounting for temporal dependence that remains after regression.

## 📏 Evaluation Metrics

Three metrics are used to compare forecasting accuracy.

- **RMSE (Root Mean Squared Error):** Measures the square root of the mean squared prediction errors.
- **MAPE (Mean Absolute Percentage Error):** Measures average absolute prediction error relative to observed values.
- **sMAPE (Symmetric Mean Absolute Percentage Error):** Provides a symmetric percentage-based measure of forecast error.

Lower values indicate better accuracy for each metric, although the metrics may rank models differently.

The Ljung–Box test is used alongside these metrics to assess whether meaningful autocorrelation remains in the model residuals.

## 💡 Key Findings

### 1. November Is the Dominant Seasonal Peak

The time series displays recurring search spikes in November. Models that include seasonal components generally represent the observed patterns better than a trend-only regression model.

### 2. Seasonal Components Improve Model Representation

The trend-only model (M5) performs poorly because it cannot capture recurring seasonal spikes. Adding monthly seasonal components substantially improves the representation of the data.

### 3. Modeling Residual Dependence Matters

The hybrid model (M8) incorporates ARMA modeling to capture residual autocorrelation left by the deterministic regression component.

### 4. Hybrid TSR with ARMA Errors Is Selected

Based on the report's combined assessment of test-set performance and residual diagnostics, M8 is selected as the final model.

Its Ljung–Box test p-value is approximately **0.0549**, slightly above the 0.05 significance threshold. This suggests that the remaining residual autocorrelation is not statistically significant at the 5% level under the tested diagnostic setup.

## 🏆 Model Performance

The following table summarizes the **testing-period results reported in the study**.

| Model | RMSE | MAPE | sMAPE |
|---|---:|---:|---:|
| M1 — Deterministic Trend + Seasonality | 16.3 | 1.35 | 0.745 |
| M2 — Stochastic Trend + Deterministic Seasonality | 17.0 | 0.916 | 0.606 |
| M3 — Deterministic Trend + Stochastic Seasonality | 17.4 | 2.44 | 1.01 |
| M4 — Stochastic Trend + Seasonality | 17.3 | 2.11 | 0.96 |
| M5 — Trend Only | 26.7 | 3.36 | 1.19 |
| M6 — Trend + Seasonality | 16.7 | 2.16 | 0.950 |
| M7 — Trend + Seasonality + Calendar Variation | 16.7 | 2.16 | 0.950 |
| **M8 — Hybrid TSR + ARMA Errors** | **16.8** | **1.03** | **0.652** |

*Values are reproduced from the report. M8 is the selected model based on the combined evaluation, not because it has the lowest value for every individual accuracy metric.*

### Residual Diagnostic: Ljung–Box Test

| Model | p-value | White Noise Assessment |
|---|---:|---|
| M1 | 0.0040 | No |
| M2 | 0.0005 | No |
| M3 | 0.2260 | Yes |
| M4 | 0.3000 | Yes |
| M5 | 0.0000 | No |
| M6 | 0.0000 | No |
| M7 | 0.0000 | No |
| **M8** | **0.0549** | **Yes, marginal** |

The results show why forecast accuracy alone is not sufficient for model selection. Although M8 does not have the lowest RMSE or MAPE individually, it offers a balance between test-set accuracy and residual adequacy.

## 🔮 Forecasting

The selected hybrid model is used to generate monthly forecasts for **January–December 2026**.

The forecasting framework combines:

- Estimated trend effects.
- Monthly seasonal effects.
- The November Black Friday calendar effect.
- ARMA-based residual dynamics.
- A 95% prediction interval to represent forecast uncertainty.

The report expects the recurring Black Friday search spike to continue. However, the magnitude of extreme peaks remains difficult to predict precisely, so forecasts should be interpreted as estimates rather than exact future values.

## 🛠️ Tools and Techniques

**Statistical Methods**
- Time Series Regression
- ARIMA and ARIMAX
- Fourier Seasonality
- Calendar Variation Modeling
- Hybrid TSR with ARMA Errors
- Forecast Accuracy Evaluation
- ACF and Ljung–Box Residual Diagnostics
- Prediction Intervals

## 📁 Project Structure

Suggested repository structure:

```text
black-friday-search-volume-forecasting/
│
├── README.md
├── data/
│   └── README.md
├── scripts/
│   └── time_series_analysis.R
├── reports/
│   └── Project_Report.pdf
└── figures/
    ├── time_series_pattern.png
    ├── model_comparison.png
    ├── residual_diagnostics.png
    └── forecast_2026.png
```

*This structure is a recommendation. Update it to reflect the files actually uploaded to the repository.*

## 👩‍💻 Team Members

This project was developed by:

- **Maria Immaculata Dyah Hita Widowati**
- Danella Citra Aldarena
- Ruth Wahyu Sedjati Priyambodo
- Nicholas Brian Ariella

## 🎓 Academic Information

| Detail | Information |
|---|---|
| Course | Time Series Analysis project |
| Program | Undergraduate Statistics |
| Department | Department of Statistics |
| Institution | Institut Teknologi Sepuluh Nopember (ITS) |
| Location | Surabaya, Indonesia |

---

<p align="center">
  <i>Turning search trends into insights through statistical forecasting.</i>
</p>
