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

The complete analytical workflow included initial data exploration and profiling in **Microsoft Excel**, data preparation with **Power Query**, data modeling and measure development using **DAX**, exploratory analysis, investigation of unusual patterns, and the creation of four interactive Power BI dashboard pages.

---

## Dashboard Preview

### 1. Credit Card Transaction Overview

The overview page provides a high-level summary of overall transaction performance and monthly trends.

**Key metrics:**

- **$571.84M** total transaction amount
- **13.31M** total transactions
- **$42.98** average transaction amount
- **1,219** unique transacting customers

The monthly transaction trend shows overall growth during the earlier part of the analyzed period, followed by a more stable pattern in later years. Recurring short-term declines were also identified and investigated during the exploratory phase.

![Credit Card Transaction Overview](images/01_transaction_overview.png)

---

### 2. Card & Product Analysis

This page analyzes card portfolio performance across **Debit, Credit, and Debit (Prepaid)** cards and supports interactive filtering by card brand.

**Key metrics:**

- **4,071** active cards
- **$14.35K** average credit limit
- **$140.47K** average spend per active card
- **3.27K** average transactions per active card

**Key findings:**

- Debit cards generated approximately **$326M** in transaction value.
- Credit cards generated approximately **$226M**.
- Debit (Prepaid) cards generated approximately **$20M**.
- Debit had the largest number of active cards at **2,359**.
- Credit cards generated the highest average spend per active card at approximately **$167K**.
- Debit cards recorded the highest average transaction frequency per active card at approximately **3,510 transactions**.

The results show that debit dominates overall portfolio activity and transaction frequency, while credit generates greater monetary value per active card.

![Card and Product Analysis](images/02_card_product_analysis.png)

---

### 3. Customer & Merchant Analysis

This page combines customer demographic analysis with merchant-category performance.

**Customer KPIs:**

- **2,000** total customer profiles
- **45** average customer age
- **$469.1K** average spend per active customer
- **710** average credit score

The customer base is broadly distributed across age groups:

| Age Group | Customers |
|---|---:|
| 18–29 | 480 |
| 30–39 | 351 |
| 40–49 | 371 |
| 50–59 | 352 |
| 60+ | 446 |

The **18–29** segment is the largest individual age group, while customers aged **60+** also represent a substantial part of the customer base.

**Merchant insights:**

- **Money Transfer** leads merchant categories by total transaction amount at approximately **$53M**.
- **Grocery Stores and Supermarkets** lead by transaction frequency at approximately **1.59M transactions**.
- **Cruise Lines** have the highest average transaction amount among the displayed categories at approximately **$1,551**.

These results demonstrate that total transaction value, transaction frequency, and average transaction size reveal different dimensions of merchant performance.

![Customer and Merchant Analysis](images/03_customer_merchant_analysis.png)

---

### 4. Geographic Analysis

The geographic dashboard explores transaction activity across physical merchant locations while representing online transactions separately.

**Key metrics:**

- Approximately **13M** total transactions
- **199** merchant regions
- Approximately **12K** merchant cities
- **1.07K** average transactions per merchant city
- Approximately **2M** online transactions

Among U.S. states:

| State | Transaction Amount |
|---|---:|
| California | $59M |
| Texas | $42M |
| New York | $40M |
| Florida | $29M |
| Illinois | $20M |

Among the leading cities:

| City | Transaction Amount |
|---|---:|
| Houston | $6.6M |
| Miami | $3.6M |
| Louisville | $3.2M |
| San Francisco | $3.2M |
| Atlanta | $3.1M |

The United States represents the strongest concentration of physical merchant activity in the dashboard, while the map also displays international merchant locations present in the source data.

Approximately **2 million transactions** were identified as online transactions. These records typically use:

```text
merchant_city = ONLINE
```

and do not have meaningful physical state geography. They were therefore retained in the overall analysis but represented separately from physical geographic rankings.

![Geographic Analysis](images/04_geographic_analysis.png)

---

## Key Insights

The analysis revealed several important findings:

