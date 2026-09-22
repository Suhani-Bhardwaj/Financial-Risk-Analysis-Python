# Financial Risk Analysis with Python – Barclays

## Project Overview

This project analyzes Barclays financial transactional data using Python to understand transaction behavior, build customer account profiles, identify financial risk indicators, detect unusual transactions, and generate business insights.

The analysis covers:

* Data cleaning and formatting
* Descriptive transaction analysis
* Credit and Debit classification
* Account-level transaction analysis
* Customer activity segmentation
* Average balance segmentation
* Transaction volume segmentation
* Financial risk identification
* Anomaly detection using the IQR method
* Data visualization
* Statistical hypothesis testing

The project uses **rule-based and statistical techniques** and does not use machine learning or deep learning models.

---

## Project Objectives

The main objectives of this project are to:

* Clean and standardize financial transactional data.
* Analyze monthly and yearly transaction patterns.
* Classify transactions into Credit and Debit categories.
* Identify top and bottom accounts based on the project's transaction-value metric.
* Detect dormant or inactive accounts.
* Segment accounts based on transaction frequency.
* Segment accounts based on average account balance.
* Segment accounts based on transaction volume.
* Identify high transaction-value accounts.
* Identify high-frequency low-balance accounts.
* Identify accounts with negative balances.
* Detect frequent large withdrawals.
* Identify overdraft transactions.
* Measure account balance volatility.
* Detect unusual transaction amounts using the IQR method.
* Identify accounts showing suspicious financial behavior based on multiple risk indicators.
* Perform an independent t-test and one-way ANOVA.
* Generate visualizations for transaction behavior and financial risk analysis.

---

# Dataset

The project uses the following dataset:

**`Barclays_Financial_Transactional_Data.csv`**

The dataset contains:

* **800 transaction records**
* **15 columns**
* Transaction data covering **January 2023 to June 2024**

### Main Columns

| Column              | Description                                       |
| ------------------- | ------------------------------------------------- |
| `TransactionID`     | Unique identifier for each transaction            |
| `CustomerID`        | Unique customer identifier                        |
| `AccountID`         | Unique account identifier                         |
| `AccountType`       | Type of customer account                          |
| `TransactionType`   | Type of transaction                               |
| `Product`           | Financial product associated with the transaction |
| `Firm`              | Firm/company information                          |
| `Region`            | Geographic region                                 |
| `Manager`           | Assigned manager                                  |
| `TransactionDate`   | Date of transaction                               |
| `TransactionAmount` | Monetary value of the transaction                 |
| `AccountBalance`    | Account balance                                   |
| `RiskScore`         | Financial risk score                              |
| `CreditRating`      | Customer credit rating                            |
| `TenureMonths`      | Customer/account tenure in months                 |

---

# Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* SciPy
* Jupyter Notebook

---

# Project Workflow

The project is divided into six major tasks:

1. Data Cleaning and Formatting
2. Descriptive Transactional Analysis
3. Customer Profile Building
4. Financial Risk Identification
5. Data Visualization
6. Hypothesis Testing

---

# Task 1: Data Cleaning and Formatting

The dataset was first inspected and cleaned before performing the analysis.

## Data Cleaning Steps

The following steps were performed:

* Displayed the first five records.
* Checked dataset dimensions.
* Examined column names.
* Checked data types and dataset information.
* Generated descriptive statistics.
* Checked missing values.
* Checked duplicate records.
* Removed commas, dollar signs, and extra spaces from financial fields.
* Converted `TransactionAmount` and `AccountBalance` into numeric format.
* Converted `TransactionDate` into datetime format.
* Standardized `AccountType` values using trimming and title case.
* Standardized `TransactionType` values using trimming and title case.

### Cleaning Output

The cleaned dataset was saved as:

`Output/Cleaned_Barclays_Data.csv`

---

# Task 2: Descriptive Transactional Analysis

## Credit and Debit Classification

The dataset does not directly contain Credit and Debit labels.

Therefore, the following business rule was applied throughout the project.

### Credit Transactions

* Deposit

