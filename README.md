# Internship

# Internship Project – Forecasting Critical Loads

This repository contains the complete implementation of two forecasting pipelines for energy load prediction as part of a summer internship project.

## 🔍 Models Implemented

### 1. SARIMA (Statistical)
- Folder: [`SARIMA/`](./SARIMA)
- Based on time series decomposition, stationarity testing, and manual tuning.
- Predicts Very, Medium, and Low Critical Loads for December 2023.
- Visual and quantitative evaluation (MAE, RMSE).

### 2. LSTM (Deep Learning)
- Folder: [`LSTM/`](./LSTM)
- Uses a custom PyTorch-based LSTM model trained on past load data.
- Forecasts and visualizes December loads.
- Includes model checkpoint and evaluation metrics.

## 📁 Dataset
- Historical critical load data: `RnD_CriticalLoadHistory_2023.xlsx`
- 15-minute resolution, covering all of 2023.

## 🧪 Technologies Used
- Python (Pandas, NumPy, Matplotlib)
- Statsmodels (SARIMA)
- PyTorch (LSTM)
- Google Colab / Jupyter
