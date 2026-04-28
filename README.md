# 🛒 M5 Walmart Supply Chain Digital Twin
### **End-to-End Medallion Architecture for Large-Scale Demand Forecasting**

[![Databricks](https://img.shields.io/badge/Platform-Databricks-orange?style=flat-square&logo=databricks)](https://www.databricks.com/)
[![Python](https://img.shields.io/badge/Language-Python-blue?style=flat-square&logo=python)](https://www.python.org/)
[![ML](https://img.shields.io/badge/Model-LightGBM-green?style=flat-square)](https://lightgbm.readthedocs.io/)

## 📊 Project Overview
This project implements a high-fidelity digital twin of Walmart’s supply chain, processing **30,490 products** across **10 stores** in 3 states (CA, TX, WI). Utilizing the **Medallion Architecture**, the system transforms **30M+ rows** of raw transactional data into a precision-engineered "Gold" forecast layer.

### 🎯 Key Performance Metrics
* **Forecast Bias:** **-1.68%** (Highly accurate, conservative estimate to minimize inventory waste).
* **Global Accuracy:** **98.3%** across all items and stores.
* **Error Metrics:** **1.96 RMSE** / **1.00 MAE**.
* **Resource Efficiency:** Reduced RAM footprint by **60%** through custom data-type optimization, enabling Big Data processing on a single-node free cluster.

---

## 🏗️ Technical Architecture (The Medallion Model)

### **🥉 Phase 1: Silver Layer (Data Engineering)**
* **Memory Optimization:** Implemented a custom downcasting utility to convert `float64` to `float32` and `int64` to `int16`, bypassing the hardware constraints of the Databricks Community Edition.
* **Signal Engineering:** Generated historical "Memory" features, including **7-day/28-day Lags** and **Rolling Moving Averages** to capture weekly and monthly demand momentum.
* **Contextual Joins:** Integrated **SNAP benefit schedules**, holiday markers, and historical **Selling Prices** to provide the model with socio-economic context.

### **🥈 Phase 2: The Forecasting Brain (Modeling)**
* **Global LightGBM Model:** Trained a single, unified regressor to learn shared demand patterns across all categories simultaneously.
* **Chronological Validation:** Enforced a strict time-series split, training on historical data and validating against a hidden **28-day future window** to ensure real-world generalizability.
* **Model Serialization:** Exported the trained booster as a persistent **Joblib artifact (.pkl)**, decoupling the model from the training environment for downstream deployment.

### **🥇 Phase 3: Gold Layer (Inference & Business Logic)**
* **Production Inference:** Loaded the model artifact to generate forecasts for the 850,000+ item-day combinations in the test set.
* **Business Safety:** Applied output clipping to ensure no negative sales predictions, aligning with retail physical constraints.
* **Analysis:** Performed **Feature Importance Analysis**, identifying that historical momentum and pricing signals are the primary drivers of stock-outs.

---
🚀 **Live Demo:** [M5 Walmart Supply Chain Digital Twin](https://huggingface.co/spaces/Akmr008/m5-walmart-supply-chain-digital-twin)

## 🛠️ Tech Stack
* **Environment:** Databricks (Community Edition)
* **Data Engineering:** Python (Pandas, NumPy)
* **Machine Learning:** LightGBM, Scikit-Learn
* **Operations:** Git, Model Serialization (Joblib), Parquet Storage

---

## 📂 Repository Structure
* `01_Data_Engineering_Silver.ipynb`: Ingestion, optimization, and signal engineering.
* `02_Model_Training_Evaluation.ipynb`: Model training, hyperparameter tuning, and serialization.
* `03_Gold_Layer_Inference.ipynb`: Final forecast generation and business metric reporting.
* `README.md`: Project documentation and impact summary.

---

## 🧠 Strategic Conclusion
The achievement of a **-1.68% forecast bias** demonstrates a robust system capable of enterprise-level accuracy. By mastering the hardware constraints of a free cloud tier, this project proves that strategic data engineering (downcasting and signal creation) is just as critical to machine learning success as the algorithm itself.