1. **Transaction activity generally increased over the analyzed period.**  
   Monthly transaction amounts were generally lower during the earlier years and reached higher levels in later periods.

2. **Recurring short-term transaction declines were identified and investigated.**  
   Several sharp monthly declines appeared repeatedly in the transaction trend. Investigation showed that these patterns were recurring rather than isolated anomalies or simple missing-data issues.

3. **Debit cards dominate overall portfolio activity.**  
   Debit generated approximately **$326M** in transaction value and represented **2,359 active cards**, making it the largest card type by both metrics.

4. **Credit cards generate the highest average spend per active card.**  
   Despite having fewer active cards than debit, credit cards recorded approximately **$167K average spend per active card**.

5. **Different merchant categories lead under different performance metrics.**  
   Money Transfer leads by total transaction value, Grocery Stores and Supermarkets lead by transaction count, and Cruise Lines lead the displayed categories by average transaction amount.

6. **Customer age groups are broadly distributed.**  
   No single age group overwhelmingly dominates the customer population, although customers aged **18–29** form the largest individual segment.

7. **California is the leading U.S. state by transaction value.**  
   California generated approximately **$59M**, followed by Texas at approximately **$42M** and New York at approximately **$40M**.

8. **Online transactions represent a substantial part of overall activity.**  
   Approximately **2 million transactions** were identified as online transactions and handled separately from physical geographic analysis.

---

## Investigation of Recurring Monthly Transaction Declines

During the exploratory phase, the monthly transaction trend revealed recurring sharp declines in transaction amount.

These declines were investigated to determine whether they were caused by factors such as:

- Missing transaction records
- Incomplete months
- Data-quality problems
- Specific merchant categories
- Geographic concentration
- Other unusual transaction patterns

The investigation showed that the declines appeared repeatedly throughout the dataset rather than as isolated anomalies. They were therefore retained as part of the observed transaction behavior rather than removed or artificially corrected.

A temporary exploratory page was used during development to support this investigation and validate unusual analytical results. It was intentionally excluded from the final four-page dashboard because its purpose was analytical investigation rather than final reporting.

For more detail about the investigation and the overall analytical workflow, see [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md).

---

## Data-Quality Investigations

A central principle throughout this project was:

> **Investigate unusual values before removing them.**

Several data-quality questions were examined during the project.

### Negative Transaction Amounts

Negative transaction amounts were retained because they may represent legitimate financial events such as:

- Refunds
- Reversals
- Corrections
- Returned purchases

Without sufficient evidence that these records were errors, removing them could eliminate valid financial activity.

### Missing Merchant States and Online Transactions

During geographic analysis, a blank category initially appeared in state-level transaction rankings.

Investigation showed that many records without a `merchant_state` had:

```text
merchant_city = ONLINE
```

Because online transactions do not necessarily have meaningful physical state geography, the final approach was to:

- Retain online transactions in the overall dataset
- Exclude blank states from physical state rankings
- Represent online activity separately through an **Online Transactions** KPI

### International Merchant Locations

The geographic map contained merchant locations outside the United States.

These records were not automatically removed because international merchant activity can be legitimate, and there was insufficient evidence to classify all international locations as errors.

### Merchant States vs Merchant Regions

The source `merchant_state` field contains more distinct values than the standard 50 U.S. states because it includes a broader range of geographic values.

To avoid a misleading label, the corresponding dashboard KPI was named:

**Merchant Regions**

The Top 10 States ranking focuses on leading recognizable U.S. states.

### High Average Transaction Values

Cruise Lines showed an average transaction amount of approximately **$1,551**, significantly higher than the other displayed categories.

The result was investigated as a potential anomaly but retained because high-value cruise and travel purchases are commercially plausible.

### Customer Profiles vs Unique Transacting Customers

The report contains two different customer-related figures:

- **2,000 total customer profiles**
- **1,219 unique transacting customers**

These metrics answer different analytical questions. The first represents customer profiles in the customer dataset, while the second represents customers associated with transaction activity in the analyzed transaction data.

---

## Dataset

The project uses the **Transactions Fraud Datasets** published by **computingvictor** on Kaggle.

