# Supermarket Sales Analysis Project
This project involves analyzing supermarket sales data to uncover key business insights. It includes data extraction, transformation, and visualization using SQL and Power BI. The goal is to analyze sales trends, identify top-selling products, and help the business make data-driven decisions.

## Tools and Technologies:
- SQL for data extraction and analysis
- Power BI for data visualization
- GitHub for version control and collaboration

## Installation Instructions:
1. Clone the repository: //git clone https://github.com/your-username/Supermarket-Sales-Analysis.git
2. Open the SQL scripts in your SQL editor (e.g., MySQL Workbench, SQL Server Management Studio) to run them.
3. Open the Power BI file (`Supermarket-Sales-Analysis.pbix`) in Power BI Desktop to explore the dashboard.

```
## Project Description:

### 1. Data Collection:
- The data used in this project includes sales data from a supermarket, with columns like invoice number, total sales, product line, and date.

### 2. SQL Analysis:
- I wrote SQL queries to transform and analyze the data. Here are some of the key queries I used:
   - Query for **total sales by product line**:
     ```sql
     SELECT product_line, SUM(total_sales) AS total_sales
     FROM supermarket_sales
     GROUP BY product_line;
     ```
   - Query for **top 5 best-selling products**:
     ```sql
     SELECT month_name, product_line, total_sales
     FROM (
         SELECT DATENAME(MONTH, date) AS month_name, product_line, SUM(total_sales) AS total_sales,
         RANK() OVER (PARTITION BY MONTH(date) ORDER BY SUM(total_sales) DESC) AS rank_per_month
         FROM supermarket_sales
         GROUP BY DATENAME(MONTH, date), product_line, MONTH(date)
     ) AS ranked
     WHERE rank_per_month <= 5
     ORDER BY month_name;
     ```

### 3. Power BI Visualization:
- I used Power BI to create interactive dashboards that allow users to explore total sales trends, top-performing products, and other sales insights. The dashboard includes:
   - **Bar/line charts** for monthly sales trends.
   - **Pie charts** showing the contribution of each product line to total sales.
   - **Top product rankings** based on sales volume and revenue.

### 4. Business Insights:
- The analysis revealed that certain product lines perform better in specific months, and the top-selling products were identified for future marketing and stocking strategies.
```
## Demo:
You can view the project in action here: [Link to Power BI Report] ([https://app.powerbi.com/links/4rib6QT_HQ?ctid=6f60f0b3-5f06-4e09-9715-989dba8cc7d8&pbi_source=linkShare](url)).
![Power BI Dashboard] ([https://github.com/Dechenthakuri/supermarket-sales/blob/main/dashboard.png?raw=true](url))   
([https://github.com/Dechenthakuri/supermarket-sales/blob/main/nextpage.png?raw=true](url))

