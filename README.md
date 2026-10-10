# Data Wrangling Case Study: US Supply Chain GHG Emission Factors

## Project Overview
This project demonstrates the end-to-end data cleaning, wrangling, and restructuring of the **US EPA Supply Chain Greenhouse Gas (GHG) Emission Factors** dataset. The project traces the process of transforming messy, unformatted, and concatenated records into a standardized, production ready dataset.

---

## Data Wrangling Pipeline (From Raw to Sorted)

### 1. Initial State (Unsorted / Raw Sheet)
The initial raw dataset (`Supply_chain_emission_factors_U`) presented structural inconsistencies:
* **Tilde-Separated Strings (Rows 2–21):** All seven data attributes were merged into a single tilde delimited string in Column A (e.g., `111CA~Farms~carbon dioxide~kg/2018 USD, purchaser price~0.467~0.046~0.513`).
* **Pipe-Separated Strings (Rows 224–235):** Commodity sectors `622` (Hospitals), `623` (Nursing facilities), and `624` (Social assistance) had four metadata fields merged into Column B using pipe (`|`) delimiters (e.g., `Hospitals|carbon dioxide|kg/2018 USD...`), leaving essential target columns empty (`NaN`).
* **Unstructured Extra Columns:** Temporary parsing resulted in auxiliary, unaligned working columns (`Unnamed: 7` through `Unnamed: 13`).

### 2. Data Cleaning & Transformation Operations
* **Delimited Text Splitting (`~` Delimiters):** Used text splitting functions to separate concatenated records into distinct schema fields:
  - `Commodity Code`
  - `Commodity Name`
  - `Substance`
  - `Unit, purchaser price`
  - `Supply Chain Emission Factors without Margins`
  - `Margins of Supply Chain Emission Factors`
  - `Supply Chain Emission Factors with Margins`
* **Sub String Extraction (`|` Delimiters):** Parsed pipe delimited values in sector codes `622–624` to extract missing `Substance`, `Unit`, and baseline `Emission Factor` values into columns C, D, and E.
* **Schema Realignment & Column Consolidation:** Deleted redundant temporary working columns (columns H through N) and merged all parsed records into a single 7 column matrix.

### 3. Final State (Sorted / Cleaned Sheet)
The final sheet (`Sorted Supply_chain_emission_fa`) achieves a fully structured tabular format:
* **Schema Uniformity:** 264 entries aligned across 7 standardized columns.
* **Data Integrity:** Numeric fields (`Emission Factors`, `Margins`) converted to proper numeric formats (`float64`).
* **Completeness:** All concatenated fields expanded and properly populated across all industry sectors.

---

## Dataset Schema Reference

| Column Name | Description | Data Type | Example Value |
| :--- | :--- | :--- | :--- |
| **Commodity Code** | NAICS based industry/sector code | String / Numeric | `111CA` |
| **Commodity Name** | Description of the commodity/sector | String | `Farms` |
| **Substance** | Greenhouse gas category | String | `carbon dioxide` |
| **Unit**| Standard measurement metric | String | `kg/2018 USD, purchaser price` |
| **Purchaser price** | Standard measurement metric | String | ` purchaser price` |
| **Emission Factors w/o Margins** | Direct emission intensity | Float | `0.467` |
| **Margins** | Supply chain trade & transport margins | Float | `0.046` |
| **Emission Factors with Margins** | Total combined supply chain factor | Float | `0.513` |

---

## Tools & Technologies Used
* **Spreadsheet Software:** Google Sheets (SPLIT, Text-to-Columns)

## Background & Context
This project was completed as part of the **ALX Africa Data Science Program** to demonstrate practical data wrangling, schema standardization, and dataset cleaning using Google Sheets.
