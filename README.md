# Data_Cleaning_process
# Hotel Booking Demand - Data Cleaning Project

## 📋 Project Overview

This project is focused on cleaning the **Hotel Booking Demand Dataset** from Kaggle, which includes hotel reservation data collected from July 2015 to August 2017. The dataset features booking details from both city and resort hotels and contains 32 columns with 119,390 rows in its original form.

The goal of this project was to transform the raw dataset into an analysis-ready format by:
- Identifying and handling missing values
- Removing duplicate and near-duplicate records
- Detecting and treating outliers
- Correcting data inconsistencies and invalid values
- Validating data integrity
- Documenting the cleaning process

---


---

## 🔧 Key Tasks Performed

### ✅ Missing Value Handling
- Filled missing values in:
  - `children`: Replaced with 0 (assumed no children)
  - `country`: Replaced with `'Unknown'`
  - `agent` and `company`: Replaced with 0 (no agent/company involved)

### ✅ Duplicate & Outlier Removal
- Removed exact and near-duplicate rows
- Treated outliers in:
  - `lead_time` using Z-score (removed rows with Z > 3)
  - `adr` using IQR method

### ✅ Inconsistency Fixes
- Dropped rows with total guests = 0
- Standardized `country` values to uppercase
- Handled invalid values in `meal` and other categories
- Converted `reservation_status_date` to datetime format

### ✅ Feature Engineering
- `total_guests` = `adults` + `children` + `babies`
- `total_stay_nights` = `stays_in_weekend_nights` + `stays_in_week_nights`
- `season` = derived from arrival month
- `estimated_total_spend` = `adr` × `total_guests` × `total_stay_nights`

### ✅ Validation
- Checked that all guest counts > 0
- Verified arrival years were between 2015 and 2017
- Removed invalid negative values in ADR

---

## 📦 Dataset Source

> [Hotel Booking Demand Dataset on Kaggle](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)

---

## ▶️ How to Run

1. Open `data_cleaning_process.ipynb` in Jupyter Notebook or Google Colab.
2. Run all cells from top to bottom.
3. Cleaned output will be saved in the `/data/` and `/reports/` folders.

---

## 👤 Author

- **Student Name:** *M.N.P.Wickramarathna*
- **Course:** Intelligent Systems
- **Institution:** *Horizon Campus*
- **Date:** *2025-07-29*

---

## 📃 License

This project is developed solely for academic purposes and is not intended for commercial use.

---


