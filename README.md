# SQL Project - Data Cleaning: Layoffs 2022

## Overview
This project focuses on cleaning and standardizing the "Layoffs 2022" dataset from Kaggle to ensure data accuracy, usability, and readiness for analysis. The dataset contains records of company layoffs, including details such as company names, industries, dates, and other associated metrics.

**Dataset Source**: [Layoffs 2022 on Kaggle](https://www.kaggle.com/datasets/swaptr/layoffs-2022)


**Key Objectives**:
1. **Ensure data integrity**: Remove duplicates, correct inconsistencies, and standardize entries.
2. **Handle missing data**: Identify and appropriately address null or blank values.
3. **Prepare data for analysis**: Eliminate irrelevant rows and columns, and structure the dataset to facilitate exploratory data analysis (EDA).


How to Use
1. Clone or download the dataset from Kaggle.
2. Import the dataset into your SQL environment.
3. Run the provided SQL scripts sequentially to clean the data, see [data cleaning.sql](<Data Cleaning.sql>).
4. Use the cleaned table (world_layoffs.layoffs_staging2) for your analysis.


---

## Steps in Data Cleaning Process

### 1. **Setting Up a Staging Table**
   - Created a staging table (`world_layoffs.layoffs_staging`) to work on the raw data while preserving the original dataset.
   - Used the `CREATE TABLE ... LIKE` and `INSERT ... SELECT` commands to duplicate the structure and content of the staging table.


---

### 2. **Removing Duplicates**
   - Identified duplicates using the `ROW_NUMBER()` function with a `PARTITION BY` clause.
   - Retained only unique rows by deleting entries where `row_num > 1`.
   - Introduced an additional column (`row_num`) temporarily to help filter duplicates.


---

### 3. **Standardizing Data**
   - **Industry Column**:
     - Replaced blanks with `NULL` for easier handling.
     - Populated missing values by referencing other entries for the same company.
     - Standardized variations in industry names (e.g., `Crypto Currency` and `CryptoCurrency` → `Crypto`).
   - **Country Column**:
     - Removed trailing punctuation (e.g., `United States.` → `United States`).
   - **Date Column**:
     - Converted string date formats to a consistent `DATE` format using `STR_TO_DATE` and modified the column type.


---

### 4. **Handling Null Values**
   - Retained null values in numeric columns (e.g., `total_laid_off`, `percentage_laid_off`, `funds_raised_millions`) for accurate calculations during analysis.
   - Removed rows where both `total_laid_off` and `percentage_laid_off` were null as these provided no usable data.

---

### 5. **Removing Irrelevant Data**
   - Eliminated the temporary column (`row_num`) after duplicates were handled.
   - Dropped rows and columns deemed unnecessary for analysis.

---

## Final Dataset Structure
After cleaning, the dataset in `world_layoffs.layoffs_staging2` is:
- Ready for exploratory analysis with consistent and standardized data.
- Free of duplicates and irrelevant rows/columns.
- Structured to allow straightforward queries and computations.

---

## SQL Highlights
Key SQL techniques used:
- **Data Duplication and Staging**:
  ```sql
  CREATE TABLE world_layoffs.layoffs_staging LIKE world_layoffs.layoffs;
  INSERT INTO world_layoffs.layoffs_staging SELECT * FROM world_layoffs.layoffs;

---

Future Enhancements
Implement automated scripts for periodic data cleaning.
Develop visualizations using tools like Power BI or Tableau to explore trends in layoffs by industry, geography, and time.
Author: Joseph Maldonado
Location: Charlotte, NC
Skills Applied: SQL, Data Cleaning, Data Standardization
