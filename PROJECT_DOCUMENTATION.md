# Project Documentation — Credit Card Transaction Analysis

## 1. Project Overview

This project presents an end-to-end analysis of a large financial transaction dataset containing approximately **13.31 million credit card transactions** recorded between **January 2010 and October 2019**, with a total transaction value of approximately **$571.84 million**.

The purpose of the project was to transform raw financial data into an interactive Power BI reporting solution capable of answering business questions related to:

- Overall transaction performance and trends
- Card portfolio performance
- Customer demographics and spending behavior
- Merchant category performance
- Geographic transaction patterns
- Online versus physical transaction activity

The project was completed using **Microsoft Excel, Power Query, Power BI, and DAX**.

The complete analytical workflow included:

1. Dataset selection and initial exploration
2. Data profiling in Excel
3. Data cleaning and transformation with Power Query
4. Investigation of missing and unusual values
5. Preparation of cleaned analytical tables
6. Power BI data modeling
7. DAX measure development
8. Exploratory analysis
9. Investigation of unexpected analytical results
10. Dashboard design and refinement
11. Final validation and documentation

The final Power BI report contains four analytical pages:

1. **Credit Card Transaction Overview**
2. **Card & Product Analysis**
3. **Customer & Merchant Analysis**
4. **Geographic Analysis**

A temporary exploratory page was also used during development to investigate unusual patterns and validate analytical results. This investigation page was intentionally excluded from the final dashboard because its purpose was analytical validation rather than final reporting.

---

## 2. Dataset Source

The dataset used in this project is publicly available on Kaggle:

**Financial Transactions Dataset: Analytics**  
**Author:** computingvictor  
**Platform:** Kaggle  
**Source:** https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets

The dataset contains large-scale financial transaction data together with customer and card information.

For this project, the data was used to analyze:

- Transaction trends
- Card portfolio performance
- Customer demographics
- Merchant-category behavior
- Geographic transaction patterns
- Online transaction activity

The complete raw dataset is not included in the GitHub repository due to its large size. It can be downloaded directly from the original Kaggle source.

---

## 3. Dataset Scope

The final analysis covers approximately **13.31 million transactions** between **January 2010 and October 2019**.

### Key Dataset Metrics

| Metric | Value |
|---|---:|
| Total transaction amount | $571.84M |
| Total transactions | 13.31M |
| Average transaction amount | $42.98 |
| Unique transacting customers | 1,219 |
| Customer profiles | 2,000 |
| Active cards | 4,071 |
| Analysis period | Jan 2010 – Oct 2019 |

The data used for analysis includes transaction-level information and related customer and card attributes.

Important transaction fields include:

- Transaction ID
- Transaction date and time
- Customer/client ID
- Card ID
- Transaction amount
- Transaction channel/use-chip information
- Merchant ID
- Merchant city
- Merchant state/region
- ZIP code
- Merchant Category Code (MCC)
- MCC description
- Error status

Customer information includes fields such as:

- Customer ID
- Current age
- Credit score
- Geographic attributes
- Income-related attributes
- Number of credit cards

Card information includes fields such as:

- Card ID
- Customer/client ID
- Card brand
- Card type
- Credit limit
- Account opening date
- Other card characteristics

---

## 4. Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Initial data profiling and exploratory analysis |
| **Power Query** | Data import, cleaning, transformation, and preparation |
| **Power BI** | Data modeling, dashboard development, and interactive visualization |
| **DAX** | KPI calculations and analytical measures |

---

## 5. Analytical Workflow

The project followed an iterative analytical process.

Rather than moving directly from raw data to dashboard creation, the data was first explored and profiled to understand:

- What information was available
- How tables were connected
- Which fields contained missing values
- Which values appeared unusual
- Which metrics could provide useful business insights
- Which analytical questions could be answered reliably

The general workflow was:

```text
Raw Dataset
    ↓
Initial Data Exploration
    ↓
Excel Data Profiling
    ↓
Power Query Cleaning & Transformation
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
Validation & Refinement
    ↓
Final Four-Page Power BI Report
```

