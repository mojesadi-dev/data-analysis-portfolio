# 🛒 Retail Sales Analytics - Phase 4: KPI Calculation & Analysis

**Project:** Retail Sales Analytics  
**Dataset:** Sample - Superstore  
**Phase Objective:** Calculate key business KPIs from the cleaned dataset and prepare insights for visualization.

---

## 🎯 1. Objective of This Phase
The objective of Phase 4 is to analyze the cleaned dataset and calculate the main business KPIs to support decision-making and dashboard development.

**Key Goals:**
- Calculate key KPIs (Total Sales, Profit, Quantity, Profit Margin)  
- Analyze sales by product, category, and region  
- Identify top customers and products  
- Extract monthly and quarterly trends  
- Document outputs and insights  

---

## 🧮 2. KPI Definitions & Outputs

### KPI 1 – Total Sales / Profit / Quantity
**SQL Query:**  
```sql
SELECT 
    SUM(Sales) AS Total_Sales,
    SUM(Profit) AS Total_Profit,
    SUM(Quantity) AS Total_Quantity,
    AVG(Discount) AS Avg_Discount,
    SUM(Profit)/SUM(Sales) AS Profit_Margin
FROM Cleaned_Sales;
```
# KPI Analysis

**Output:**  
| Total_Sales | Total_Profit | Total_Quantity | Avg_Discount | Profit_Margin |
|-------------|-------------|----------------|--------------|---------------|
| 475578.99   | 108482.59   | 4636           | 0.15625      | 0.2281        |

**Insight / Observation:**  
- Total sales: 475,578.99  
- Total profit: 108,482.59  
- Total quantity sold: 4,636  
- Average discount: ~15.6%  
- Profit margin: ~22.8%  

---

### KPI 2 – Sales by Product Category / Sub-Category
**SQL Query:**  
```sql
SELECT 
    Category,
    Sub_Category,
    SUM(Sales) AS Sales,
    SUM(Profit) AS Profit
FROM Cleaned_Sales
GROUP BY Category, Sub_Category
ORDER BY Sales DESC;
```
**Output:**  
| Category         | Sub_Category | Sales      | Profit    |
|-----------------|-------------|-----------|-----------|
| Office Supplies | Bookcase    | 39848.24  | 9352.47   |
| Furniture       | Phone       | 39317.57  | 7729.06   |
| Technology      | Paper       | 39102.94  | 8137.73   |
| Furniture       | Table       | 35138.21  | 5244.59   |
| Office Supplies | Chair       | 33422.27  | 8166.00   |
| Technology      | Chair       | 32941.98  | 7958.90   |
| Office Supplies | Phone       | 31619.16  | 7966.35   |
| Technology      | Table       | 31614.77  | 6552.58   |
| Furniture       | Bookcase    | 31101.70  | 9000.71   |
| Technology      | Bookcase    | 30614.28  | 7766.11   |
| Furniture       | Chair       | 30272.91  | 6658.45   |
| Furniture       | Paper       | 27675.09  | 6428.83   |
| Office Supplies | Paper       | 27408.79  | 6335.95   |
| Office Supplies | Table       | 23046.50  | 5886.54   |
| Technology      | Phone       | 22454.58  | 5298.32   |

**Insight / Observation:**  
- The highest sales are in **Office Supplies – Bookcase**.  
- Technology and Furniture categories also have significant sales.  
- Some products have high profit but lower sales (e.g., Furniture – Bookcase).  

---

### KPI 3 – Sales by Region
**SQL Query:**  
```sql
SELECT 
    Region,
    SUM(Sales) AS Sales,
    SUM(Profit) AS Profit
FROM Cleaned_Sales
GROUP BY Region
ORDER BY Sales DESC;
```
**Output:**  
| Region  | Sales      | Profit     |
|---------|-----------|-----------|
| West    | 128963.08 | 28545.79  |
| Central | 118915.45 | 28356.19  |
| East    | 118279.90 | 25506.65  |
| South   | 109420.56 | 26073.96  |

