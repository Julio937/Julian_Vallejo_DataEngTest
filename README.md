# Technical_Test_Repo
**Minero Financial Reports Scraper**

This repository contains a Selenium- and Requests-based pipeline to download quarterly “Consolidated Financial Statements” PDFs (Q1–Q4) for years 2021–2025 from the Mineros Investors site, store them under `bronze/<year>_Q<quarter>/`, and record metadata in a Parquet file.

## Prerequisites and Dependencies Installation

1. **Python 3.8+** installed and available on PATH.
2. **Chromedriver** matching your Chrome version, placed in your PATH or project directory.
3. Install Python dependencies:

   ```bash
   pip install pandas pyarrow requests selenium nbconvert
   ```

## Exact Commands to Run Each Task Individually

1. **Task 1 – Execute extraction notebook**:
   - Change to your notebook directory (replace <YOUR_PROJECT_PATH>):
   ```bash
   cd /d "<YOUR_PROJECT_PATH>\task1"
   ```
   example:
   
   ```bash
   cd C:\Downloads\DataEngineer_TechnicalTest\repo\task1
   ```
   - Execute the notebook:
   ```bash
   python -m nbconvert --to notebook --execute extraction_notebook.ipynb --ExecutePreprocessor.timeout=600
   ```

## Complete Pipeline Execution Instructions


This script will:

* Launch a headless Chrome browser
* Close the cookies popup if present
* Iterate year tabs 2021–2025
* Expand all accordion sections
* Download only the “Consolidated Financial Statements” PDF files
* Save each PDF to `bronze/<year>_Q<quarter>/`
* Compute and append metadata to `bronze/metadata_bronze.parquet`

## Expected Outputs and File Locations

* **Downloaded PDFs**: `bronze/2021_Q1/`, `bronze/2021_Q2/`, …, `bronze/2025_Q4/`
* **Metadata file**: `bronze/metadata_bronze.parquet`

  * Contains columns: `filename`, `filesize`, `sha256`, `download_timestamp`

## Estimated Execution Time

* **Cold start** (no files downloaded): \~2–3 minutes (depends on network latency)
* **Subsequent runs** (idempotent, skips existing): \~30–60 seconds

---

*Last updated: August 3, 2025*
