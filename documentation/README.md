# RetailPulse Analytics – Technical Documentation

## 1. Project Overview

RetailPulse Analytics is an end-to-end Power BI retail analytics project designed to demonstrate a complete business intelligence workflow.

The project covers the full lifecycle:

**Raw Excel Data → Power Query → Data Cleaning → Data Modeling → DAX → Dashboard Development → QA Validation → Row-Level Security → Power BI Service → Gateway → Scheduled Refresh**

The solution analyzes:

- Sales performance
- Profitability
- Orders and units sold
- Product performance
- Customer performance
- Returns and refunds
- Delivery performance
- Regional performance
- Business targets and achievement

---

# 2. Technology Stack

| Technology | Purpose |
|---|---|
| Microsoft Excel | Raw source data |
| Power BI Desktop | Data preparation, modeling and reporting |
| Power Query | ETL and data transformation |
| DAX | Business calculations and KPIs |
| Power BI Service | Report publishing and sharing |
| Power BI Gateway | Refreshing local Excel data |
| GitHub | Portfolio documentation and project versioning |

---

# 3. Source Dataset

The project uses an Excel workbook:

`RetailPulse_PowerBI_Practice_Dataset.xlsx`

The source data contains information related to:

- Sales transactions
- Customers
- Products
- Stores
- Regions
- Returns
- Sales and profit targets
- Order and delivery dates

The workbook was imported into Power BI Desktop for transformation and analysis.

---

# 4. Data Preparation – Power Query

The raw Excel data was transformed using Power Query before being loaded into the Power BI model.

The ETL process included:

- Inspecting source tables
- Validating column names
- Assigning appropriate data types
- Cleaning transactional data
- Preparing date columns
- Checking blank and invalid values
- Preparing sales data for analysis
- Preparing returns data
- Preparing target data
- Creating reusable dimension tables
- Checking keys used in model relationships

The cleaned sales table was maintained as:

`Fact_Sales_Clean`

This ensured that reporting calculations were based on a controlled analytical dataset rather than directly on unvalidated raw data.

---

# 5. Data Model

The project follows a dimensional modeling approach.

## Fact Tables

### Fact_Sales_Clean

Contains transactional sales information used for:

- Net sales
- Profit
- Orders
- Units sold
- Discounts
- Delivery calculations
- Customer analysis
- Product analysis

### Fact_Returns

Contains return transactions used for:

- Returned orders
- Return rate
- Refund amount
- Return reasons
- Return trends

### Fact_Targets

Contains business targets used for comparison against actual performance.

Targets include:

- Sales targets
- Profit targets
- Order targets

---

# 6. Dimension Tables

The analytical model contains the following dimension tables:

### Dim_Date

Central calendar table used for sales time intelligence.

### Dim_ReturnDate

Separate date dimension used for return-date analysis.

### Dim_Product

Contains product-related attributes.

### Dim_Customer

Contains customer-related attributes.

### Dim_Store

Contains store information.

### Dim_Region

Contains regional information and supports regional filtering and Row-Level Security.

---

# 7. Measures Table

A dedicated table named:

`_Measures`

was created to organize business calculations separately from transactional tables.

This makes the semantic model easier to maintain and navigate.

---

# 8. Data Relationships

Relationships were created between dimension tables and fact tables to support dimensional filtering.

The model connects dimensions such as:

- Date
- Product
- Customer
- Store
- Region

to the appropriate fact tables.

Particular attention was given to date relationships because sales and returns represent different business events.

`Dim_Date` supports primary sales analysis while `Dim_ReturnDate` supports return-date analysis.

Relationship behavior was validated to avoid incorrect filter propagation and ambiguous calculations.

---

# 9. Core DAX Measures

The project contains measures covering several analytical areas.

## Sales Measures

Examples include:

- Total Net Sales
- Total Profit
- Total Orders
- Units Sold
- Average Order Value
- Profit Margin %
- Discount %

## Time Intelligence

Measures were developed for:

- Sales Previous Year
- Sales YoY %
- Sales Previous Month
- Sales MoM %
- Sales YTD
- Profit Previous Year
- Profit YoY %
- Profit YTD
- Orders Previous Year

These measures use the dedicated date dimension.