The process was intentionally iterative. Findings discovered during visualization sometimes raised new questions about the underlying data, which required additional investigation before the dashboards were finalized.

---

## 6. Initial Data Profiling in Excel

Before dashboard development, the data was examined to understand its structure, completeness, and analytical potential.

The profiling process focused on:

- Row counts
- Column names
- Data types
- Missing values
- Null values
- Distinct values
- Duplicate considerations
- Minimum and maximum values
- Negative transaction amounts
- Merchant location fields
- Merchant Category Codes
- Relationships between transaction, customer, and card identifiers

The Excel-based stage also provided practical experience with:

- Power Query
- Pivot tables
- XLOOKUP/VLOOKUP
- Conditional formatting
- Ranking
- Unique-value exploration

The objective was not simply to remove missing or unusual values. Instead, the goal was to understand what each field represented and determine whether unusual records were errors, legitimate business events, or limitations of the source data.

---

## 7. Working With a Large Transaction Dataset

One of the main technical challenges was the size of the transaction data.

The final analysis contains approximately:

**13.31 million transaction records**

This significantly exceeds Excel's standard worksheet limit of **1,048,576 rows**.

Therefore, the full transaction dataset could not simply be displayed in a standard Excel worksheet.

### Solution

The complete transaction data was processed through **Power Query** and subsequently analyzed in **Power BI**.

This made it possible to work with the full dataset without restricting the analysis to only the rows that could be displayed directly in an Excel worksheet.

An important distinction was made between:

- The number of rows Excel can display in a worksheet
- The volume of data Power Query can process
- The data that can be loaded into the Power BI analytical model

This ensured that the final dashboard used the complete transaction dataset rather than an accidental subset.

---

## 8. Power Query Preparation

Power Query was used to import, inspect, and prepare the data for analysis.

The main cleaned analytical tables used in Power BI included:

- `Transactions_Clean`
- `Cards_Clean`
- `Users_Clean`

The preparation process included:

- Checking data types
- Reviewing null and blank values
- Preserving meaningful transaction records
- Preparing fields for relationships
- Supporting geographic analysis
- Supporting merchant-category analysis
- Preparing data for DAX measures and dashboard KPIs

A key analytical principle throughout this stage was:

> **Do not remove unusual data without evidence that it is invalid.**

Records were investigated before decisions were made about whether they should be retained, excluded from a specific analysis, or handled separately.

---

## 9. Merchant Category Codes and Descriptions

The transaction data included Merchant Category Codes (`mcc`) together with human-readable merchant category descriptions (`mcc_description`).

For dashboard reporting, `mcc_description` was used because category names such as:

- Money Transfer
- Grocery Stores and Supermarkets
- Wholesale Clubs
- Drug Stores and Pharmacies
- Service Stations
- Cruise Lines

are significantly easier for users to interpret than numeric MCC codes.

Merchant descriptions were merged directly into the transaction table during data preparation, so a separate MCC table was not required for the final dashboard model.

---

## 10. Data-Quality Investigations

Several unusual patterns were discovered during profiling and dashboard development. These were investigated before any decision was made to modify or exclude data.

### 10.1 Negative Transaction Amounts

Negative transaction values were identified during initial data profiling.

These records were not automatically removed because negative financial transactions may represent legitimate business events such as:

- Refunds
- Reversals
- Corrections
- Returned purchases

Without sufficient evidence that these values were errors, removing them would risk deleting legitimate financial activity and artificially increasing total transaction values.

### Decision

Negative transactions were retained in the analytical dataset.

---

### 10.2 Missing Merchant States

During development of the Geographic Analysis page, an unnamed category initially appeared as the largest bar in the state-level transaction amount ranking.

This required investigation because a blank value was dominating a geographic chart.

Reviewing the underlying data showed that many records with blank `merchant_state` values had:

```text
merchant_city = ONLINE
```

This provided a reasonable explanation for the missing geographic information.

Online transactions do not necessarily correspond to a meaningful physical merchant location, so the absence of a physical state was not automatically classified as a data-quality error.

### Final approach

