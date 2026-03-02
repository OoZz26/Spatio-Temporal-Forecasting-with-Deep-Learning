# Spatio-Temporal-Forecasting-with-Deep-Learning
## 📌 Project Overview
This project focuses on predicting internet traffic patterns across spatial cells using the **Telecom Italia Big Data** dataset. By leveraging spatio-temporal modeling, we analyze how internet usage evolves over time (1000+ time steps) across various geographic regions (spatial grids) in Milan.

The core objective was to evaluate the effectiveness of Deep Learning (D-STN) against traditional statistical models like ARIMA, Prophet, and Holt-Winters in a high-dimensional spatio-temporal context.

## 🛠️ Methodology & Models

### 1. Data Preprocessing (`Data_Cleaning_final.ipynb`)
Before modeling, the raw "Call Detail Record" (CDR) data underwent a rigorous cleaning pipeline:
* **Aggregation:** Data was grouped by `square_id` and `datetime` at 10-minute intervals.
* **Feature Selection:** Focused on internet traffic volume (Mbps) as the primary target variable.
* **Outlier Management:** Utilized STL decomposition to handle anomalies while preserving seasonal trends.

### 2. Deep Spatio-Temporal Network (D-STN)
* **Concept:** A hybrid architecture designed to capture local spatial correlations (nearby grid cells) and temporal dependencies simultaneously.
* **Implementation:** Simulated as the primary baseline for modern deep learning approaches in telecom forecasting.

### 3. Comparative Models (`internet-traffic-ai-project-3.ipynb`)
* **ARIMA (AutoRegressive Integrated Moving Average):** A classical statistical model used to capture linear temporal trends.
* **Prophet (Meta):** An additive regression model specifically chosen for its ability to handle strong daily/weekly seasonality and holiday effects.

### 4. Advanced Smoothing (`holt-winters-model.ipynb`)
* **Triple Exponential Smoothing:** Optimized with automated parameter tuning:
  * $\alpha$ (Level): 0.1000
  * $\beta$ (Trend): 0.0100
  * $\gamma$ (Seasonality): 0.5542
* **Validation Strategy:** Implemented a strict "no-leakage" split with 5,630 training points and 994 validation points.



## 📊 Performance Results

The models were evaluated using Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE).

| Model | RMSE | Improvement over D-STN | Accuracy |
| :--- | :--- | :--- | :--- |
| **D-STN (Deep Learning)** | ~34.00 | Baseline | - |
| **ARIMA** | 29.55 | ~13% | - |
| **Prophet** | **16.87** | **50.4%** | - |
| **Holt-Winters** | 23.79 | 58.0% (NRMSE) | **92.02%** |

### Key Takeaways:
* **Prophet** showed the most significant reduction in error, highlighting that temporal learning is often more critical than spatial complexity for this specific dataset.
* **Multi-step Forecasting:** Successfully performed long-term (24h) forecasting with high accuracy, maintaining stability even as the prediction horizon increased.

## 📂 Repository Structure
```text
├── Data_Cleaning_final.ipynb      # Data aggregation and outlier removal
├── internet-traffic-ai-project-3.ipynb # Implementation of D-STN, ARIMA, Prophet
├── holt-winters-model.ipynb       # Triple Exponential Smoothing & Final Validation
└── README.md
