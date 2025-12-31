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
    SUM(Quantity) AS Total_Quantity
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Sales, 
        Profit, 
        Quantity
    FROM Cleaned_Sales
) t;
```
# KPI Analysis

**Output:**  
| Total_Sales | Total_Profit | Total_Quantity | Avg_Discount | Profit_Margin |
|-------------|-------------|----------------|--------------|---------------|
| 256646.38   | 58577.34   | 2525           | 0.15625      | 0.2281        |
		

**Insight / Observation:**  
- Total sales: 256646.38  
- Total profit: 58577.34  
- Total quantity sold: 2525  
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
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Category, 
        Sub_Category, 
        Sales, 
        Profit
    FROM Cleaned_Sales
) t
GROUP BY Category, Sub_Category
ORDER BY Sales DESC;
```

**Output:**

| Category        | Sub_Category | Sales      | Profit    |
|----------------|-------------|-----------|-----------|
| Furniture       | Phone       | 22,373.15 | 4,563.92  |
| Technology      | Paper       | 21,408.12 | 4,420.52  |
| Office Supplies | Bookcase    | 19,370.01 | 4,642.69  |
| Office Supplies | Chair       | 17,965.29 | 4,186.80  |
| Technology      | Table       | 17,527.43 | 3,476.85  |
| Furniture       | Table       | 17,349.65 | 2,934.92  |
| Technology      | Chair       | 17,344.14 | 3,898.31  |
| Furniture       | Chair       | 17,133.39 | 3,820.61  |
| Furniture       | Bookcase    | 17,020.48 | 5,363.25  |
| Furniture       | Paper       | 16,807.68 | 4,008.79  |
| Office Supplies | Phone       | 16,057.58 | 3,908.47  |
| Technology      | Bookcase    | 15,566.43 | 3,980.23  |
| Office Supplies | Paper       | 14,396.32 | 3,234.01  |
| Technology      | Phone       | 14,152.08 | 3,219.16  |
| Office Supplies | Table       | 12,174.63 | 2,918.81  |

**Insight / Observation:**

- Highest sales are in **Furniture – Phone** and **Technology – Paper**.
- Some products like **Furniture – Bookcase** have lower sales but higher profit, highlighting high-margin niches.
- Office Supplies sub-categories show consistent sales with balanced profitability.

---

### KPI 3 – Sales by Region
**SQL Query:**  
```sql
SELECT 
    Region,
    SUM(Sales) AS Sales,
    SUM(Profit) AS Profit
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Region, 
        Sales, 
        Profit
    FROM Cleaned_Sales
) t
GROUP BY Region
ORDER BY Sales DESC;
```

**Output:**

| Region  | Sales     | Profit    |
|---------|----------|-----------|
| West    | 69,526.07 | 15,287.04 |
| East    | 64,577.63 | 13,989.20 |
| Central | 63,282.81 | 15,644.37 |
| South   | 59,259.87 | 13,656.73 |

**Insight / Observation:**

- The **West region** has the highest sales, while the **South region** has the lowest.
- Profit distribution is relatively balanced across regions, with Central showing slightly higher profitability despite lower sales.
- Regional performance can inform targeted marketing and inventory strategies.
---

### KPI 4 – Top Customers
**SQL Query:**  
```sql
SELECT TOP 10
    Customer_Name,
    SUM(Sales) AS Total_Sales,
    SUM(Profit) AS Total_Profit
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Customer_Name, 
        Sales, 
        Profit
    FROM Cleaned_Sales
) t
GROUP BY Customer_Name
ORDER BY Total_Sales DESC;

```

**Output:**

| Customer_Name | Total_Sales | Total_Profit |
|---------------|------------|--------------|
| Customer 52   | 1,068.72   | 67.04        |
| Customer 75   | 994.87     | 30.50        |
| Customer 122  | 993.32     | -5.92        |
| Customer 22   | 991.41     | 57.25        |
| Customer 213  | 985.01     | 247.90       |
| Customer 68   | 981.38     | 194.01       |
| Customer 84   | 981.37     | 208.28       |
| Customer 77   | 981.33     | 34.19        |
| Customer 323  | 980.57     | -28.49       |
| Customer 249  | 978.74     | 205.59       |

