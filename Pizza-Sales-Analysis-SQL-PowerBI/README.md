# 🍕 Pizza Sales Analysis | SQL Server & Power BI

**End-to-end sales analytics portfolio project** exploring revenue, ordering trends, pizza category performance, and best- and worst-selling products through SQL queries and a two-page interactive Power BI dashboard.

![Pizza Sales Overview](images/home_dashboard.png)

## Project overview
A pizza retailer wants to understand overall sales performance, ordering patterns, and product demand. This project uses **48,620 transaction line items from 2015** to answer practical business questions and present results in a Power BI report.

**Tools:** Microsoft SQL Server (T-SQL), Power BI, CSV  
**Focus:** KPI analysis, aggregation, ranking, time trends, interactive reporting

## Business questions
- How much revenue was generated, and how many orders and pizzas were sold?
- Which days and months had the most orders?
- Which pizza categories and sizes generated the most revenue?
- Which five pizzas performed best and worst by revenue, quantity, and order count?

## Dataset
- **Source:** `data/pizza_sales.csv` (included in this repository)
- **Rows:** 48,620 pizza order line items
- **Columns:** 12
- **Period:** January 1–December 31, 2015
- **Unique orders:** 21,350
- **Missing values:** None detected in the provided CSV
- **Fields:** `pizza_id`, `order_id`, `pizza_name_id`, `quantity`, `order_date`, `order_time`, `unit_price`, `total_price`, `pizza_size`, `pizza_category`, `pizza_ingredients`, `pizza_name`

> Each row represents a pizza line item, **not** a unique customer or unique order. Order-level KPIs use `COUNT(DISTINCT order_id)`.

## Key performance indicators
| KPI | Result |
| --- | ---: |
| Total revenue | **817,860.05** |
| Average order value | **38.31** |
| Total pizzas sold | **49,574** |
| Total orders | **21,350** |
| Average pizzas per order | **2.32** |

*Currency is not explicitly documented in the source dataset; amounts are shown without an assumed currency symbol.*

## Dashboard pages

### 1. Sales overview
![Sales Overview](images/home_dashboard.png)

Includes KPI cards, daily and monthly order trends, sales share by pizza category and size, pizza category quantities, and a category slicer/date filters.

### 2. Best & worst sellers
![Best and Worst Sellers](images/best_worst_sellers.png)

Compares the top five and bottom five pizza products by **revenue**, **quantity**, and **distinct order count**.

## Insights from the provided data
1. **Classic** is the highest-revenue category at **220,053.10**, about **26.91%** of overall sales.
2. **Large (L)** pizzas contribute the highest sales value at **375,318.70**, about **45.89%** of revenue.
3. **The Thai Chicken Pizza** leads revenue at **43,434.25**.
4. **The Brie Carre Pizza** has the lowest revenue at **11,588.50**.
5. The report indicates **Friday and Saturday** as high-order days and **July and January** as strong months for order volume.

## Business recommendations
- Plan staffing and ingredients around busier days and seasonal demand.
- Monitor the best-selling pizzas to reduce stockout risk.
- Review low-performing items before deciding whether to adjust promotions, pricing, or menu placement.
- Track category and size contribution regularly to support purchasing decisions.

*These are proposed actions based on descriptive analysis; the dataset does not establish that any recommendation will improve outcomes.*

## SQL analysis
SQL Server queries cover `SUM`, `COUNT(DISTINCT ...)`, `GROUP BY`, `DATENAME`, `DATEPART`, `TOP`, ordering, percentages, and product rankings.

- [`sql/analysis_queries.sql`](sql/analysis_queries.sql): organized, reviewed SQL Server queries
- [`sql/original_analysis.sql`](sql/original_analysis.sql): original uploaded working file (retained for transparency)
- [`docs/Pizza_Sales_SQL_Queries.docx`](docs/Pizza_Sales_SQL_Queries.docx): original SQL documentation

**Note:** The original SQL file includes an invalid `MONTH(order_id)` expression; the reviewed query file uses `MONTH(order_date)` instead. Percentages in the reviewed file use a consistent whole-period denominator.

## How to run
1. Download or clone this repository.
2. Open `dashboard/Pizza_Sales_Dashboard.pbix` in **Power BI Desktop**.
3. If prompted about a missing data source, go to **Transform data → Data source settings → Change Source** and point it to the downloaded `data/pizza_sales.csv` file. Apply changes and refresh.
4. For SQL practice, import the CSV into a SQL Server table named `pizza_sales`. Ensure `order_date` is stored as a date (the CSV uses `DD-MM-YYYY`), then run `sql/analysis_queries.sql` in SQL Server Management Studio.
5. Explore the dashboard's category and date filters and compare the two pages.

## Repository structure
```text
Pizza-Sales-Analysis-SQL-PowerBI/
├── README.md
├── data/
│   └── pizza_sales.csv
├── dashboard/
│   └── Pizza_Sales_Dashboard.pbix
├── images/
│   ├── home_dashboard.png
│   └── best_worst_sellers.png
├── sql/
│   ├── analysis_queries.sql
│   └── original_analysis.sql
└── docs/
    └── Pizza_Sales_SQL_Queries.docx
```

## Skills demonstrated
**SQL Server:** business KPI queries, aggregations, distinct counts, grouping, date functions, ranking and sorting.  
**Power BI:** report design, KPI cards, slicers, cross-page navigation, categorical and time-series visualizations.  
**Business analysis:** interpreting trends, comparing product performance, and recommending follow-up actions.

## About this project
This is a **personal portfolio project** developed to demonstrate hands-on SQL and Power BI skills for an entry-level **Data Analyst** role. It uses historical sample sales data, not a live business deployment.
