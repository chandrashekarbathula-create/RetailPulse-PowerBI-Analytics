# RetailPulse – Power BI Retail Analytics

## 📊 Project Overview

RetailPulse is an end-to-end retail analytics project developed using Microsoft Power BI.

The project transforms raw Excel retail data into an interactive business intelligence solution covering sales, profitability, customers, products, returns, delivery performance, and business targets.

The project demonstrates the complete BI development lifecycle:

Raw Data → Data Cleaning → Data Transformation → Data Modeling → DAX → Dashboard Development → QA Validation → Row-Level Security → Power BI Service → Gateway → Scheduled Refresh

---

## 🛠 Tools & Technologies

- Microsoft Power BI Desktop
- Power Query
- DAX
- Microsoft Excel
- Power BI Service
- On-premises Data Gateway
- GitHub

---

## 📁 Data Model

The solution uses a dimensional data model containing:

### Dimension Tables

- Dim_Date
- Dim_Product
- Dim_Customer
- Dim_Store
- Dim_Region
- Dim_ReturnDate

### Fact Tables

- Fact_Sales_Clean
- Fact_Returns
- Fact_Targets

A dedicated `_Measures` table is used to organize business measures.

---

## 🧹 Data Preparation

Raw Excel data was imported into Power BI and transformed using Power Query.

Data preparation included:

- Data type validation
- Removing unnecessary data
- Cleaning sales data
- Date handling
- Creating dimension tables
- Preparing sales, returns, and target fact tables
- Validating keys and relationships
- Creating a dedicated date dimension

---

## 🔗 Data Modeling

Relationships were created between the dimension and fact tables to support accurate filtering and analysis.

The model was designed around dimensional modeling principles with dimension tables filtering transactional fact tables.

Special handling was implemented for sales dates and return dates using dedicated date dimensions.

---

## 🧮 DAX & KPI Development

Business measures were created using DAX, including:

### Sales KPIs

- Total Net Sales
- Total Orders
- Units Sold
- Average Order Value
- Sales Previous Year
- Sales YoY %
- Sales Previous Month
- Sales MoM %
- Sales YTD

### Profit KPIs

- Total Profit
- Profit Margin %
- Profit Previous Year
- Profit YoY %
- Profit YTD

### Returns KPIs

- Returned Orders
- Return Rate %
- Total Refund Amount
- Refund Rate %

### Delivery KPIs

- On-Time Orders
- Late Orders
- On-Time Delivery %
- Late Delivery %
- Average Delay Days
- Average Actual Ship Days
- Average Promised Days

### Target KPIs

- Sales Target
- Sales Target Achievement %
- Sales Target Variance
- Profit Target
- Profit Target Achievement %
- Profit Target Variance
- Order Target
- Order Target Achievement %
- Order Target Variance

---

## 📈 Dashboard Pages

The Power BI report contains six main analytical pages:

1. Executive Overview
2. Sales Performance
3. Product & Customer Analysis
4. Returns Analysis
5. Delivery & Operations
6. Target Performance

---

## 🔍 QA & Validation

Dedicated QA pages were developed to validate calculations before deployment.

QA checks included:

- Sales measure validation
- Time intelligence validation
- Returns validation
- Delivery KPI validation
- Target KPI validation
- Relationship/filter validation

This helped ensure that dashboard values matched the underlying transactional data.

---

## 🔐 Row-Level Security

Row-Level Security (RLS) was implemented to restrict report data by region.

Example role:

**South Region**

```DAX
[Region] = "South"
