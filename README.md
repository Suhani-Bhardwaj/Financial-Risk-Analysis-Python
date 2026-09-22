# Financial Risk Analysis with Python – Barclays

## Project Overview

This project focuses on analyzing Barclays financial transactional data using Python to understand customer transaction behavior, identify financial risk indicators, build customer profiles, and generate meaningful business insights.

The analysis covers data cleaning, transaction analysis, customer segmentation, financial risk identification, anomaly detection, data visualization, and statistical hypothesis testing.

The project uses rule-based and statistical techniques rather than machine learning or deep learning models.

---

## Project Objectives

The main objectives of this project are to:

* Clean and standardize financial transactional data.
* Analyze monthly and yearly transaction patterns.
* Classify transactions into Credit and Debit categories.
* Identify top-performing and bottom-performing accounts based on net inflow.
* Detect dormant or inactive accounts.
* Segment customers based on activity, account balance, and transaction volume.
* Identify accounts with financial risk indicators.
* Detect frequent large withdrawals and overdraft accounts.
* Measure account balance volatility.
* Detect unusual transaction amounts using the IQR method.
* Identify accounts showing suspicious transaction behavior.
* Perform statistical hypothesis testing using an independent t-test and one-way ANOVA.
* Generate visualizations to communicate financial and customer insights.

---

## Dataset

The project uses the following dataset:

**Barclays_Financial_Transactional_Data.csv**

The dataset contains **800 transaction records and 15 columns**.

### Main Columns

| Column            | Description                                       |
| ----------------- | ------------------------------------------------- |
| TransactionID     | Unique identifier for each transaction            |
| CustomerID        | Unique customer identifier                        |
| AccountID         | Unique account identifier                         |
| AccountType       | Type of customer account                          |
| TransactionType   | Type of transaction                               |
| Product           | Financial product associated with the transaction |
| Firm              | Firm/company information                          |
| Region            | Geographic region                                 |
| Manager           | Assigned manager                                  |
| TransactionDate   | Date of transaction                               |
| TransactionAmount | Monetary value of the transaction                 |
| AccountBalance    | Account balance                                   |
| RiskScore         | Financial risk score                              |
| CreditRating      | Customer credit rating                            |
| TenureMonths      | Customer/account tenure in months                 |

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* SciPy
* Jupyter Notebook

---

## Project Workflow

The project is divided into six major tasks:

1. Data Cleaning and Formatting
2. Descriptive Transactional Analysis
3. Customer Profile Building
4. Financial Risk Identification
5. Data Visualization
6. Hypothesis Testing

---

# Task 1: Data Cleaning and Formatting

The raw financial dataset was first inspected and cleaned before performing further analysis.

### Data Cleaning Steps

* Displayed the first five records.
* Checked dataset dimensions.
* Examined column names.
* Checked data types and dataset information.
* Generated descriptive statistics.
* Checked missing values.
* Checked duplicate records.
* Removed special characters from financial fields.
* Converted financial fields into numeric format.
* Validated and formatted the transaction date column.
* Standardized account type names.
* Standardized transaction categories.

### Cleaning Outcome

After cleaning:

* Financial fields were converted into appropriate numeric formats.
* Transaction dates were converted into datetime format.
* Account types and transaction categories were standardized.
* Missing values and duplicate records were checked.
* A cleaned version of the dataset was generated for further analysis.

---

# Task 2: Descriptive Transactional Analysis

## Credit and Debit Classification

The dataset does not directly contain Credit and Debit labels.

Therefore, the following business rule was used throughout the project.

### Credit Transactions

* Deposit

### Debit Transactions

* Withdrawal
* Payment
* Transfer

This classification was consistently applied during transaction analysis.

---

## Monthly Transaction Analysis

The project creates:

* Month and Year columns.
* Credit transaction summaries.
* Debit transaction summaries.
* Monthly net transaction volume.
* Yearly transaction summaries.

### Net Transaction Volume

**Net Transaction Volume = Total Credits − Total Debits**

The analysis shows that debit transactions are higher than credit transactions in every month of the analyzed period, resulting in a negative net transaction volume throughout the period.

---

## Top Performing Accounts

Accounts were analyzed based on their net inflow.

Net inflow was calculated using the transaction amounts associated with each account.

Accounts with higher positive net inflows were identified as top-performing accounts based on the project's defined metric.

Output:

`Output/Top_Performing_Accounts.csv`

---

## Bottom Performing Accounts

Accounts with the lowest net inflow were identified for further monitoring and customer engagement analysis.

Output:

`Output/Bottom_Performing_Accounts.csv`

---