---

# 10. Returns Measures

Return analytics includes measures such as:

- Returned Orders
- Returned Orders Trend
- Return Rate %
- Total Refund Amount
- Refund Rate %

Return analysis was validated separately because return transactions have their own dates and analytical context.

---

# 11. Delivery Measures

Delivery and operational KPIs include:

- On-Time Orders
- Late Orders
- On-Time Delivery %
- Late Delivery %
- Average Actual Ship Days
- Average Promised Days
- Average Delay Days

These measures allow the report to evaluate operational performance in addition to financial performance.

---

# 12. Target Measures

Target analysis compares actual business results against planned targets.

Measures include:

- Sales Target
- Sales Target Achievement %
- Sales Target Variance
- Profit Target
- Profit Target Achievement %
- Profit Target Variance
- Order Target
- Order Target Achievement %
- Order Target Variance

This enables management to identify the difference between actual and planned performance.

---

# 13. Report Pages

The final report contains six main analytical pages.

## 1. Executive Overview

Provides a high-level management view of:

- Net Sales
- Profit
- Orders
- Units Sold
- Profit Margin
- Returns
- Refund Amount
- On-Time Delivery
- Late Orders
- Average Delay
- Monthly Sales Trend
- Regional Sales
- Top Products

## 2. Sales Performance

Focuses on:

- Sales trends
- Year-over-Year analysis
- Month-over-Month analysis
- Average Order Value
- Discounts
- Profitability

## 3. Product & Customer Analysis

Analyzes:

- Product performance
- Customer performance
- Sales contribution
- Units sold
- Orders
- Average Order Value

## 4. Returns Analysis

Analyzes:

- Returned orders
- Return rate
- Refund amount
- Refund rate
- Return reasons
- Return trends

## 5. Delivery & Operations

Tracks:

- On-Time Delivery
- Late Orders
- Actual Ship Days
- Promised Delivery Days
- Average Delay

## 6. Target Performance

Compares actual performance against:

- Sales targets
- Profit targets
- Order targets

using achievement and variance measures.

---

# 14. QA Framework

Dedicated QA pages were created before deployment.

These include:

- QA Measures
- QA Targets
- QA Returns
- QA Delivery
- QA Test
- Temporary Table visual

These pages were used to validate calculations independently of the presentation dashboards.

---

# 15. QA Validation Example

A test scenario using:

**Year = 2024**  
**Region = South**

produced the following key results:

| KPI | Result |
|---|---:|
| Total Net Sales | 4.55M |
| Total Profit | 1.12M |
| Total Orders | 245 |
| Units Sold | 405 |
| Profit Margin | 24.63% |
| On-Time Delivery | 52.24% |
| Late Orders | 117 |
| Average Delay Days | 2.38 |

These values were checked across report visuals and QA pages to validate filter propagation and calculation consistency.

---

# 16. Return Validation

Return calculations were validated independently using the QA Returns page.

For the selected test context, individual return records and return-reason categories were inspected.

Return reasons included examples such as:

- Quality Issue
- Changed Mind
- Late Delivery
- Damaged
- Wrong Item

This validation helped confirm the return calculation logic and return-date filtering behavior.

---

# 17. Row-Level Security

Row-Level Security was implemented to restrict report data by region.

A role named:

`South Region`

was created.

The RLS rule was applied to `Dim_Region`:

```DAX
[Region] = "South"
```

The role was tested in Power BI Desktop using **View as**.

During testing:

- Only South-region data was displayed.
- The Region slicer was restricted to South.
- Report visuals responded correctly to the security filter.

The role was subsequently published to Power BI Service and a user was assigned to the role.

---

# 18. Publishing to Power BI Service

After development and validation, the PBIX report was published to Power BI Service.

Publishing created:

- Power BI Report
- Power BI Semantic Model

The report was then opened in Power BI Service and validated after deployment.

---

# 19. On-Premises Data Gateway

Because the source Excel workbook resides on a local Windows file path, an On-premises Data Gateway in personal mode was installed and configured.

The gateway was successfully registered and confirmed as:

**Online and ready to be used**

The semantic model was then associated with the personal gateway.

---

# 20. Data Source Credentials

