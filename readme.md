# Real-Time Bike Share Station Availability Prediction

## Internship Assessment Project

---

# Project Overview

This project predicts bike-share stations that are at risk of becoming empty using near real-time Citi Bike GBFS operational data.

The system uses data preprocessing, feature engineering, exploratory data analysis, and machine learning techniques to identify operational station risks and improve bike redistribution planning.

---

# Problem Statement

Bike-sharing systems often face operational imbalance where certain stations become empty or fully occupied during peak demand periods. This project aims to predict stations at risk of becoming empty using near real-time operational data from Citi Bike GBFS feeds.

The prediction system helps operators:

* improve bike redistribution efficiency
* reduce empty station complaints
* enhance customer experience
* support smart mobility management

---

# Dataset Source

GBFS Feed:
[https://gbfs.citibikenyc.com/gbfs/2.3/gbfs.json](https://gbfs.citibikenyc.com/gbfs/2.3/gbfs.json)

Reference:
[https://citibikenyc.com/system-data](https://citibikenyc.com/system-data)

---

# About the Dataset

The GBFS (General Bikeshare Feed Specification) feed provides near real-time operational bike-share data including:

* Available bikes
* Available docks
* Station capacity
* Station operational status
* Geographic coordinates
* Timestamp updates

The dataset is updated frequently and reflects live station conditions.

---

# Problem Type

* Classification
* Forecasting-oriented operational prediction

---

# Project Workflow

1. Fetch real-time GBFS operational data
2. Merge station information and station status feeds
3. Clean and preprocess the dataset
4. Handle missing and inconsistent values
5. Engineer operational and temporal features
6. Perform exploratory data analysis
7. Train a machine learning classification model
8. Evaluate prediction performance
9. Visualize high-risk stations using an interactive map

---

# Data Collection

The project uses two GBFS feeds:

1. Station Information Feed
2. Station Status Feed

The datasets were fetched using the Python `requests` library and merged using the `station_id` column.

---

# Data Cleaning Steps

The following preprocessing and cleaning operations were performed:

* Handled missing numerical values
* Replaced missing categorical values with 'Unknown'
* Converted UNIX timestamps into datetime format
* Removed invalid operational records
* Filtered stations with zero capacity
* Removed negative bike and dock availability values
* Checked for duplicate records
* Standardized datatypes for machine learning

---

# Feature Engineering

The following engineered features were created:

* bike_ratio
* dock_ratio
* is_weekend
* is_peak_hour
* day_of_week
* hour

These features helped the model understand operational patterns and temporal station behavior.

---

# Target Variable

The target variable used in this project is:

`empty_risk_next_30_min`

Since the GBFS feed does not directly provide future empty-risk labels, the target variable was engineered using operational assumptions.

Formula:

bike_ratio = available_bikes / capacity

If:

bike_ratio < 0.10

Then:

* Label = 1 → High Empty Risk
* Label = 0 → Low Empty Risk

This approach approximates stations likely to become empty in the near future.

---

# Exploratory Data Analysis (EDA)

EDA was performed to understand station operational behavior and availability patterns.

Visualizations included:

* Bike availability distribution
* Bike ratio distribution
* Capacity vs available bikes scatterplot
* Peak-hour operational analysis
* Correlation heatmap
* Outlier detection analysis

EDA helped identify:

* operational imbalance patterns
* peak-hour demand behavior
* high-risk station trends
* feature relationships

---

# Abnormal Pattern Detection

IQR-based outlier detection was used to identify abnormal bike availability patterns.

This helped detect:

* unusually empty stations
* unusually full stations
* operational anomalies

---

# Machine Learning Model

Model Used:

* Random Forest Classifier

Evaluation Metrics:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix

---

# Why Random Forest?

Random Forest was selected because it:

* handles nonlinear relationships effectively
* performs well on structured tabular datasets
* reduces overfitting using ensemble learning
* is robust against noisy operational data
* provides feature importance analysis

---

# Feature Importance Analysis

Feature importance analysis showed that:

* bike_ratio
* available bike count
* dock_ratio

were among the strongest predictors of empty-risk.

---

# Visualization

The project includes:

* Exploratory Data Analysis charts
* Correlation heatmap
* Feature importance graph
* Interactive Folium station risk map

The Folium map visualizes:

* Red markers → High-risk stations
* Green markers → Safer stations

---

# Key Insights

* Stations with low bike availability ratios are highly prone to empty-risk situations.
* Peak commuting hours significantly influence station imbalance.
* Bike availability ratio was one of the strongest predictive indicators.
* Real-time operational monitoring can improve bike redistribution planning.

---

# Assumptions

* Stations with less than 10% bike availability were considered high empty-risk stations.
* Real-time snapshots were used instead of historical time-series data.
* Peak commuting hours were approximated using operational assumptions.
* Current operational conditions were used to approximate near-future station risk.

---

# Limitations

* No historical sequential data was available.
* Weather and traffic data were not integrated.
* Future station states were approximated using operational logic.
* The model is based on near real-time snapshots rather than long-term forecasting.

---

# Future Improvements

Potential future improvements include:

* Historical time-series forecasting
* Weather data integration
* Traffic and event-based demand analysis
* Advanced ML models like XGBoost or LSTM
* Real-time dashboard deployment
* Live alert systems for operators

---

# Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* Folium
* Requests API

---

# How to Run

## 1. Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn requests folium
```

## 2. Open Jupyter Notebook

Run the notebook file:

`bike_share_prediction.ipynb`

## 3. Execute All Cells Sequentially

The notebook will:

* fetch live GBFS data
* preprocess the dataset
* train the prediction model
* generate visualizations
* create the station risk map

---

# Project Structure

```text
bike-share-prediction/
│
├── bike_share_prediction.ipynb
├── README.md
├── requirements.txt
├── station_risk_map.html
```

---

# Business Impact

This system can help bike-sharing operators:

* improve redistribution efficiency
* reduce empty station complaints
* optimize operational planning
* improve customer satisfaction
* support smart mobility initiatives

---

# Project Outcome

This project demonstrates how near real-time operational bike-share feeds can be transformed into predictive insights using data science and machine learning techniques.

The developed system provides a scalable foundation for intelligent bike redistribution and smart urban mobility management.
