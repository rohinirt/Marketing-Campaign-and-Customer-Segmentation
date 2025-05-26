# Marketing-Campaign-and-Customer-Segmentation

Tableau Link: https://public.tableau.com/app/profile/rohini.tembhurnikar/viz/Marketing_17480166106200/CUSTOMERS

## Objective

The objective of this project is to develop a comprehensive Tableau dashboard that visualizes and analyzes customer segmentation, spending behavior, purchase patterns, and marketing campaign performance. By transforming and cleaning the dataset, and applying intuitive visual storytelling, the dashboard helps businesses understand which customer segments drive the most value, how campaigns are performing across demographics, and where to focus marketing efforts to maximize engagement and revenue.

## Dataset Overview (Data Dictionary)

| Column Name             | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| ID                      | Unique customer identifier                                                  |
| Year_Birth              | Year of birth of the customer                                               |
| Education               | Education level (Basic, Graduation, Master, PhD, etc.)                      |
| Marital_Status          | Marital status of the customer                                              |
| Income                  | Customer’s yearly household income                                          |
| Kidhome                 | Number of children in household                                             |
| Teenhome                | Number of teenagers in household                                            |
| Dt_Customer             | Date of customer enrollment                                                 |
| Recency                | Number of days since last purchase                                          |
| MntWines, MntFruits... | Amount spent on each product category                                       |
| NumWebPurchases         | Number of web purchases made                                                |
| NumCatalogPurchases     | Number of catalog purchases made                                            |
| NumStorePurchases       | Number of in-store purchases                                                |
| NumDealsPurchases       | Purchases made with discounts                                               |
| NumWebVisitsMonth       | Number of web visits in last month                                          |
| AcceptedCmp1–5          | Whether the customer accepted campaign 1 to 5                               |
| Response                | Whether the customer accepted the last campaign                            |
| Complain                | Whether the customer complained                                             |
| Z_CostContact, Z_Revenue| Constant values (not used for analysis)                                     |

---

## Data Preparation & Cleaning

- Null values in spending fields were imputed using the **average value per product category**.
- The dataset was divided into **four sheets**:
  1. **Customer Details** – demographic and personal attributes
  2. **Spending Details** – unpivoted using Power Query to format as: `ID | ProductType | SpendingValue`
  3. **Purchase Details** – unpivoted to: `ID | PurchaseType | PurchaseCount`
  4. **Campaign Details** – unpivoted to: `ID | Campaign | AcceptedFlag`
- All columns were renamed for clarity and consistency.
- Grouping of fields like **age** and **income** was handled using Tableau’s **calculated fields**.


## Tableau Sections & Key Visuals

###  Key Calculated Fields in Tableau
#### Age Group (for segmentation)
```
IF [Year_Birth] >= 1998 THEN "18–25"
ELSEIF [Year_Birth] >= 1988 THEN "26–35"
ELSEIF [Year_Birth] >= 1978 THEN "36–45"
ELSEIF [Year_Birth] >= 1968 THEN "46–55"
ELSEIF [Year_Birth] >= 1958 THEN "56–65"
ELSE "66+"
END
```
#### Income Group (based on range)
```
IF [Income] <= 20000 THEN "Low Income"
ELSEIF [Income] <= 40000 THEN "Lower-Mid Income"
ELSEIF [Income] <= 60000 THEN "Upper-Mid Income"
ELSEIF [Income] <= 80000 THEN "High Income"
ELSE "Very High Income"
END 
```

#### Recency Segment
```
IF [Recency] <= 15 THEN "0–15 Highly Engaged"
ELSEIF [Recency] <= 45 THEN "16–45 Engaged"
ELSEIF [Recency] <= 75 THEN "46–75 Slipping Away"
ELSE "76–99 Churn Risk"
END
```

The dashboard is divided into 4 pages
### 1. **Customers**
- Customer distribution by Age Group, Income Group, Education, and Marital Status
- Complaint rate, kids at home
- RFM Analysis
- (Recency buckets): Engaged, Slipping Away, Churn Risk

### 2. **Spending**
- Total and Average Spending per Product
- Spending patterns by Age Group, Income Group, Education, and Marital Status
- KPIs: 
  - **Total Revenue**: `SUM(Spending)`
  - **Average Revenue per Customer (ARPC)**: `Total Revenue / COUNT(ID)`
  - **Average Order Value (AOV)**: `Total Revenue / Total Purchases`
  - **Revenue per Product Type**: `SUM(Spending) GROUP BY Product`

### 3. **Purchases**
- Total purchases and average purchases by channel (Web, Store, Catalog, Deals)
- Channel preference by demographics
- KPIs:
  - **Total Purchases**: `SUM(PurchaseCount)`
  - **Average Purchases per Customer**: `Total Purchases / COUNT(ID)`
  - **Average Web Visits**: `AVG(WebVisistsMonth)`
  - **Purchase Per Channel** : `SUM(Purchases)/COUND(Channel)`


### 4. **Campaigns**
- Campaign acceptance by Age, Income, Education, Marital Status
- Total acceptances per campaign

## Results & Insights
Wines generated the highest revenue, followed by Meat and Gold products.

Customers aged 46–55 and those in the High/Very High Income bracket showed the highest average spend.

Web is the most used purchase channel, especially by higher-educated customers.

Campaign 1 and Campaign 3 had the highest acceptance rates across most customer segments.

Around 23% of customers fall into the Churn Risk category, indicating potential for retention campaigns.

Customers with no kids contributed to over 85% of total revenue — a critical insight for targeting.

## Conclusion
This dashboard provides actionable insights into marketing performance, customer segmentation, and product-level spend. By cleaning and reshaping the data and applying analytical logic in Tableau, we reveal valuable patterns that businesses can use to improve targeting, enhance campaign ROI, and retain valuable customers.

