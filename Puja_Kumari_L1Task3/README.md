# Task 3 - Cleaning Data

## Objective
Demonstrate professional-level data cleaning skills by taking a deliberately messy dataset and systematically transforming it into a clean, analysis-ready dataset, with every decision documented.

## Dataset
[Retail Store Sales: Dirty for Data Cleaning](https://www.kaggle.com/datasets/ahmedmohamed2003/retail-store-sales-dirty-for-data-cleaning) (Kaggle) — 12,575 transaction records built specifically for data cleaning practice.

## Tools Used
Python, pandas, numpy, Jupyter Notebook

## Cleaning Approach

**1. Data Quality Report:** Identified missing values in 5 columns (Item, Price Per Unit, Quantity, Total Spent, Discount Applied), confirmed 0 duplicate rows, and found categorical columns (Category, Payment Method, Location) already consistently formatted.

**2. Recalculation over imputation:** Since `Total Spent = Price Per Unit × Quantity`, missing values in any one of these three columns were recalculated from the other two where possible — a more accurate approach than dropping rows or filling with a generic average. This fully recovered `Price Per Unit`; the 604 rows missing both `Quantity` and `Total Spent` were handled by imputing `Quantity` with the median and recalculating `Total Spent`.

**3. Categorical imputation:** `Item` (1,213 missing, ~10%) was filled with `"Unknown Item"` rather than dropped, to avoid losing otherwise valid data in other columns.

**4. Judgment-based imputation:** `Discount Applied` (4,199 missing, ~33%) was filled with `False`, based on the reasoning that a high missing rate in a True/False field likely represents unrecorded "no discount" cases rather than truly unknown data — this assumption is explicitly documented in the notebook.

**5. Outlier detection (IQR method):** Found 60 outliers in `Total Spent`, all representing the mathematically maximum valid transaction (max Price × max Quantity = ₹410). Since the underlying values were legitimate, these were **retained** rather than removed.

## Before vs. After Summary

| Metric | Before | After |
|---|---|---|
| Null count | 4,229 (across 5 columns) | 0 |
| Duplicate count | 0 | 0 |
| Row count | 12,575 | 12,575 |
| Transaction Date dtype | text (str) | datetime64 |

## Output
Cleaned dataset saved to [`Dataset/retail_store_sales_cleaned.csv`](Dataset/retail_store_sales_cleaned.csv)

## Notebook
See [`Task3_Data_Cleaning.ipynb`](Task3_Data_Cleaning.ipynb) for the full analysis with code and detailed reasoning behind each cleaning decision.