During the first Power BI Service refresh attempt, the refresh failed because data-source credentials were missing.

The issue was diagnosed through the refresh error details.

The local Excel data source credentials were then configured through the semantic model settings.

After updating the credentials, the data source was successfully recognized.

---

# 21. Refresh Validation

An on-demand refresh was performed after configuring the gateway and credentials.

The first attempt failed because the required credentials were not yet available.

After correcting the data-source configuration, the next refresh completed successfully.

This confirmed that the complete refresh pipeline was working:

```text
Local Excel File
       ↓
On-Premises Data Gateway
       ↓
Power BI Semantic Model
       ↓
Power BI Report
```

---

# 22. Scheduled Refresh

Automatic refresh was configured in Power BI Service.

Configuration:

- Frequency: Daily
- Time zone: UTC+05:30 Chennai, Kolkata, Mumbai, New Delhi
- Refresh time: 9:00 AM
- Failure notifications: Enabled for semantic model owner

This allows the deployed semantic model to automatically retrieve updated source data through the gateway.

---

# 23. Production Deployment Flow

The final deployment architecture is:

```text
Excel Source
     ↓
Power Query ETL
     ↓
Clean Fact & Dimension Tables
     ↓
Power BI Semantic Model
     ↓
DAX Measures
     ↓
QA Validation
     ↓
Row-Level Security
     ↓
Power BI Report
     ↓
Power BI Service
     ↓
On-Premises Gateway
     ↓
Scheduled Refresh
```

---

# 24. Project Challenges Solved

Several realistic BI development issues were handled during the project.

### Date Relationship Issue

Unmatched return dates initially produced blank date-group results.

The date model and return-date handling were corrected and validated.

### Relationship Configuration

Model relationships and filtering behavior were reviewed to ensure calculations responded correctly to dimensions.

### Return Calculation Validation

Return calculations were separately validated using QA tables to distinguish return-event calculations from sales-context calculations.

### Power BI Service Credentials

Scheduled refresh initially failed because the local source credentials were unavailable to Power BI Service.

The data source was configured through the gateway and credentials were updated.

### Scheduled Refresh

After resolving the gateway and credential configuration, an on-demand refresh completed successfully and the daily refresh schedule was activated.

---

# 25. Skills Demonstrated

This project demonstrates practical experience with:

**Power BI**
- Report development
- Interactive dashboards
- Filters and slicers
- KPI reporting

**Power Query**
- ETL
- Data cleaning
- Data transformation
- Data type management

**Data Modeling**
- Fact and dimension modeling
- Relationships
- Date dimensions
- Filter propagation

**DAX**
- Aggregation measures
- Ratio measures
- Time intelligence
- Target calculations
- Operational KPIs

**Quality Assurance**
- Dedicated QA pages
- Measure validation
- Filter testing
- Reconciliation

**Security**
- Row-Level Security
- Role creation
- User assignment

**Deployment**
- Power BI Service
- Semantic models
- On-premises gateway
- Data-source credentials
- Scheduled refresh

**Version Control & Portfolio**
- GitHub repository structure
- Technical documentation
- Dataset documentation
- Dashboard screenshots
- PBIX distribution

---

# 26. Repository Structure

```text
RetailPulse-PowerBI-Analytics/
│
├── README.md
│
├── dashboard/
│   ├── README.md
│   └── RetailPulse_Analytics.pbix
│
├── dataset/
│   ├── README.md
│   └── RetailPulse_PowerBI_Practice_Dataset.xlsx
│
├── documentation/
│   └── README.md
│
└── screenshots/
    ├── README.md
    ├── 01-executive-overview.png
    ├── 02-sales-performance.png
    ├── 03-product-customer-analysis.png
    ├── 04-returns-analysis.png
    ├── 05-delivery-operations.png
    └── 06-target-performance.png
```

---

# 27. End-to-End Project Summary

This project demonstrates the complete lifecycle of a Power BI analytics solution:

**Business Requirement → Raw Data → ETL → Data Model → DAX → Dashboard → QA → Security → Deployment → Gateway → Automated Refresh**

The result is a portfolio-ready retail analytics solution demonstrating both report-development skills and practical Power BI deployment knowledge.