### Debit Transactions

* Withdrawal
* Payment
* Transfer

The resulting `TransactionCategory` column contains:

* Credit
* Debit
* Other

---

## Monthly Transaction Analysis

The project creates:

* Month
* Year
* Monthly Credit Summary
* Monthly Debit Summary
* Monthly Net Transaction Summary
* Yearly Transaction Summary

### Net Transaction Formula

**Net Transaction = Total Credits − Total Debits**

The analysis covers **18 months from January 2023 to June 2024**.

Debit transaction amounts were higher than credit transaction amounts in every analyzed month, resulting in a negative monthly net transaction value throughout the period.

### Output Files

* `Output/Monthly_Credit_Summary.csv`
* `Output/Monthly_Debit_Summary.csv`
* `Output/Monthly_Transaction_Summary.csv`
* `Output/Yearly_Transaction_Summary.csv`

---

## Top Accounts Based on Transaction Value

The notebook groups transactions by `AccountID` and calculates the **sum of `TransactionAmount`** for each account.

The 10 accounts with the highest aggregate transaction amount were identified.

The notebook refers to this metric as **net inflow**, although the implementation is based on the total of the transaction amounts rather than a separate Credit-minus-Debit calculation at account level.

### Output

`Output/Top_Performing_Accounts.csv`

### Visualization

`Images/top_performing_accounts.png`

---

## Bottom Accounts Based on Transaction Value

The 10 accounts with the lowest aggregate transaction amount were identified using the same account-level calculation.

### Output

`Output/Bottom_Performing_Accounts.csv`

### Visualization

`Images/bottom_performing_accounts.png`

---

## Dormant or Inactive Accounts

An account was considered dormant when the gap between two consecutive transactions for the same account was:

**60 days or more**

This is a **project-specific criterion** used for this analysis.

The analysis identified:

* **317 transaction records** associated with qualifying 60+ day gaps
* **166 unique accounts** with at least one qualifying gap

### Output

`Output/Dormant_Accounts.csv`

---

# Task 3: Customer Profile Building

The project builds account profiles using:

* Transaction frequency
* Average account balance
* Transaction volume

---

## Customer Activity Levels

Activity levels were defined according to the total number of transactions performed by each account.

| Activity Level  | Criteria                 |
| --------------- | ------------------------ |
| High Activity   | More than 7 transactions |
| Medium Activity | 4–7 transactions         |
| Low Activity    | Less than 4 transactions |

The dataset contains **193 unique accounts**.

### Visualization

`Images/customer_activity_levels.png`

---

## Balance Segmentation

Average account balance was calculated for each account.

Accounts were then divided into three balance segments using the **33rd and 66th percentile thresholds**:

* Low Balance
* Medium Balance
* High Balance

The calculated thresholds were based on the distribution of average account balances.

### Visualization

`Images/balance_segments.png`

---

## Transaction Volume Segmentation

Transaction volume was calculated as the **sum of transaction amounts associated with each account** during the analysis period.

Accounts were divided into:

* Low Volume
* Medium Volume
* High Volume

using the **33rd and 66th percentile thresholds**.

This segmentation identifies accounts with comparatively higher monetary transaction activity.

### Visualization

`Images/transaction_volume_segments.png`

---

## High Transaction-Value Accounts

The 10 accounts with the highest aggregate transaction amount were identified as high transaction-value accounts.

### Output

`Output/High_Net_Inflow_Accounts.csv`

---

## High-Frequency Low-Balance Accounts

Accounts were identified using both:

* Medium or High Activity
* Low Balance

These accounts combine relatively high transaction frequency with comparatively low average balances and may require additional monitoring or customer engagement.

### Output

`Output/High_Frequency_Low_Balance.csv`

---

## Accounts with Negative or Near-Zero Average Balance

The project also checks accounts whose **average account balance is less than or equal to zero**.

### Output

`Output/Negative_Balance_Accounts.csv`

For this dataset, the resulting output contains **no accounts** meeting this specific average-balance criterion.

This analysis is separate from the overdraft analysis in Task 4, which checks individual transaction records with negative account balances.

