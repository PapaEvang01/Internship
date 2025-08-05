# 🔋 Internship Project – Forecasting Cooling and Critical Loads

This repository presents two complete forecasting pipelines for energy load prediction, developed during my summer internship at **ΙΩΝΙΚΗ** in Xanthi, Greece.

The project supports real-world **autonomous hybrid energy systems** by predicting both **critical** and **cooling** energy loads using statistical and deep learning approaches.

---

## ⚙️ System Overview

The energy system under study includes:

- **Photovoltaic Panels:** 40 kW  
- **Battery Storage:** 120 kWh  
- **Charge Controller & Inverter**  
- **Critical Loads:** 5 kW (e.g., 24/7 servers)  
- **Cooling Loads:** Dynamic, temperature-driven  
- **Environmental Data:** Solar irradiance & weather forecasts

🎯 **Goal:** Enable intelligent energy planning and autonomy through accurate, data-driven load forecasting.

---

## 🌞 Energy Behavior Summary

- **Daily Pattern:**  
  PV peaks at 12:00–15:00. Cooling load increases in the afternoon and drops at night.

- **Seasonal Pattern:**
  - **Summer:** High production & high cooling demand  
  - **Winter:** Low production & low cooling demand  
  - **Spring/Fall:** Balanced

A **wind turbine** supports generation in low-sun seasons (mainly winter).

---

## 🎯 Project Goals

- Forecast short- and mid-term energy demand  
- Support proactive battery and load scheduling  
- Enhance long-term system planning

---

## 🧠 Modeling Approach

This project uses two forecasting pipelines tailored to each load type:

### 1️⃣ Cooling Loads → Forecasted with LSTM

Cooling loads represent the energy needed for air conditioning and temperature control—especially during summer. These loads are:

- Highly variable (depend on temperature, humidity, time of day)  
- Nonlinear and seasonally influenced  
- Not strictly periodic or stationary  

🔹 **Why LSTM?**

Long Short-Term Memory (LSTM) networks are ideal for such patterns because they:

- Learn long-term dependencies in sequential data  
- Handle noisy, non-stationary trends  
- Model complex environmental effects on energy consumption  
- Predict accurately using past consumption patterns only

---

### 2️⃣ Critical Loads → Forecasted with SARIMA

Critical loads refer to essential operations (e.g., servers) that run continuously and follow a stable pattern. These loads are:

- Predictable and repetitive  
- Less impacted by weather or time of day  
- Best modeled using statistical methods

🔹 **Why SARIMA?**

Seasonal ARIMA (SARIMA) is effective for:

- Stationary and seasonally stable time series  
- Capturing recurring consumption cycles  
- Producing interpretable, low-variance forecasts

---

📅 **Training Period:** January – November 2023  
🔮 **Forecast Target:** December 2023  

This hybrid setup ensures robust forecasting for both **structured** and **dynamic** load behaviors.

---

## 📁 Dataset Details

- **File:** `RnD_CriticalLoadHistory_2023.xlsx`  
- **Resolution:** 15-minute intervals  
- **Total Records:** 35,040  
- **Time Span:** Jan 1 – Dec 31, 2023  

### Key Features:
- Solar irradiance  
- PV production  
- Battery discharge  
- Critical Loads (Very / Medium / Low)  
- Cooling Load  
- Total energy consumption

### 🧾 Sample Records

| Timestamp     | Irradiance (Wh/m²) | PV→Battery (kWh) | PV→Load (kWh) | Bat→Load (kWh) | PV Prod (kWh) | Very Critical (kWh) | Medium Critical (kWh) | Low Critical (kWh) | Cooling (kWh) | Total Consumption (kWh) |
|---------------|--------------------|------------------|---------------|----------------|----------------|----------------------|------------------------|--------------------|----------------|--------------------------|
| 1/1/23 00:00  | 0.00               | 0.00             | 0.00          | 0.37           | 0.00           | 0.15                 | 0.06                   | 0.08               | 0.08           | 0.37                     |
| 1/1/23 00:15  | 0.00               | 0.00             | 0.00          | 0.36           | 0.00           | 0.16                 | 0.07                   | 0.08               | 0.05           | 0.36                     |
| 1/1/23 00:30  | 0.00               | 0.00             | 0.00          | 0.37           | 0.00           | 0.15                 | 0.09                   | 0.08               | 0.05           | 0.37                     |
| 1/1/23 00:45  | 0.00               | 0.00             | 0.00          | 0.35           | 0.00           | 0.16                 | 0.08                   | 0.07               | 0.04           | 0.35                     |
| 1/1/23 01:00  | 0.00               | 0.00             | 0.00          | 0.36           | 0.00           | 0.16                 | 0.07                   | 0.07               | 0.07           | 0.36                     |

> ℹ️ All numeric values are expressed in **kilowatt-hours (kWh)**, except irradiance (**Wh/m²**).  
> The file was preprocessed to convert decimal commas to dots and parse timestamps.

---

## 🔮 Forecasting Scope

Each model was trained on data from **January to November** and tested on **December 2023**, simulating a real-world scenario.  
This validates their ability to generalize and forecast **future months or full years**.

---

# 📦 Project Structure & Models

## 1️⃣ SARIMA Model – Statistical Forecasting

📁 `SARIMA_model/`  
🎯 **Target:** Very, Medium, and Low Critical Loads  
⚙️ **Technique:** Seasonal ARIMA

### Features:
- ADF Stationarity Test  
- ACF/PACF for parameter tuning  
- Seasonal modeling with `(p,d,q)(P,D,Q)[s]` configuration

### Output Summary:
- Forecasted CSVs per load type  
- December forecast plots (`*_december_forecast.png`)  
- Full-year plots with overlay  
- Evaluation metrics: MAE, RMSE

---

## 2️⃣ LSTM Model – Deep Learning Forecast

📁 `LSTM_model/`  
🎯 **Target:** Cooling Load  
🧠 **Technique:** Long Short-Term Memory (LSTM)

### Features:
- Trained on normalized sequences  
- Handles nonlinear and noisy behavior  
- Captures both seasonal and daily dynamics

### Output Summary:
- Forecasted plots for December and full year  
- Saved model: `cooling_lstm_fullmodel.pth`  
- Evaluation metrics: MAE, RMSE, R²

---

## 🧪 Evaluation & Results

### 🔢 Cooling Load Forecasting (LSTM)

| Metric | Value      |
|--------|------------|
| MAE    | 0.065 kWh  |
| RMSE   | 0.167 kWh  |
| R²     | 0.938      |

✅ The LSTM model explained over **93%** of the variance in actual cooling loads.

---

### 🔢 Critical Load Forecasting (SARIMA)

| Load Type            | MAE (kWh) | RMSE (kWh) |
|----------------------|-----------|------------|
| Very Critical Load   | ~0.03     | ~0.05      |
| Medium Critical Load | ~0.04     | ~0.06      |
| Low Critical Load    | ~0.05     | ~0.08      |

✅ SARIMA models performed consistently across all critical load categories.

---

## Conclusion

This internship project demonstrates how combining **statistical** and **deep learning** methods enables effective forecasting for autonomous hybrid energy systems.

- **SARIMA** was ideal for structured, consistent critical loads  
- **LSTM** captured complex, nonlinear cooling behaviors

These models support:

- Intelligent battery/inverter scheduling  
- Prioritization of critical operations  
- Optimized integration of renewable sources

📈 The system is now capable of **year-round forecasting**, enabling AI-driven energy management and planning.

---

📌 *Developed as part of my internship at ΙΩΝΙΚΗ (Summer 2025)*
