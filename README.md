# Financial Data Analysis Pipeline

A Python pipeline that extracts financial metrics from PDF, Excel, and CSV financial files, cleans and stores the data in SQLite, calculates financial KPIs with pandas and SQL, and exports Power BI-ready reports and charts.

# What This Project Does

This project takes financial files from an input folder and turns them into a clean dataset for analysis.

The pipeline:

1. Reads PDF, Excel, or CSV financial files
2. Extracts key financial values
3. Organizes the data into a structured table
4. Stores the cleaned data in a SQLite database
5. Calculates financial KPIs using pandas and SQL
6. Exports CSV files for Power BI
7. Creates basic charts for quick checking

# Supported Input Files

Put all input files inside the `input_files/` folder.

Supported file types:

- `.pdf`
- `.xlsx`
- `.xls`
- `.csv`

# File Naming

Use this file name format when possible:

company_year_month.filetype

Examples:

company_a_2024_01.csv  
company_b_2024_02.xlsx  
company_c_april_2024.pdf  

The pipeline uses the file name to identify:

- company
- year
- month
- period
- source file
- source type

Example:

company_a_2024_01.csv

is read as:

company = company_a  
year = 2024  
month = 01  
period = 2024-01  
source_type = csv  

# CSV Input

CSV files should already be organized in columns.

Recommended CSV columns:

company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings

Example:

company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings  
company_a,2024,01,500000,300000,120000,450000,900000,300000,200000,150000  
company_b,2024,01,400000,300000,80000,500000,750000,250000,180000,100000  

# PDF and Excel Input

PDF and Excel files should include recognizable financial labels, such as:

Service revenue  
Sales revenue  
Net income  
Total operating expenses  
Total assets  
Total current assets  
Total current liabilities  
Retained earnings  

The parser searches for these labels and extracts the matching values.

# Why CSV, Excel, and PDF Inputs Look Different

The input instructions are different because each file type stores data differently.

CSV files are usually already structured, so the pipeline reads columns directly.

Excel files may have multiple sheets, blank rows, or messy formatting, so the pipeline converts the sheet into text and searches for financial labels.

PDF files are usually the messiest, so the pipeline extracts text and searches for financial labels.

Even though the input formats are different, the final goal is the same:

turn financial files into one clean dataset for analysis.

# KPIs Calculated

The pipeline calculates:

- Total revenue
- Profit margin
- Operating expense ratio
- Current ratio
- Asset-to-liability ratio

Formulas:

total_revenue = service_revenue + sales_revenue

profit_margin = net_income / total_revenue

operating_expense_ratio = operating_expenses / total_revenue

current_ratio = current_assets / liabilities

asset_to_liability_ratio = total_assets / liabilities

# Setup Instructions

Before running the project, install the required packages:

pip install pandas matplotlib pdfplumber openpyxl

# How to Run

1. Put your PDF, Excel, or CSV files inside the `input_files/` folder.

2. Run the script:

python3 financial_pipeline.py

If your computer uses `python` instead of `python3`, run:

python financial_pipeline.py

# Output

The pipeline creates an `output/` folder with:

- `financial_data_with_kpis.csv`
- `financial_analysis.db`
- `all_records.csv`
- `sql_calculated_kpis.csv`
- `highest_profit_margin.csv`
- `strongest_liquidity.csv`
- `largest_total_assets.csv`
- `revenue_by_company.csv`
- `revenue_by_period.csv`
- `average_profit_margin_by_company.csv`
- chart images

The main file for Power BI is:

output/financial_data_with_kpis.csv

# Power BI Dashboard

Use `financial_data_with_kpis.csv` in Power BI to create:

- KPI cards
- revenue charts
- profit margin charts
- company comparisons
- period trends
- financial summary tables

# Privacy Note

Do not upload private financial statements to a public GitHub repository.

For portfolio use, use public reports, anonymized files, or synthetic sample data.

# Future Improvements

Possible future upgrades:

- Add more flexible financial label matching
- Add support for scanned PDFs or OCR
- Add data validation checks
- Add optional AI-generated summaries from already-computed KPI results
- Add a Streamlit app for uploading files
- Build a full Power BI dashboard

# Project Purpose

I built this project to connect my quantitative research background with business data analysis. It practices common data analyst tasks: cleaning messy data, storing records in a database, calculating KPIs, writing SQL queries, and preparing outputs for dashboard reporting.