---

# Task 4: Financial Risk Identification

Several rule-based and statistical techniques were used to identify potential financial risk indicators.

---

## Frequent Large Withdrawals

A withdrawal was considered large when its transaction amount was greater than or equal to the **75th percentile (Q3)** of all withdrawal transactions.

The calculated threshold was approximately:

**75,853.67**

There were:

* **210 withdrawal transactions**
* **53 large-withdrawal transactions**
* **45 unique accounts** associated with those large withdrawals

### Output

`Output/Frequent_Large_Withdrawals.csv`

Accounts with repeated large withdrawals may require additional review as part of financial risk monitoring.

---

## Overdraft Accounts

An overdraft transaction was identified when:

**`AccountBalance < 0`**

The dataset contains:

* **14 transaction records**
* **14 unique accounts**

with negative account balances.

### Output

`Output/Overdraft_Accounts.csv`

Negative account balances may indicate overdraft situations and can be considered for additional financial monitoring.

---

## Balance Volatility

Balance volatility was measured using the **standard deviation of account balances for each account**.

A higher standard deviation indicates greater variation in account balance across the available transactions.

### Output

`Output/Balance_Volatility.csv`

---

## Transaction Amount Anomalies

The **Interquartile Range (IQR)** method was used to identify unusually high or low transaction amounts.

### IQR Formula

**IQR = Q3 − Q1**

### Lower Bound

**Q1 − 1.5 × IQR**

### Upper Bound

**Q3 + 1.5 × IQR**

For this dataset, the calculated boundaries were approximately:

* **Lower bound:** -27,901.92
* **Upper bound:** 135,395.34

Transactions outside these boundaries were classified as anomalies.

The analysis identified:

**7 anomalous transaction records**

### Output

`Output/Transaction_Anomalies.csv`

An anomaly represents an unusual transaction amount according to the statistical rule. It does **not** by itself confirm fraud.

---

## Suspicious Transaction Behaviour

For this project, an account was classified as suspicious if it met **at least one** of the following conditions:

* Frequent large withdrawals
* Negative account balance
* Presence of anomalous transactions

These conditions were combined using a set-based approach to create a broader financial risk screening measure.

### Result

**57 unique accounts** were identified as suspicious according to the project's defined criteria.

### Output

`Output/Suspicious_Accounts.csv`

Suspicious accounts should be interpreted as accounts requiring additional review, not as confirmed fraudulent accounts.

---

# Task 5: Data Visualization

The project includes visualizations covering transaction behavior, account balances, customer segmentation, credit ratings, and financial risk.

## Visualizations

### 1. Transaction Amount Distribution

Shows the distribution of transaction amounts and helps identify the overall range and extreme values.

`Images/transaction_amount_distribution.png`

### 2. Account Balance Distribution

Shows the distribution of account balances across transaction records.

`Images/account_balance_distribution.png`

### 3. Transaction Amount by Account Type

Compares the **average transaction amount** across different account types.

`Images/accounttype_transaction_amount.png`

### 4. Average Risk Score by Region

Compares average risk scores across different regions.

`Images/riskscore_region.png`

### 5. Credit Rating Distribution

Shows the distribution of credit rating values in the dataset.

`Images/credit_rating_distribution.png`

### 6. Customer Activity Levels

Shows the distribution of accounts across High, Medium, and Low activity levels.

`Images/customer_activity_levels.png`

### 7. Monthly Credit vs Debit Trend

Compares monthly Credit and Debit transaction amounts.

`Images/monthly_credit_vs_debit.png`

### 8. Balance Segmentation

Shows the distribution of accounts across Low, Medium, and High Balance segments.

`Images/balance_segments.png`

### 9. Transaction Volume Segmentation

Shows the distribution of accounts across Low, Medium, and High transaction-volume segments.

`Images/transaction_volume_segments.png`

### 10. Top Performing Accounts

Shows the 10 accounts with the highest aggregate transaction amount according to the project's account-level metric.

`Images/top_performing_accounts.png`

