# RetailPulse Dataset

This folder contains the source Excel dataset used to build the **RetailPulse Power BI Analytics** project.

## Source File

`RetailPulse_PowerBI_Practice_Dataset.xlsx`

The Excel workbook acts as the raw data source for the Power BI solution.

---

## Data Processing Flow

The raw Excel data was imported into Power BI and transformed using Power Query.

```text
Raw Excel Dataset
        ↓
Power Query
        ↓
Data Cleaning & Transformation
        ↓
Fact and Dimension Tables
        ↓
Power BI Data Model
        ↓
DAX Measures
        ↓
Interactive Reports
Final Power BI Model
Fact Tables
Fact_Sales_Clean
Fact_Returns
Fact_Targets
Dimension Tables
Dim_Date
Dim_ReturnDate
Dim_Product
Dim_Customer
Dim_Store
Dim_Region
Measures

A dedicated _Measures table is used to organize the DAX measures used throughout the report.

Data Preparation

Power Query was used to prepare the dataset before analysis.

The preparation process included:

Validating column data types
Cleaning transactional sales data
Handling date fields
Preparing sales, returns, and target data
Creating reusable dimension tables
Validating keys used in relationships
Removing or correcting invalid records where required
Preparing the model for dimensional analysis
Date Modeling

A dedicated Dim_Date table supports time-intelligence calculations including:

Previous Year
Year-over-Year %
Previous Month
Month-over-Month %
Year-to-Date

A separate Dim_ReturnDate is used for return-date analysis.

Data Quality Validation

The transformed data was validated through dedicated QA report pages before final deployment.

Validation covered:

Sales totals
Orders
Returns
Refunds
Delivery metrics
Target calculations
Date relationships
Filter behavior
Purpose

This dataset is provided as part of a portfolio project demonstrating an end-to-end Power BI workflow from raw data preparation through modeling, DAX, visualization, QA, security, deployment, and scheduled refresh
