# 🛒 E-commerce Profitability Analysis

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **Business Question:** Which product categories, regions, and time periods are actually driving profit — and which are silently losing money?

---

## 📌 Project Overview

This end-to-end analytics project simulates a real e-commerce business scenario. Using PostgreSQL for data storage and transformation, and Power BI with DAX for visualization, I built a dashboard that helps business stakeholders make data-driven decisions on pricing, inventory, and marketing spend.

---

## 🎯 Key Business Questions Answered

- Which product categories generate the most revenue vs. the most profit?
- What is the month-over-month trend in orders and revenue?
- Which regions are underperforming despite high order volumes?
- What is the average order value (AOV) across customer segments?
- Where is the business losing margin silently?

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| PostgreSQL | Data storage, cleaning, and SQL querying |
| SQL | Aggregations, joins, CTEs, window functions |
| Power BI | Interactive dashboard and visualization |
| DAX | Custom KPIs, calculated columns, time intelligence |

---

## 📊 Dashboard Preview

!(https://github.com/subhankar-das18/E-commerce-Profitability-Analysis/blob/main/screenshot/dashboard_preview.png?raw=true)


---

## 🔍 Key SQL Queries Used

```sql
-- Revenue and profit by category
SELECT 
    category,
    SUM(revenue) AS total_revenue,
    SUM(profit) AS total_profit,
    ROUND(SUM(profit) / SUM(revenue) * 100, 2) AS profit_margin_pct
FROM orders
GROUP BY category
ORDER BY total_profit DESC;

-- Month-over-month revenue trend
SELECT 
    DATE_TRUNC('month', order_date) AS month,
    SUM(revenue) AS monthly_revenue,
    LAG(SUM(revenue)) OVER (ORDER BY DATE_TRUNC('month', order_date)) AS prev_month,
    ROUND((SUM(revenue) - LAG(SUM(revenue)) OVER (ORDER BY DATE_TRUNC('month', order_date))) 
        / LAG(SUM(revenue)) OVER (ORDER BY DATE_TRUNC('month', order_date)) * 100, 2) AS mom_growth_pct
FROM orders
GROUP BY month;
```

---

## 📈 Key DAX Measures

```dax
-- Total Profit Margin %
Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0) * 100

-- Month-over-Month Revenue Growth
MoM Revenue Growth % = 
VAR CurrentMonth = [Total Revenue]
VAR PrevMonth = CALCULATE([Total Revenue], DATEADD('Date'[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth, 0) * 100
```

---

## 💡 Key Insights (What I Found)

- 📦 **Electronics** had the highest revenue but the lowest profit margin — high return rates were eating into margins
- 📉 **3 regions** showed high order volume but negative net profit after shipping costs
- 📅 **Q4 (Oct–Dec)** drove 38% of annual revenue — seasonal demand heavily concentrated
- 🛍️ **Top 20% of customers** generated 65% of total revenue (Pareto principle confirmed)

---

## 📂 Repository Structure

```
E-commerce-Profitability-Analysis/
│
├── sql/
│   ├── create_tables.sql
│   ├── data_cleaning.sql
│   └── analysis_queries.sql
│
├── dashboard/
│   └── ecommerce_dashboard.pbix
│
├── data/
│   └── sample_data.csv
│
└── README.md
```

---

## 🚀 How to Run This Project

1. Clone this repository
2. Import `sample_data.csv` into PostgreSQL using the `create_tables.sql` script
3. Run `analysis_queries.sql` to explore the data
4. Open `ecommerce_dashboard.pbix` in Power BI Desktop to view the dashboard

---

## 👤 Author

**Subhankar Das** — Aspiring Data Analyst from Kolkata, India

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/YOUR-LINK)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/subhankar-das18)