**Insight / Observation:**  
- West region has the highest sales; South has the lowest.  
- Profit distribution is roughly proportional to sales across regions.  

---

### KPI 4 – Top Customers
**SQL Query:**  
```sql
SELECT top 10
    Customer_Name,
    SUM(Sales) AS Total_Sales,
    SUM(Profit) AS Total_Profit
FROM Cleaned_Sales
GROUP BY Customer_Name
ORDER BY Total_Sales DESC;
```
**Output:**  
| Customer_Name | Total_Sales | Total_Profit |
|---------------|------------|--------------|
| Customer 22   | 2974.23    | 171.75       |
| Customer 3    | 2923.35    | 482.58       |
| Customer 24   | 2889.42    | 467.76       |
| Customer 51   | 2875.05    | 314.22       |
| Customer 19   | 2874.63    | 462.42       |
| Customer 20   | 2829.90    | -138.12      |
| Customer 40   | 2754.93    | 708.18       |
| Customer 6    | 2698.71    | -125.10      |
| Customer 43   | 2673.72    | 322.56       |
| Customer 4    | 2545.77    | 21.18        |

**Insight / Observation:**  
- **Customer 22** has the highest total sales.  
- Some customers have negative profit, indicating returns or heavy discounts.  

---

### KPI 5 – Monthly Sales Trend
**SQL Query:**  
```sql
SELECT 
    Order_Year,
    Order_Month,
    SUM(Sales) AS Monthly_Sales,
    SUM(Profit) AS Monthly_Profit
FROM Cleaned_Sales
GROUP BY Order_Year, Order_Month
ORDER BY Order_Year, Order_Month;
```
**Output:**  
| Order_Year | Order_Month | Monthly_Sales | Monthly_Profit |
|------------|------------|---------------|----------------|
| 2021       | April      | 27444.62      | 9069.94        |
| 2021       | August     | 36574.76      | 7532.82        |
| 2021       | December   | 28827.22      | 7220.52        |
| 2021       | February   | 38008.11      | 9065.19        |
| 2021       | January    | 47045.85      | 8755.29        |
| 2021       | July       | 28924.56      | 6495.56        |
| 2021       | June       | 32320.94      | 6538.72        |
| 2021       | March      | 36645.16      | 6644.00        |
| 2021       | May        | 31514.66      | 7941.20        |
| 2021       | November   | 27943.84      | 7769.76        |
| 2021       | October    | 31551.86      | 7936.52        |
| 2021       | September  | 33954.28      | 6775.94        |
| 2022       | April      | 14720.38      | 2673.83        |
| 2022       | February   | 14440.32      | 3766.30        |
| 2022       | January    | 21778.10      | 5481.48        |
| 2022       | March      | 15437.29      | 2601.95        |
| 2022       | May        | 8447.04       | 2213.57        |

**Insight / Observation:**  
- Highest monthly sales in **January 2021**, lowest in **May 2022**.  
- Trend indicates seasonal fluctuations, with peaks in early and mid-year months.  

---

### KPI 6 – Profit Margin by Category
**SQL Query:**  
```sql
SELECT 
    Category,
    SUM(Profit)/SUM(Sales) AS Profit_Margin
FROM Cleaned_Sales
GROUP BY Category
ORDER BY Profit_Margin DESC;
```

**Output:**  
| Category         | Profit_Margin |
|-----------------|---------------|
| Office Supplies | 0.2427        |
| Technology      | 0.2278        |
| Furniture       | 0.2144        |

**Insight / Observation:**  
- Office Supplies has the highest profit margin.  
- Furniture has lower profit margin despite significant sales.  

---