- Online transactions were retained in the overall transaction dataset.
- Blank `merchant_state` values were excluded from physical state rankings.
- Online activity was represented separately using a dedicated KPI.
- Approximately **2 million online transactions** were identified in the final dashboard.

This prevented online activity from distorting physical geographic analysis while preserving valid transaction records.

---

### 10.3 Online Transactions

A dedicated DAX measure was created to identify online transaction activity:

```DAX
Online Transactions =
CALCULATE(
    [Total Transactions],
    Transactions_Clean[merchant_city] = "ONLINE"
)
```

During development, this measure initially appeared to return a blank result.

Additional test measures were created to investigate whether the `ONLINE` records were being detected correctly.

The issue was eventually traced to an active selection on another chart, which was applying cross-filter context to the KPI card.

After clearing the chart selection, the measure correctly returned approximately:

**2 million online transactions**

### Analytical lesson

Unexpected Power BI results are not always caused by incorrect DAX or bad data. They may result from:

- Visual selections
- Cross-filtering
- Page filters
- Visual filters
- Relationship behavior
- Filter context

This investigation demonstrated the importance of checking report interactions when validating measures.

---

### 10.4 International Merchant Locations

When the geographic map was first created, merchant locations appeared across the United States as well as in other parts of the world.

This raised the question of whether the international points represented:

- Legitimate international merchant transactions
- Incorrect source data
- Geographic ambiguity in Power BI's mapping engine

The source data contained international-looking geographic values, and there was insufficient evidence to conclude that all non-U.S. locations were erroneous.

### Decision

International merchant locations were retained.

The project followed the principle that data should not be deleted simply because it appears unusual. A value should be removed only when there is reasonable evidence that it is invalid, incorrectly recorded, or outside the defined analytical scope.

---

### 10.5 Merchant States vs Merchant Regions

The source field `merchant_state` contains more distinct values than the standard 50 U.S. states.

The final dashboard initially used the KPI label:

**Merchant States**

However, the field includes a broader range of geographic values, including international region-like values.

Using the term "states" for all 199 distinct values would therefore be misleading.

### Decision

The KPI was renamed:

**Merchant States → Merchant Regions**

The final Geographic Analysis page shows:

- **13M** Total Transactions
- **199** Merchant Regions
- **12K** Merchant Cities
- **1.07K** Average Transactions per Merchant City
- **2M** Online Transactions

The Top 10 States chart continues to focus on recognizable U.S. states.

---

### 10.6 Unusually High Average Transaction Amounts

During merchant-category analysis, Cruise Lines showed an average transaction amount of approximately:

**$1,551**

This was substantially higher than the other displayed categories, most of which had average transaction amounts around $700–$800.

Because the difference was significant, the value was treated as something requiring investigation rather than being accepted or removed automatically.

### Interpretation

A high average transaction amount is commercially plausible for cruise bookings and travel-related purchases, which can involve significantly larger individual transactions than everyday categories such as groceries, restaurants, or service stations.

### Decision

The Cruise Lines result was retained.

### Analytical lesson

An unusual value is not automatically an error. Outliers should be evaluated in their business context before being removed or modified.

---

### 10.7 Total Customers vs Unique Transacting Customers

The final report contains two different customer-related figures:

- **2,000 Total Customers**
- **1,219 Unique Customers**

These values appear on different dashboard pages and answer different analytical questions.

The **2,000 Total Customers** KPI represents customer profiles available in the customer dataset.

The **1,219 Unique Customers** KPI represents customers associated with transaction activity in the analyzed transaction table.

### Decision

Both metrics were retained because they represent different analytical populations.

This distinction is important when working with relational datasets: the total number of customer records does not necessarily equal the number of customers appearing in transaction activity.

---

## 11. Customer Age Group Creation

To make customer demographics easier to interpret, the continuous `current_age` field was transformed into five age groups:

- 18–29
- 30–39
- 40–49
- 50–59
- 60+

A calculated column was created using DAX:

