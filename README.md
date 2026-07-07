# 🧹 Sales Order Data Cleaning Project

Cleaning and standardizing a messy, real-world-style sales dataset using **Python** and **pandas** — turning 256 inconsistent records into a validated, analysis-ready dataset with zero missing values and zero duplicates.

---

## 📌 Why this project

Raw business data is rarely clean. Dates come in five different formats, category names get misspelled, order IDs get duplicated by accident, and prices show up with currency symbols mixed in. This project simulates that reality and solves it end-to-end using pandas — the same kind of cleanup that's often the first (and most underrated) step in any data analysis or reporting pipeline.

---

## 📊 Results at a glance

| Metric | Before | After |
|---|---|---|
| Total Rows | 256 | 169 |
| Duplicate Order IDs | 13 | 0 |
| Missing Values (total) | 205 | 0 |
| Date Formats in Use | 5+ | 1 (`DD-MM-YYYY`) |
| Category Spelling Variants | 6 | 4 |
| Invalid Quantity Entries | 34 | 0 |

---

## 🔧 What was wrong with the raw data

- **13 duplicate Order IDs** with gaps in the numeric sequence
- **Order Date** stored in 5+ formats interchangeably (`2024-08-04`, `02-07-2024`, `04/07/2024`, `May 04, 2024`)
- **Category** with inconsistent spelling/casing (`Stationery` vs `Stationary`, `electronics` vs `Electronics`)
- **Product Name** with inconsistent casing and double spaces
- **Payment Method** with mixed casing (`credit card`, `CASH`, `PayPal`) and 29 missing values
- **Quantity** containing a text value (`"five"`), plus zero/negative entries
- **Unit Price** stored as text with currency symbols (`$255.15`, `USD 332.33`)
- **205 missing values** spread across 6 columns

---

## 🛠️ How it was fixed

| Problem | Approach |
|---|---|
| Duplicate Order IDs | Scanned sequentially; renumbered or dropped based on surrounding sequence, instead of blindly deleting valid rows |
| Mixed date formats | Custom parser tried multiple known formats per value, then standardized output to one format |
| Category / Payment Method inconsistencies | Stripped whitespace, mapped inconsistent spellings via `.replace()`, applied `.str.title()` |
| Invalid Quantity | Replaced text (`"five"` → `5`); removed rows with zero/negative/missing quantity |
| Currency-formatted Unit Price | Regex to strip symbols/text while preserving decimal points, then converted to numeric |
| Missing values | Filled with sensible defaults/derived values (e.g. `Total Sales = Quantity × Unit Price`) instead of dropping rows outright |

Full step-by-step methodology and code is in cleaning.ipynb.

---

## 💡 Key decisions worth highlighting

- **Didn't just drop duplicates** — checked whether the duplicate ID was a data-entry error (renumber) or a true accidental repeat (drop), to avoid losing valid orders.
- **Didn't assume one date format** — built a small multi-format parser instead of guessing, since a single wrong assumption would've silently corrupted valid dates.
- **Didn't drop every row with a missing value** — filled columns like `Total Sales` and `Customer Email` using derived logic, preserving more usable data.

---

## 📁 Repository Structure

```
├── sample_sales_data_messy.xlsx     # Raw, uncleaned dataset
├── cleaning.ipynb                   # Full cleaning pipeline (Python/pandas)
├── cleaned_sales_data.xlsx          # Final cleaned output
├── Sales_Data_Cleaning_Report.docx  # Detailed written report
└── README.md
```

---

## 🧰 Tools Used

- Python 3
- pandas
- Jupyter Notebook
- Microsoft Excel (source format)

---

## 🚀 What I'd improve next

- Standardize casing in the `Sales Rep` column (a few entries remain lowercase, e.g. `john smith`)
- Automate format detection using regex-based classification instead of a fixed list of formats
- Add unit tests to validate the cleaning pipeline against new incoming data

---

## 📄 Full Report

A detailed write-up with methodology, before/after tables, and challenges faced is available in Sales_Data_Cleaning_Report.docx


