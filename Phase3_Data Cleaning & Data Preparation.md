# 🧹 Phase 3 – Data Cleaning & Data Preparation
**Project:** Retail Sales Analytics  
**Dataset:** Sample – Superstore  
**Phase Objective:** Prepare high-quality, analytics-ready data for KPI calculation and dashboard development  

---

## 🎯 1. Objective of This Phase
The primary objective of Phase 3 is to clean, standardize, and prepare the dataset to ensure it is reliable, consistent, and suitable for analytical processing. This phase focuses on improving data quality while preserving business-relevant information for downstream analysis.

Key goals include:
- Handling missing and inconsistent values
- Validating data integrity and granularity
- Standardizing formats and categorical values
- Creating derived fields for analytical use
- Preparing the dataset for SQL analysis and Power BI modeling

---

## 🧾 2. Data Cleaning Scope
The cleaning and preparation process covered the following data domains:

- Order & Shipping Information
- Customer Attributes
- Geographic Fields
- Product Hierarchy
- Sales & Profit Metrics
- Time-based Fields

---

## ⚠️ 3. Missing Values Handling

### 🔍 Identified Issues
- Missing values observed in **Postal Code**
- No missing values in critical transactional or financial metrics

### 🛠 Cleaning Strategy
| Column Name  | Issue Description        | Applied Action |
|-------------|--------------------------|----------------|
| Postal Code | Missing values           | Replaced with `"Unknown"` / kept as NULL |
| Sales       | No missing values        | No action required |
| Profit      | No missing values        | No action required |
| Quantity    | No missing values        | No action required |

**Rationale:**  
Records with missing geographic attributes were preserved to avoid losing valid sales and profit data.

---

## 🧬 4. Duplicate Records & Granularity Validation

### 🔍 Findings
- No fully duplicated rows detected
- Repeated **Order ID** values identified due to line-item level granularity

### 🛠 Actions Taken
- No records removed
- Defined analytical grain as **Order Line Item**
- Aggregations designed to account for multiple products per order

**Key Consideration:**  
All KPI calculations (Total Sales, Profit, Quantity) are performed at the line-item level unless explicitly aggregated.

---

## 🔢 5. Data Type & Format Standardization

### 🛠 Standardization Actions
| Column Name        | Data Type Action |
|-------------------|----------------|
| Order Date        | Converted to Date |
| Ship Date         | Converted to Date |
| Sales             | Numeric (Decimal) |
| Profit            | Numeric (Decimal) |
| Quantity          | Integer |
| Discount          | Decimal (0–1 range) |
| Postal Code       | Text (preserve leading zeros) |

This ensures compatibility with time-based analysis and BI tools.

---

## 🏷️ 6. Categorical Data Normalization

### 🔍 Identified Issues
- Minor casing inconsistencies
- Leading and trailing whitespaces in text fields

### 🛠 Applied Cleaning Steps
- Trimmed whitespace
- Standardized casing (Title Case)
- Validated unique values for:
  - Category
  - Sub-Category
  - Segment
  - Ship Mode
  - Region

**Benefit:**  
Prevents duplicated categories and ensures clean filtering in dashboards.

---

## 🧠 7. Feature Engineering (Derived Columns)

To support trend analysis and KPI reporting, the following derived fields were created:

| Derived Column       | Description |
|--------------------|-------------|
| Order Year          | Year extracted from Order Date |
| Order Month         | Month name derived from Order Date |
| Order Month Number  | Numeric month for sorting |
| Order Quarter       | Calendar quarter (Q1–Q4) |
| Shipping Delay      | Days between Order Date and Ship Date |
| Profit Margin       | Profit / Sales |

These features enable time intelligence and performance analysis.

---

## 📊 8. Data Validation & Outlier Review

### 🔍 Validation Checks
- Negative profit values identified and confirmed as valid (discounts/returns)
- No zero or negative sales detected
- Discount values reviewed and validated

### ✅ Decision
No outliers were removed, as all values reflect realistic business scenarios.

---

## 📐 9. Final Dataset Readiness

### ✅ Data Quality Status
- Fully cleaned and standardized
- Analytics-ready structure
- Suitable for SQL querying and BI modeling

### 🎯 Supported Analysis
- Total Sales and Profit KPIs
- Sales by Category, Region, and Segment
- Top Customers and Products
- Monthly and Quarterly Trends
- Profitability and Margin Analysis

---

## ✅ Phase 3 Outcome
The dataset has been successfully cleaned, validated, and enriched. All identified data quality issues have been addressed, and the dataset is now ready for advanced analysis.

**Next Phase:**  
➡️ **Phase 4 – SQL Analysis & KPI Calculation**

---
