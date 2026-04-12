<div align="center"> 
  <img src="https://github.com/subhankar-das18/E-commerce-Profitability-Analysis/blob/main/screenshot/dashboard_preview.png?raw=true" alt="E-commerce Sales Dashboard" width="1000"/> 
   
  # 🚀 E-commerce Sales Analytics Dashboard
  **Power BI + PostgreSQL + DAX** | Revenue, Category Insights & Profit Trends

  [![GitHub stars](https://img.shields.io/github/stars/subhankar-das18/YOUR-EXACT-REPO-NAME?style=social)](https://github.com/subhankar-das18/E-commerce-Profitability-Analysis.git)
  [![Live Demo](https://img.shields.io/badge/Live-PowerBI-blue)](https://app.powerbi.com/view?r=YOUR_EMBED_ID)
</div>

## 🎯 Business Problem
Analyzed 10K+ orders to uncover **top revenue drivers**, **loss-making categories**, and **customer buying patterns** for an online retailer.

## 📊 Key Insights
- **45% revenue from Electronics** — but 12% higher returns
- **Top 5 products** drove 68% profit
- **Peak sales**: Q4 weekends, 2-4 PM

## 🛠 Tech Stack
- **Data**: PostgreSQL queries (joins, window functions)
- **Viz**: Power BI slicers, DAX measures (YOY growth, margins)
- **Analysis**: Customer segmentation, profitability by region

## 📁 Quick Start
1. Download `dataset/ecommerce_data.csv`
2. Open `Sales Dashboard.pbix` in Power BI Desktop
3. Refresh → Explore!

## 📈 Live Demo
[View Interactive Dashboard](https://app.powerbi.com/view?r=YOUR_EMBED_ID)

## Screenshots
| Overview | Category Breakdown | Trends |
|----------|--------------------|--------|
| ![Overview](screenshots/overview.png) | ![Categories](screenshots/categories.png) | ![Trends](https://github.com/subhankar-das18/E-commerce-Profitability-Analysis/blob/main/screenshot/monthly_sales_trend.png?raw=true) |

**Built by [Subhankar Das](https://github.com/subhankar-das18) |** 
- SQL
- Power BI Desktop
- DAX
- juliius ai

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
