# Supermarket Sales Analysis Project
This project involves analyzing supermarket sales data to uncover key business insights. It includes data extraction, transformation, and visualization using SQL and Power BI. The goal is to analyze sales trends, identify top-selling products, and help the business make data-driven decisions.

## Tools and Technologies:
- SQL for data extraction and analysis
- Power BI for data visualization
- GitHub for version control and collaboration

## Installation Instructions:
1. Clone the repository: 
2. Open the SQL scripts in your SQL editor (e.g., MySQL Workbench, SQL Server Management Studio) to run them.
3. Open the Power BI file (`Supermarket-Sales-Analysis.pbix`) in Power BI Desktop to explore the dashboard.

## Project Description:

### 1. Data Collection:
- I utilize the data from a kaggle. It includes sales data from a supermarket with columns: 
Invoice number,
City
Gender
Product_Line
Unit_price
Quantity
Total
Date
Payment
cogs
Gross_income.
It have 1000 data(rows).

### 2. SQL Analysis:
- I wrote SQL queries to transform and analyze the data. Here are some of the key queries I used:
  --- Find the total $$ earned for each product per each month
   SELECT DATENAME(MONTH, DATE) AS month_name, SUM(total) AS total_per_month
   FROM supermarket_sales
   GROUP BY DATENAME(MONTH, DATE), MONTH(DATE)  -- Extracts the numerical month (e.g., 1 for January, 2 for February).
   ORDER BY MONTH(DATE);
   
   -- finding product that made max amount of sales per each month 
   SELECT month_name, product_line, total_earned_income
   FROM (select datename(month, date) as month_name, month(date) as month_number , product_line,sum(total) as total_earned_income, rank() over (partition by month(date) order by sum(total) DESC ) as rank_per_day
   	from supermarket_sales
   	group by datename(month, date), product_line, month(date)
   	) as ranked
   where rank_per_day =1
   order by month_number;
   
   -- Find percentage of sales by products categories
   SELECT product_line, 
          (total_earned / SUM(total_earned) OVER () * 100) as per_sales_byProduct
   FROM (
       SELECT product_line, SUM(total) as total_earned
       FROM supermarket_sales
       GROUP BY product_line
   ) as total_earned_eachproduct
   
   -- Find total products sold per each category 
   SELECT product_line, SUM(quantity) as total_quantity
   from supermarket_sales
   group by product_line
   
   -- Top 5 best sellers of the month by orders and revenue
   SELECT month_name, product_line, total_earned_income
   FROM (select datename(month, date) as month_name, month(date) as month_number , product_line,sum(total) as total_earned_income, rank() over (partition by month(date) order by sum(total) DESC ) as rank_per_day
   	from supermarket_sales
   	group by datename(month, date), product_line, month(date)
   	) as ranked
   where rank_per_day <=5
   order by month_number;
   
   --Bottom 5 worst sellers of the month by orders and revenue
   SELECT month_name, product_line, total_earned_income, rank_per_day
   FROM (select datename(month, date) as month_name, month(date) as month_number , product_line,sum(total) as total_earned_income, rank() over (partition by month(date) order by sum(total) ASC ) as rank_per_day
   	from supermarket_sales
   	group by datename(month, date), product_line, month(date)
   	) as ranked
   where rank_per_day <=5
   order by month_number;

### 3. Power BI Visualization:
- I used Power BI to create interactive dashboards that allow users to explore total sales trends, top-performing products, and other sales insights. The dashboard includes:
   - **Bar/line charts** for monthly sales trends.
   - **Pie charts** showing the contribution of each product line to total sales.
   - **Top product rankings** based on sales volume and revenue.
     

### 4. Business Insights:
- The analysis revealed that certain product lines perform better in specific months, and the top-selling products were identified for future marketing and stocking strategies.

## Demo:
You can view the project in action here: [Link to Power BI Report] ([https://app.powerbi.com/links/4rib6QT_HQ?ctid=6f60f0b3-5f06-4e09-9715-989dba8cc7d8&pbi_source=linkShare](url)).
![Power BI Dashboard] ([[https://github.com/Dechenthakuri/supermarket-sales/blob/main/dashboard.png])   
([https://github.com/Dechenthakuri/supermarket-sales/blob/main/nextpage.png)

