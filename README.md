# E-Commerce-Data-Analysis-with-SQL
# E-Commerce SQL Data Analysis

This guide demonstrates how to use SQL for extracting valuable insights from an e-commerce database. It includes sample queries and their outputs for various business analysis scenarios.

## Table of Contents
1. [Top Product Sales Analysis](#top-product-sales-analysis)
2. [Average Order Value by Customer Type](#average-order-value-by-customer-type)
3. [Customer Lifetime Value Analysis](#customer-lifetime-value-analysis)
4. [Product Category Performance](#product-category-performance)
5. [Profitability by Customer Segment](#profitability-by-customer-segment)
6. [Daily Sales Trend Analysis](#daily-sales-trend-analysis)
7. [Query Optimization Tips](#query-optimization-tips)

## Top Product Sales Analysis

Identifies the top 5 best-selling products based on total quantity sold.

```sql
#TOP 5 SALES GROUP BY PRODUCT
select Product, Sum(Quantity)as Total_Sales from "e-commerce dataset" group by Product order by Total_Sales desc limit 5;
```

**Output:**
| Product | Total_Sales |
|---------|------------|
| Titan watch | 2436 |
| Formal Shoes | 2418 |
| Suits | 2362 |
| Sports Wear | 2356 |
| T-Shirts | 2355 |

**Business Insight:** Titan watches are the top-selling product, closely followed by Formal Shoes. The top 5 products have similar sales volumes, suggesting consistent performance across these popular items.

## Average Order Value by Customer Type

Calculates the average sales amount by customer login type, rounded to 2 decimal places.

```sql
#AVERAGE ORDER VALUE BY CUSTOMER LOGIN PRODUCT
select Customer_Login_type, round(avg(Sales),2) as Average_Sales from "e-commerce dataset" group by Customer_Login_type
```

**Output:**
| Customer_Login_type | Average_Sales |
|---------------------|--------------|
| Member | 160.1 |
| Guest | 164.39 |
| New | 180.25 |
| First Sign-Up | 171.83 |

**Business Insight:** New customers have the highest average order value at $180.25, while members have the lowest at $160.1. This suggests that new customers might be making larger initial purchases, while members may be making more frequent but smaller purchases.

## Customer Lifetime Value Analysis

Identifies the top 10 customers with the highest lifetime value based on total spending and profit generated.

```sql
#Customers with highest lifetime values
select Customer_Id, sum(Sales) as Total_Spent, Sum(Profit) as Total_Profit from "e-commerce dataset" 
group by Customer_Id order by Total_Spent desc 
limit 10;
```

**Output:**
| Customer_Id | Total_Spent | Total_Profit |
|-------------|------------|-------------|
| 39084 | 881 | 480.3 |
| 13264 | 853 | 475.3 |
| 16533 | 805 | 422.8 |
| 58117 | 773 | 406.3 |
| 34222 | 762 | 365.7 |
| 39369 | 726 | 426.9 |
| 32056 | 713 | 404.5 |
| 13810 | 710 | 321.2 |

**Business Insight:** The top customer (ID: 39084) has spent $881 and generated $480.3 in profit. There's a strong correlation between total spending and total profit across high-value customers, with profit margins averaging around 54% for these top customers.

## Product Category Performance

Analyzes sales, profit, and quantity metrics aggregated by product category.

```sql
# TOTAL SALES, TOTAL PROFIT, TOTAL QUANTITY BY PRODUCT CATEGORY
select Product_Category , sum(Sales) as total_sales, Sum(profit) as Total_Profit,
sum(Quantity) as Total_Quantity from "e-commerce dataset" group by Product_Category;
```

**Output:**
| Product_Category | total_sales | Total_Profit | Total_Quantity |
|-----------------|------------|-------------|---------------|
| Auto & Accessories | 904166 | 396292.6 | 14849 |
| Fashion | 1738202 | 828782.3 | 25789 |

**Business Insight:** The Fashion category significantly outperforms Auto & Accessories in all metrics, with nearly twice the sales ($1.74M vs $904K), profit ($829K vs $396K), and quantity sold (25.8K vs 14.8K).

## Profitability by Customer Segment

Compares average shipping costs and profit margins across different customer segments.

```sql
#SALES VS PROFIT
select round(avg(Shipping_Cost),2) as Total_Sales, round(avg(Profit),2) as Total_Profit from "e-commerce dataset" group by Customer_Login_type;
```

**Output:**
| Total_Sales | Total_Profit |
|------------|-------------|
| 7.42 | 74.16 |
| 7.82 | 78.18 |
| 8.18 | 81.99 |
| 7.78 | 77.78 |

**Business Insight:** There's a positive correlation between shipping costs and profit margins across customer segments. The segment with the highest shipping cost ($8.18) also has the highest profit margin ($81.99), suggesting that customers willing to pay more for shipping may also generate higher profits.

## Daily Sales Trend Analysis

Tracks daily sales amounts to identify trends and patterns over time.

```sql
#DAILY SALES TREND
select Order_Date, sum(Sales) as Daily_Sales from "e-commerce dataset" group by Order_Date order by Order_Date asc;
```

**Output:**
| Order_Date | Daily_Sales |
|------------|------------|
| 2018-01-01 | 3473 |
| 2018-01-02 | 3780 |
| 2018-01-03 | 4854 |
| 2018-01-04 | 5261 |
| 2018-01-05 | 5924 |
| 2018-01-06 | 4721 |
| 2018-01-07 | 4547 |
| 2018-01-08 | 3859 |

**Business Insight:** Sales show an upward trend from Jan 1-5, 2018, peaking at $5,924 on Jan 5, followed by a decline over the weekend (Jan 6-7) and into Monday (Jan 8). This pattern suggests weekday shopping is stronger than weekend shopping in this period.

## Conclusion

SQL provides powerful tools for analyzing e-commerce data and extracting actionable business insights. By mastering these query techniques, you can gain a deeper understanding of product performance, customer behavior, and overall business health.