```DAX
Age Group =
SWITCH(
    TRUE(),
    Users_Clean[current_age] < 30, "18-29",
    Users_Clean[current_age] < 40, "30-39",
    Users_Clean[current_age] < 50, "40-49",
    Users_Clean[current_age] < 60, "50-59",
    "60+"
)
```

The categories were displayed in logical age order:

```text
18–29 → 30–39 → 40–49 → 50–59 → 60+
```

rather than being sorted by customer count.

This improved readability and made the demographic analysis more intuitive.

---

## 12. Power BI Model and DAX Measures

The Power BI report combines cleaned transaction, customer, and card data to support analysis across multiple business dimensions.

Measures created during the project included:

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

These measures supported:

- Executive KPIs
- Time-series analysis
- Card-type comparisons
- Card-brand filtering
- Customer demographic analysis
- Merchant-category rankings
- Geographic analysis
- Online transaction analysis

---

## 13. Dashboard 1 — Credit Card Transaction Overview

### Purpose

Provide an executive-level summary of transaction activity and show how transaction value developed over time.

### KPIs

| KPI | Value |
|---|---:|
| Total Transaction Amount | $571.84M |
| Total Transactions | 13.31M |
| Average Transaction Amount | $42.98 |
| Unique Customers | 1,219 |

### Visuals

- Four KPI cards
- Year slicer
- Monthly Transaction Amount Trend line chart

### Analysis

The monthly transaction trend generally increased during the earlier years of the dataset before becoming more stable in later periods.

Recurring sharp declines are visible throughout the time series.

These may reflect seasonal patterns, but additional analysis by calendar month would be required to confirm the exact nature of the seasonality.

The Year slicer allows users to interactively focus on individual years.

### Business interpretation

The overview provides a high-level picture of:

- Overall transaction scale
- Average transaction size
- Customer participation
- Long-term development of transaction activity

---

## 14. Dashboard 2 — Card & Product Analysis

### Purpose

Compare card portfolio performance across card types and allow interactive filtering by card brand.

### KPIs

| KPI | Value |
|---|---:|
| Active Cards | 4,071 |
| Average Credit Limit | $14.35K |
| Average Spend per Active Card | $140.47K |
| Average Transactions per Active Card | 3.27K |

### Transaction Amount by Card Type

| Card Type | Transaction Amount |
|---|---:|
| Debit | $326M |
| Credit | $226M |
| Debit (Prepaid) | $20M |

### Active Cards by Card Type

| Card Type | Active Cards |
|---|---:|
| Debit | 2,359 |
| Credit | 1,351 |
| Debit (Prepaid) | 361 |

### Average Spend per Active Card

| Card Type | Average Spend |
|---|---:|
| Credit | $167K |
| Debit | $138K |
| Debit (Prepaid) | $55K |

### Average Transactions per Active Card

| Card Type | Average Transactions |
|---|---:|
| Debit | 3,510 |
| Credit | 3,042 |
| Debit (Prepaid) | 2,537 |

### Business interpretation

Debit cards dominate:

- Total transaction value
- Number of active cards
- Transaction frequency per active card

Credit cards, however, generate the highest average spend per active card.

This suggests different usage patterns:

- Debit cards appear to be used more broadly and frequently.
- Credit cards generate greater monetary value per active card.

The page includes a **Card Brand slicer** for interactive portfolio analysis.

---

## 15. Dashboard 3 — Customer & Merchant Analysis

### Purpose

Combine customer demographics with merchant-category performance.

### Customer KPIs

| KPI | Value |
|---|---:|
| Total Customers | 2,000 |
| Average Customer Age | 45 |
| Average Spend per Active Customer | $469.1K |
| Average Credit Score | 710 |

### Customer Age Distribution

| Age Group | Customers |
|---|---:|
| 18–29 | 480 |
| 30–39 | 351 |
| 40–49 | 371 |
| 50–59 | 352 |
| 60+ | 446 |

The customer base is broadly distributed across age groups.

The largest group is **18–29**, while customers aged **60+** also represent a substantial part of the population.

### Top Merchant Categories by Transaction Amount

Leading categories include:

