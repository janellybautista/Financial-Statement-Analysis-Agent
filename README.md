# Financial-Statement-Analysis-Agent
A pipeline that extracts financial metrics from company filings, cleans and stores them in SQL, analyzes trends and ratios, and exports Excel-ready reports and dashboards with optional AI-generated summaries.

# Setup Instructions

Before running `analysis_agent.py`, follow these steps:

1. **Initialize OpenAI by adding the API key**:
   In the script, initialize the OpenAI client by adding your API key:
   ```python
   client = OpenAI(api_key="type_key_here")

2. **Modify the input file path**:
  Go to the "Main script" and update the input file path to point to your PDF:
   ```python
   pdf_path = "Add_path_to_Sample_Financial_Statements.pdf"

# Output

This agent analyzes the imported PDF with OpenAI, plots the relevant data from the file and generates a LaTeX report. 



# Financial Data Analysis Pipeline

This project is a Python-based financial data analysis pipeline that extracts financial information from PDF, Excel, and CSV files, organizes the data into structured tables, stores the results in a SQLite database, calculates financial KPIs using pandas and SQL, and exports clean datasets for reporting in Power BI.

The goal of this project is to practice a full data analyst workflow:

Messy financial files → Python extraction/cleaning → SQLite database → KPI calculations → CSV outputs → Power BI dashboard

## Features

- Reads financial data from PDF, Excel, and CSV files
- Extracts company/entity, year, month, period, source file, and file type from file names
- Organizes financial fields into a structured dataset
- Stores cleaned data in a SQLite database
- Calculates financial KPIs using pandas and SQL
- Exports CSV files for Power BI
- Generates basic Python charts for quick visual checks

## Project Structure

financial-data-analysis-pipeline/
├── financial_pipeline.py
├── input_files/
├── output/
├── README.md
└── requirements.txt

## Input File Instructions

Place all files inside the `input_files/` folder before running the pipeline.

This project supports:

- PDF files: `.pdf`
- Excel files: `.xlsx` or `.xls`
- CSV files: `.csv`

## Recommended File Naming Format

Use this format:

companyname_year_month.filetype

Examples:

company_a_2024_01.csv  
company_a_2024_02.xlsx  
company_b_2024_01.pdf  
company_b_april_2024.xlsx  

The pipeline uses the file name to identify:

- company/entity
- year
- month
- reporting period
- source file
- file type

For example:

company_a_2024_01.csv

will be read as:

company: company_a  
year: 2024  
month: 01  
period: 2024-01  
source_type: csv  

## CSV Input Format

CSV files should use structured columns like this:

company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings

Example:

company,year,month,service_revenue,sales_revenue,net_income,operating_expenses,total_assets,current_assets,liabilities,retained_earnings  
company_a,2024,01,500000,300000,120000,450000,900000,300000,200000,150000  
company_b,2024,01,400000,300000,80000,500000,750000,250000,180000,100000  
company_c,2024,01,600000,200000,150000,420000,1000000,350000,220000,180000  

If `company`, `year`, or `month` are missing from the CSV, the pipeline will try to extract them from the file name.

## PDF and Excel Input Format

PDF and Excel files should contain recognizable financial labels such as:

Service revenue  
Sales revenue  
Net income  
Total operating expenses  
Total assets  
Total current assets  
Total current liabilities  
Retained earnings  

The parser searches for these labels and extracts the matching financial values.

Example file names:

company_a_2024_01.pdf  
company_b_2024_02.xlsx  

## KPIs Calculated

The pipeline calculates the following financial KPIs:

Total revenue = service_revenue + sales_revenue

Profit margin = net_income / total_revenue

Operating expense ratio = operating_expenses / total_revenue

Current ratio = current_assets / liabilities

Asset-to-liability ratio = total_assets / liabilities

## SQL Analysis

The pipeline stores the cleaned financial data in a SQLite database called:

output/financial_analysis.db

It also runs SQL queries to generate outputs such as:

- all financial records
- SQL-calculated KPIs
- highest profit margin
- strongest liquidity
- largest total assets
- revenue by company
- revenue by reporting period
- average profit margin by company

## Output Files

After running the pipeline, outputs are saved in the `output/` folder.

Main output files include:

financial_data_with_kpis.csv  
financial_analysis.db  
all_records.csv  
sql_calculated_kpis.csv  
highest_profit_margin.csv  
strongest_liquidity.csv  
largest_total_assets.csv  
revenue_by_company.csv  
revenue_by_period.csv  
average_profit_margin_by_company.csv  
total_revenue_by_company.png  
profit_margin_by_company.png  
total_revenue_by_period.png  

The main cleaned dataset for Power BI is:

output/financial_data_with_kpis.csv

## Power BI Use

The file `financial_data_with_kpis.csv` can be imported into Power BI to create a dashboard with:

- KPI cards for total revenue, net income, profit margin, current ratio, and asset-to-liability ratio
- bar charts comparing revenue by company
- bar charts comparing profit margin by company
- period-based revenue trends
- tables showing financial records and calculated KPIs
- slicers for company, year, month, period, and source type

## How to Run the Project

### 1. Install required packages

pip install pandas matplotlib pdfplumber openpyxl

### 2. Add input files

Create or open the `input_files/` folder and place your PDF, Excel, or CSV files inside it.

Example:

input_files/
├── company_a_2024_01.csv
├── company_b_2024_01.xlsx
└── company_c_2024_01.pdf

### 3. Run the pipeline

python3 financial_pipeline.py

If your system uses `python` instead of `python3`, run:

python financial_pipeline.py

### 4. Check the output folder

After the script runs, open the `output/` folder to view the generated files.

## Example Workflow

1. User places financial files in `input_files/`
2. Python reads PDF, Excel, or CSV files
3. The pipeline extracts financial values
4. Data is cleaned and organized into a structured table
5. KPIs are calculated with pandas
6. Data is saved to SQLite
7. SQL queries calculate and rank financial metrics
8. CSV files are exported for Power BI
9. Power BI dashboard visualizes the final results

## Privacy Note

Do not upload private or confidential financial statements to a public GitHub repository.

For portfolio or demo use, use:

- synthetic financial data
- public financial reports
- anonymized sample files

This repository should not include private school, company, vendor, employee, donor, or student financial information.

## Future Improvements

Possible future upgrades include:

- adding more flexible parsing rules for different financial statement formats
- supporting scanned PDFs with OCR or document parsing tools
- adding automated data validation checks
- building a full Power BI dashboard
- adding LLM-generated summaries from already-computed KPI results
- creating a Streamlit app for uploading files and viewing results interactively

## Project Purpose

I built this project to connect my quantitative research background with business data analysis. The project practices common data analyst tasks: cleaning messy financial data, organizing records in a database, calculating KPIs, writing SQL queries, and preparing outputs for dashboard reporting.
