 
# 🌍 Air-quality Prediction using Advanced ML for the Indo-Gangetic Plain (IGP)

## 📖 Project Overview

Air pollution is a major environmental and public health concern in the **Indo-Gangetic Plain (IGP)**, where **PM2.5 concentrations often exceed national and international safety thresholds**.
This project focuses on predicting **PM2.5 levels** using **advanced machine learning (ML) models** applied to multi-station, multi-parameter datasets.

The aim is to build reliable, data-driven models that capture both **pollution patterns and key driving factors**, helping inform **early warnings, policymaking, and urban planning** in the region.

---

## 📊 Data Description

### 📌 Source

* Data was **downloaded from the official CPCB (Central Pollution Control Board, India) website**.
* All available **station-level CSV files** were **combined into a single Excel file (`all_station11.csv`)** for uniform processing.

### 📌 Coverage

* **Geographic region**: Monitoring stations across **Delhi and NCR**, representing the core of the IGP urban pollution belt.
* **Timeline**: Continuous air-quality and meteorological data spanning **2017 – 2024**.
* **Frequency**: Hourly recordings aggregated into **daily or monthly averages** for analysis and modeling.

### 📌 Stations (sample list)

* Anand Vihar, Ashok Vihar, Bawana, Mandir Marg, Punjabi Bagh, Pusa, R.K. Puram, Jahangirpuri, Jawaharlal Nehru Stadium, Sri Aurobindo Marg
* Alipur, Chandni Chowk, Najafgarh, Narela, Nehru Nagar, Okhla Phase-2, Patparganj, Sonia Vihar, Vivek Vihar, Wazirpur
* Aya Nagar, Burari Crossing, CRRI Mathura Road, DTU, NSIT Dwarka, North Campus DU, Shadipur, Sirifort, and others.

### 📌 Parameters

* **Pollutants:** PM2.5 (µg/m³), PM10, NO₂, SO₂, O₃, CO, etc.
* **Meteorological:** Temperature (AT, °C), Barometric Pressure (BP, mmHg), Humidity (RH), Wind Speed/Direction, etc.
* **Engineered Features:** Hourly weights, monthly weights, day-of-week indicators, etc.

---

## 🎯 Objectives

1. **Data Preprocessing & Cleaning**

   * Merge all CPCB station datasets into a structured format.
   * Handle missing values, unify timestamps, and ensure station–parameter consistency.

2. **Exploratory Analysis**

   * Study seasonal/temporal pollution trends.
   * Compare **Pre-COVID, During-COVID, and Post-COVID** periods.

3. **Clustering of Stations**

   * Apply **KMeans clustering** to group monitoring stations with similar air-quality patterns.

4. **Prediction Models**

   * Implement advanced ML models for PM2.5 prediction:

     * **Decision Tree (baseline)**
     * **Random Forest (ensemble, robust)**
     * **XGBoost (gradient boosting, state-of-the-art for tabular data)**

5. **Feature Importance & Interpretability**

   * Identify which pollutants and meteorological parameters most strongly affect PM2.5 predictions.
   * Station-level importance plots to highlight **local drivers**.

6. **Filtered Feature Modeling**

   * Refit Random Forest models using only **high-importance features**, improving **generalization (Test R²)**.

---

## 🧑‍💻 Methodology

1. **Data Pipeline**

   * Load CPCB station data from Excel (`all_station11.csv`).
   * Preprocess: convert `Timestamp` → datetime, set as index, resample to daily averages.
   * Remove duplicate/engineered columns (`.1`, `hour_weight`, etc.).

2. **Station Clustering**

   * Normalize station data and apply **KMeans + PCA**.
   * Assign each station to a cluster → compare regional pollution dynamics.

3. **Model Training**

   * Train-test split: **Train (< Jan 2024), Test (≥ Jan 2024)**.
   * Features: temporal (month, day, hour), engineered PM2.5 weights, meteorological readings.
   * Models: Decision Tree, Random Forest, XGBoost.

4. **Evaluation Metrics**

   * **R² Score**: explained variance (primary).
   * Train vs Test R² comparison to detect overfitting.
   * Highlighted that ensembles (RF, XGB) generalize better than Decision Trees.

5. **Feature Importance**

   * Combined importance across clusters and stations.
   * Station-wise bar plots for top 15 features → insights into key drivers (e.g., **NO₂, BP, Temperature**).

6. **Filtered Feature Refit**

   * Re-trained RF models using **only important features** per station.
   * Improved Test R² for several stations (e.g., Pusa = 0.75, Okhla Phase-2 = 0.66).

---

## 📈 Results

* **Decision Trees** → Severe overfitting (Train R² = 1.0, Test R² often < 0).
* **Random Forest & XGBoost** → Better generalization; many stations Test R² ≈ 0.4–0.7.
* **Feature filtering** → Significant improvement in Test R² for multiple stations.
* **Top drivers** → NO₂, PM2.5 weights, Temperature (AT), and Barometric Pressure (BP).
* **Weak stations** → Some locations (e.g., Wazirpur, DTU, Aya Nagar) underperform, likely due to **data sparsity or missing features**.


 
