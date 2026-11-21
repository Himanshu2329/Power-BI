# ShopNest: E-Commerce Sales, Delivery & Revenue Analytics Dashboard

[https://img.shields.io/badge/Platform-Microsoft%20Power%20BI-F2C811]
[https://img.shields.io/badge/Language-DAX-blue]
[https://img.shields.io/badge/ETL-Power%20Query%20(M]-green)
[https://img.shields.io/badge/Architecture-Star%20Schema-purple]
[https://img.shields.io/badge/Status-Portfolio%20Case%20Study-lightgrey]

## Repository Files & Naming Note
- **`NexusGoods.pbix`** — Power BI Desktop workbook for the **ShopNest Store** dashboard *(saved under the working filename `NexusGoods.pbix`; all report pages, branding, and visuals inside the file belong to the ShopNest case study)*.
- **`ShopNest Dash Board Report.docx`** — Page-by-page walkthrough of all 9 dashboard views and key findings.

## Dashboard Previews
### Executive Overview
<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/3e178483-6c6b-4199-829f-97ea3c12fb6f" />


### Delayed vs. On-Time Orders
<img width="940" height="869" alt="image" src="https://github.com/user-attachments/assets/0e678e9d-ad06-449f-970a-a44b856aa5c1" />


### State-Wise Sales Analysis
<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/518f0184-1ae7-423e-8886-aa954c55b9cc" />


## Dataset & Scope
- **Dataset:** Public Brazilian e-commerce transactional dataset (27 states such as SP, RJ, MG, BA; payment methods including Credit Card and Boleto), branded as **ShopNest Store** for this analytics case study.
- **Coverage:** `04-09-2016` to `29-08-2018` — **98.239K orders/customers**, **72 product categories**, **27 states**, and **13.59M total sales** (13.44M on the Overview view).
- **Scope Note:** All regional performance gaps, delay bottlenecks, and inventory/logistics insights represent **analytical findings from historical sample data**, not measured post-deployment business results.

## Refresh & Setup
- **Refresh Mode:** Static historical dataset embedded inside `NexusGoods.pbix` (manual refresh in Power BI Desktop; no automated cloud gateway or live database connection configured).
- **How to View:** Download `NexusGoods.pbix` and open it in Microsoft Power BI Desktop, or read `ShopNest Dash Board Report.docx` for all 9 visual pages.

## Data Modeling & ETL (Power Query)
- **Star Schema:** `Fact_Sales` connected to `Dim_Customers`, `Dim_Date`, and `Dim_Products`.
- **Power Query (M) Steps:** Data type normalization, missing-value handling, delivery delay flagging (actual delivery date > estimated delivery date), and conditional order-value classification.

## Key KPIs & DAX Definitions
- **Total Sales (13.59M / 13.44M overview):** Sum of item/order sales value across the selected date range (`SUM(Fact_Sales[Price])`).
- **Total Orders (98K / 98.239K):** Distinct count of customer orders (`DISTINCTCOUNT(Fact_Sales[Order_ID])`).
- **Average Order Value — AOV (136.80 – 138.35):** Total sales divided by unique orders (`DIVIDE([Total Sales], [Total Orders])`).
- **Delayed Orders (9,445) & % Delayed (9.61%):** Count and share of orders where actual delivery date is later than the estimated delivery date (`DIVIDE([Delayed Orders], [Total Orders])`).
- **Average Delay Days (15.75):** Mean delivery delay duration across late orders.
- **Average Freight / Shipping Cost (19.99):** Mean shipping fee per order (`AVERAGE(Fact_Sales[Freight_Value])`).
- **Average Product Rating (4.07 / 5):** Mean customer review score across all reviews (57.42K 5-star reviews, 57.42%).

## Key Findings (2016–2018)
- **Growth:** Orders grew from near-zero in late 2016 to **45K in 2017** (6.1M sales) and **53K in 2018** (7.3M sales).
- **Top Categories:** **Health Beauty** leads all 72 categories, followed by Watches Gifts, Bed Bath Table, and Sports Leisure.
- **Delivery Bottlenecks:** **9,445 orders (9.61%)** arrived late (avg. 15.75 days), led by Bed Bath Table (891) and Health Beauty (868), with spikes in March and December.
- **Regional & Seasonal Patterns:** **SP (5.1M)**, **RJ (1.8M)**, and **MG (1.6M)** drive the highest sales while **Qtr 2** is the peak season (4.1M sales / 29.1K orders) and **Qtr 4** is the lowest (2.4M / 18.0K).
- **Payments:** **Credit Card** accounts for **75.35% (10.91M)** of sales, followed by **Boleto (17.42%, 2.52M)**.
