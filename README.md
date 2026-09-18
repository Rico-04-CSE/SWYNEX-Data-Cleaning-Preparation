# SWYNEX-Data-Cleaning-Preparation

**Task 1 — Data Cleaning & Preparation**
Internship: Data Analyst Internship, SWYNEX Technologies (Data & AI domain)

## Overview
This project cleans and prepares a real-world cafe sales transactions dataset that was intentionally built with common data quality issues, for practicing data cleaning in Python (pandas).

## Dataset
**Cafe Sales — Dirty Data for Cleaning Training**
- Source: [Kaggle](https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training)
- 10,000 transaction records, 8 columns: `Transaction ID`, `Item`, `Quantity`, `Price Per Unit`, `Total Spent`, `Payment Method`, `Location`, `Transaction Date`

## Files
| File | Description |
|---|---|
| `dirty_cafe_sales.csv` | Original raw dataset (before cleaning) |
| `SWYNEX_Data_Cleaning_Preparation.ipynb` | Jupyter/Colab notebook containing the full cleaning process |
| `cleaned_cafe_sales.csv` | Final cleaned dataset (after cleaning) |
| `README.md` | This file |

## Issues identified in the raw data
Explored with `.head()`, `.tail()`, `.shape`, `.info()`, `.isnull().sum()`, `.duplicated().sum()`, and `.value_counts()` on every column.

- **Missing values (blank cells)** across every column, heaviest in `Location` (3,265) and `Payment Method` (2,579)
- **Inconsistent placeholder values** — two different strings, `"ERROR"` and `"UNKNOWN"`, both used across every column to represent invalid/missing data instead of one consistent marker
- **Incorrect data types** — `Quantity`, `Price Per Unit`, and `Total Spent` were loaded as text, and `Transaction Date` as a plain string, because the `ERROR`/`UNKNOWN` placeholders mixed into those columns prevented pandas from inferring the correct type
- **Duplicate records** — checked both full-row duplicates (`.duplicated()`) and duplicate `Transaction ID`s; **0 found** in this dataset — a validation step worth doing even when the result comes back clean

## Cleaning steps performed
1. **Explored the data** — shape, dtypes, missing-value counts, and value counts per column, to understand the scope of the problem before touching anything
2. **Standardized inconsistent placeholders** — replaced every `"ERROR"` and `"UNKNOWN"` string with a proper `NaN`, so both are treated the same way instead of as two different "valid" categories
3. **Fixed data types**
   - `Quantity`, `Price Per Unit`, `Total Spent` → converted to numeric with `pd.to_numeric(errors="coerce")`
   - `Transaction Date` → converted to `datetime` with `pd.to_datetime(errors="coerce")`
4. **Handled missing values**
   - Categorical columns (`Item`, `Payment Method`, `Location`) → filled with the **mode** (most frequent value) of each column
   - Numeric columns (`Quantity`, `Price Per Unit`, `Total Spent`) → filled with the **median** of each column
   - Any `Total Spent` values still missing after that → recalculated as `Quantity × Price Per Unit`
   - `Transaction Date` → filled with the **median transaction date**
5. **Rounded values** — `Quantity` to whole numbers, `Price Per Unit` and `Total Spent` to 2 decimal places
6. **Validated the result** — re-ran `.isnull().sum()` and `.duplicated().sum()` to confirm zero missing values and zero duplicates before saving

## Before vs. After
| Metric | Before | After |
|---|---|---|
| Rows | 10,000 | 10,000 |
| Duplicate rows | 0 | 0 |
| Column dtypes | all text (`object`) | correct `int64` / `float64` / `datetime` |
| Missing values (total, incl. `"ERROR"`/`"UNKNOWN"`) | 10,082 across all columns | 0 |
| `Item` missing | 969 | 0 (filled with mode: `Juice`) |
| `Payment Method` missing | 3,178 | 0 (filled with mode: `Digital Wallet`) |
| `Location` missing | 3,961 | 0 (filled with mode: `Takeaway`) |
| `Quantity` / `Price Per Unit` / `Total Spent` missing | 479 / 533 / 502 | 0 / 0 / 0 |
| `Transaction Date` missing | 460 | 0 (filled with the median date) |

## How to reproduce
Open `SWYNEX_Data_Cleaning_Preparation.ipynb` in Jupyter or Google Colab, place `dirty_cafe_sales.csv` in the same directory (or upload it to Colab), and run all cells top to bottom. This produces `cleaned_cafe_sales.csv`.

## Submitted as part of
SWYNEX Technologies — Data Analyst Internship, Task 1: Data Cleaning & Preparation
