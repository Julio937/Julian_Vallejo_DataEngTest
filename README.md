# Technical_Test_Repo

**Minero Financial Reports Scraper**

This repository contains:

* A Selenium- and Requests-based pipeline (Task 1) to download quarterly “Consolidated Financial Statements” PDFs (Q1–Q4) for years 2021–2025 from the Mineros Investors site into `bronze/<year>_Q<quarter>/` and record metadata.
* A PDF-to-Parquet transformation (Task 2) to extract all tables from the Q1 2025 report into a normalized long format, saving to `silver/q1_2025_tables.parquet`.

## Prerequisites and Dependencies Installation

1. **Python 3.8+** installed and available on PATH.
2. **Chromedriver** matching your Chrome version.
3. Install Python dependencies:

   ```bash
   pip install pandas pyarrow requests selenium nbconvert pdfplumber
   ```

## Exact Commands to Run Each Task Individually

1. **Task 1 – Execute extraction notebook**:

   * Change to the extraction directory (replace `<YOUR_PROJECT_PATH>`):

     ```bat
     cd /d "<YOUR_PROJECT_PATH>/task1"
     ```

     \*Example: \**`cd C:/Downloads/DataEngineer_TechnicalTest/repo/task1`*
   * Activate your Python environment if needed (e.g., `conda activate myenv`)
   * Execute the notebook:

     ```bat
     python -m nbconvert --to notebook --execute extraction_notebook.ipynb --ExecutePreprocessor.timeout=600
     ```

2. **Task 2 – Table extraction & silver-layer**:

   * Change to the silver transformation directory (replace `<YOUR_PROJECT_PATH>`):

     ```bat
     cd /d "<YOUR_PROJECT_PATH>/task2/silver"
     ```

     \*Example: \**`cd D:/DataEngineer_TechnicalTest/Julian_Vallejo_DataEngTest/task2/silver`*
   * Execute the notebook:

     ```bat
     python -m nbconvert --to notebook --execute bronze_to_silver.ipynb --ExecutePreprocessor.timeout=600
     ```

## Complete Pipeline Execution Instructions

### Bronze extraction

This script will:

* Launch a headless Chrome browser
* Close the cookies popup if present
* Iterate year tabs 2021–2025
* Expand all accordion sections
* Download only the “Consolidated Financial Statements” PDF files
* Save each PDF to `bronze/<year>_Q<quarter>/`
* Compute and append metadata to `bronze/metadata_bronze.parquet`

### Silver transformation

This notebook will:

* Read the Q1 2025 Consolidated Financial Statements PDF from `bronze/2025_Q1/`
* Extract all structured tables into a long, normalized format
* Save the combined tables to `silver/q1_2025_tables.parquet`

## Expected Outputs and File Locations

* **Downloaded PDFs**: `bronze/2021_Q1/`, …, `bronze/2025_Q4/`
* **Metadata file**: `bronze/metadata_bronze.parquet`
* **Table output**: `silver/q1_2025_tables.parquet`
* Fields: `table_name`, `row_label`, `column_header`, `value`, `currency`, `page_number`

## Estimated Execution Time

* **Cold start** (no files downloaded): \~2–3 minutes (network-dependent)
* **Subsequent runs** (idempotent, skips existing): \~30–60 seconds

*Last updated: August 3, 2025*