1. Money Transfer — approximately **$53M**
2. Grocery Stores and Supermarkets — approximately **$41M**
3. Wholesale Clubs — approximately **$38M**
4. Drug Stores and Pharmacies — approximately **$35M**
5. Service Stations — approximately **$30M**

### Top Merchant Categories by Number of Transactions

Leading categories include:

1. Grocery Stores and Supermarkets — approximately **1.59M transactions**
2. Miscellaneous Food Stores — approximately **1.46M**
3. Service Stations — approximately **1.42M**
4. Eating Places and Restaurants — approximately **1.00M**

### Top Merchant Categories by Average Transaction Amount

Cruise Lines lead the displayed categories with an average transaction amount of approximately:

**$1,551**

### Business interpretation

Merchant performance depends heavily on the metric being evaluated.

- Money Transfer leads by total transaction value.
- Grocery Stores and Supermarkets lead by transaction frequency.
- Cruise Lines lead the displayed categories by average transaction size.

A category with many transactions is not necessarily the category generating the greatest total value or the largest individual transactions.

This demonstrates why merchant performance should be evaluated from multiple analytical perspectives.

---

## 16. Dashboard 4 — Geographic Analysis

### Purpose

Analyze physical merchant locations and geographic concentration while representing online activity separately.

### KPIs

| KPI | Value |
|---|---:|
| Total Transactions | 13M |
| Merchant Regions | 199 |
| Merchant Cities | 12K |
| Average Transactions per Merchant City | 1.07K |
| Online Transactions | 2M |

### Visuals

- Bubble map of Transaction Amount by Merchant Location
- Top 10 States by Transaction Amount
- Top 10 Cities by Transaction Amount

### Leading States

| State | Transaction Amount |
|---|---:|
| California | $59M |
| Texas | $42M |
| New York | $40M |
| Florida | $29M |
| Illinois | $20M |

### Leading Cities

| City | Transaction Amount |
|---|---:|
| Houston | $6.6M |
| Miami | $3.6M |
| Louisville | $3.2M |
| San Francisco | $3.2M |
| Atlanta | $3.1M |

### Business interpretation

Transaction activity is strongly concentrated in major U.S. markets.

California leads state-level transaction value, while Houston is notably ahead of the other cities shown in the ranking.

The map also contains international merchant points. These were retained because there was insufficient evidence to classify them as invalid.

Online transactions were represented separately because they do not have meaningful physical state geography.

---

## 17. Dashboard Design Decisions

The final report was organized into four focused analytical perspectives:

1. **Transaction Overview**
2. **Card & Product Analysis**
3. **Customer & Merchant Analysis**
4. **Geographic Analysis**

The design follows several principles:

- Consistent title and subtitle placement
- KPI cards positioned at the top of each page
- Clear visual hierarchy
- Limited use of slicers to avoid unnecessary complexity
- Consistent number formatting
- Coordinated colors across analytical groups
- Separation of physical geography from online activity
- Use of Top 10 rankings for focused comparisons
- Removal of temporary exploratory pages from the final report

The dashboard prioritizes readability and analytical clarity rather than maximizing the number of visuals.

---

## 18. Temporary Investigation Page

During dashboard development, a separate temporary page was used for exploratory investigation.

This page supported:

- Investigation of unusual monthly transaction patterns
- Validation of unexpected analytical results
- Examination of suspicious values
- Testing of temporary measures
- Comparison of underlying records

The investigation page was useful during the analytical process but was not included in the final four-page report.

### Reason for exclusion

Not every exploratory analysis needs to become part of the final dashboard.

The final report should contain visuals that clearly support business questions and provide useful insights to the intended audience.

The investigation process was therefore documented, while the temporary page itself was excluded from the final presentation.

---

## 19. Challenges & Solutions