**Insight / Observation:**

- **Customer 52** leads in total sales, with a moderate profit contribution.  
- Some customers, like **Customer 122** and **Customer 323**, show negative profits, indicating returns or heavy discounts.  
- Top customers contribute significantly to revenue, suggesting potential focus for loyalty programs and targeted promotions.

---

### KPI 5 – Monthly Sales Trend
**SQL Query:**  
```sql
SELECT 
    Order_Year,
    Order_Month,
    SUM(Sales) AS Monthly_Sales,
    SUM(Profit) AS Monthly_Profit
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Order_Year, 
        Order_Month, 
        Sales, 
        Profit
    FROM Cleaned_Sales
) t
GROUP BY Order_Year, Order_Month
ORDER BY Order_Year, Order_Month;

```
### KPI 5 – Monthly Sales Trend

**Output:**

| Order_Year | Order_Month | Monthly_Sales | Monthly_Profit |
|------------|------------|---------------|----------------|
| 2021       | April      | 13,722.31     | 4,534.97       |
| 2021       | August     | 18,287.38     | 3,766.41       |
| 2021       | December   | 14,413.61     | 3,610.26       |
| 2021       | February   | 14,075.14     | 3,320.15       |
| 2021       | January    | 15,681.95     | 2,918.43       |
| 2021       | July       | 14,462.28     | 3,247.78       |
| 2021       | June       | 16,160.47     | 3,269.36       |
| 2021       | March      | 18,322.58     | 3,322.00       |
| 2021       | May        | 15,757.33     | 3,970.60       |
| 2021       | November   | 13,971.92     | 3,884.88       |
| 2021       | October    | 15,775.93     | 3,968.26       |
| 2021       | September  | 16,977.14     | 3,387.97       |
| 2022       | April      | 14,720.38     | 2,673.83       |
| 2022       | February   | 14,440.32     | 3,766.30       |
| 2022       | January    | 15,993.31     | 4,120.62       |
| 2022       | March      | 15,437.29     | 2,601.95       |
| 2022       | May        | 8,447.04      | 2,213.57       |

**Insight / Observation:**

- Highest monthly sales in **March and August 2021**, lowest in **May 2022**.  
- Sales and profit show seasonal fluctuations, with peaks early and mid-year.  
- Trend analysis can guide inventory planning and promotional campaigns.

---

### KPI 6 – Profit Margin by Category
**SQL Query:**  
```sql
SELECT 
    Category,
    SUM(Profit)/SUM(Sales) AS Profit_Margin
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Category, 
        Profit, 
        Sales
    FROM Cleaned_Sales
) t
GROUP BY Category
ORDER BY Profit_Margin DESC;
```

**Output:**

| Category        | Profit_Margin |
|----------------|---------------|
| Office Supplies | 0.2362       |
| Furniture       | 0.2281       |
| Technology      | 0.2208       |

**Insight / Observation:**

- **Office Supplies** has the highest profit margin among categories.  
- **Furniture** and **Technology** have slightly lower margins, indicating opportunities for cost optimization or pricing strategy adjustments.  
- Monitoring category-level margins helps prioritize high-margin product segments for marketing and sales focus.
---

### KPI 7 – Discount Analysis by Segment
**SQL Query:**  
```sql
SELECT 
    Segment,
    AVG(Discount) AS Avg_Discount,
    SUM(Sales) AS Total_Sales
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Segment, 
        Sales, 
        Discount
    FROM Cleaned_Sales
) t
GROUP BY Segment;
```

**Output:**

| Segment      | Avg_Discount | Total_Sales |
|-------------|--------------|------------|
| Consumer     | 0.1538       | 95,070.92  |
| Corporate    | 0.1566       | 84,603.86  |
| Home Office  | 0.1520       | 76,437.24  |

