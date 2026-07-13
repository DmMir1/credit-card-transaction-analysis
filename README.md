# Credit Card Transaction Analysis | Power BI

## Project Overview

This project presents an end-to-end analysis of approximately **13.31 million credit card transactions** recorded between **January 2010 and October 2019**, representing a total transaction value of approximately **$571.84 million**.

The goal was to transform a large financial transaction dataset into an interactive **Power BI reporting solution** that provides insights into:

- Overall transaction performance and monthly trends
- Card portfolio performance and transaction behavior
- Customer demographics and spending patterns
- Merchant category performance
- Geographic transaction distribution
- Online versus physical transaction activity

The complete analytical workflow included initial data exploration and profiling in **Microsoft Excel**, data cleaning and transformation with **Power Query**, data modeling and measure development using **DAX**, exploratory analysis, investigation of unusual patterns, and the creation of four interactive Power BI dashboard pages.

---

## Dashboard Preview

### 1. Credit Card Transaction Overview

The overview page provides a high-level summary of overall transaction performance and monthly trends.

Key metrics include:

- **$571.84M** in total transaction amount
- **13.31M** total transactions
- **$42.98** average transaction amount
- **1,219** unique customers

The monthly trend shows overall growth in transaction value between 2010 and 2019, alongside recurring short-term declines that were investigated during the exploratory analysis.

![Credit Card Transaction Overview](images/01_transaction_overview.png)

---

### 2. Card & Product Analysis

This page analyzes card portfolio performance across **Debit, Credit, and Debit (Prepaid)** cards.

Key metrics include:

- **4,071** active cards
- **$14.35K** average credit limit
- **$140.47K** average spend per active card
- **3.27K** average transactions per active card

The analysis shows that debit cards generate the highest overall transaction value and account for the largest number of active cards. Credit cards, however, have the highest average spend per active card, while debit cards record the highest average number of transactions per active card.

![Card and Product Analysis](images/02_card_product_analysis.png)

---

### 3. Customer & Merchant Analysis

This page combines customer demographic analysis with merchant transaction performance.

Customer KPIs include:

- **2,000** total customers
- **45** average customer age
- **$469.1K** average spend per active customer
- **710** average credit score

The customer base is distributed relatively evenly across age groups, with the **18–29** segment representing the largest group.

Merchant analysis highlights different dimensions of performance:

- **Money Transfer** generates the highest total transaction amount.
- **Grocery Stores and Supermarkets** record the highest number of transactions.
- **Cruise Lines** have the highest average transaction amount.

These results demonstrate that transaction value, transaction frequency, and average transaction size can produce substantially different merchant rankings.

![Customer and Merchant Analysis](images/03_customer_merchant_analysis.png)

---

### 4. Geographic Analysis

The geographic dashboard explores transaction activity across merchant locations worldwide.

Key metrics include:

- Approximately **13M** total transactions
- **199** merchant regions
- Approximately **12K** merchant cities
- **1.07K** average transactions per merchant city
- Approximately **2M** online transactions

The United States represents the strongest concentration of physical merchant activity.

Among U.S. states:

- **California** ranks first with approximately **$59M** in transaction value.
- **Texas** follows with approximately **$42M**.
- **New York** ranks third with approximately **$40M**.

The city-level analysis identifies the highest-value merchant cities, while the map provides a global view of transaction activity across physical merchant locations.

![Geographic Analysis](images/04_geographic_analysis.png)

---

## Key Insights

The analysis revealed several important findings:

1. **Transaction value increased over time.**  
   Monthly transaction amounts generally increased from approximately $4.4M–$4.6M in the early part of the dataset to around $5M per month in later years.

2. **Recurring short-term transaction declines were identified and investigated.**  
   During exploratory analysis, several sharp monthly declines appeared in the transaction trend. Further investigation showed that these patterns were recurring and were not caused by simple missing-data issues.

3. **Debit cards dominate overall transaction value and card volume.**  
   Debit cards generated approximately **$326M** in transaction value and represented **2,359 active cards**, making them the largest card type in the portfolio.

4. **Credit cards generate the highest average spend per active card.**  
   Despite having fewer active cards than debit cards, credit cards recorded approximately **$167K average spend per active card**.

5. **Different merchant categories lead under different performance metrics.**  
   Money Transfer leads by total transaction value, Grocery Stores and Supermarkets lead by transaction count, and Cruise Lines lead by average transaction amount.

