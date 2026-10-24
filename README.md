# 🍕 Pizza Sales Analysis | SQL Server & Power BI

### 📊 End-to-End Sales Performance & Business Intelligence Project

![SQL Server](https://img.shields.io/badge/SQL_Server-Data_Analysis-CC2927?style=for-the-badge)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge)
![Data Analytics](https://img.shields.io/badge/Data_Analytics-Business_Insights-0078D4?style=for-the-badge)

## 📌 Project Overview

This project analyzes **48,620 pizza sales transactions** using SQL Server and Power BI to evaluate business performance, identify sales trends, and understand product-level revenue contributions.

The objective is to transform transactional sales data into meaningful business insights through SQL queries and interactive Power BI dashboards.

The project focuses on five key business metrics, sales trends, category performance, and identifying the best- and worst-selling pizzas.

**Project Highlights:**
- 48,620 transaction records
- 21,350 unique orders
- 5 business KPIs
- 2 interactive Power BI dashboard pages
- SQL-based business analysis
- Product performance and sales trend analysis

---

## 🎯 Business Problem

A pizza business needs to understand its sales performance to make informed decisions about inventory, staffing, promotions, and product offerings.

This project addresses the following business questions:

1. What is the total revenue generated?
2. What is the average order value?
3. How many pizzas were sold?
4. Which days and months have the highest order volumes?
5. Which pizza categories and sizes contribute the most revenue?
6. Which pizzas generate the highest and lowest revenue?
7. Which pizzas perform best and worst by quantity and order count?

---

## 🛠️ Tools & Technologies

| Technology | Purpose |
|---|---|
| SQL Server | Business data analysis |
| SQL Server Management Studio | Writing and executing SQL queries |
| Power BI | Interactive dashboard development |
| DAX | KPI measures and calculations |
| CSV | Transactional data source |

### SQL Concepts Applied

- Aggregate Functions: `SUM()`, `COUNT()`
- `GROUP BY`
- `ORDER BY`
- `WHERE`
- `TOP`
- `DISTINCT`
- Subqueries
- Date Functions
- Data Type Conversion using `CAST()`

---

## 📂 Dataset Information

The dataset contains pizza sales transactions from January to December 2015.

| Attribute | Details |
|---|---|
| Dataset | Pizza Sales |
| Total Records | 48,620 |
| Total Columns | 12 |
| Time Period | January–December 2015 |
| Data Format | CSV |
| Analysis Tools | SQL Server and Power BI |

### Dataset Columns

| Column | Description |
|---|---|
| pizza_id | Pizza sales record identifier |
| order_id | Unique order identifier |
| pizza_name_id | Pizza product identifier |
| quantity | Quantity purchased |
| order_date | Date of purchase |
| order_time | Time of purchase |
| unit_price | Unit selling price |
| total_price | Total sales amount |
| pizza_size | Pizza size |
| pizza_category | Pizza category |
| pizza_ingredients | Pizza ingredients |
| pizza_name | Pizza product name |

---

## 📊 Key Performance Indicators

The Power BI dashboard presents five business KPIs.

| KPI | Result |
|---|---:|
| 💰 Total Revenue | 817.86K |
| 🛒 Total Orders | 21,350 |
| 🍕 Total Pizzas Sold | 49,574 |
| 📈 Average Order Value | 38.31 |
| 📦 Average Pizzas Per Order | 2.32 |

### KPI Calculations

**1. Total Revenue**

```sql
SELECT SUM(total_price) AS Total_Revenue
FROM pizza_sales;
```

**2. Average Order Value**

```sql
SELECT
    CAST(
        SUM(total_price) * 1.0 /
        COUNT(DISTINCT order_id)
        AS DECIMAL(10,2)
    ) AS Average_Order_Value
FROM pizza_sales;
```

**3. Total Pizzas Sold**

```sql
SELECT SUM(quantity) AS Total_Pizzas_Sold
FROM pizza_sales;
```

**4. Total Orders**

```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales;
```

**5. Average Pizzas Per Order**

```sql
SELECT
    CAST(
        SUM(quantity) * 1.0 /
        COUNT(DISTINCT order_id)
        AS DECIMAL(10,2)
    ) AS Average_Pizzas_Per_Order
FROM pizza_sales;
```

---

## 📈 Power BI Dashboard

The project contains two interactive Power BI dashboard pages.

### 🏠 Dashboard 1: Sales Overview

![Pizza Sales Overview](images/home_dashboard.png)

**Dashboard Features:**

- Total Revenue
- Average Order Value
- Total Pizzas Sold
- Total Orders
- Average Pizzas Per Order
- Daily Order Trends
- Monthly Order Trends
- Sales Distribution by Pizza Category
- Sales Distribution by Pizza Size
- Total Pizzas Sold by Category
- Date and Category Filters

**Purpose:** Monitor overall business performance and understand sales patterns.

### 🏆 Dashboard 2: Best & Worst Sellers

![Best and Worst Sellers](images/best_worst_sellers.png)

**Dashboard Features:**

- Top 5 Pizzas by Revenue
- Top 5 Pizzas by Quantity
- Top 5 Pizzas by Total Orders
- Bottom 5 Pizzas by Revenue
- Bottom 5 Pizzas by Quantity
- Bottom 5 Pizzas by Total Orders

**Purpose:** Identify high-performing and underperforming products to support menu planning, promotions, and inventory decisions.

---

## 🔍 SQL Business Analysis

SQL queries were used to answer business questions and validate sales performance.

### 1. Daily Order Trends

```sql
SELECT
    DATENAME(WEEKDAY, order_date) AS Order_Day,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(WEEKDAY, order_date);
```

### 2. Monthly Order Trends

```sql
SELECT
    DATENAME(MONTH, order_date) AS Month_Name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY
    MONTH(order_date),
    DATENAME(MONTH, order_date)
ORDER BY MONTH(order_date);
```

### 3. Revenue Contribution by Pizza Category

```sql
SELECT
    pizza_category,
    CAST(SUM(total_price) AS DECIMAL(10,2))
        AS Total_Revenue,
    CAST(
        SUM(total_price) * 100.0 /
        (SELECT SUM(total_price) FROM pizza_sales)
        AS DECIMAL(10,2)
    ) AS Revenue_Percentage
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Total_Revenue DESC;
```

### 4. Top 5 Pizzas by Revenue

```sql
SELECT TOP 5
    pizza_name,
    SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
```

### 5. Bottom 5 Pizzas by Revenue

```sql
SELECT TOP 5
    pizza_name,
    SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;
```

### 6. Top 5 Pizzas by Quantity

```sql
SELECT TOP 5
    pizza_name,
    SUM(quantity) AS Total_Pizzas_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizzas_Sold DESC;
```

### 7. Bottom 5 Pizzas by Quantity

```sql
SELECT TOP 5
    pizza_name,
    SUM(quantity) AS Total_Pizzas_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizzas_Sold ASC;
```

---

## 💡 Key Business Insights

### 1. Overall Sales Performance

- Total revenue reached approximately **817.86K**.
- The business processed **21,350 unique orders**.
- A total of **49,574 pizzas** were sold.
- Customers purchased approximately **2.32 pizzas per order**.

### 2. Daily Sales Trends

- **Friday** recorded the highest number of orders.
- Saturday also showed strong order activity.
- These patterns suggest higher demand toward the weekend.

### 3. Monthly Sales Trends

- **July** recorded the highest order volume.
- January recorded the lowest order volume.
- Monthly variations can help inform operational planning.

### 4. Pizza Category Performance

- The **Classic** category contributed the highest revenue.
- Large-sized pizzas generated the largest share of revenue.

### 5. Best-Selling Products

- **The Thai Chicken Pizza** generated the highest revenue.
- **The Classic Deluxe Pizza** was a leading product by quantity and order volume.

### 6. Underperforming Products

- **The Brie Carre Pizza** generated the lowest revenue.
- Lower-performing pizzas may benefit from further evaluation of pricing, demand, and promotional opportunities.

---

## 💼 Business Recommendations

Based on the sales analysis, the following recommendations could support business decision-making.

**1. Improve Inventory Planning**

Monitor demand for popular pizza categories and maintain appropriate stock levels during high-demand periods.

**2. Optimize Weekend Staffing**

Consider allocating additional staff during Friday and Saturday peak periods to support customer demand.

**3. Promote Low-Performing Products**

Evaluate promotional campaigns and combo offers for pizzas with lower sales volumes.

**4. Focus on High-Performing Products**

Feature popular pizzas in promotional campaigns and menu recommendations.

**5. Monitor Monthly Sales Trends**

Use historical order patterns to support staffing, inventory, and promotional planning.

These recommendations are proposed actions based on historical sales patterns and have not been tested for business impact.

---

## 📁 Project Structure

```text
Pizza-Sales-Analysis-SQL-PowerBI/
│
├── README.md
│
├── data/
│   └── pizza_sales.csv
│
│── Pizza_Sales_Dashboard.pbix
│
├── images/
│   ├── home_dashboard.png
│   └── best_worst_sellers.png
│
├── sql/
│   └── analysis_queries.sql
│
└── docs/
    └── Pizza_Sales_SQL_Queries.docx
```

---

## 🚀 How to Run This Project

### SQL Server

1. Install SQL Server and SQL Server Management Studio.
2. Create a new database.
3. Import `pizza_sales.csv` into a table named `pizza_sales`.
4. Open the SQL queries in SSMS.
5. Execute the queries to analyze business performance.

### Power BI

1. Install Power BI Desktop.
2. Download the `.pbix` file from the repository.
3. Open the dashboard in Power BI Desktop.
4. Update the dataset source path if required.
5. Refresh the data and explore the dashboard.

---

## 🎯 Skills Demonstrated

- SQL-Based Data Analysis
- Business Intelligence
- Power BI Dashboard Development
- KPI Development and Reporting
- Sales Performance Analysis
- SQL Aggregation and Filtering
- Data Visualization
- Product Performance Analysis
- Business Problem-Solving
- Data-Driven Decision-Making

---

## 👩‍💻 About Me

**Priyadharshini V C | Aspiring Data Analyst**

I am a Computer Science graduate developing practical expertise in SQL, Python, Advanced Excel, Power BI, and Tableau.

I enjoy transforming raw datasets into meaningful business insights through SQL analysis, data visualization, and interactive dashboards.

Through hands-on analytics projects, I am strengthening my analytical thinking, technical skills, and ability to communicate findings effectively.

I am actively seeking entry-level Data Analyst opportunities where I can apply my knowledge, contribute to business decisions, and continue developing my professional skills.

### 🔗 Connect With Me

**GitHub:** [priyadharshini-data-analyst](https://github.com/priyadharshini-data-analyst)

**Project Repository:** [Pizza Sales Analysis](https://github.com/priyadharshini-data-analyst/Pizza-Sales-Analysis-SQL-PowerBI)

---

## ⭐ Conclusion

This project demonstrates the use of SQL Server and Power BI to analyze transactional sales data, monitor business KPIs, identify sales trends, and evaluate product performance.

It strengthened my practical understanding of SQL querying, business analysis, dashboard development, and communicating data-driven insights.

**⭐ If you find this project useful, consider starring the repository!**
