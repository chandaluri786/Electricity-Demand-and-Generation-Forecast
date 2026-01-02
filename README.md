# Electricity-Demand-and-Generation-Forecast

## Overview
This project focuses on **short-term forecasting of renewable electricity generation** from **solar photovoltaic (PV)** and **wind**, along with **overall electricity demand forecasting**. The goal is to understand **seasonal, temporal, and environmental drivers** of renewable generation, evaluate multiple **time-series modeling approaches**, and identify the most accurate forecasting framework to support **energy planning and grid management**.

The analysis is based on **three years (2019–2021) of high-frequency 5-minute interval data**, combining meteorological variables with energy production and demand measurements.

---

## Objectives
- Forecast short-term solar (PV) and wind electricity production  
- Forecast overall electricity demand  
- Analyze seasonal and environmental drivers of renewable generation  
- Compare SARIMA and SARIMAX models across energy variables  
- Identify optimal forecasting strategies for renewable-only energy systems  

---

## Dataset
- **Source:** Rojas Ortega et al. (2023), Mendeley Data  
- **Time span:** 2019–2021  
- **Resolution:** 5-minute intervals  
- **Observations:** 315,648  
- **Key variables:**
  - Solar PV production (MW)
  - Wind production (MW)
  - Electricity demand (MW)
  - Irradiance (GHI, DNI, DHI)
  - Wind speed, temperature, humidity
  - Calendar features (season, day of week)
    
**Data Source**
https://data.mendeley.com/datasets/fdfftr3tc2/1

**Dataset characteristics**
- No missing values  
- High temporal resolution capturing rapid renewable fluctuations  
- Strong annual seasonality  
- Well-suited for seasonal time-series models  

---

## Methodology

### Data Preparation
- Datetime parsing and indexing
- Removal of redundant columns
- Correction of anomalous negative production values
- Temporal aggregation (monthly) for trend and stationarity analysis

### Exploratory Data Analysis
- Strong **annual seasonality** observed in PV, wind, and demand
- PV peaks during summer months; wind shows moderate but noisy seasonality
- Electricity demand peaks in summer due to cooling loads
- Persistent **supply–demand gap** between renewables and demand
- Correlation analysis identified key exogenous variables:
  - **PV:** Irradiance (GHI, DNI, DHI), humidity
  - **Wind:** Wind speed, humidity
  - **Demand:** Temperature

Stationarity tests (ADF), seasonal decomposition, and ACF/PACF analysis confirmed:
- Non-stationarity in all series
- Strong yearly seasonality  
- Need for both regular and seasonal differencing  

---

## Modeling Approach
The following models were evaluated:

- **SARIMA** (univariate seasonal ARIMA)
- **SARIMAX** (SARIMA with exogenous variables)

### Model Setup
- Seasonal period: 12 (monthly seasonality)
- Train–test split:
  - Train: 2019–2020 (80%)
  - Test: 2021 (20%)
- Grid search over ARIMA and seasonal parameters
- Model selection based on RMSE, MAE, MAPE, and R²

---

## Results & Key Findings

### Model Performance Summary
- **PV Production:** SARIMAX significantly outperforms SARIMA  
  - MAPE ≈ 2%, R² ≈ 0.99  
  - Irradiance variables capture weather-driven variability
- **Wind Production:** SARIMAX provides modest improvement  
  - Wind speed helps, but wind remains inherently noisy
- **Electricity Demand:** SARIMA outperforms SARIMAX  
  - Internal seasonality dominates demand behavior
  - Temperature alone does not justify model complexity

### Final Recommendation
A **hybrid modeling strategy** performs best:
- Use **SARIMAX** for **solar and wind generation**
- Use **SARIMA** for **electricity demand**

---

## Discussion & Applications
The forecasts reveal clear seasonal dominance of renewable sources:
- Summer and late spring: high PV output supports storage charging and load shifting
- Autumn and winter: increased reliance on wind and storage discharge
- Shoulder seasons: balanced renewable contribution

These insights enable:
- Improved storage scheduling
- Better demand-response activation
- Enhanced grid reliability in renewable-only systems

---
## Tools & Technologies
- Python  
- Pandas, NumPy  
- Matplotlib / Seaborn  
- Statsmodels  
- Jupyter Notebook  

