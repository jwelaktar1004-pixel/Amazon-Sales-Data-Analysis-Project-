📘 Amazon Sales Data Analysis Project Report
🧾 1. Project Overview

Objective:
To analyze historical sales data to identify top-performing branches, products, and customers; understand purchasing patterns and deal sizes; evaluate revenue trends over time; and provide actionable insights for strategic business decisions.

Tools Used:

SQL (MySQL): Data cleaning, transformation, and creating analytical views

Power BI: Dashboard visualization and KPI reporting

Python (Optional): For preprocessing and EDA (if used earlier)

Dataset Columns:
Invoice ID, Branch, City, Customer Type, Gender, Product Line, Unit Price, Quantity, Tax 5%, Total, Date, Time, Payment, COGS, Gross Income, Rating

⚙️ 2. Data Preparation (SQL Phase)
✅ Key Steps:

Data Cleaning

Replaced nulls with 0

Ensured correct data types for Date and Time columns

Converted Date format using STR_TO_DATE()

Feature Engineering

Added new columns:

ALTER TABLE amazon
ADD COLUMN timeofday VARCHAR(20),
ADD COLUMN dayname VARCHAR(20),
ADD COLUMN monthname VARCHAR(20);


Populated them:

UPDATE amazon
SET 
  timeofday = CASE 
                WHEN HOUR(Time) BETWEEN 0 AND 11 THEN 'Morning'
                WHEN HOUR(Time) BETWEEN 12 AND 17 THEN 'Afternoon'
                ELSE 'Evening'
              END,
  dayname = DAYNAME(STR_TO_DATE(Date, '%d-%m-%Y')),
  monthname = MONTHNAME(STR_TO_DATE(Date, '%d-%m-%Y'));


Analytical Views Created

amazon_time_insights — for sales by time/day/month

vw_productline_performance — to classify product lines as Good or Bad

vw_monthly_revenue — monthly revenue and profit summary

vw_branch_sales — branch-level performance

❓ 3. Business Questions Answered (28 Total)
#	Question	Insight / KPI
1	Count of distinct cities	3 (Yangon, Naypyitaw, Mandalay)
2	Each branch’s city	A–Yangon, B–Mandalay, C–Naypyitaw
3	Distinct product lines	6 total
4	Most frequent payment method	Ewallet
5	Product line with highest sales	Food and Beverages
6	Monthly revenue trend	Jan peaked highest
7	Peak month for COGS	Jan
8	Highest revenue product line	Food and Beverages
9	City with highest revenue	Naypyitaw
10	Highest VAT product line	Fashion Accessories
11	Good/Bad product classification	4 “Good”, 2 “Bad”
12	Branch exceeding avg products sold	Branch C
13	Product line by gender	Health & Beauty → Female, Sports → Male
14	Avg rating per product line	Electronics highest (≈ 8.5/10)
15	Sales occurrences by time of day	Afternoon highest
16	Customer type with highest revenue	Member
17	City with highest VAT %	Naypyitaw
18	Customer type with highest VAT	Member
19	Distinct customer types	2 (Member, Normal)
20	Distinct payment methods	3
21	Most frequent customer type	Member
22	Customer type with highest purchase freq	Member
23	Predominant gender	Female
24	Gender distribution per branch	Female > Male in A, C; Male > Female in B
25	Time of day with most ratings	Evening
26	Highest rating time per branch	Branch A → Evening
27	Day with highest avg ratings	Sunday
28	Highest avg ratings per branch	Branch C on Friday
📊 4. Power BI Dashboard Design
Dashboard 1 – Sales Overview

KPIs: Total Sales, Total Profit, Avg Rating, Transactions

Charts:

Line Chart → Monthly Revenue

Bar Chart → Top Product Lines by Sales

Dashboard 2 – City & Branch Insights

Map: Revenue by City

Clustered Bar: Branch vs. Revenue

Donut Chart: Sales Share by Branch

Dashboard 3 – Customer Analysis

Bar Chart: Gender Distribution per Branch

Pie Chart: Sales by Customer Type

Stacked Bar: Customer Type vs. Revenue

Dashboard 4 – Time Analysis
Visual	Type	Field Setup
Sales by Time of Day	Clustered Column Chart	X → timeofday, Y → SUM(Total)
Avg Rating by Time	Line Chart	X → timeofday, Y → AVERAGE(Rating)
Sales per Weekday	Matrix / Heatmap	Rows → dayname, Columns → timeofday, Values → COUNT(Sales)
Dashboard 5 – Product Line Performance

Bar Chart: Product Line vs. Profit

Clustered Column: Product Line vs. Rating

Pie Chart: Performance (Good vs. Bad)

Dashboard 6 – Payment Insights

Bar Chart: Payment Method Frequency

Pie Chart: Revenue by Payment Method

Dashboard 7 – Rating Insights

Line Chart: Average Rating by Day & Branch

Area Chart: Ratings over Time of Day

Dashboard 8 – KPI Summary

4 KPI Cards (Sales, Profit, Avg Rating, Transactions)

Date, Branch, and Product Line Slicers for interactivity

💡 5. Key Insights Summary

Branch C (Naypyitaw) generated the highest revenue and customer satisfaction.

Ewallet is the most preferred payment method.

Food and Beverages leads in total sales; Electronics in ratings.

Afternoon sales dominate across all branches.

Female customers contribute a slightly higher share overall.

Member customers generate more revenue than Normal customers.

Friday evenings record the highest average customer ratings.

📈 6. Business Recommendations

Focus marketing on top-performing cities (Naypyitaw).

Offer loyalty perks for Member customers to sustain high revenue.

Improve visibility and pricing of “Bad” performing product lines.

Boost staff allocation during Afternoon peak hours.

Promote Ewallet offers since it’s the most used method.

🏁 7. Conclusion

The data-driven analysis and Power BI dashboards provide valuable insights into sales, customer behavior, and product performance.
These findings can help management optimize inventory, improve marketing targeting, and increase profitability strategically.
