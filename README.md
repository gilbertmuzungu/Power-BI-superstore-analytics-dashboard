# Power-BI-superstore-analytics-dashboard
End-to-end Power BI project with data modeling, custom DAX measures, and interactive sales &amp; profit analytics.

📊 Superstore Analytics Dashboard – Power BI Project

📌 Project Overview
This project analyzes sales, profit, and returns data for a Superstore dataset using Power BI.
It covers the entire process — from data preparation to data modeling and interactive visualizations — to deliver business insights and key performance indicators (KPIs) for decision-making.

🔧 Steps & Workflow
1. Data Preparation
Loaded Returns and Orders tables into Power BI.

Removed unnecessary columns for better performance and cleaner modeling:

From Returns: Removed Returned column.

From Orders: Removed Row ID, Ship Date, Ship Mode, Customer ID, and Product ID.

Verified data types and ensured date fields were properly formatted.

2. Data Modeling
Created a Date Table using DAX:

DAX
Date Table =
ADDCOLUMNS(
    CALENDAR(
        MIN(Orders[Order Date]),
        MAX(Orders[Order Date])
    ),
    "start of month", EOMONTH([Date], -1) + 1
)
Established a relationship between the Date Table and Orders table.

3. DAX Measures
Key Metrics
DAX
Sales = SUM(Orders[Sales])

Profit = SUM(Orders[Profit])

% Returned orders =
VAR _total_orders = DISTINCTCOUNT(Orders[Order ID])
VAR _returned_orders = DISTINCTCOUNT(Returns2[Order ID])
VAR _perc = DIVIDE(_returned_orders, _total_orders)
RETURN _perc
Year-over-Year Comparisons

DAX
Sales PY = CALCULATE([Sales], SAMEPERIODLASTYEAR('Date Table'[Date]))

Profit PY = CALCULATE([Profit], SAMEPERIODLASTYEAR('Date Table'[Date]))

% Returned orders PY =
CALCULATE([% Returned orders], SAMEPERIODLASTYEAR('Date Table'[Date]))

vs - % returned orders = [% Returned orders] - [% Returned orders PY]

vs PY - profit = DIVIDE([Profit] - [Profit PY], [Profit PY])

vs PY - Sales = DIVIDE([Sales] - [Sales PY], [Sales PY])

4. Visualizations
The dashboard includes:

KPI Cards for:

Sales

Profit

% Returned Orders

YoY comparisons

Sales vs Previous Year Trend line chart.

Profit by Product bar chart with positive/negative profit coloring.

Profit by State map visualization.

Sales by Segment donut chart.

Interactive filters for:

Customer Name

Segment

Country/Region

Date

🎯 Key Insights
Identified top-performing product categories and high-return products.

Highlighted regions and states with highest profitability.

Year-over-year growth trends in sales and profit.

Segment-wise contribution to total sales.

🛠 Tools & Technologies
Power BI Desktop

DAX (Data Analysis Expressions)

Data Modeling

Data Transformation with Power Query



Data Transformation with Power Query