| Challenge | Solution |
|---|---|
| Very large transaction dataset | Used Power Query and Power BI to work with approximately 13.31M records |
| Excel worksheet row limit | Processed the complete dataset through Power Query rather than relying on direct worksheet display |
| Blank state category in geographic ranking | Investigated source records and identified online transactions as a major cause |
| Online activity affecting geographic interpretation | Created a separate Online Transactions KPI and excluded blank states from physical rankings |
| International map points appeared unusual | Retained them because international merchant activity can be legitimate and there was insufficient evidence to classify them as errors |
| Negative transaction values | Preserved them as potentially legitimate refunds, reversals, corrections, or returns |
| High Cruise Lines average transaction amount | Investigated the business context and retained the plausible value |
| DAX measure appeared blank | Identified an active visual selection and filter context as the cause |
| Different customer counts appeared across pages | Distinguished total customer profiles from unique transacting customers |
| Merchant State KPI was potentially misleading | Renamed it to Merchant Regions |
| Merchant category descriptions needed to be available directly | Merged MCC descriptions into the transaction table |
| Temporary investigation work was not suitable for final presentation | Documented the investigation but excluded the exploratory page from the final report |

---

## 20. Key Analytical Lessons

### Investigate before deleting

Unusual values are not automatically errors.

Negative transactions, missing states, international locations, and high-value merchant categories can all have legitimate explanations.

### Understand filter context

Unexpected DAX results can be caused by:

- Visual selections
- Cross-filtering
- Filters
- Relationships
- Evaluation context

Checking filter context should be part of Power BI troubleshooting.

### Choose metrics carefully

Transaction amount, transaction frequency, average transaction size, active-card count, and activity per card reveal different aspects of performance.

A single metric rarely tells the complete story.

### Separate digital and physical geography

Online transactions should not be forced into a physical location model when meaningful geographic information does not exist.

### Keep final dashboards focused

Exploratory pages are valuable during analysis, but not every investigation belongs in the final presentation.

The final report should contain only visuals that support clear analytical questions.

### Use business context when evaluating anomalies

An unusually high or low value should be assessed against the nature of the underlying business activity before being classified as incorrect.

---

## 21. Key Business Findings

### Debit dominates overall portfolio activity

Debit cards lead in:

- Total transaction value
- Number of active cards
- Transaction frequency per active card

### Credit generates greater value per active card

Credit cards produce approximately **$167K in average spend per active card**, compared with approximately **$138K for debit cards**.

### Transaction value and frequency reveal different merchant leaders

Money Transfer leads by total transaction amount, while Grocery Stores and Supermarkets lead by transaction count.

### Cruise Lines represent a high-value purchase category

The average displayed transaction amount for Cruise Lines is approximately **$1,551**.

### Geographic activity is concentrated in major U.S. markets

California leads states by transaction amount at approximately **$59M**, while Houston leads cities at approximately **$6.6M**.

### Online transactions form a meaningful independent channel

Approximately **2 million transactions** were identified as online and therefore cannot be meaningfully assigned to a physical state.

### The customer base spans multiple generations

The customer population is broadly distributed across age groups, with particularly strong representation among customers aged **18–29** and **60+**.

---

## 22. Skills Demonstrated

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

---

## 23. Repository Structure

```text
credit-card-transaction-analysis/
│
├── README.md
├── PROJECT_DOCUMENTATION.md
├── Credit_Card_Transaction_Analysis.pbix
│
├── images/
│   ├── 01_transaction_overview.png
│   ├── 02_card_product_analysis.png
│   ├── 03_customer_merchant_analysis.png
│   └── 04_geographic_analysis.png
│
└── data/
    └── README.md
```

---

## 24. Final Outcome

The completed project consists of four interactive Power BI dashboard pages supported by a large analytical dataset and custom DAX measures.

The project demonstrates the ability to:

- Work with millions of transaction records
- Profile and transform complex data
- Investigate ambiguous data-quality issues
- Build meaningful business KPIs
- Develop interactive Power BI reports
- Analyze transactions from multiple perspectives
- Troubleshoot DAX and filter-context issues
- Interpret patterns without overstating conclusions
- Document analytical decisions and limitations

The final result is a portfolio-ready business intelligence project that demonstrates both technical Power BI skills and the analytical reasoning required to transform raw financial data into meaningful business insights.

A central principle guided the entire project:

> **Unexpected values should be investigated in their business context before being classified as errors or removed from the data.**