## Dormant or Inactive Accounts

An account was considered dormant when the gap between two consecutive transactions was:

**60 days or more**

This is a project-specific criterion used for the analysis.

Output:

`Output/Dormant_Accounts.csv`

---

# Task 3: Customer Profile Building

Customer accounts were segmented using transaction frequency, average balance, and transaction volume.

## Customer Activity Levels

Activity levels were defined according to the number of transactions performed by each account.

| Activity Level  | Criteria                 |
| --------------- | ------------------------ |
| High Activity   | More than 7 transactions |
| Medium Activity | 4–7 transactions         |
| Low Activity    | Less than 4 transactions |

This segmentation helps identify highly active accounts as well as accounts with lower transaction engagement.

---

## Balance Segmentation

Accounts were segmented into:

* Low Balance
* Medium Balance
* High Balance

Percentile-based thresholds were used to create the balance segments.

The balance segmentation is also visualized in:

`Images/balance_segments.png`

---

## Transaction Volume Segmentation

Transaction volume represents the total monetary value of transactions associated with an account during the analysis period.

Accounts were segmented into Low, Medium, and High transaction-volume groups using percentile-based thresholds.

This helps identify accounts with comparatively high monetary transaction activity.

The transaction-volume segmentation is visualized in:

`Images/transaction_volume_segments.png`

---

## High Net Inflow Accounts

Accounts with high net inflows were identified as part of the customer profiling analysis.

Output:

`Output/High_Net_Inflow_Accounts.csv`

---

## High-Frequency Low-Balance Accounts

Accounts were identified using the following criteria:

* Medium or High Activity
* Low Balance

These accounts may require additional monitoring or customer engagement.

Output:

`Output/High_Frequency_Low_Balance.csv`

---

## Negative or Near-Zero Balance Accounts

Accounts with negative or near-zero balances were identified for closer financial monitoring.

Output:

`Output/Negative_Balance_Accounts.csv`

---

# Task 4: Financial Risk Identification

Several rule-based and statistical techniques were used to identify potential financial risk indicators.

## Frequent Large Withdrawals

A withdrawal was considered large when its transaction amount was greater than or equal to the **75th percentile (Q3)** of all withdrawal transactions.

This data-driven threshold was used instead of an arbitrary monetary threshold.

Output:

`Output/Frequent_Large_Withdrawals.csv`

---

## Overdraft Accounts

Accounts with a negative account balance were treated as overdraft accounts for this project.

Output:

`Output/Overdraft_Accounts.csv`

---

## Balance Volatility

Balance volatility was measured using the standard deviation of account balances for each account.

A higher standard deviation indicates greater fluctuations in account balance over the analyzed transactions.

Output:

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

Transactions falling outside these boundaries were classified as anomalies.

Output:

`Output/Transaction_Anomalies.csv`

An anomaly indicates an unusual transaction amount according to the statistical rule. It does not by itself confirm fraud.

---

## Suspicious Transaction Behaviour

For this project, an account was classified as showing suspicious transaction behavior if it met **at least one** of the following conditions:

* Frequent large withdrawals
* Negative account balance
* Presence of anomalous transactions

These conditions were combined to create a broader financial risk screening approach.

### Result

A total of **57 accounts** were identified as suspicious according to the project's defined criteria.

Output:

`Output/Suspicious_Accounts.csv`

---

# Task 5: Data Visualization

Several visualizations were created to understand transaction behavior, customer profiles, and financial risk.

## Visualizations

### 1. Transaction Amount by Account Type

File:

`Images/accounttype_transaction_amount.png`

This visualization compares transaction amounts across different account types.

### 2. Account Balance Distribution

File:

`Images/account_balance_distribution.png`

This visualization shows the distribution of account balances.

### 3. Balance Segments

File:

`Images/balance_segments.png`

This visualization shows the distribution of accounts across different balance segments.

### 4. Bottom Performing Accounts

File:

`Images/bottom_performing_accounts.png`

This visualization presents accounts with comparatively lower net inflow.

### 5. Credit Rating Distribution

File:

`Images/credit_rating_distribution.png`

This visualization shows the distribution of customer credit ratings.

### 6. Customer Activity Levels

File:

`Images/customer_activity_levels.png`

This visualization shows the distribution of accounts across High, Medium, and Low activity levels.

### 7. Monthly Credit vs Debit

File:

`Images/monthly_credit_vs_debit.png`

This visualization compares monthly credit and debit transaction trends.

### 8. Risk Score by Region

File:

`Images/riskscore_region.png`

This visualization compares average risk scores across regions.

### 9. Top Performing Accounts

File:

