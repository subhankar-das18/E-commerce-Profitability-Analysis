# E-commerce Sales Dashboard (PostgreSQL + Power BI)

## Overview
This project analyzes a small e-commerce dataset using PostgreSQL for data storage and SQL practice, then visualizes the results in Power BI with DAX measures and an interactive sales dashboard. The goal was to answer core business questions around revenue, customers, order volume, geography, product category performance, and order status trends.

## Business Problem
An online store needs a simple executive dashboard to monitor:
- Revenue performance over time
- Which countries generate the most revenue
- Which product categories perform best
- Total customers, total orders, and average order value
- The breakdown of completed, cancelled, and pending orders

## Tools Used
- PostgreSQL
- SQL
- Power BI Desktop
- DAX

## Dataset Structure
The dashboard was built from four related tables:
- `Customers` — customer details and country
- `Orders` — order date, customer, and order status
- `Order_Items` — quantity and unit price for each order line
- `Products` — product name and category

## Data Model
Relationships used in Power BI:
- `Customers[customer_id]` 1-to-many `Orders[customer_id]`
- `Orders[order_id]` 1-to-many `Order_Items[order_id]`
- `Products[product_id]` 1-to-many `Order_Items[product_id]`

This model supports slicing revenue by customer, country, product, and order status.

## Key DAX Measures
```DAX
Total Revenue =
SUMX (
    'Order_Items',
    'Order_Items'[quantity] * 'Order_Items'[unit_price]
)

Total Orders =
DISTINCTCOUNT ( 'Orders'[order_id] )

Total Customers =
DISTINCTCOUNT ( 'Customers'[customer_id] )

Average Order Value =
DIVIDE ( [Total Revenue], [Total Orders] )

Completed Revenue =
CALCULATE (
    [Total Revenue],
    'Orders'[order_status] = "Completed"
)

Completed Orders =
CALCULATE (
    [Total Orders],
    'Orders'[order_status] = "Completed"
)
```

## Dashboard Features
The dashboard includes:
- KPI cards for Total Customers, Total Revenue, Total Orders, and Average Order Value
- A line chart showing monthly revenue trend
- A bar chart for revenue by country
- A bar chart for revenue by product category
- A pie chart for order status distribution

## Key Insights
- The dataset currently shows **3 unique customers**, **5 total orders**, and **14,600 total revenue**.
- The **Average Order Value is 2,920**, which suggests relatively high-value purchases per order.
- **India is the leading market**, contributing the vast majority of total revenue.
- **Fashion is the top-performing product category**, ahead of Electronics and Home.
- Most orders are **Completed**, while Cancelled and Pending orders form a much smaller share.

## Business Interpretation
This dashboard suggests that the store currently depends heavily on one geography and one main category for revenue. That concentration is useful for short-term focus, but it also highlights opportunities to diversify country reach and product performance.

## What I Learned
Through this project, I practiced:
- Writing SQL queries for joins, aggregation, filtering, and business analysis
- Building a relational data model in Power BI
- Creating reusable DAX measures for KPIs
- Designing a beginner-friendly business dashboard
- Turning charts into business insights for storytelling

## Future Improvements
Possible next steps for this project:
- Add slicers for date, country, and order status
- Create a second dashboard page for customer-level analysis
- Add top products and repeat customer metrics
- Expand the dataset to include profit, discounts, and returns

## Author
**Subhankar Das**  
Aspiring Data Analyst focused on SQL, Power BI, Excel, and portfolio-driven learning.
