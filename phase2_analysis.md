# Phase 2 - Data Understanding & Data Assessment

## 1. Dataset Overview

**Dataset Name:** Sample - Superstore  
**Domain:** Retail Sales  
**Format:** Excel  
**Granularity:** Order line-item level  

The dataset represents historical retail sales transactions. Each record corresponds to a product-level entry within a customer order. The data includes order information, customer attributes, product hierarchy, sales metrics, and profitability measures.

This phase focuses on understanding the structure, scope, and quality of the data before performing any cleaning or transformation.

---

## 2. Data Structure Summary

The dataset consists of the following logical groups of fields:

- **Order Information:** Order ID, Order Date, Ship Date, Ship Mode  
- **Customer Information:** Customer ID, Customer Name, Segment  
- **Geographical Information:** Country, Region, State, City, Postal Code  
- **Product Information:** Category, Sub-Category, Product Name  
- **Sales Metrics:** Sales, Quantity, Discount, Profit  

The dataset structure is suitable for both transactional analysis and aggregated reporting.

---

## 3. Data Dictionary

| Column Name     | Description                                      | Data Type |
|-----------------|--------------------------------------------------|-----------|
| Order ID        | Unique identifier for each customer order        | String    |
| Order Date      | Date when the order was placed                   | Date      |
| Ship Date       | Date when the order was shipped                  | Date      |
| Ship Mode       | Shipping method used                             | String    |
| Customer ID     | Unique identifier for each customer              | String    |
| Customer Name   | Customer full name                               | String    |
| Segment         | Customer segment classification                  | String    |
| Country         | Country of the transaction                       | String    |
| Region          | Sales region                                     | String    |
| State           | State name                                       | String    |
| City            | City name                                        | String    |
| Postal Code     | Postal or ZIP code                               | String    |
| Category        | High-level product category                      | String    |
| Sub-Category    | Product sub-category                             | String    |
| Product Name    | Product description                              | String    |
| Sales           | Total sales value for the line item              | Numeric   |
| Quantity        | Number of units sold                             | Integer   |
| Discount        | Discount applied to the sale                     | Numeric   |
| Profit          | Profit generated from the sale                   | Numeric   |

---

## 4. Missing Values Assessment

A preliminary assessment of missing values was performed across all columns.

- Most core transactional and sales-related fields are fully populated.
- Missing values were observed primarily in specific geographical attributes (e.g. postal code).
- No critical sales metrics (Sales, Quantity, Profit) were found to be missing.

**Observation:**  
Missing geographic attributes may affect location-based aggregation and mapping but do not prevent overall sales or trend analysis.

---

## 5. Duplicate Records Assessment

Duplicate checks were performed at different levels:

- No fully identical rows were identified.
- Repeated Order IDs were observed, which is expected due to the line-item structure of retail transactions where a single order can contain multiple products.

**Observation:**  
Duplicate Order IDs do not indicate data quality issues and should be handled appropriately during aggregation and KPI calculations.

---

## 6. Data Type and Format Review

- Date fields are consistently represented and suitable for time-based analysis.
- Numeric fields (Sales, Profit, Quantity, Discount) contain valid numeric values.
- Categorical fields show consistent labeling, though minor standardization (e.g. casing, trimming) may be required.
- Postal Code is stored as a string to preserve leading zeros where applicable.

---

## 7. Key Observations for Data Cleaning Phase

Based on the data assessment:

- Minor missing values require handling in selected columns.
- Categorical fields may require standardization.
- Aggregation logic must account for line-item granularity.
- The dataset is suitable for KPI calculation, trend analysis, and dashboard development after cleaning.

---

**Outcome of Phase 2:**  
The dataset structure, limitations, and data quality considerations have been identified and documented. The project is ready to proceed to the data cleaning and preparation phase.