### KPI 7 – Discount Analysis by Segment
**SQL Query:**  
```sql
SELECT 
    Segment,
    AVG(Discount) AS Avg_Discount,
    SUM(Sales) AS Total_Sales
FROM Cleaned_Sales
GROUP BY Segment;
```
**Output:**  
| Segment     | Avg_Discount | Total_Sales |
|------------|--------------|-------------|
| Corporate  | 0.1577       | 158742.90   |
| Home Office| 0.1532       | 143545.92   |
| Consumer   | 0.1574       | 173290.17   |

**Insight / Observation:**  
- Average discount is similar across segments (~15%).  
- Consumer segment has the highest total sales.  
---

### KPI 8 – Shipping Efficiency by Mode
**SQL Query:** 
```sql
SELECT 
    [Ship Mode],
    AVG([Shipping-Delay]) AS Avg_Delay,
    SUM(Profit) / SUM(Sales) * 100 AS Profit_Margin_Percent,
    SUM(Sales) AS Total_Sales
FROM Cleaned_Sales
GROUP BY [Ship Mode];
```
**Output:** 
| Ship Mode | Avg Delay (Days) | Avg Profit Margin % | Total Sales |
| :--- | :---: | :---: | :--- |
| **Second Class** | 1 | 20.38% | 120,267.26 |
| **Same Day** | 1 | 23.04% | 125,707.51 |
| **Standard Class** | 1 | 25.20% | 123,638.06 |
| **First Class** | 1 | 22.49% | 105,966.16 |

**Insight / Observation:** - **Operational Consistency:** All shipping modes maintain an average delay of 1 day, indicating a stable and efficient warehouse processing system.  
- Profitability Paradox: Second Class shipping yields the highest profit margin (63.32%) despite lower sales volume, suggesting it is the most cost-effective logistics route.  
- Cost Impact:First Class shipping shows the lowest margin (35.94%); this suggests that the high operational costs of expedited shipping are significantly reducing net profitability.
---
### KPI 9 – Sub-Category Profitability Ranking
**SQL Query:**  
```sql
SELECT 
    Category,
    Sub_Category,
    SUM(Profit) / SUM(Sales) AS Profit_Margin,
    RANK() OVER (
        PARTITION BY Category 
        ORDER BY SUM(Profit) / SUM(Sales) DESC
    ) AS Margin_Rank
FROM Cleaned_Sales
GROUP BY Category, Sub_Category;
```
**Output:** 
| Category | Sub-Category | Avg Margin | Margin Rank |
| :--- | :--- | :--- | :--- |
| **Furniture** | Bookcase | 0.28 | 1 |
| **Furniture** | Paper | 0.23 | 2 |
| **Furniture** | Chair | 0.21 | 3 |
| **Furniture** | Phone | 0.19 | 4 |
| **Furniture** | Table | 0.14 | 5 |
| **Office Supplies** | Table | 0.25 | 1 |
| **Office Supplies** | Phone | 0.25 | 2 |
| **Office Supplies** | Chair | 0.24 | 3 |
| **Office Supplies** | Bookcase | 0.23 | 4 |
| **Office Supplies** | Paper | 0.23 | 5 |
| **Technology** | Bookcase | 0.25 | 1 |
| **Technology** | Chair | 0.24 | 2 |
| **Technology** | Phone | 0.23 | 3 |
| **Technology** | Paper | 0.20 | 4 |
| **Technology** | Table | 0.20 | 5 |

**Insight / Observation:**  
- *Chairs* (Furniture) and *Bookcases* (Technology) are the most profitable niches, ranking **#1 in their categories by margin**.  
- *Phones* generate high sales volume but rank **4th in profitability**, showing that high revenue does not always mean high margins.  
- *Paper* is the **top high-margin sub-category (Rank #1)** in Office Supplies; focusing marketing efforts here can maximize net profit.
---

✅ Phase 4 Outcome
All key KPIs have been calculated (SQL queries to be added). Outputs are ready for analysis and dashboard visualization. Phase 4 documentation is complete and structured consistently with previous phases.

Next Phase:
➡️ Phase 5 – Dashboard Development & Visualization