### 11. Bottom Performing Accounts

Shows the 10 accounts with the lowest aggregate transaction amount according to the project's account-level metric.

`Images/bottom_performing_accounts.png`

---

# Task 6: Hypothesis Testing

Two statistical tests were performed to examine relationships between account balances and customer segmentation.

A significance level of:

**α = 0.05**

was used.

---

## Independent t-Test

### Objective

To compare average account balances between:

* High Transaction Volume accounts
* Low Transaction Volume accounts

### Null Hypothesis (H₀)

There is no significant difference in average account balance between High Transaction Volume and Low Transaction Volume accounts.

### Alternative Hypothesis (H₁)

High Transaction Volume accounts have significantly higher average account balances than Low Transaction Volume accounts.

### Result

* **t-statistic:** -0.553
* **p-value:** 0.5813

Since the p-value is greater than 0.05, the null hypothesis was not rejected.

Based on this dataset and test, there was no statistically significant difference in average account balances between the compared transaction-volume groups.

---

## One-Way ANOVA

### Objective

To determine whether average account balances differ among:

* High Activity accounts
* Medium Activity accounts
* Low Activity accounts

### Null Hypothesis (H₀)

The average account balance is the same across High, Medium, and Low Activity groups.

### Alternative Hypothesis (H₁)

At least one activity group has a significantly different average account balance.

### Result

* **F-statistic:** 0.5957
* **p-value:** 0.5522

Since the p-value is greater than 0.05, the null hypothesis was not rejected.

Based on this dataset and test, there was no statistically significant difference in average account balances across the High, Medium, and Low Activity groups.

---

# Key Findings

## Data Cleaning

* Financial transaction data was inspected and cleaned.
* Financial fields were converted into numeric format.
* Transaction dates were converted to datetime format.
* Account types and transaction categories were standardized.
* Missing values and duplicate records were checked.
* A cleaned dataset was generated.

## Transaction Analysis

* The dataset contains 800 transaction records.
* Transactions were classified into Credit and Debit categories.
* Debit transaction amounts were higher than credit transaction amounts in every analyzed month.
* Monthly and yearly transaction summaries were generated.
* Top and bottom accounts were identified using the project's aggregate transaction-value calculation.
* Accounts with transaction gaps of 60 days or more were identified.

## Customer Profiling

* 193 unique accounts were analyzed.
* Accounts were classified into High, Medium, and Low Activity groups.
* Accounts were segmented using average account balance.
* Accounts were segmented using transaction volume.
* High transaction-value accounts were identified.
* High-frequency low-balance accounts were identified.
* Accounts with average balances less than or equal to zero were checked.

## Financial Risk Analysis

* Large withdrawals were identified using the 75th percentile threshold.
* 45 accounts were associated with large withdrawal transactions.
* 14 accounts had negative account-balance transactions.
* Account balance volatility was calculated using standard deviation.
* 7 transaction records were identified as IQR-based anomalies.
* 57 unique accounts were identified through the combined suspicious-account criteria.

## Statistical Analysis

* An independent t-test was performed.
* A one-way ANOVA was performed.
* Both tests produced p-values greater than 0.05.
* The analysis did not find statistically significant differences in average account balances for the tested groups.

---

# Business Recommendations

Based on the analytical results, the project suggests the following areas for financial monitoring and customer management:

* Monitor accounts with negative account balances.
* Review accounts associated with repeated large withdrawals.
* Investigate transactions identified as statistical anomalies.
* Review accounts showing multiple risk indicators.
* Use activity and balance segmentation to understand different customer groups.
* Consider targeted financial products and engagement strategies for high-value customer segments.
* Use additional verification before treating unusual transactions as potential financial misconduct or fraud.

---

# Project Outputs

## Output Files