6. **Customer age groups are relatively evenly distributed.**  
   No single age group overwhelmingly dominates the customer base, although customers aged **18–29** form the largest individual segment.

7. **California is the leading U.S. state by transaction value.**  
   California generated approximately **$59M**, followed by Texas at approximately **$42M** and New York at approximately **$40M**.

8. **Online transactions represent a substantial part of overall activity.**  
   Approximately **2 million transactions** were classified as online transactions.

---

## Investigation of Recurring Monthly Transaction Declines

During the exploratory phase, the monthly transaction trend revealed recurring sharp declines in transaction amount.

These declines were investigated to determine whether they were caused by:

- Missing transaction records
- Incomplete months
- Data-quality problems
- Specific merchant categories
- Geographic concentration
- Other unusual transaction patterns

The investigation showed that the declines appeared repeatedly throughout the dataset rather than as isolated anomalies. They were therefore retained as part of the observed transaction behavior rather than removed or artificially corrected.

This investigation was performed during the analytical process but was intentionally excluded from the final four dashboard pages to maintain a focused and concise reporting experience.

More information about the analytical process is available in [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md).

---

## Dataset

The project uses the **Transactions Fraud Datasets** published by **computingvictor** on Kaggle.

The source dataset contains multiple files related to:

- Transaction records
- Customer information
- Card information
- Merchant information
- Fraud labels

For this project, the primary focus was **transaction, customer, card, merchant, and geographic analysis rather than fraud detection**. Fraud analysis was intentionally excluded from the current project scope.

Dataset source:

https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets

The raw source datasets are not included in this repository because of their large size. They can be obtained directly from the original Kaggle source.

---

## Data Preparation and Cleaning

The data preparation process involved both **Microsoft Excel** and **Power Query**.

### Data Profiling in Excel

Excel was used during the initial exploration and profiling stage to:

- Review dataset structure
- Inspect column data types
- Identify missing values
- Examine unusual and negative transaction amounts
- Explore merchant category codes (MCC)
- Review geographic fields
- Create pivot tables and summary analyses
- Validate assumptions before dashboard development

The original Excel profiling workbook is not included in this repository due to its large file size of approximately **385 MB**. The workbook was used for initial data exploration, profiling, pivot-table analysis, validation, and investigation of data-quality issues.

The key findings and methodology from this stage are documented in [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md).

### Data Transformation with Power Query

Power Query was used to prepare analytical tables for Power BI. The transformation process included:

- Importing source data
- Assigning appropriate data types
- Handling missing and blank values
- Preparing transaction dates
- Cleaning geographic fields
- Creating analytical columns where required
- Preparing customer, card, and transaction tables for analysis

Special attention was given to unusual values rather than automatically removing them. For example, negative transaction amounts were investigated as potentially valid refund activity.

---

## Data Model and DAX

The Power BI solution uses cleaned analytical tables representing:

- Transactions
- Users and customers
- Cards
- Merchant information
- Geographic attributes

DAX measures were developed to calculate key business metrics, including:

- Total Transaction Amount
- Total Transactions
- Average Transaction Amount
- Unique Customers
- Active Cards
- Average Credit Limit
- Average Spend per Active Card
- Average Transactions per Active Card
- Average Spend per Active Customer
- Average Customer Age
- Average Credit Score
- Merchant Cities
- Merchant Regions
- Average Transactions per Merchant City
- Online Transactions

These measures provide dynamic calculations that respond to report filters and user interactions.

---

## Tools and Technologies

| Tool | Purpose |
|------|---------|
| **Microsoft Excel** | Initial data exploration, profiling, pivot tables, and validation |
| **Power Query** | Data cleaning, transformation, and preparation |
| **Power BI** | Data modeling, interactive dashboards, and visual analysis |
| **DAX** | Business metrics and analytical measures |
| **Git & GitHub** | Version control, documentation, and project presentation |
| **Git LFS** | Storage and versioning of the large Power BI `.pbix` file |

---

## Project Structure

```text
credit-card-transaction-analysis/
│
├── images/
│   ├── 01_transaction_overview.png
│   ├── 02_card_product_analysis.png
│   ├── 03_customer_merchant_analysis.png
│   └── 04_geographic_analysis.png
│
├── .gitattributes
├── Credit_Card_Transaction_Analysis.pbix
├── PROJECT_DOCUMENTATION.md
└── README.md
