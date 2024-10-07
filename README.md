# CSR Spending and Beneficiaries: Nigerian Banks
## About
###
This dataset contains information on corporate social responsibility (CSR) spending by major Nigerian banks, including Zenith Bank, Guaranty Trust Bank (GT Bank), First Bank of Nigeria, Ecobank Nigeria, Wema Bank, Access Bank, United Bank for Africa (UBA), Diamond Bank, Union Bank of Nigeria, and Fidelity Bank. The dataset tracks quarterly CSR expenditures (Q1, Q2, Q3, and Q4) and the number of beneficiaries impacted by these initiatives over several years.
## Table of Contents
- [About](#about)
- [Introduction](#introduction)
  - [Brief Overview of The Project](#brief-overview-of-the-project)
  - [Purpose of The Analysis](#purpose-of-the-analysis)
  - [Data Sources](#data-sources)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
  - [Data Loading](#1-data-loading)
  - [Handling Missing Values](#2-handling-missing-values)
  - [Changing Month Abbreviations](#3-changing-month-abbreviations-eg-jan-feb-sep-to-full-month-names)
  - [Splitting the Region Column into Two Separate Columns](#4-splitting-the-region-column-into-two-separate-columns)
  - [Other Useful Data Cleaning Processes](#other-useful-data-cleaning-processes)
- [Exploratory Data Analysis(EDA)](#exploratory-data-analysis-eda)
  - [Summary Statistics](#summary-statistics)
  - [Data Visualization]
  - [Correlations and Relationships]

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
- **Month**: The month when the CSR activities occurred.
- **Quarter**: The quarter of the year (Q1, Q2, Q3, Q4).
- **Total_Amount_Spent**: The total amount spent on CSR activities during that period.
- **Beneficiaries**: The number of individuals benefiting from the CSR activities.
- **Region**: The region where the CSR activity took place, categorized into North Central (NC), North East (NE), North West (NW), South West (SW), South East (SE), and South South (SS).

## Data Cleaning and Preparation
#### 1. Data Loading
- The CSR dataset is first loaded into Excel using the **Import from Text/CSV** option in the **Data** tab. This process imports the raw dataset for analysis.

---

#### 2. Handling Missing Values
**Step 1**: Identify missing values
- To identify missing values in Excel, use conditional formatting:
  - Select the entire dataset.
  - Navigate to the **Home** tab -> **Conditional Formatting** -> **New Rule**.
  - Choose **Format only cells that contain**, and select **Blanks**.
  - Apply a format (e.g., a light red fill) to highlight missing values.

**Step 2**: Handle missing values
- For columns like `Total_Amount_Spent` or `Beneficiaries`, missing values can be imputed using either the average or median.
  - Formula to calculate the average:
    ```excel
    =IF(ISBLANK(C2), AVERAGE(C:C), C2)
    ```
  - This formula replaces missing values in column C (Total Amount Spent) with the average of the column.
  - Similarly, apply this to other numerical columns like `Beneficiaries`.

---

#### 3. Changing Month Abbreviations (e.g., Jan, Feb, Sep) to Full Month Names

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

#### 4. Splitting the `Region` Column into Two Separate Columns

**Step 1**: Separate `South` and `(SS)` into two columns
- The `Region` column contains values like `South (SS)`. To split this into two columns:
  - Formula to extract the first part (`South`):
    ```excel
    =LEFT(F2, FIND("(", F2)-2)
    ```
**Step 2**: Changing "South" to "South South"
- Some values may be "South," which we want to change to "South South."
  - Formula to change `South` to `South South`
    ```excel
    =IF(H2="South", "South South", H2)
    ```

---

#### Other Useful Data Cleaning Processes

- **Removing duplicates**: To ensure no duplicate records, select the dataset and go to **Data** -> **Remove Duplicates**.
- **Standardizing case**: Ensure consistent capitalization in the `Bank` and `Region` columns by using:
  ```excel
  =PROPER(A2)
  ```
  This formula converts text to title case (capitalizing the first letter of each word).
- **Handling inconsistent entries**: For any inconsistencies in categorical data (e.g., different spellings of the same bank), use the `Find and Replace` feature (`Ctrl + H`) to standardize the names.

---

## Exploratory Data Analysis (EDA)
#### Summary Statistics

Below is a summary of key statistics for the dataset, including measures of central tendency, dispersion, and distribution of the CSR spending data across various banks.

| Statistic              | Value                  |
|------------------------|------------------------|
| **Total Rows**         | 50,000                 |
| **Total Columns**      | 6                      |
| **Distinct Banks**     | 10                     |
| **Time Period**        | 12 Months              |

#### CSR Spending (₦)

| Metric              | Value            |
|---------------------|------------------|
| **Mean (Average)**  | $32,012.72       |
| **Median**          | $30,824.13       |
| **Minimum Spending**| $5,000.35        |
| **Maximum Spending**| $74,991.07       |
| **Standard Deviation** | $16,731.67       |

#### Beneficiaries by Region

| Region             | Total Beneficiaries | Average Beneficiaries per Bank |
|--------------------|---------------------|--------------------------------|
| **South South (SS)** | 11,874,029        | 756                            |
| **South West (SW)**  | 8,582,222         | 754                            |
| **North Central (NC)** | 2,327,957       | 507                            |
| **North West (NW)**  | 2,332,157         | 506                            |
| **North East (NE)**  | 2,273,751         | 501                            |
| **South East (SE)**  | 4,672,951         | 509                            |

### Key Insights
- **Highest Spending:** Q3 has the highest spending across all banks, likely due to holiday and summer activities.
- **Beneficiaries:** The **South-South** region received the highest number of beneficiaries, followed by **South-West**.
- **Spending Patterns:** The spending fluctuates throughout the year, with peak spending during Q3.

## Correlations and Relationships
#### 1. CSR Spending Across Quarters (Q1, Q2, Q3, Q4)
- **Relationship:** Analyzing how CSR spending changes over time can reveal seasonal or cyclical trends, particularly focusing on quarters (Q1, Q2, Q3, Q4).
- **Analysis:** Calculating the correlation between spending in different quarters can uncover any patterns (e.g., whether high spending in one quarter predicts high spending in another).
- **Potential Insights:**
  - Positive correlation between **Q3** and **Q4** might suggest consistently high spending during the end of the year, due to summer and holiday activities.
  - Weak or negative correlation between **Q1** and **Q4** may indicate seasonal variations in spending.
**Example:**
```excel
=CORREL(B2:B50001, C2:C50001)  'Correlate Q1 and Q2 spending
```

#### 2. CSR Spending vs. Beneficiaries
- **Relationship:** Higher CSR spending may be correlated with an increase in the number of beneficiaries. You can assess if higher expenditures lead to more people benefiting from the CSR activities.
- **Analysis:** Compute the correlation between the **Total_Amount_Spent** and the **Beneficiaries** column to assess the relationship.
- **Potential Insights:**
  - A high positive correlation would suggest more spending results in more beneficiaries.
  - A low or no correlation could suggest spending is not always tied directly to beneficiary count (e.g., some high-cost projects may benefit fewer people).
**Example:**
```excel
=CORREL(D2:D50001, E2:E50001)  'Correlate spending with beneficiaries
```

#### 3. CSR Spending by Region
- **Relationship:** Spending levels might vary by region, revealing trends in how CSR budgets are geographically allocated.
- **Analysis:** Summarize the total spending per region and compare across all regions to identify patterns in how banks prioritize their CSR activities.
- **Potential Insights:**
  - South-South (SS) could receive more CSR funding than other regions, followed by South West (SW).
  - Regions with fewer funds and beneficiaries may suggest areas for CSR expansion or greater focus.
**Example (PivotTable):**
Summarize Total_Amount_Spent by Region to visualize spending distribution.

#### 4. Spending Trends Across Banks
- **Relationship:** Compare how different banks (e.g., Zenith Bank, GT Bank) allocate their CSR budgets to reveal trends or priorities.
- **Analysis:** Compare the total CSR spending across all banks to identify which banks are more committed to CSR activities.
- **Potential Insights:**
  - Larger banks like Zenith Bank or GT Bank are likely to spend more on CSR.
  - Similar spending patterns across banks might indicate industry-wide trends or shared priorities.
**Example (PivotTable):**
Summarize Total_Amount_Spent by Bank to analyze spending trends.

#### 5. Beneficiaries by Region
- **Relationship:** Investigating the number of beneficiaries in each region compared to CSR spending can highlight how resources are distributed.
- **Analysis:** By correlating the number of beneficiaries with CSR spending, you can assess if certain regions are receiving adequate attention based on their needs.
- **Potential Insights:**
  - South-South (SS) and South West (SW) are likely to have more beneficiaries due to higher CSR spending.
  - Northern regions may receive fewer beneficiaries if less spending is allocated to them.
**Example (Excel Formula):**
```excel
=CORREL(E2:E50001, F2:F50001)  'Correlate beneficiaries with regions
```
---
#### Example Insights from the CSR Dataset
- **Seasonal Spending:** A strong positive correlation between Q3 and Q4 may indicate a pattern of higher spending during the end of the year (e.g., due to holidays).
- **Regional Focus:** The South-South (SS) region is likely to receive the highest CSR funding, while other regions may require more focus.
- **Bank Comparison:** Larger banks (e.g., Zenith Bank, GT Bank) are likely to allocate more resources to CSR activities compared to smaller banks.
- **Beneficiary Distribution:** Higher CSR spending tends to correlate with a higher number of beneficiaries in regions with significant social needs (e.g., South-South and South West)