**Insight / Observation:**

- Average discounts are similar across segments (~15%).  
- **Consumer segment** generates the highest total sales.  
- Discount strategy appears consistent; focus could be on segment-specific promotions to further boost revenue.
---

### KPI 8 – Shipping Efficiency by Mode
**SQL Query:** 
```sql
SELECT 
    [Ship Mode],
    AVG([Shipping-Delay]) AS Avg_Delay,
    SUM(Profit) / SUM(Sales) * 100 AS Profit_Margin_Percent,
    SUM(Sales) AS Total_Sales
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        [Ship Mode], 
        Sales, 
        Profit, 
        [Shipping-Delay]
    FROM Cleaned_Sales
) t
GROUP BY [Ship Mode];
```

**Output:**

| Ship Mode       | Avg_Delay | Profit_Margin_Percent | Total_Sales |
|----------------|-----------|----------------------|------------|
| First Class     | 1         | 20.57                | 65,550.01  |
| Same Day        | 1         | 23.03                | 70,653.19  |
| Second Class    | 1         | 23.54                | 55,773.39  |
| Standard Class  | 1         | 24.25                | 64,669.79  |

**Insight / Observation:**

- All shipping modes maintain a consistent average delay of 1 day, indicating operational efficiency.  
- **Standard Class** shows the highest profit margin, while **First Class** has the lowest, highlighting cost impact of expedited shipping.  
- Efficient shipping modes can be leveraged to optimize profitability and customer satisfaction.

**Note:** Profit margin is calculated using weighted logic (SUM(Profit) / SUM(Sales)) to ensure accurate profitability analysis at aggregated levels.

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
FROM (
    SELECT DISTINCT 
        [Order ID], 
        [Product Name], 
        Category, 
        Sub_Category, 
        Profit, 
        Sales
    FROM Cleaned_Sales
) t
GROUP BY Category, Sub_Category;
```
### KPI 9 – Sub-Category Profitability Ranking

**Output:**

| Category        | Sub_Category | Profit_Margin | Margin_Rank |
|----------------|-------------|---------------|-------------|
| Furniture       | Bookcase    | 0.3151        | 1           |
| Furniture       | Paper       | 0.2385        | 2           |
| Furniture       | Chair       | 0.2229        | 3           |
| Furniture       | Phone       | 0.2039        | 4           |
| Furniture       | Table       | 0.1691        | 5           |
| Office Supplies | Phone       | 0.2434        | 1           |
| Office Supplies | Table       | 0.2397        | 2           |
| Office Supplies | Bookcase    | 0.2396        | 3           |
| Office Supplies | Chair       | 0.2330        | 4           |
| Office Supplies | Paper       | 0.2246        | 5           |
| Technology      | Bookcase    | 0.2556        | 1           |
| Technology      | Phone       | 0.2274        | 2           |
| Technology      | Chair       | 0.2247        | 3           |
| Technology      | Paper       | 0.2064        | 4           |
| Technology      | Table       | 0.1983        | 5           |

**Insight / Observation:**

- **Furniture – Bookcase** and **Technology – Bookcase** are the most profitable niches in their categories.  
- Some high-sales products like **Furniture – Phone** have lower profit margins, highlighting potential areas for margin improvement.  
- Sub-category ranking helps focus marketing and inventory strategies on high-margin products to maximize net profitability.
---

### Data Quality & Assumptions

During KPI validation, duplicated transactional records were identified.
As the dataset lacks a unique Product ID, Order ID and Product Name were used
as a composite key to remove duplicated rows and ensure accurate KPI aggregation.


✅ Phase 4 Outcome
All key KPIs have been calculated (SQL queries to be added). Outputs are ready for analysis and dashboard visualization. Phase 4 documentation is complete and structured consistently with previous phases.

Next Phase:
➡️ Phase 5 – Dashboard Development & Visualization
