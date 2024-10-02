# CSR Spending and Beneficiaries: Nigerian Banks
## About
###
This dataset contains information on corporate social responsibility (CSR) spending by major Nigerian banks, including Zenith Bank, Guaranty Trust Bank (GT Bank), First Bank of Nigeria, Ecobank Nigeria, Wema Bank, Access Bank, United Bank for Africa (UBA), Diamond Bank, Union Bank of Nigeria, and Fidelity Bank. The dataset tracks quarterly CSR expenditures (Q1, Q2, Q3, and Q4) and the number of beneficiaries impacted by these initiatives over several years.
## Table of Contents
- [Introduction](#introduction)
  - [Brief Overview of The Project](#brief-overview-of-the-project)
  - [Purpose of The Analysis](#purpose-of-the-analysis)
  - [Data Sources](#data-sources)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
  - [Data Loading](#data-loading)
  - [Handling Missing Values](####handling-missing-values)
  - [Outlier Detection and Treatment](#outlier-detection-and-treatment)
  - [Data Normalization or Standardization](#data-normalization-or-standardization)
  - [Other Useful Data Cleaning Processes](#other-useful-data-cleaning-processes)

### Exploratory Data Analysis (EDA)
* Summary statistics
* Data visualization (charts, graphs)
* Correlations and relationships

### Analysis of CSR Spending
* Total CSR spending
* Spending by category (e.g., education, healthcare, community development)
* Spending by bank
* Trends over time

### Analysis of Beneficiaries
* Number of beneficiaries
* Beneficiary demographics (e.g., age, gender, location)
* Impact of CSR initiatives on beneficiaries

### Conclusion
* Key findings
* Limitations of the analysis
* Recommendations for future research
  
## Introduction
### Brief Overview of the Project
This project involves analyzing a large dataset containing corporate social responsibility (CSR) spending data from several leading Nigerian banks. The dataset includes information on CSR activities, including total amounts spent across different months and regions, the number of beneficiaries impacted, and distinctions based on quarterly periods. The analysis focuses on identifying spending patterns, regional distributions of beneficiaries, and seasonal variations in CSR activities to provide valuable insights into the social outreach efforts of these financial institutions.

### Purpose of the Analysis
The purpose of this analysis is to uncover key insights into the CSR efforts of Nigerian banks by exploring:
- **Spending Patterns**: How CSR expenditures vary across different months, quarters, and regions.
- **Beneficiary Impact**: Analyzing the number of beneficiaries in different regions and understanding the correlation between spending and beneficiaries.
- **Seasonal and Regional Trends**: Detecting peaks in spending during key periods such as holidays and summer months, and identifying which regions receive more CSR efforts.
This analysis aims to help stakeholders understand the social outreach strategies of banks and guide future CSR initiatives to achieve maximum social impact.

### Data Sources
The dataset used for this analysis is *synthetic* but modeled to reflect realistic CSR spending patterns for 10 major Nigerian banks:
- Zenith Bank
- Guaranty Trust Bank (GT Bank)
- First Bank of Nigeria
- Ecobank Nigeria
- Wema Bank
- Access Bank
- United Bank of Nigeria
- Diamond Bank
- Union Bank of Nigeria
- Fidelity Bank

The dataset includes 50,000 records with the following columns:
- **Bank**: The bank responsible for the CSR expenditure.
- **Month**: The month when the CSR activities occurred (e.g., Jan, Feb, etc.).
- **Quarter**: The quarter of the year (Q1, Q2, Q3, Q4).
- **Total_Amount_Spent**: The total amount spent on CSR activities during that period.
- **Beneficiaries**: The number of individuals benefiting from the CSR activities.
- **Region**: The region where the CSR activity took place, categorized into North Central (NC), North East (NE), North West (NW), South West (SW), South East (SE), and South South (SS).

## Data Cleaning and Preparation
#### 1. Data Loading
- The CSR dataset is first loaded into Excel using the **Import from Text/CSV** option in the **Data** tab. This process imports the raw dataset for analysis.
#### 2. Handling Missing Values
**Step 1**: Identify missing values
- To identify missing values in Excel, use conditional formatting:
  - Select the entire dataset.
  - Navigate to the **Home** tab -> **Conditional Formatting** -> **New Rule**.
  - Choose **Format only cells that contain**, and select **Blanks**.
  - Apply a format (e.g., a light red fill) to highlight missing values.

---

**Step 2**: Handle missing values
- For columns like `Total_Amount_Spent` or `Beneficiaries`, missing values can be imputed using either the average or median.
  - Formula to calculate the average:
    ```excel
    =IF(ISBLANK(C2), AVERAGE(C:C), C2)
    ```
  - This formula replaces missing values in column C (Total Amount Spent) with the average of the column.
  - Similarly, apply this to other numerical columns like `Beneficiaries`.

---

#### 3. Outlier Detection and Treatment

**Step 1**: Detecting outliers using the **Interquartile Range (IQR) method**.
- Calculate Q1 (25th percentile) and Q3 (75th percentile) for numerical columns (e.g., `Total_Amount_Spent`).
  - Formula for Q1:
    ```excel
    =PERCENTILE(C:C, 0.25)
    ```
  - Formula for Q3:
    ```excel
    =PERCENTILE(C:C, 0.75)
    ```
- Calculate IQR:
  ```excel
  =Q3 - Q1
  ```
- Outliers are data points below Q1 - 1.5 * IQR or above Q3 + 1.5 * IQR.

**Step 2**: Handling outliers
- Replace outliers with the median:
  - Formula to handle outliers:
    ```excel
    =IF(OR(C2<Q1 - 1.5*IQR, C2>Q3 + 1.5*IQR), MEDIAN(C:C), C2)
    ```
  - This formula replaces outliers in the `Total_Amount_Spent` column with the median value.

---

#### 4. Data Normalization or Standardization

**Step 1**: Normalization using **Min-Max Scaling**
- To normalize values in the `Total_Amount_Spent` column, you can use Min-Max scaling:
  ```excel
  = (C2 - MIN(C:C)) / (MAX(C:C) - MIN(C:C))
  ```
  This formula transforms values to a range between 0 and 1.

**Step 2**: Standardization using **Z-Score**
- To standardize the values in `Total_Amount_Spent`:
  ```excel
  = (C2 - AVERAGE(C:C)) / STDEV(C:C)
  ```
  This formula converts the data into a standard normal distribution (mean 0, standard deviation 1).

---

#### 5. Changing Month Abbreviations (e.g., Jan, Feb, Sep) to Full Month Names

**Step 1**: Create a lookup table
- Create a table with abbreviated months and full month names in two columns (e.g., `E1:F12`):
  - Cell `E1`: `Jan`, Cell `F1`: `January`
  - Cell `E2`: `Feb`, Cell `F2`: `February`
  - Continue for all months.

**Step 2**: Use the `VLOOKUP` function to replace abbreviations
- Formula to convert abbreviated months to full names:
  ```excel
  =VLOOKUP(B2, $E$1:$F$12, 2, FALSE)
  ```
  This formula looks up the abbreviated month in column `B` (e.g., "Jan") and returns the full month name from the lookup table.

**Step 3**: Place the full month names in a new column next to the existing month column.

---

#### 6. Splitting the `Region` Column into Two Separate Columns

**Step 1**: Separate `South` and `(SS)` into two columns
- The `Region` column contains values like `South (SS)`. To split this into two columns:
  - Formula to extract the first part (`South`):
    ```excel
    =LEFT(F2, FIND("(", F2)-2)
    ```
  - Formula to extract the second part (`SS`):
    ```excel
    =MID(F2, FIND("(", F2)+1, LEN(F2)-FIND("(", F2)-1)
    ```
  - The `LEFT` formula extracts the text before the parentheses, and the `MID` formula extracts the text inside the parentheses.

**Step 2**: Apply this to all rows to create two separate columns: one for the region name (e.g., "South") and one for the abbreviation (e.g., "SS").

---

### Other Useful Data Cleaning Processes

- **Removing duplicates**: To ensure there are no duplicate records, select the dataset and go to **Data** -> **Remove Duplicates**.
- **Standardizing case**: Ensure consistent capitalization in the `Bank` and `Region` columns by using:
  ```excel
  =PROPER(A2)
  ```
  This formula converts text to title case (capitalizing the first letter of each word).
- **Handling inconsistent entries**: For any inconsistencies in categorical data (e.g., different spellings of the same bank), use the `Find and Replace` feature (`Ctrl + H`) to standardize the names.

---

This covers the complete data cleaning and preparation process for your CSR dataset in Excel.
