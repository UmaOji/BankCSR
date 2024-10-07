# Corporate Social Responsibility: Nigerian Banks 
## About
###
This dataset contains information on corporate social responsibility (CSR) spending by major Nigerian banks, including Zenith Bank, Guaranty Trust Bank (GT Bank), First Bank of Nigeria, Ecobank Nigeria, Wema Bank, Access Bank, United Bank for Africa (UBA), Diamond Bank, Union Bank of Nigeria, and Fidelity Bank. The dataset tracks quarterly CSR expenditures (Q1, Q2, Q3, and Q4) and the number of beneficiaries impacted by these initiatives over several years.
## Table of Contents
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
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [Summary Statistics](#summary-statistics)
  - [Data Visualization]
  - [Correlations and Relationships](#correlations-and-relationships)
    - [CSR Spending by Region](#1-csr-spending-by-region)
    - [Spending Trends Across Banks](#2-spending-trends-across-banks)
    - [Beneficiaries by Region](#3-beneficiaries-by-region)
    - [Spending Trends Across CSR Areas](#4-spending-trends-across-csr-areas-eg-healthcare-education)

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
#### Brief Overview of the Project
This project involves analyzing a large dataset containing corporate social responsibility (CSR) spending data from several leading Nigerian banks. The dataset includes information on CSR activities, including total amounts spent across different months and regions, the number of beneficiaries impacted, and distinctions based on quarterly periods. The analysis focuses on identifying spending patterns, regional distributions of beneficiaries, and seasonal variations in CSR activities to provide valuable insights into the social outreach efforts of these financial institutions.

#### Purpose of the Analysis
The purpose of this analysis is to uncover key insights into the CSR efforts of Nigerian banks by exploring:
- **Spending Patterns**: How CSR expenditures vary across different months, quarters, and regions.
- **Beneficiary Impact**: Analyzing the number of beneficiaries in different regions and understanding the correlation between spending and beneficiaries.
- **Seasonal and Regional Trends**: Detecting peaks in spending during key periods such as holidays and summer months, and identifying which regions receive more CSR efforts.
This analysis aims to help stakeholders understand the social outreach strategies of banks and guide future CSR initiatives to achieve maximum social impact.

#### Data Sources
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
---
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
|------------------------|:------------------------:|
| **Total Rows**         | 50,000                 |
| **Total Columns**      | 6                      |
| **Distinct Banks**     | 10                     |
| **Time Period**        | 12 Months              |

#### CSR Spending (₦)

| Metric              | Value            |
|---------------------|:------------------:|
| **Mean (Average)**  | $32,012.72       |
| **Median**          | $30,824.13       |
| **Minimum Spending**| $5,000.35        |
| **Maximum Spending**| $74,991.07       |
| **Standard Deviation** | $16,731.67       |

#### Beneficiaries by Region

| Region               | Total Beneficiaries | Average Beneficiaries per Bank |
|----------------------|:-------------------:|:------------------------------:|
| **South South (SS)** | 11,874,029          | 756                            |
| **South West (SW)**  | 8,582,222           | 754                            |
| **North Central (NC)** | 2,327,957         | 507                            |
| **North West (NW)**  | 2,332,157           | 506                            |
| **North East (NE)**  | 2,273,751           | 501                            |
| **South East (SE)**  | 4,672,951           | 509                            |

#### Key Insights
- **Highest Spending:** Q3 has the highest spending across all banks, likely due to holiday and summer activities.
- **Beneficiaries:** The **South-South** region received the highest number of beneficiaries, followed by **South-West**.
- **Spending Patterns:** The spending fluctuates throughout the year, with peak spending during Q3.

## Correlations and Relationships
#### 1. CSR Spending by Region
- **Relationship:** Spending levels might vary by region, revealing trends in how CSR budgets are geographically allocated.
- **Analysis:** Summarize the total spending per region and compare across all regions to identify patterns in how banks prioritize their CSR activities.
- **Insights:**
  - South-South (SS) receive more CSR funding than other regions, followed by South West (SW).
  - Regions with fewer funds and beneficiaries like North-Central may suggest areas for CSR expansion or greater focus.
  
**Example (PivotTable):**  
Summarize Total_Amount_Spent by Region to visualize spending distribution.

#### 2. Spending Trends Across Banks
- **Relationship:** Compare how different banks (e.g., Zenith Bank, GT Bank) allocate their CSR budgets to reveal trends or priorities.
- **Analysis:** Compare the total CSR spending across all banks to identify which banks are more committed to CSR activities.
- **Insights:**
  - Diamond Bank and Ecobank Bank spend the most on CSR.
  - Zenith Bank spends the least on CSR.

**Example (PivotTable):**  
Summarize Total_Amount_Spent by Bank to analyze spending trends.

#### 3. Beneficiaries by Region
- **Relationship:** Investigating the number of beneficiaries in each region compared to CSR spending can highlight how resources are distributed.
- **Analysis:** Compare the number of beneficiaries with CSR spending. This will help assess if certain regions are receiving adequate attention based on their needs.
- **Insights:**
  - South-South (SS) and South West (SW) have more beneficiaries due to higher CSR spending with **15,703** and **11,380** beneficiaries respectively.
  - Northern regions have fewer beneficiaries due to fewer funds allocated to them.

**Example (PivotTable):**  
Summarize Total_Amount_Spent and Beneficiaries by Region to analyze spending distributions.

#### 4. Spending Trends Across CSR Areas (e.g., Healthcare, Education)
- **Relationship:** The analysis of spending trends across various Corporate Social Responsibility (CSR) areas, such as healthcare, education, environment, and community development, reveals the distinct patterns and priorities of organizations in their philanthropic efforts. By examining the relationship between spending in these areas, we can identify which sectors receive more funding and how this aligns with broader societal needs. 
- **Analysis:** Compare the total CSR spending across all banks to identify which banks are more committed to CSR activities.
- **Insights:**
  - **Healthcare Dominance**: The healthcare sector often receives one of the highest proportions of CSR spending, indicating a strong focus on public health and wellbeing. For example, during a health crisis, such as the COVID-19 pandemic, there is usually a significant spike in healthcare-related expenditures, overshadowing spending in other areas like education or community development. 
  - **Educational Investments**: Education spending tends to remain consistent with a total of **$323,622,057.15**, highlighting the long-term commitment of organizations to enhance educational opportunities, especially in underserved communities.
  - **Impact of External Factors**: Spending trends are highly responsive to current events and societal needs, with notable increases in areas like healthcare during crises.
  - **Emerging Focus Areas**: There is a growing trend towards environmental and community development initiatives, reflecting a shift in organizational priorities towards sustainability and social equity.

**Example (PivotTable):**  
Summarize Total_Amount_Spent and Beneficiaries by Region to analyze spending distributions.

---
