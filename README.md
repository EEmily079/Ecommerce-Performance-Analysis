# Ecommerce-Performance-Analysis

Dataset Source:
As the file is too big and not able to upload into github. you can download dataset from this link. 
🔗 https://www.kaggle.com/datasets/mmohaiminulislam/ecommerce-data-analysis/data


**Objective**
To provide actionable insights on:
•	Customer buying behaviour
•	Sales performance trend
•	Store and product contribution
•	Time-based customer activity (Morning / Afternoon / Night)



**1. Data Cleaning Process**
Excel Cleaning
Performed initial text standardization before import:
Action	Excel Formula Used
Trim extra spaces	=TRIM(text)
Proper case	=PROPER(text)
Upper case	=UPPER(text)
Lower case	=LOWER(text)
Used mainly for customer names, item names, store names, etc.
________________________________________
**2. Power Query Data Transformations**
2.1 Create Time-of-Day Label
Used transaction hour column to categorize buying time:
= Table.AddColumn(#"Previous Step", "Time Group", each
    if [hour] > 6 and [hour] <= 12 then "Morning"
    else if [hour] > 12 and [hour] <= 18 then "Afternoon"
    else if [hour] > 18 and [hour] <= 24 then "Night"
    else "Overnight"
)
Helps analyze what time customers tend to buy most.

**2.2 Add Item Group Column**
Extract category from item description before delimiter " - "
Example: Beverage - Soda → Beverage
= Table.AddColumn(#"Previous Step", "Item Group",
    each try Text.BeforeDelimiter([desc], " - ") otherwise [desc]
)
Creates a clean item category to use in slicers and grouping.

**2.3 Other Transformations**
•	Removed unnecessary columns (IDs not used in analysis)
•	Converted data types (Date → Date, Qty → Whole number, Price → Decimal)
•	Verified no blank customer or product IDs
•	Replaced null values for fields where appropriate
________________________________________

**3. Data Model Relationships**
Table	Key
Sales fact table	sales_id (or transaction id)
Customers	joins to Sales on customer_id
Items/Product table	joins to Sales on item_id
Time table (calendar)	joins on date field
Ensured one-to-many relationships and cross-filter direction: single

________________________________________
**4. Dashboard Pages & Purpose**
✅ Sales Overview
•	Total sales by year/month
•	Top selling stores & item groups
•	Trend analysis
•	Manufacturer performance
•	KPI cards (Revenue, Orders, Top locations)
✅ Customer Analysis
•	Top buyers (sorted by total sales)
•	Customer sales frequency
•	Customer purchase patterns
✅ Item Analysis
•	Sales by item group
•	Sales by item origin
•	Item-wise revenue table
•	Ranking of items by sales value
________________________________________
**5. User Interaction & Filters**
•	Year & Quarter
•	Item Group
•	Store / District
•	Customer Name
•	Sidebar navigation buttons
Allows stakeholders to drill down into specific business question