```text
Output/
├── Balance_Volatility.csv
├── Bottom_Performing_Accounts.csv
├── Cleaned_Barclays_Data.csv
├── Dormant_Accounts.csv
├── Frequent_Large_Withdrawals.csv
├── High_Frequency_Low_Balance.csv
├── High_Net_Inflow_Accounts.csv
├── Monthly_Credit_Summary.csv
├── Monthly_Debit_Summary.csv
├── Monthly_Transaction_Summary.csv
├── Negative_Balance_Accounts.csv
├── Overdraft_Accounts.csv
├── Suspicious_Accounts.csv
├── Top_Performing_Accounts.csv
├── Transaction_Anomalies.csv
└── Yearly_Transaction_Summary.csv
```

## Visualization Files

```text
Images/
├── accounttype_transaction_amount.png
├── account_balance_distribution.png
├── balance_segments.png
├── bottom_performing_accounts.png
├── credit_rating_distribution.png
├── customer_activity_levels.png
├── monthly_credit_vs_debit.png
├── riskscore_region.png
├── top_performing_accounts.png
├── transaction_amount_distribution.png
└── transaction_volume_segments.png
```

---

# Repository Structure

```text
Financial-Risk-Analysis-Python/
│
├── .gitattributes
├── Barclays_Financial_Risk_Analysis.ipynb
├── Barclays_Financial_Transactional_Data.csv
├── README.md
│
├── Images/
│   ├── accounttype_transaction_amount.png
│   ├── account_balance_distribution.png
│   ├── balance_segments.png
│   ├── bottom_performing_accounts.png
│   ├── credit_rating_distribution.png
│   ├── customer_activity_levels.png
│   ├── monthly_credit_vs_debit.png
│   ├── riskscore_region.png
│   ├── top_performing_accounts.png
│   ├── transaction_amount_distribution.png
│   └── transaction_volume_segments.png
│
└── Output/
    ├── Balance_Volatility.csv
    ├── Bottom_Performing_Accounts.csv
    ├── Cleaned_Barclays_Data.csv
    ├── Dormant_Accounts.csv
    ├── Frequent_Large_Withdrawals.csv
    ├── High_Frequency_Low_Balance.csv
    ├── High_Net_Inflow_Accounts.csv
    ├── Monthly_Credit_Summary.csv
    ├── Monthly_Debit_Summary.csv
    ├── Monthly_Transaction_Summary.csv
    ├── Negative_Balance_Accounts.csv
    ├── Overdraft_Accounts.csv
    ├── Suspicious_Accounts.csv
    ├── Top_Performing_Accounts.csv
    ├── Transaction_Anomalies.csv
    └── Yearly_Transaction_Summary.csv
```

---

# Limitations

* The analysis is based on the available historical dataset.
* The dataset contains 800 transaction records.
* The analysis covers January 2023 to June 2024.
* Risk identification is based on predefined business rules and statistical techniques.
* The project does not use machine learning or deep learning.
* The suspicious-account classification is a risk-screening approach and does not confirm fraud.
* IQR-based anomalies indicate unusual transaction amounts according to the statistical rule and require further investigation.
* The analysis is not a real-time financial monitoring system.
* The findings are specific to the available dataset and the criteria implemented in the notebook.
* The project uses a project-defined 60-day transaction-gap criterion for identifying dormant accounts.

---

# Future Enhancements

The project can be extended by:

* Developing a machine learning model for financial risk prediction.
* Implementing advanced anomaly detection techniques.
* Building a real-time transaction monitoring system.
* Adding an interactive dashboard using Power BI or Streamlit.
* Creating automated risk alerts.
* Incorporating additional customer and transaction features.
* Using historical labeled cases to develop supervised fraud or risk prediction models.

---

# Skills Demonstrated

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* SciPy
* Data Cleaning
* Exploratory Data Analysis
* Financial Data Analysis
* Account Segmentation
* Statistical Analysis
* Hypothesis Testing
* Independent t-Test
* One-Way ANOVA
* Anomaly Detection
* IQR Analysis
* Data Visualization
* Business Insight Generation

---

# Project Type

**Python Data Analytics & Financial Risk Analysis**

This project demonstrates the use of Python-based data analysis, statistical testing, account segmentation, visualization, and rule-based risk screening to transform transactional financial data into customer and financial insights.

---

# Author

**Suhani**