`Images/top_performing_accounts.png`

This visualization presents accounts with comparatively higher net inflow.

### 10. Transaction Amount Distribution

File:

`Images/transaction_amount_distribution.png`

This visualization shows the distribution of transaction amounts and helps identify unusually high or low values.

### 11. Transaction Volume Segments

File:

`Images/transaction_volume_segments.png`

This visualization shows the distribution of accounts across transaction-volume segments.

---

# Task 6: Hypothesis Testing

Two statistical tests were performed to examine relationships between account balances and customer segmentation.

A significance level of:

**α = 0.05**

was used.

---

## Independent t-Test

### Objective

To compare average account balances between High Transaction Volume and Low Transaction Volume accounts.

### Null Hypothesis (H₀)

There is no significant difference in average account balance between High Transaction Volume and Low Transaction Volume accounts.

### Alternative Hypothesis (H₁)

High Transaction Volume accounts have significantly higher average account balances than Low Transaction Volume accounts.

### Result

* **t-statistic:** -0.553
* **p-value:** 0.5813

Since the p-value is greater than 0.05, the null hypothesis was not rejected.

Based on this test and dataset, there was no statistically significant difference in average account balances between the compared transaction-volume groups.

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

Based on this test and dataset, there was no statistically significant difference in average account balances across the High, Medium, and Low Activity groups.

---

# Key Findings

## Data Cleaning

* Financial data was cleaned and standardized.
* Financial fields were converted into numeric format.
* Transaction dates were validated and formatted.
* Account types and transaction categories were standardized.
* Missing values and duplicate records were checked.

## Transaction Analysis

* Monthly and yearly transaction summaries were generated.
* Transactions were classified into Credit and Debit categories.
* Monthly debit transactions were higher than credit transactions throughout the analyzed period.
* Top and bottom performing accounts were identified using net inflow.
* Dormant accounts were identified using the project's 60-day inactivity criterion.

## Customer Profiling

* Accounts were classified into High, Medium, and Low Activity groups.
* Accounts were segmented based on average balance.
* Accounts were segmented based on transaction volume.
* High net inflow accounts were identified.
* High-frequency low-balance accounts were identified.
* Negative or near-zero balance accounts were identified.

## Financial Risk Analysis

* Frequent large withdrawals were identified using the 75th percentile threshold.
* Overdraft accounts were identified using negative account balances.
* Account balance volatility was calculated.
* Transaction anomalies were detected using the IQR method.
* 57 accounts were flagged based on the project's combined suspicious-behavior criteria.

## Statistical Analysis

* An independent t-test was performed.
* A one-way ANOVA test was performed.
* Both tests resulted in p-values greater than 0.05.
* Therefore, the analysis did not find statistically significant differences in average account balances for the tested groups.

---

# Business Recommendations

Based on the analysis, the following areas can be considered for financial monitoring and customer management:

* Closely monitor accounts with negative balances.
* Investigate accounts with repeated large withdrawals.
* Review anomalous transactions for additional verification.
* Prioritize accounts showing multiple risk indicators for further investigation.
* Use customer activity and balance segmentation for targeted banking services.
* Consider personalized financial products and engagement strategies for high-value customer segments.

---

# Project Outputs

The project generates the following analytical output files.

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
* Risk identification is based on predefined business rules and statistical techniques.
* The project does not use machine learning or deep learning.
* The identified suspicious accounts should not be interpreted as confirmed fraudulent accounts.
* Anomalous transactions indicate statistical unusualness and require further investigation.
* The analysis is not a real-time financial monitoring system.
* The findings are specific to the available dataset and project-defined criteria.

---

# Future Enhancements

The project can be extended by:

* Developing a machine learning model for risk prediction.
* Implementing advanced anomaly detection techniques.
* Building a real-time transaction monitoring system.
* Adding interactive dashboards using Power BI or Streamlit.
* Creating automated risk alerts.
* Incorporating additional customer and transaction features.
* Using historical labeled cases to develop supervised fraud or risk prediction models.

---

# Skills Demonstrated

* Python
* Pandas
* NumPy
* Data Cleaning
* Exploratory Data Analysis
* Financial Data Analysis
* Customer Segmentation
* Statistical Analysis
* Hypothesis Testing
* Independent t-Test
* One-Way ANOVA
* Anomaly Detection
* IQR Analysis
* Data Visualization
* Business Insight Generation

---

## Project Type

**Python Data Analytics & Financial Risk Analysis**

This project demonstrates the use of Python-based data analysis and statistical techniques to transform transactional financial data into customer insights and potential risk indicators.

---

## Author

**Suhani**