The source dataset contains multiple files related to:

- Transaction records
- Customer information
- Card information
- Merchant Category Codes
- Fraud labels

For this project, the focus was **transaction, card, customer, merchant-category, and geographic analysis rather than fraud detection**. Fraud analysis was intentionally excluded from the current project scope.

**Dataset source:**  
https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets

The raw source datasets are not included in this repository because of their large size. They can be obtained directly from the original Kaggle source.

---

## Data Preparation and Analysis Workflow

The project followed an iterative analytical workflow:

```text
Raw Dataset
    ↓
Initial Data Exploration
    ↓
Excel Data Profiling
    ↓
Power Query Preparation
    ↓
Data-Quality Investigation
    ↓
Clean Analytical Tables
    ↓
Power BI Data Model
    ↓
DAX Measures
    ↓
Exploratory Analysis
    ↓
Investigation of Unexpected Results
    ↓
Dashboard Development
    ↓
Validation and Refinement
    ↓
Final Four-Page Power BI Report
```

Findings discovered during visualization sometimes raised new questions about the underlying data, leading to further investigation before the dashboards were finalized.

---

## Data Profiling in Excel

Microsoft Excel was used during the initial exploration and profiling stage to:

- Review dataset structure
- Inspect column data types
- Identify missing and null values
- Examine unusual and negative transaction amounts
- Explore Merchant Category Codes (MCC)
- Review geographic fields
- Create pivot tables and summary analyses
- Practice and apply lookup functions
- Use conditional formatting and ranking
- Validate assumptions before dashboard development

The original Excel profiling workbook is not included in this repository due to its large file size of approximately **385 MB**.

The workbook was used for initial data exploration, profiling, pivot-table analysis, validation, and investigation of data-quality issues. The main findings and methodology from this stage are documented in [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md).

---

## Data Preparation with Power Query

Power Query was used to import, inspect, and prepare the data for analysis.

The cleaned analytical tables used in Power BI included:

- `Transactions_Clean`
- `Cards_Clean`
- `Users_Clean`

Preparation included:

- Checking and assigning appropriate data types
- Reviewing null and blank values
- Preparing fields for analysis
- Supporting relationships between transaction, card, and customer data
- Preparing merchant-category descriptions for reporting
- Supporting geographic analysis
- Preparing the data for DAX measures and dashboard KPIs

Unusual values were investigated before decisions were made about whether they should be retained, excluded from a specific analysis, or represented separately.

---

## Data Model and DAX

The Power BI solution combines cleaned transaction, customer, and card data to support analysis across several business dimensions.

DAX measures developed during the project include:

- Total Transaction Amount
- Total Transactions
- Average Transaction Amount
- Unique Customers
- Total Customers
- Active Cards
- Average Credit Limit
- Average Spend per Active Card
- Average Transactions per Active Card
- Average Spend per Active Customer
- Average Customer Age
- Average Credit Score
- Merchant Regions
- Merchant Cities
- Average Transactions per Merchant City
- Online Transactions

An example measure used to identify online transaction activity is:

```DAX
Online Transactions =
CALCULATE(
    [Total Transactions],
    Transactions_Clean[merchant_city] = "ONLINE"
)
```

During development, this measure initially appeared blank because an active chart selection was applying additional filter context. After clearing the visual selection, the measure correctly returned approximately **2 million online transactions**.

This demonstrated the importance of checking visual interactions and filter context when troubleshooting Power BI measures.

---

