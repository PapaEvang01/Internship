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

**Goal:** Enable intelligent energy planning and autonomy through accurate, data-driven load forecasting.

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

Two distinct forecasting pipelines:

### 1. **SARIMA** – For Critical Loads  
- Suitable for stable, seasonal patterns  
- Models: Very, Medium, and Low Critical Loads

### 2. **LSTM** – For Cooling Loads  
- Captures non-linear, weather-influenced patterns  
- Uses historical time series to predict future consumption

**Training Data:** January–November 2023  
**Forecast Target:** December 2023

---

## 📁 Dataset Details

- **File:** `RnD_CriticalLoadHistory_2023.xlsx`  
- **Resolution:** 15-minute intervals  
- **Total Records:** 35,040  
- **Time Span:** Jan 1 – Dec 31, 2023  

### Key Features
- Solar irradiance & PV production
- Battery discharge
- Load categories: Very/Medium/Low Critical + Cooling
- Total energy consumption

---

## 🔮 Forecasting Scope

Each model was trained on 11 months and tested on December 2023 — mimicking a real-world scenario.  
This validates the models’ ability to generalize and forecast **future months or entire years**.

---

# 📦 Project Structure & Models

## 1️⃣ SARIMA Model – Statistical Forecasting

📁 `SARIMA_model/`  
🎯 **Target:** Very, Medium, and Low Critical Loads  
⚙️ **Technique:** Seasonal ARIMA

### Features:
- ADF Stationarity Test  
- ACF/PACF for hyperparameter tuning  
- Seasonal modeling with `(p,d,q)(P,D,Q)[s]` configs

### Output Summary:
- Forecast CSVs (per load type)
- Monthly forecast plots (`*_december_forecast.png`)
- Full-year overlay plots
- Metrics: MAE, RMSE

---

## 2️⃣ LSTM Model – Deep Learning Forecast

📁 `LSTM_model/`  
🎯 **Target:** Cooling Load  
🧠 **Technique:** Long Short-Term Memory (LSTM) Network

### Features:
- Handles variable, nonlinear sequences
- Captures seasonal + long-term dependencies
- Trained using normalized sequences

### Output Summary:
- Forecast plots for December and full year
- Saved model: `cooling_lstm_fullmodel.pth`
- Metrics: MAE, RMSE, R²

---

## 🧪 Evaluation & Results

### 🔢 Cooling Load Forecasting (LSTM)

| Metric | Value |
|--------|-------|
| MAE    | 0.065 kWh |
| RMSE   | 0.167 kWh |
| R²     | 0.938     |

✅ Strong performance with 93.8% variance explained.

---

### 🔢 Critical Load Forecasting (SARIMA)

| Load Type           | MAE (kWh) | RMSE (kWh) |
|---------------------|-----------|------------|
| Very Critical Load  | ~0.03     | ~0.05      |
| Medium Critical Load| ~0.04     | ~0.06      |
| Low Critical Load   | ~0.05     | ~0.08      |

✅ Reliable predictions for system-critical consumption.

---

## ✅ Conclusion

This internship project successfully combined **classical time-series methods** and **deep learning** to forecast energy demand in an autonomous hybrid energy system.

- **SARIMA** is ideal for stable, seasonal loads.
- **LSTM** handles dynamic, weather-influenced cooling behavior.

These forecasts enable:

- Battery & load prioritization  
- Proactive scheduling  
- Smart renewable integration  

The system is now capable of **year-round predictions**, supporting intelligent, AI-driven energy management.

---

📌 *Developed as part of my internship at ΙΩΝΙΚΗ (Summer 2025)*  
