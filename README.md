# Weather-to-Wildfire-Prediction
# 🌲 A Chained Model for Weather Forecasting and Wildfire Risk Prediction

> **Data Science Course Project** | **Apr 2025 – Jun 2025**
> A two-stage predictive pipeline that forecasts climatic conditions in Gyeongbuk and estimates subsequent wildfire probabilities.

---

## 📌 Project Overview
With the increasing frequency of large-scale wildfires due to global warming, proactive disaster management is critical. This project focuses on the **Gyeongbuk region**, South Korea, which has recently suffered record-breaking damage. We developed a **chained machine learning architecture** to provide long-term risk simulations.

## 🏗️ System Architecture
The system employs a **Dual-Model Pipeline** linked by an internal data-processing function.

### **1. Model 1: Weather Forecaster**
* **Input:** User-specified Year and Month.
* **Target:** Predicts Temperature, Wind Speed, and Precipitation.
* **Logic:** Captures long-term climatic trends from historical data (1938–2025).

### **2. Model 2: Wildfire Risk Predictor**
* **Input:** Meteorological outputs from Model 1 + Seasonal encoding.
* **Target:** Calculates the probability of wildfire occurrence.

### **3. External Function**
* Acts as a bridge to align data formats and converts "Month" into "Season" to enhance the predictive power of Model 2.

---

## 📊 Dataset & Feature Engineering

### **1. Data Sources**
* **Regional Weather:** KMA Weather Data Service (Gyeongbuk, South Korea).
* **Wildfire Records:** Zenodo Open Dataset (Global wildfire & climate metrics).

### **2. Key Engineering**
* **Trend Capture:** Created `LINEAR_TEMP_TREND` and `YEAR_SQUARED` for non-linear climate progression.
* **Standardization:** Unified diverse units (F/C, in/mm) and handled outliers using regional mean imputation.

---

## 🤖 Modeling & Evaluation

### **[Stage 1] Climate Forecasting**
* **Algorithm:** **Stacking Regressor**
    * *Base Learners:* CatBoost (Pattern capture) & Linear Regression (Trend extrapolation).
    * *Meta-Learner:* RidgeCV.
* **Performance:** Achieved robust R² scores for temperature-related variables.

### **[Stage 2] Wildfire Risk Prediction**
* **Algorithm:** **Random Forest Classifier**
* **Optimization:** Hyperparameter tuning via **Optuna** (Bayesian Optimization).
* **Metric:** Optimized using a custom weighted score of **ROC AUC** and **PR AUC** to address data imbalance.

---

## 📂 Directory Structure

```text
.
├── datasets/                 # Raw and processed datasets
├── notebooks/                # Experimentation & Logic
│   ├── model_1/              # Preprocessing & Modeling (Stage 1)
│   ├── model_2/              # Preprocessing & Modeling (Stage 2)
│   └── connecting_func/      # Chained pipeline integration
├── reports/                  # Proposal.pdf & Final_Report.pdf
├── images/                   # Visualizations for README
└── README.md