## Tools and Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Initial data exploration, profiling, pivot tables, and validation |
| **Power Query** | Data import, preparation, and transformation |
| **Power BI** | Data modeling, dashboard development, and interactive visualization |
| **DAX** | KPI calculations and analytical measures |
| **Git & GitHub** | Version control, documentation, and portfolio presentation |
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
```

The Power BI report is stored using **Git Large File Storage (Git LFS)** because the `.pbix` file is approximately **319 MB** and exceeds GitHub's standard browser upload limit.

The raw source datasets and the original Excel profiling workbook are not included because of their large file sizes. The original data is publicly available through Kaggle, while the analytical workflow and Excel-based profiling process are documented in `PROJECT_DOCUMENTATION.md`.

---

## Dashboard Features

The final Power BI report includes:

- Four analytical dashboard pages
- KPI summary cards
- Monthly transaction trend analysis
- Year filtering
- Card brand filtering
- Card type comparison
- Customer demographic analysis
- Merchant-category analysis
- Geographic transaction mapping
- State and city rankings
- Online transaction analysis
- Interactive filtering between relevant visuals

---

## Challenges and Solutions

| Challenge | Solution |
|---|---|
| Approximately 13.31M transaction records | Used Power Query and Power BI to work with the complete analytical dataset |
| Excel worksheet row limit | Processed the full transaction data through Power Query rather than relying on direct worksheet display |
| Blank state category in geographic analysis | Investigated the underlying records and identified online transactions as a major cause |
| Online activity affecting physical geographic rankings | Created a separate Online Transactions KPI and excluded blank states from physical state rankings |
| International map points appeared unusual | Retained them because there was insufficient evidence to classify all international activity as erroneous |
| Negative transaction values | Preserved them as potentially legitimate refunds, reversals, corrections, or returns |
| High Cruise Lines average transaction amount | Investigated the business context and retained the plausible value |
| Online Transactions DAX measure appeared blank | Identified an active visual selection and filter context as the cause |
| Different customer counts across dashboard pages | Distinguished total customer profiles from unique transacting customers |
| Merchant States KPI could be misleading | Renamed it to Merchant Regions |
| Temporary investigation page was not suitable for the final report | Documented the investigation but excluded the exploratory page from the final four-page dashboard |

---

## How to Explore the Project

1. Review the four dashboard screenshots in this README for a quick visual overview.
2. Read [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md) for a detailed description of the workflow, data profiling, investigations, challenges, DAX measures, and dashboard development.
3. Clone the repository with Git LFS installed to obtain the complete Power BI report.
4. Open `Credit_Card_Transaction_Analysis.pbix` in Microsoft Power BI Desktop to explore the interactive report.

> **Note:** Because the `.pbix` file is managed through Git LFS, cloning the repository with Git LFS installed is the most reliable way to obtain the complete Power BI report file.

---

## Skills Demonstrated

This project demonstrates practical experience with:

- Data profiling
- Exploratory data analysis
- Large dataset analysis
- Microsoft Excel
- Power Query
- Power BI data modeling
- DAX measure development
- KPI design
- Time-series analysis
- Card portfolio analysis
- Customer demographic analysis
- Merchant-category analysis
- Geographic analysis
- Data-quality investigation
- Filter-context troubleshooting
- Business interpretation
- Interactive dashboard development
- Technical documentation
- Git and GitHub project presentation

---

## Future Improvements

Potential future extensions of the project include:

- Fraud detection analysis using the provided fraud labels
- More detailed online versus physical transaction comparisons
- Transaction segmentation using additional customer attributes
- Advanced geographic drill-down analysis
- Time-series forecasting
- Additional Power BI drill-through pages and report tooltips

---

## Author

**Dmytro Miroshnikov**

Junior Data Analyst with experience in **SQL, Excel, Python, Power BI, Tableau, data cleaning, data visualization, and business-oriented analytical projects**.

---

## Acknowledgments

The dataset used in this project was published by **computingvictor** on Kaggle.

**Original dataset:**  
https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets

---

## Conclusion

This project demonstrates an end-to-end analytical workflow using **Excel, Power Query, Power BI, and DAX** to transform approximately **13.31 million financial transactions** into an interactive business intelligence solution.

The analysis revealed distinct patterns across transaction trends, card products, customer demographics, merchant categories, geographic locations, and online transaction activity.

Beyond the final dashboards, the project emphasizes a core analytical principle:

> **Unexpected values should be investigated in their business context before being classified as errors or removed from the data.**

The final result is a four-page Power BI report supported by documented data profiling, data-quality investigation, custom DAX measures, and a reproducible analytical decision-making process.
