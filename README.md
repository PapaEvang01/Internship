# Internship

## Internship Project – Forecasting Cooling and Critical Loads

This repository contains the complete implementation of two forecasting pipelines for energy load prediction, developed during my summer internship at **ΙΩΝΙΚΗ**, a company based in Xanthi, Greece.

During this internship, I applied my Python and deep learning skills to support energy forecasting for a real-world autonomous hybrid energy system. 
The project focused on modeling and predicting both **critical loads** and **cooling loads** using statistical and neural network approaches.

---

### ⚙️ System Context

The energy system under study includes:

- **Photovoltaic Panels** – 40 kW
- **Battery Storage** – 120 kWh
- **Charge Controller & Inverter**
- **Critical Loads** – 5 kW (e.g., servers operating 24/7)
- **Cooling Loads** – Variable, dependent on temperature
- **Environmental Data** – Solar irradiance and weather forecasts

The objective is to achieve **energy autonomy** across both daily and seasonal cycles. 
Predicting energy consumption—especially cooling loads—is essential for intelligent load scheduling, battery use, and energy optimization.

---

### 🔍 Energy Behavior Summary

- **Daily Pattern:**  
  Solar production peaks between 12:00–15:00; cooling loads rise in the afternoon and drop at night.

- **Seasonal Pattern:**  
  - **Summer:** High production but also high cooling demand  
  - **Winter:** Low production and minimal cooling use  
  - **Spring/Fall:** Balanced production and stable consumption  

A wind turbine complements production during low-sun periods (especially winter).

---

### 🎯 Project Objectives

- Develop models to forecast energy loads using historical and environmental data
- Enable proactive energy management (battery scheduling, critical load prioritization)
- Support real-time decision-making for future energy planning

---

### 🧠 Modeling Approach

Two forecasting models were developed, tailored to the nature of each load type:

- **SARIMA (Seasonal ARIMA)** for **Critical Loads**  
  Critical loads (e.g., servers) follow predictable, stable trends.  
  SARIMA was chosen for its effectiveness in modeling stationary time series with seasonal components.

- **LSTM (Long Short-Term Memory Network)** for **Cooling Loads**  
  Cooling loads are dynamic and nonlinear, with patterns influenced by weather and time of day.  
  LSTM was used to capture long-term dependencies and fluctuations using historical sequences.

Both models were trained using data from **January to November 2023**, with the goal of **predicting the entire month of December**. This setup simulates real-world operation, where the system predicts future consumption based on past trends.  
The long-term goal is to generalize these models to **forecast a full year ahead** using similar methods.

---

### 📁 Dataset Overview

- **File:** `RnD_CriticalLoadHistory_2023.xlsx`  
- **Resolution:** 15-minute intervals  
- **Time Span:** January 1 – December 31, 2023  
- **Total Records:** 35,040  

**Key Features:**
- Solar irradiance  
- PV production and flow (to battery, to consumers)  
- Battery discharge  
- Very / Medium / Low Critical Loads  
- Cooling Load  
- Total Consumption  

---

### 🧾 Sample Data

| Timestamp     | Irradiance | PV→Bat | PV→Load | Bat→Load | PV Prod | VCL  | MCL  | LCL  | Cooling | Total |
|---------------|------------|--------|---------|----------|---------|------|------|------|---------|-------|
| 1/1/23 0:00   | 0.00       | 0.00   | 0.00    | 0.37     | 0.00    | 0.15 | 0.06 | 0.08 | 0.08    | 0.37  |
| 1/1/23 0:15   | 0.00       | 0.00   | 0.00    | 0.36     | 0.00    | 0.16 | 0.07 | 0.08 | 0.05    | 0.36  |
| 1/1/23 0:30   | 0.00       | 0.00   | 0.00    | 0.37     | 0.00    | 0.15 | 0.09 | 0.08 | 0.05    | 0.37  |
| 1/1/23 0:45   | 0.00       | 0.00   | 0.00    | 0.35     | 0.00    | 0.16 | 0.08 | 0.07 | 0.04    | 0.35  |
| 1/1/23 1:00   | 0.00       | 0.00   | 0.00    | 0.36     | 0.00    | 0.16 | 0.07 | 0.07 | 0.07    | 0.36  |

---

### 🔮 Forecasting Scope

The models were evaluated by predicting **December 2023**, using the preceding 11 months for training.  
This practical forecasting window aligns with how energy systems operate: predicting the upcoming period based on observed past behavior.

A successful December forecast indicates readiness to forecast **any future month or full year**, aiding in long-term system design, scheduling, and energy planning.

