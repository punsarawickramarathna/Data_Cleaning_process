# Data Cleaning Report: Hotel Booking Demand Dataset

## Executive Summary

The Hotel Booking Demand dataset from Kaggle contains detailed information about hotel reservations made between July 2015 and August 2017 across two hotel types: city and resort. The primary goal of this data cleaning task was to prepare the dataset for exploratory data analysis and modeling by identifying and resolving missing values, removing duplicates and outliers, fixing inconsistencies, and validating logical constraints.

### Key Actions Taken:
- Replaced missing values in key columns (`children`, `country`, `agent`, `company`)
- Removed both exact and near-duplicate records
- Treated outliers in `adr` and `lead_time` using IQR and Z-score methods
- Standardized data formats and handled illogical guest combinations
- Engineered new features such as total stay nights, seasons, and estimated total spend
- Created a reproducible cleaning pipeline for future datasets

---

## Data Quality Assessment

### Original Dataset Characteristics:
- **Rows:** 119,390
- **Columns:** 32
- **Types:** Mixed (categorical, numerical, datetime)

### Identified Issues:
- **Missing Values:**
  - `children` had NaNs (likely meaning no children)
  - `country`, `agent`, and `company` contained nulls
- **Duplicates:**
  - ~40 exact duplicate records found
- **Outliers:**
  - Unreasonably high values in `lead_time` and `adr` skewed statistical metrics
- **Inconsistencies:**
  - Guest counts (`adults`, `children`, `babies`) summed to 0 in some rows
  - Categorical values like `meal` and `country` were not standardized
- **Date Formatting Issues:**
  - Inconsistent or unparsed dates in `reservation_status_date`

---

## Cleaning Methodology

### Missing Value Handling:
- `children`: Filled with 0 assuming no children
- `country`: Filled with `'Unknown'` to retain rows and indicate uncertainty
- `agent`, `company`: Filled with 0 indicating no agent/company involved

### Duplicates:
- Removed exact duplicates using `df.duplicated()`
- Removed near duplicates by comparing key columns like hotel, arrival date, and guests

### Outlier Detection & Treatment:
- Applied Z-score method to `lead_time`, removing rows with Z > 3
- Applied IQR method to `adr`, removing extreme high/low values outside IQR

### Inconsistency Fixes:
- Converted `country` codes to uppercase for consistency
- Converted `reservation_status_date` to proper datetime format
- Dropped rows where total number of guests (adults + children + babies) = 0
- Corrected invalid meal entries by mapping them to `'Undefined'`

### Feature Engineering:
- `total_guests`: Sum of adults, children, babies
- `total_stay_nights`: Sum of weekday and weekend nights
- `season`: Derived from month number
- `is_cancelled_flag`: Binary label from reservation status
- `estimated_total_spend`: ADR × nights × guests

### Data Validation:
- Ensured all guest counts were positive
- Confirmed all arrival years were between 2015 and 2017
- Removed rows with negative `adr` values

---

## Results and Impact

| Metric                    | Before Cleaning | After Cleaning  |
|--------------------------|----------------|-----------------|
| Rows                     | 119,390         | ~115,900        |
| Columns                  | 32              | 33 (added `total_guests`) |
| Missing Values           | 14,000+         | 0               |
| Duplicate Rows           | ~40             | 0               |
| Outliers Removed         | ~3,000+         | 0 remaining     |
| Invalid Guest Rows       | ~180            | 0               |

The final dataset is clean, consistent, and ready for analysis. Quality improvements make the dataset more reliable for forecasting, clustering, and visualization.

---

## Recommendations

- **Improve Data Entry Validation:** Enforce guest count > 0 at source system
- **Use Default Values Cautiously:** Instead of missing agent/company values, consider a dedicated `'None'` category
- **Log Data Provenance:** Track source channels and intermediaries for better segmentation
- **Standardize Input Forms:** Ensure uniform formats for country codes and categorical fields
- **Automate Cleaning Pipeline:** Use reusable Python functions to clean future hotel booking data consistently

---
>