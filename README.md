# Climatologically-driven temporal predictive modeling of dengue cases in Philippine locations

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/graphical_abstract.jpg" width=50% height=50%>
</p> 

Dengue fever remains a significant public health concern in the Philippines, with outbreaks driven by complex climatological and environmental factors. This project explores **predictive modeling techniques** using **time series analysis** and **machine learning** to forecast dengue cases in **Bulacan, Quezon City, and Rizal**—areas identified within the same dengue case cluster.

The project integrates climate variables, historical dengue case trends, and statistical models such as **SARIMAX**, alongside machine learning approaches like **Stochastic Gradient Descent (SGD) Regressor** to improve forecasting accuracy.

🔗 [Research Paper](https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/documents/written_report.pdf) | [Presentation](https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/documents/presentation_material.pdf)

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
  - **Temporal Feature Engineering** – Ordinally encoded day, month, and year from the date, calculated lagged 4-week moving averages and applied Fourier series transformations.
  - **Geographical Feature Engineering** – Added latitude, longitude, and location label features.
  - **Anomaly Detection** – Density-Based Spatial Clustering of Applications with Noise (DBSCAN).

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/DBSCAN.png" width=50% height=50%>
</p> 

  - **Climate Feature Selection** – Selected based on their relevance to environmental factors–solar radiation (Group 1), cloud cover (Group 2), hydrological variables (Group 3), temperature (Group 4), and wind speed (Group 5).
  - **Univariate Correlation Check** – Remove highly correlated features chec with Pearson Univariate Correlation Analysis.

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/correlation.png" width=50% height=50%>
</p> 

  - **Temporal Splitting and Time Series Cross-Validation** – 70% of the data (January 10, 2016, to July 14, 2019) was for training. 30% of the data (July 21, 2019, to January 10, 2021) was for testing. 

### 3. Model Training
- **Statistical Models:** (Optimized with Auto-ARIMA) SARIMA, SARIMAX.
- **Machine Learning Models:** (Selected with TPOT and optimized with Optuna) SGD Regressor, XGBoost.
- **Validation:** Time-series cross-validation (70% training, 30% testing).

### 4. Evaluation Metrics
- **Mean Absolute Error (MAE):** Measures the average prediction error.
- **Root Mean Squared Error (RMSE):** Penalizes large errors.
- **R² Score:** Indicates model fit and predictive power.

### 5. Outbreak Prediction
- Detected unexpected dengue case surges based on a moving average threshold defined by the [WHO technical handbook for dengue surveillace](https://www.who.int/publications/i/item/9789241549738). 

## 📊 Results

### 1. Dengue Incidence Prediction 
<div align="center">

| Model          | MAE    | RMSE   | R-squared |
|----------------|--------|--------|-----------|
| SARIMA         | 130.87 | 175.85 | -5.14%    |
| SARIMAX        | 77.37  | 89.36  | 73.14%    |
| XGBoost        | 58.48  | 91.08  | 71.93%    |
| SGDRegressor   | **32.26**  | **59.32**  | **83.40%**    |

</div>

- **SGDRegressor achieved the best performance** with the lowest error and highest accuracy.  
- Compared to **SARIMA** that performed poorly, **SARIMAX** performed well due to the inclusion of exogenous variables.  
- **XGBoost overfitted** and failed to predict sudden spikes accurately.

<p align="center">
<img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/predict_SGDRegressor.png" width=70% height=70%>
</p> 

### 2. Dengue Outbreak Prediction 
- Bulacan: The model predicted an outbreak before July, but the actual outbreak occurred later.
- Rizal: The model predicted 10 outbreaks, but only 5 were actual outbreaks. Additionally, an outbreak was predicted in January 2020, but it actually occurred in late 2019. No outbreaks were predicted for the end of 2020, despite actual case spikes.
- Quezon City: Only one outbreak prediction (before July 2019) matched the actual outbreak. The model missed all 2020 outbreaks, indicating a need for better generalization.

<p float="left">
  <img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/outbreak_Bulacan.png" width="30%" />
  <img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/outbreak_QC.png" width="30%" />
  <img src="https://github.com/MaryNathalie/Dengue-Forecasting-in-Philippine-Locations-Through-Climate-Based-Predictive-Models/blob/main/images/outbreak_Rizal.png" width="30%" />
</p>

## 🔍 Key Insights & Future Work
### 1. Sensitivity of Outbreak Thresholds
- Small variations in data significantly impact predictions, leading to false positives or missed outbreaks.
- More robust thresholding methods and improved feature engineering are needed to enhance outbreak detection.

### 2. Model Improvements
- The models struggled to differentiate between true outbreaks and case spikes.
- Instead of predicting case counts, models could classify whether an outbreak will occur in a specific location.

### 3. Spatial Dependencies in Dengue Cases
Dengue outbreaks are spatially correlated. To improve predictions:
- Incorporating additional features such as population density, demographics, healthcare access, and city indices may improve accuracy.
- Training models on specific locations, using previous weeks' data from adjacent areas as input features.
- Incorporating spatial clustering or location coordinates into models to capture geographic trends.

### 4. Deep Learning for Time-Series Forecasting
- While traditional models provided useful insights, more complex architectures could enhance forecasting:
- LSTM & GRU networks: Proven effective for sequential data, capturing long-term dependencies.
- Attention Mechanisms: Could help models focus on critical time periods for outbreak prediction.
