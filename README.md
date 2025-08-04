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

## 🔍 Models Implemented

This project includes two forecasting pipelines tailored to the characteristics of different energy loads:

---

### 1. SARIMA Model (Statistical)

📁 **Folder:** `SARIMA_model/`  
📌 **Target:** Very, Medium, and Low Critical Loads  
📈 **Technique:** Seasonal ARIMA (SARIMA)

The SARIMA model is built upon classical time series analysis techniques such as:

- Time series decomposition
- Stationarity testing (ADF)
- Parameter tuning via ACF/PACF
- Seasonal modeling with `(p,d,q)(P,D,Q)[s]` configurations

It is well-suited for critical loads due to their regular, stable patterns over time.

#### 📂 Folder Structure

SARIMA_model/
├── code/
│ └── SARIMA.ipynb # Full pipeline: decomposition, tuning, training, forecasting
├── inputs/ # Critical load input data (15-minute resolution)
├── results/ # Forecasts and plots

#### 📤 Output Summary

1. **Forecasted CSVs:**
   - `very_critical_sarima_forecast.csv`
   - `medium_critical_sarima_forecast.csv`
   - `low_critical_sarima_forecast.csv`  
   *(Each includes: Timestamp, Actual_Load_kWh, Predicted_Load_kWh)*

2. **Prediction Plots (December only):**
   - `very_critical_loads_december_forecast.png`
   - `medium_critical_loads_december_forecast.png`
   - `low_critical_loads_december_forecast.png`

3. **Full-Year Plots with Forecast Overlay:**
   - `very_critical_full_year_forecast.png`
   - `medium_critical_full_year_forecast.png`
   - `low_critical_full_year_forecast.png`

📊 Evaluation Metrics: MAE and RMSE are calculated to quantify accuracy for each load class.

---

### 2. LSTM Model (Deep Learning)

📁 **Folder:** `LSTM_model/`  
📌 **Target:** Cooling Load  
🤖 **Technique:** Long Short-Term Memory (LSTM) Neural Network

Cooling load consumption exhibits nonlinear, temperature-sensitive, and time-dependent behavior. LSTM networks are well-suited to this because they can:

- Learn long-term dependencies
- Handle noisy and variable sequences
- Perform univariate prediction using historical consumption only

#### 🧠 Theoretical Background

LSTM extends standard RNNs by introducing gated memory cells:
- **Forget Gate** – discards irrelevant past info  
- **Input Gate** – stores new relevant input  
- **Output Gate** – determines what to expose from memory  
This structure helps retain meaningful patterns across time without losing signal quality.

#### 📂 Folder Structure

LSTM_model/
├── code/
│ └── cooling_Loads_predictions_with_LSTM.ipynb # Full pipeline: load, preprocess, train, evaluate
├── inputs/ # Input: 15-min cooling load data (2023)
├── results/ # Output plots and predictions

#### 📊 Input Dataset

- Format: `.xlsx` (15-minute intervals)
- Period: January 1 – December 31, 2023
- Total entries: 35,040 rows  
- Column of interest: **Cooling Load (kWh)**  
  *(Preprocessing includes datetime parsing and decimal conversion)*

**Sample:**

| Timestamp     | Cooling Load (kWh) |
|---------------|--------------------|
| 1/1/23 0:00   | 0.08               |
| 1/1/23 0:15   | 0.05               |
| 1/1/23 0:30   | 0.05               |
| 1/1/23 0:45   | 0.04               |
| 1/1/23 1:00   | 0.07               |

#### ⚙️ Model Workflow

1. Load and clean the dataset
2. Normalize values using Min-Max scaling
3. Create training sequences from past timesteps
4. Train over 20 epochs using zero-sensitive loss
5. Predict all of December 2023
6. Save trained model (`cooling_lstm_fullmodel.pth`)

#### 📤 Visualization Outputs

- `cooling_december_prediction.png` – Actual vs predicted cooling loads (December)
- `cooling_actual_full_year.png` – Full-year raw consumption plot
- `full_year_with_december_overlay.png` – Overlay of prediction on real trend

---

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

