Retail Sales Analytics — Power BI Dashboard Project
A comprehensive end-to-end Power BI dashboard project built on a retail superstore sales dataset. This project demonstrates data cleaning, DAX measures, and professional interactive reporting across Sales, Product, and Regional dimensions.

Dataset Overview
Field	Description
Order ID	Unique identifier for each transaction
Order Date	Date the order was placed (2021–2024)
Ship Date	Estimated delivery date
Ship Mode	Shipping method (Standard, Second, First, Same)
Customer Name	Full name of the purchasing customer
Segment	Customer type: Consumer / Corporate / Home Office
Region	Geographic region: West / East / Central / South
State / City	State and city of delivery
Category	Product family: Technology / Furniture / Office Supplies
Sub-Category	Detailed product group (17 sub-categories)
Product Name	Specific product description
Sales	Gross revenue for the line item
Quantity	Units ordered
Discount	Discount rate applied (0–50%)
Profit	Net profit after discount and COGS
Dashboard Pages
1. Executive KPI Summary
Total Sales, Total Profit, Total Orders, Avg Order Value
YoY growth badges on every KPI
Sparkline trend for each KPI card
2. Monthly Sales Trend
Area chart: Sales (filled area) vs Profit (line overlay)
Month-by-month view for the selected year
Peak-month annotation
3. Regional Analysis
Horizontal bar chart: Sales and Profit by region
State-level drill-down map
Region performance ranking table
4. Product Analysis
Grouped bar chart by sub-category
Category toggle filter (Technology / Furniture / Office Supplies)
Top-10 products ranked by revenue
5. Customer Segment Analysis
Donut chart: Revenue split by Consumer / Corporate / Home Office
Segment profitability comparison
6. Transaction Detail Table
Full paginated and searchable record list
Sortable on all numeric columns
CSV export per page view
DAX Measures Used
-- Total Sales
Total Sales = SUM(Sales[Sales])
-- Total Profit
Total Profit = SUM(Sales[Profit])
-- Profit Margin %
Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)
-- Total Orders (distinct order count)
Total Orders = DISTINCTCOUNT(Sales[Order ID])
-- Average Order Value
Avg Order Value = DIVIDE([Total Sales], [Total Orders], 0)
-- YoY Sales Growth
Sales Growth YoY =
VAR CurrentYear = CALCULATE([Total Sales], YEAR(Sales[Order Date]) = MAX(YEAR(Sales[Order Date])))
VAR PriorYear = CALCULATE([Total Sales], YEAR(Sales[Order Date]) = MAX(YEAR(Sales[Order Date])) - 1)
RETURN DIVIDE(CurrentYear - PriorYear, PriorYear, 0)
-- YoY Profit Growth
Profit Growth YoY =
VAR CurrentYear = CALCULATE([Total Profit], YEAR(Sales[Order Date]) = MAX(YEAR(Sales[Order Date])))
VAR PriorYear = CALCULATE([Total Profit], YEAR(Sales[Order Date]) = MAX(YEAR(Sales[Order Date])) - 1)
RETURN DIVIDE(CurrentYear - PriorYear, PriorYear, 0)
-- Running Total Sales (for trend chart)
Running Sales =
CALCULATE([Total Sales],
    FILTER(ALLSELECTED(Sales[Order Date]),
        Sales[Order Date] <= MAX(Sales[Order Date])))
-- Sub-Category Rank by Sales
Sub-Category Rank =
RANKX(ALL(Sales[Sub-Category]), [Total Sales], , DESC, DENSE)

Interactive Slicers
Slicer	Values
Year	2021, 2022, 2023, 2024
Region	West, East, Central, South
Segment	Consumer, Corporate, Home Office
Category	Furniture, Office Supplies, Technology
All slicers are cross-filtered — selecting a region updates all charts simultaneously.

Data Cleaning Steps
Remove duplicates on Order ID
Standardize date formats to YYYY-MM-DD
Handle nulls in Profit column (replace with 0 for cancelled orders)
Trim whitespace on Product Name and Customer Name
Validate numeric fields — reject negative Sales values
Normalize text case on Region and Category columns
Create date table in Power BI (for time-intelligence DAX)
Add calculated columns: Year, Month Number, Month Name, Quarter, Day of Week
Business Insights
Technology drives 45%+ of revenue but Furniture sub-categories (Tables, Bookcases) frequently run negative profit margins due to high discount rates.
Q4 spike every year: November and December account for 28–32% of annual sales — critical for inventory planning.
West region leads in total sales volume; Central lags significantly and warrants targeted sales strategy.
Consumer segment dominates at ~52% of orders, but Corporate customers have 18% higher avg order value.
Discount abuse: Orders with discounts above 30% often generate negative profit — a pricing policy concern.
Files Included
/
├── data/
│   └── superstore_sales.csv        # Raw dataset (2,400 records)
├── powerbi/
│   └── sales_dashboard.pbix        # Power BI Desktop file
├── docs/
│   ├── README.md                   # This file
│   ├── resume_description.md       # Project description for resume
│   └── implementation_guide.md    # Step-by-step build guide
└── web-dashboard/                  # Interactive web version of dashboard

Tools & Technologies
Power BI Desktop — Report authoring and DAX measures
Power Query (M Language) — Data cleaning and transformation
DAX — Business measures and KPI calculations
Excel / CSV — Source data format
Web Dashboard — React + Recharts interactive version (this app)
Requirements
Power BI Desktop (free download from Microsoft)
Windows 10/11 (Power BI Desktop is Windows-only)
The .pbix file can be published to Power BI Service (cloud) for sharing
License
MIT — free to use for portfolio and learning purposes.
