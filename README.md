# HCL_StreamSync
📊 Sales ETL Data Engineering Project (IICS + SQL)
🚀 Overview

This project demonstrates a complete end-to-end ETL (Extract, Transform, Load) pipeline built using Informatica Intelligent Cloud Services (IICS) and a relational database (SQL Server/Oracle).

The pipeline processes sales transaction data, performs data cleansing, integrates master data, and generates analytical reports (KPIs).

🏫 Project Context
Event: Campus Visit – IMS Ghaziabad
Date: 23 March 2026
Domain: Data Engineering / ETL / Analytics
📁 Dataset Description
🔹 Source Files
File Name	Records	Description
Sales_transactions.csv	16,070	Clean transactional data
Sales_transactions_dirty.csv	1,014	Dirty data requiring cleansing
Product_master.csv	50	Product details
Store_master.csv	8	Store details
🧱 Architecture & Workflow
🔹 Step 1: Data Ingestion
Imported all CSV files into IICS as Source Objects
Created mappings to read transactional and master data
🔹 Step 2: Data Cleansing (Dirty File Handling)

Applied transformation rules:

✔ Convert negative values to positive
✔ Reject invalid records:

Quantity = 0
Discount > 100%
Missing unit price
Null Store ID / Product ID
Invalid date format

✔ Standardized date format → MM/DD/YYYY
✔ Identified duplicate transactions
✔ Applied lookup transformations:

Product Lookup → UNIT_PRICE, CATEGORY, BRAND
Store Lookup → STORE_NAME, CITY, STATE
🔹 Step 3: Data Loading

Loaded processed data into staging tables:

Table Name	Description
STG_SALES_CLEAN	Cleaned sales data
STG_PRODUCT	Product master
STG_STORE	Store master
FACT_SALES	Integrated dataset
🧮 Key Calculations
GROSS_AMOUNT = UNIT_PRICE * QUANTITY
DISCOUNT_VALUE = GROSS_AMOUNT * (DISCOUNT_PERCENT / 100)
NET_REVENUE = GROSS_AMOUNT - DISCOUNT_VALUE
📊 Output Reports (KPIs)
✅ Task 1: Clean Sales Data

File: TGT_CLEAN_SALES.csv

Consolidated clean + valid records
Includes enriched fields from lookups
❌ Task 2: Rejected Records

File: TGT_REJECTED_SALES.csv

Stores invalid records
Includes rejection reason

Example:

Missing PRODUCT_ID → REJECTED
Invalid QUANTITY → REJECTED
📈 Task 3: Category Summary

File: TGT_CATEGORY_SUMMARY.csv

Metrics:

Total Transactions
Total Quantity
Total Revenue

Grouped by:

Month
Category
🥇 Task 4: Top 3 Products Monthly

File: TGT_TOP_3_PRODUCTS_MONTHLY.csv

Identifies best-selling products per month
Uses ranking (RANK / DENSE_RANK)
📉 Task 5: Lowest Selling Product

File: TGT_LOWEST_SELLING_PRODUCT_MONTHLY.csv

Identifies least-performing products
Excludes zero-sales products
🏬 Task 6: Top 5 Products per Store

File: TGT_TOP_5_PRODUCTS_PER_STORE.csv

Store-wise product ranking
Based on quantity sold
🏆 Task 7: Store Leaderboard

File: TGT_STORE_SALES_LEADERBOARD.csv

Metrics:

Total Revenue
Total Transactions
Ranking by revenue
💎 Task 8: High Value Transactions (Compulsory)

File: TGT_HIGH_VALUE_TRANSACTIONS.csv

Filters transactions:
NET_AMOUNT > Monthly Average
🔧 Technologies Used
Informatica Intelligent Cloud Services (IICS)
SQL (Oracle / SQL Server)
CSV Data Sources
ETL Transformations
Expression
Router
Joiner
Aggregator
Lookup
🔍 Key Concepts Implemented
Data Cleansing & Validation
Data Transformation
Lookup Enrichment
Aggregation & KPIs
Ranking (Top N Analysis)
Data Rejection Handling
ETL Pipeline Design
⚠️ Important Business Rules
Transactions without valid product/store → Rejected
Only valid records used for KPI computation
Duplicate detection based on:
TRANSACTION_ID + STORE_ID + DATE + PRODUCT_ID
🎯 Project Outcome

✔ Built a complete ETL pipeline
✔ Improved data quality and reliability
✔ Generated business insights dashboards (CSV reports)
✔ Demonstrated real-world data engineering workflow

💡 Future Enhancements
Dashboard visualization (Power BI / Tableau)
Real-time data streaming
Automation using scheduling
Cloud deployment
