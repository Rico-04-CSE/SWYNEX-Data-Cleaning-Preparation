# SWYNEX Task 1 – Data Cleaning & Preparation

## Project Overview

This project was completed for **Task 1: Data Cleaning & Preparation** of the SWYNEX Technologies internship.

The objective is to take a raw, intentionally messy cafe sales dataset, identify common data-quality problems, clean the data using Python, and prepare a final dataset suitable for analysis.

### Dataset

- **Dataset:** Dirty Cafe Sales
- **File:** `dirty_cafe_sales.csv`
- **Rows:** 10,000
- **Columns:** 8
- **Source:** Kaggle – Cafe Sales - Dirty Data for Cleaning Training
- **Dataset type:** Synthetic practice dataset created for data-cleaning training

Source:
https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training

---

## Task Requirements Covered

The project addresses the main requirements given in Task 1:

- Identify missing values
- Identify duplicate records
- Identify incorrect data types
- Identify inconsistent/invalid values
- Clean the dataset using Python
- Export a cleaned dataset
- Document the cleaning process in this README

---

## Dataset Columns

| Column | Description |
|---|---|
| Transaction ID | Unique transaction identifier |
| Item | Cafe item purchased |
| Quantity | Number of items purchased |
| Price Per Unit | Price of one item |
| Total Spent | Total transaction amount |
| Payment Method | Payment method used |
| Location | In-store or takeaway |
| Transaction Date | Date of the transaction |

---

## Problems Found in the Raw Dataset

Initial inspection showed the following issues:

### 1. Missing Values

Missing values were found in several columns.

| Column | Missing Values |
|---|---:|
| Item | 333 |
| Quantity | 138 |
| Price Per Unit | 179 |
| Total Spent | 173 |
| Payment Method | 2,579 |
| Location | 3,265 |
| Transaction Date | 159 |

### 2. Invalid Values

The dataset contains values such as:

- `ERROR`
- `UNKNOWN`

These values were treated as missing values because they do not represent valid information for analysis.

### 3. Incorrect Data Types

The raw CSV initially loaded most columns as `object` (text), including:

- Quantity
- Price Per Unit
- Total Spent
- Transaction Date

These columns were converted to appropriate numeric/date formats.

### 4. Duplicate Records

No duplicate rows were found in the original dataset.

The `Transaction ID` column was also checked for duplicate IDs, and no duplicate transaction IDs were found.

---

## Cleaning Method Used

The following cleaning steps were performed:

### Step 1 – Replace Invalid Values

`ERROR` and `UNKNOWN` were replaced with missing values (`NaN`).

### Step 2 – Convert Data Types

- `Quantity` → numeric
- `Price Per Unit` → numeric
- `Total Spent` → numeric
- `Transaction Date` → datetime

### Step 3 – Handle Missing Categorical Values

Missing values in:

- Item
- Payment Method
- Location

were filled using the **mode** (most frequent value).

### Step 4 – Handle Missing Numeric Values

Missing values in:

- Quantity
- Price Per Unit

were filled using the **median**.

Median was used because it is simple and less affected by extreme values.

### Step 5 – Handle Total Spent

For missing `Total Spent` values, the value was calculated using:

`Total Spent = Quantity × Price Per Unit`

Existing valid Total Spent values were retained.

### Step 6 – Handle Missing Dates

Missing transaction dates were filled using the median transaction date, which was:

`2023-07-02`

### Step 7 – Final Validation

After cleaning:

- Missing values = 0
- Duplicate rows = 0
- Transaction IDs remain unique
- Numeric columns have numeric data types
- Transaction Date is stored as a datetime-compatible date
- Dataset contains 10,000 rows and 8 columns

---

## Tools Used

- Python
- Google Colab
- Pandas
- NumPy

The project intentionally uses beginner-friendly Python and Pandas code.

---

## Google Colab Workflow

The project can be performed in Google Colab using the following workflow:

1. Open Google Colab.
2. Upload `dirty_cafe_sales.csv`.
3. Import Pandas and NumPy.
4. Load the CSV file.
5. Inspect the dataset.
6. Check missing values.
7. Check duplicate records.
8. Check data types.
9. Identify `ERROR` and `UNKNOWN` values.
10. Clean the dataset.
11. Validate the cleaned data.
12. Export `cleaned_cafe_sales.csv`.

---

## Final Output

The main output of this project is:

`cleaned_cafe_sales.csv`

The cleaned dataset contains **10,000 rows and 8 columns** and is prepared for further analysis.

---

## Project Structure

```text
SWYNEX-Data-Cleaning-Preparation/
│
├── dirty_cafe_sales.csv
├── cleaned_cafe_sales.csv
└── README.md
```

---

## Learning Outcome

Through this task, I learned how to:

- Load CSV data using Pandas
- Inspect a dataset before cleaning
- Identify missing values
- Identify duplicate records
- Detect invalid values such as `ERROR` and `UNKNOWN`
- Convert columns to appropriate data types
- Handle missing categorical and numerical data
- Create calculated values using existing columns
- Validate a cleaned dataset
- Export the final dataset as a CSV file
- Document a data-cleaning project for GitHub
