# Climatology-Driven-Dengue-Case-Forecasting-in-the-Philippines-Using-Time-Series-and-Machine-Learning

### 📌 Overview
Dengue fever remains a significant public health concern in the Philippines, with outbreaks driven by complex climatological and environmental factors. This project explores **predictive modeling techniques** using **time series analysis** and **machine learning** to forecast dengue cases in **Bulacan, Quezon City, and Rizal**—areas identified within the same dengue case cluster.

The project integrates climate variables, historical dengue case trends, and statistical models such as **SARIMAX**, alongside machine learning approaches like **Stochastic Gradient Descent (SGD) Regressor** to improve forecasting accuracy.

### 🎯 Objectives
- Develop a predictive model for **dengue cases** using climatological and time-series data.
- Analyze the impact of **climate factors** on dengue incidence.
- Compare traditional statistical models **(SARIMA, SARIMAX)** with **machine learning models**.
- Identify potential **outbreak periods** for proactive health interventions.

### 🏭 Data Sources
1. **Dengue Case Data**
- Weekly confirmed cases and deaths from January 10, 2016, to January 10, 2021 in 126 locations across the Philippines.
- Sourced from the Department of Health-Epidemiology Bureau and hosted by the Humanitarian Data Exchange, labeled as [DOH-Epi Dengue Data 2016-2021](https://data.humdata.org/dataset/philippine-dengue-cases-and-deaths).

2. **Climate Data**
- Daily meteorological variables for each location, retrieved based on geographic coordinates.
- Obtained from [NASA’s POWER Project](https://power.larc.nasa.gov/) via its API.
- 59 selected climate features, aligned with the study’s objectives, are detailed in the paper.

### 🏗 Methodology
1. **Data Preprocessing:**
- **Temporal alignment:** Weekly aggregation of climate data.
- **Stationarity checks:** Augmented Dickey-Fuller (ADF) test.
- **Feature selection:** Correlation analysis to remove redundant features.
- **Anomaly detection:** DBSCAN clustering for outlier removal.

2. **Model Training:**
- **Statistical Models:** SARIMA, SARIMAX (Auto-ARIMA tuning).
- **Machine Learning Models:** SGD Regressor, XGBoost (optimized via Optuna and TPOT).
- **Validation:** Time-series cross-validation (70% training, 30% testing).

3. **Evaluation Metrics:**
- **Mean Absolute Error (MAE):** Measures the average prediction error.
- **Root Mean Squared Error (RMSE):** Penalizes large errors.
- **R² Score:** Indicates model fit and predictive power.

4. **Outbreak Prediction**:
- Defined based on a moving average threshold, detecting unexpected dengue case surges.

### 📊 Results
1. SGD Regressor achieved the best performance with:
- MAE: 32.26
- RMSE: 59.32
- R² Score: 83.40%
2. The model successfully captured seasonal dengue trends, but struggled with outbreak predictions, indicating a need for further feature engineering.

### 🔍 Key Insights & Future Work
1. Feature Expansion: Incorporating demographic and urbanization data could enhance accuracy.
2. Deep Learning Approaches: Testing LSTMs, GRUs, and Attention Mechanisms for better sequential modeling.
3. Spatial Dependencies: Exploring how dengue cases in nearby locations influence each other.
