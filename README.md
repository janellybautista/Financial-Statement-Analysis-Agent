# Financial Data Analysis Pipeline

A Python pipeline that extracts financial metrics from **PDF, Excel, and CSV financial files**, cleans and stores the data in **SQLite**, calculates financial KPIs with **pandas and SQL**, and exports **Power BI-ready reports and charts**.

---

## What This Project Does

This project takes financial files from an input folder and turns them into a clean dataset for analysis.

```text
PDF / Excel / CSV files
        ↓
Python extraction and cleaning
        ↓
SQLite database
        ↓
KPI calculations with pandas and SQL
        ↓
CSV outputs and charts
        ↓
Power BI dashboard
```

The pipeline:

1. Reads PDF, Excel, or CSV financial files
2. Extracts key financial values
3. Organizes the data into a structured table
4. Stores the cleaned data in a SQLite database
5. Calculates financial KPIs using pandas and SQL
6. Exports CSV files for Power BI
7. Creates basic charts for quick checking

---

## Supported Input Files

Place all files inside the `input_files/` folder.

| File Type | Extension | How the Pipeline Reads It |
|---|---|---|
| PDF | `.pdf` | Extracts text and searches for financial labels |
| Excel | `.xlsx`, `.xls` | Reads all sheets in the workbook and searches for financial labels |
| CSV | `.csv` | Reads structured columns directly |

Excel files can contain one or more sheets. The pipeline reads all sheets in the workbook, so users do not need to split each sheet into a separate Excel file.

Note: For cleaner analysis, each PDF or Excel file should represent one company/entity and one reporting period when possible. If one workbook contains multiple companies or periods across different sheets, the parser may need additional logic to separate them correctly.

---

## File Naming Format

Use this format when possible:

```text
company_year_month.filetype
```

Examples:

```text
company_a_2024_01.csv
company_b_2024_02.xlsx
company_c_april_2024.pdf
```

The pipeline uses the file name to identify metadata.

Example:

```text
company_a_2024_01.csv
```

is read as:

| Field | Value |
|---|---|
| company | `company_a` |
| year | `2024` |
| month | `01` |
| period | `2024-01` |
| source_type | `csv` |

---

## CSV Input Format

CSV files should already be organized in columns.

Recommended columns:

```text
company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings
```

Example:

```csv
company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings
company_a,2024,01,500000,300000,120000,450000,900000,300000,200000,150000
company_b,2024,01,400000,300000,80000,500000,750000,250000,180000,100000
company_c,2024,01,600000,200000,150000,420000,1000000,350000,220000,180000
```

If `company`, `year`, or `month` are missing from the CSV, the pipeline will try to extract them from the file name.

---

## PDF and Excel Input Format

PDF and Excel files should include recognizable financial labels, such as:

```text
Service revenue
Sales revenue
Net income
Total operating expenses
Total assets
Total current assets
Total current liabilities
Retained earnings
```

The parser searches for these labels and extracts the matching values.

Note: The parser currently uses regex patterns for common financial labels. If a PDF or Excel file uses different wording, abbreviations, or unusual formatting, the patterns in `financial_pipeline.py` may need to be updated.

---

## KPIs Calculated

| KPI | Formula |
|---|---|
| Total revenue | `service_revenue + sales_revenue` |
| Profit margin | `net_income / total_revenue` |
| Operating expense ratio | `operating_expenses / total_revenue` |
| Current ratio | `current_assets / liabilities` |
| Asset-to-liability ratio | `total_assets / liabilities` |

---

## Setup Instructions

Install the required packages:

```bash
pip install pandas matplotlib pdfplumber openpyxl
```

---

## How to Run

1. Add your files to the `input_files/` folder.

Example:

```text
input_files/
├── company_a_2024_01.csv
├── company_b_2024_01.xlsx
└── company_c_2024_01.pdf
```

2. Run the pipeline:

```bash
python3 financial_pipeline.py
```

If your computer uses `python` instead of `python3`, run:

```bash
python financial_pipeline.py
```

---

## Output

The pipeline creates an `output/` folder.

Main outputs:

```text
output/
├── financial_data_with_kpis.csv
├── financial_analysis.db
├── all_records.csv
├── sql_calculated_kpis.csv
├── highest_profit_margin.csv
├── strongest_liquidity.csv
├── largest_total_assets.csv
├── revenue_by_company.csv
├── revenue_by_period.csv
├── average_profit_margin_by_company.csv
├── total_revenue_by_company.png
├── profit_margin_by_company.png
└── total_revenue_by_period.png
```

The main file for Power BI is:

```text
output/financial_data_with_kpis.csv
```

---

## Power BI Dashboard

Use `financial_data_with_kpis.csv` in Power BI to create:

- KPI cards
- revenue charts
- profit margin charts
- company comparisons
- period trends
- financial summary tables

Suggested dashboard fields:

| Dashboard Element | Fields |
|---|---|
| KPI cards | `total_revenue`, `net_income`, `profit_margin`, `current_ratio` |
| Revenue chart | `company`, `total_revenue` |
| Profitability chart | `company`, `profit_margin` |
| Time trend | `period`, `total_revenue` |
| Slicers | `company`, `year`, `month`, `source_type` |

---

## Privacy Note

Do not upload private financial statements to a public GitHub repository.

For portfolio use, use:

- public financial reports
- anonymized files
- synthetic sample data

This repository should not include private school, company, vendor, employee, donor, or student financial information.

---

## Future Improvements

- Add more flexible financial label matching
- Add support for scanned PDFs or OCR
- Add data validation checks
- Add optional AI-generated summaries from already-computed KPI results
- Add a Streamlit app for uploading files
- Build a full Power BI dashboard

---

## Project Purpose

I built this project to connect my quantitative research background with business data analysis.

It practices common data analyst tasks:

- cleaning messy data
- storing records in a database
- calculating KPIs
- writing SQL queries
- preparing outputs for dashboard reporting
