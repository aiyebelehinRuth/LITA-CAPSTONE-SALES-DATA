# Sales Data for a Retail Store
---
### Project Overview
---
This data analysis project aims to provide insights into the sales performance of a Retail store over a period of 2 years. By analyzing various aspects of the sales data we seek to identify trends,make data-driven recommendations and gain a deeper understanding of the stores and products performance.

### Data Sources
---
Sales Data:The primary dataset used for this analysis is the "Capstone_Sales_data.csv" file, containing detailed information about each sales made by the stores in each Region.

### Tools Used
---
- Excel - For Data cleaning[Download here](https://microsoft.com)
- SQL server - For Data Analysis
- Power BI - For creating reports and Data visualizations


### Data Cleaning/preparation
---
In the initial data preparation phase, we performed the following tasks:
1. Data Loading and inspection
2. Data cleaning and formating
3. Adding new column for Revenue


### Exploratory Data Analysis
---
EDA involves exploring the sales data to answer key questions like;

- Using pivot tables to summarize total sales by product, region, and month.

- Using Excel formulas to calculate metrics such as average sales per product and total revenue by region.
  
- Writing queries to extract key insights like

- retrieving the total sales for each product category.

- finding the number of sales transactions in each region.

- finding the highest-selling product by total sales value.

- calculating total revenue per product.

- calculate monthly sales totals for the current year.

- find the top 5 customers by total purchase amount.

- calculate the percentage of total sales contributed by each region.

- identify products with no sales in the last quarter.
  
- lastly creating a Power BI Dashboard.
  
### Data Analysis
---
we will have our SQL Queries here;

```SQL
select*from[dbo].[LITA_Capstone_sales]

-----retrieve the total sales for each product category----
select product,SUM(CAST(Quantity AS int)*CAST(unitprice AS int))
AS Totalsales from[dbo].[LITA_Capstone_sales]
Group by Product

----find the number of sales transactions in each region---
select Region, count(*) AS [Number of sales Transaction]
from[dbo].[LITA_Capstone_sales] 
Group by Region

---find the highest-selling product by total sales value---
select Top 1 product,
SUM(CAST(quantity AS int)*CAST(unitprice AS int))AS totalsales
from[dbo].[LITA_Capstone_sales]
Group by product
order by Totalsales DESC

-----calculate total revenue per product.--------
select product,sum(CAST(quantity AS int)*CAST(unitprice AS int))
AS TotalRevenue
from [dbo].[LITA_Capstone_sales]
Group by product

----calculate monthly sales totals for the current year---
Select Month(orderdate) AS Month,
sum(CAST(Quantity AS int)*CAST(unitprice AS int)) AS Monthlysales
from[dbo].[LITA_Capstone_sales]
where YEAR(orderdate)=YEAR(GETDATE())
Group by Month(orderdate)
order by Month

---find the top 5 customers by total purchase amount.---
select Top 5 customer_ID, sum(CAST(quantity AS int)*CAST(Unitprice AS int))
AS Totalpurchase 
from [dbo].[LITA_Capstone_sales]
Group by customer_ID
order by Totalpurchase DESC

---calculate the percentage of total sales contributed by each region---
WITH Totalsales AS (
select sum(CAST(quantity AS int)*CAST(Unitprice AS int))
AS Totalrevenue from [dbo].[LITA_Capstone_sales]
)
Select Region, sum(CAST(quantity AS int)*CAST(Unitprice as INT))
AS Regionsales,sum(CAST(quantity AS int)*CAST(unitprice AS int))*100.0/(select Totalrevenue
from Totalsales)AS Percentageoftotalsales
from [dbo].[LITA_Capstone_sales]
Group by Region

---identify products with no sales in the last quarter--
SELECT DISTINCT Product from[dbo].[LITA_Capstone_sales]
where product NOT IN (
SELECT product from [dbo].[LITA_Capstone_sales]
where orderdate>=Dateadd(qq,-1,getdate())
)
```

