# M5 Walmart Supply Chain Digital Twin

This project implements a high-scale demand forecasting system for 30,490 products across 10 Walmart stores. It utilizes the **Medallion Architecture** to process 30M+ rows of transactional data and trains a **Global LightGBM Model** for multi-step forecasting.

## 🚀 Project Status: Phase 1 Completed (2026-03-08)

### **Bronze to Silver: High-Scale Data Engineering**
We successfully transitioned from raw, compressed data to a machine-learning-ready Silver Layer.

- **Memory Optimization**: Implemented a custom downcasting utility to reduce the memory footprint of 30M+ rows by over **60%**, converting `float64` to `float32` and `int64` to `int16`.
- **Signal Engineering**: Generated historical "Signal" features including **7-day** and **28-day lags** and rolling moving averages.
- **Contextual Joins**: Integrated **Calendar Hooks** (SNAP benefits for CA, TX, and WI) and product **Selling Prices** into a single global table.
- **Data Persistence**: Finalized the Silver Layer and persisted it as an optimized **Parquet file** in Databricks Volumes for high-speed loading.



---

## 🛠️ Tech Stack
- **Environment**: Databricks (Spark Cluster)
- **Language**: Python (Pandas/NumPy)
- **Architecture**: Medallion (Bronze/Silver/Gold)
- **Storage**: Parquet (Optimized for 30M+ rows)

---

## 📊 Next Steps: Phase 2
The next sprint will focus on building the "brain" of the digital twin:
- **Global Model Training**: Implementing a single **LightGBM Regressor** to learn demand patterns across all 3,049 items simultaneously.
- **Time-Series Validation**: Setting up a strict chronological split (Training: Years 1-4 | Testing: Final 28 days) to ensure no data leakage.
- **Hyperparameter Tuning**: Optimizing the booster for RMSE (Root Mean Squared Error) to maximize forecasting accuracy.