---


---

#### 🧾 Sample Data (Very/Medium/Low Critical Loads)

| Timestamp     | Very | Medium | Low |
|---------------|------|--------|-----|
| 1/1/23 0:00   | 0.15 | 0.06   | 0.08 |
| 1/1/23 0:15   | 0.16 | 0.07   | 0.08 |
| 1/1/23 0:30   | 0.15 | 0.09   | 0.08 |
| 1/1/23 0:45   | 0.16 | 0.08   | 0.07 |
| 1/1/23 1:00   | 0.16 | 0.07   | 0.07 |

---

#### 📘 Theoretical Notes

SARIMA is a time-tested model designed to handle both trend and seasonality in time series data.  
It relies on:
- Differencing to remove trends
- ACF/PACF plots to identify autoregressive and moving average terms
- Manual or grid search tuning for seasonal parameters `(P,D,Q,s)`

---

#### ⚙️ Workflow Summary

1. Perform ADF test for stationarity
2. Apply differencing (if needed)
3. Tune parameters manually or with grid search
4. Train SARIMA models separately for VCL, MCL, LCL
5. Forecast December 2023
6. Evaluate predictions and save results

---

#### 📤 Output Summary

**1. Forecasted CSVs**
- `very_critical_sarima_forecast.csv`
- `medium_critical_sarima_forecast.csv`
- `low_critical_sarima_forecast.csv`

**2. Prediction Plots (December)**
- `very_critical_loads_december_forecast.png`
- `medium_critical_loads_december_forecast.png`
- `low_critical_loads_december_forecast.png`

**3. Full-Year Overlays**
- `very_critical_full_year_forecast.png`
- `medium_critical_full_year_forecast.png`
- `low_critical_full_year_forecast.png`

---

#### 📊 Evaluation Metrics (December 2023)

| Load Type           | MAE (kWh) | RMSE (kWh) |
|---------------------|-----------|------------|
| Very Critical Load  | ~0.03     | ~0.05      |
| Medium Critical Load| ~0.04     | ~0.06      |
| Low Critical Load   | ~0.05     | ~0.08      |

---

### 2. LSTM Model (Deep Learning)

📁 **Folder:** `LSTM_model/`  
🎯 **Target:** Cooling Load  
🤖 **Technique:** Long Short-Term Memory (LSTM) Neural Network

---

#### 📂 Folder Structure



📅 **Prediction Scope for Both Models**

Both models are trained on data from **January–November 2023** and tested on **December 2023**.  
The success of this setup demonstrates their potential to **forecast any future month or full year**, enabling proactive and intelligent energy planning.

---

## 📈 Results & Evaluation

Both models were evaluated on **December 2023**, using metrics such as:

- **MAE (Mean Absolute Error)**
- **RMSE (Root Mean Squared Error)**
- **R² (R-squared / Coefficient of Determination)**
  
---

### 🔢 LSTM – Cooling Load Forecasting Results

| Metric | Value |
|--------|-------|
| MAE    | 0.065 kWh |
| RMSE   | 0.167 kWh |
| R²     | 0.938 |

 **Interpretation:**
- The model is highly accurate, with predictions deviating by less than 0.07 kWh on average.
- RMSE confirms stable prediction across the test set.
- The R² score indicates that the model explains **93.8%** of the variance in actual cooling loads.

---

### 🔢 SARIMA – Critical Loads Forecasting Results

| Load Type           | MAE (kWh) | RMSE (kWh) |
|---------------------|-----------|------------|
| Very Critical Load  | ~0.03     | ~0.05      |
| Medium Critical Load| ~0.04     | ~0.06      |
| Low Critical Load   | ~0.05     | ~0.08      |

 **Interpretation:**
- SARIMA models performed well across all three load types.
- Prediction errors remained small and consistent, suitable for planning critical resource availability.

---

## ✅ Conclusion

This project demonstrates the successful use of both **statistical** and **deep learning** methods to forecast energy demand for an autonomous hybrid energy system.

- **LSTM** proved highly effective for modeling **cooling loads**, capturing non-linear patterns and long-term dependencies with high accuracy.
- **SARIMA** effectively modeled **critical loads**, where seasonality and trend dominate consumption behavior.

Both models were able to **accurately forecast December 2023** using only historical data, validating their use in **forward-looking, real-world deployments**.  
This forecasting capability can support:

- Intelligent battery and inverter scheduling  
- Prioritization of critical loads  
- Smart integration of renewables and storage systems

The system is now ready to forecast **entire future years** with confidence — a critical step toward fully autonomous, AI-driven energy management.

