# Climatologically-driven temporal predictive modeling of dengue cases in Philippine locations

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/graphical_abstract.jpg" width=50% height=50%>
</p> 

Dengue fever remains a significant public health concern in the Philippines, with outbreaks driven by complex climatological and environmental factors. This project explores **predictive modeling techniques** using **time series analysis** and **machine learning** to forecast dengue cases in **Bulacan, Quezon City, and Rizal**—areas identified within the same dengue case cluster.

The project integrates climate variables, historical dengue case trends, and statistical models such as **SARIMAX**, alongside machine learning approaches like **Stochastic Gradient Descent (SGD) Regressor** to improve forecasting accuracy.

🔗 Research Paper | Presentation

## 🎯 Objectives
- Develop a predictive model for **dengue cases** using climatological and time-series data.
- Analyze the impact of **climate factors** on dengue incidence.
- Compare traditional statistical models **(SARIMA, SARIMAX)** with **machine learning models**.
- Identify potential **outbreak periods** for proactive health interventions.

## 🏭 Data Sources

<div align="center">
  
| Dataset           | Details                                                                                | Source                                               |
|-------------------|----------------------------------------------------------------------------------------|------------------------------------------------------|
| Dengue Cases Data | Weekly confirmed cases and deaths (2016-2021) in 126 locations across the Philippines. | [DOH-Epi Dengue Data](https://data.humdata.org/dataset/philippine-dengue-cases-and-deaths) |
| Climate Data      | Daily meteorological variables (rainfall, temperature, humidity, etc.)                 | [NASA’s POWER Project](https://power.larc.nasa.gov/) |

</div> 

> [!NOTE]
> 59 climate features were selected that aligned with the study’s objectives.

## 🏗 Methodology

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/project_methodology.png" width=60% height=60%>
</p> 

### 1. Data Preprocessing
- **Temporal Alignment:** Aggregated daily climate data to match dengue case granularity.
- **Data Imputation:** Forward Fill Imputation.
- **Location Clustering:** t-SNE Dimensionality Reduction and K-Means Clustering based on dengue cases and climate patterns.

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/clustered_cities.png" width=50% height=50%>
</p> 

- **Stationarity Check:** Augmented Dickey-Fuller (ADF) Test to ensuring data stability for time series modeling.

<div align="center">
  
| Location     | Test Statistic | p-value  | Stationary? |
|--------------|----------------|----------|--------------|
| Bulacan      | -4.6872        | 8.89e-5  | ✅ Yes      |
| Quezon City  | -3.8470        | 0.0025   | ✅ Yes      |
| Rizal        | -3.9619        | 0.0016   | ✅ Yes      |

</div>

### 2. Feature Processing
  - Temporal Feature Engineering – Creating lagged variables, Fourier transformations, etc.
  - Geographical Feature Engineering – Adding latitude, longitude, and location-based features.
  - Anomaly Detection – Identifying outliers using DBSCAN.
  - Climate Feature Selection – Choosing the most relevant meteorological variables.
  - Univariate Correlation Check – Reducing multicollinearity.
  - Temporal Splitting and Time Series Cross-Validation – Ensuring proper model evaluation.

### 3. Model Training
- **Statistical Models:** SARIMA, SARIMAX (Auto-ARIMA tuning).
- **Machine Learning Models:** SGD Regressor, XGBoost (optimized via Optuna and TPOT).
- **Validation:** Time-series cross-validation (70% training, 30% testing).

### 4. Evaluation Metrics
- **Mean Absolute Error (MAE):** Measures the average prediction error.
- **Root Mean Squared Error (RMSE):** Penalizes large errors.
- **R² Score:** Indicates model fit and predictive power.

### 5. Outbreak Prediction
- Defined based on a moving average threshold, detecting unexpected dengue case surges.

## 📊 Results
1. SGD Regressor achieved the best performance with:
- MAE: 32.26
- RMSE: 59.32
- R² Score: 83.40%
2. The model successfully captured seasonal dengue trends, but struggled with outbreak predictions, indicating a need for further feature engineering.

### 🔍 Key Insights & Future Work
1. Feature Expansion: Incorporating demographic and urbanization data could enhance accuracy.
2. Deep Learning Approaches: Testing LSTMs, GRUs, and Attention Mechanisms for better sequential modeling.
3. Spatial Dependencies: Exploring how dengue cases in nearby locations influence each other.
