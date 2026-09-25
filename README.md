# 🛒 ShopNest: Enterprise Sales & Revenue Analytics Dashboard

<p align="left">
  <img src="https://img.shields.io/badge/Platform-Microsoft%20Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/Language-DAX-0078D4?style=for-the-badge" />
  <img src="https://img.shields.io/badge/ETL-Power%20Query%20(M)-217346?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Architecture-Star%20Schema-3776AB?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Production%20Ready-success?style=for-the-badge" />
</p>

An end-to-end Business Intelligence solution built on **Microsoft Power BI** to analyze multi-tier e-commerce transaction data, identify revenue leakages, track regional territory trends, and resolve inventory misallocations.

---

## 📌 Business Problem & Context
Executive stakeholders and operations managers faced severe visibility gaps across multi-regional distribution networks:
- **Scattered Data Records:** Over 3,000+ transaction records were stored across disparate operational flat files without centralized aggregation.
- **Inventory Imbalances:** Inability to isolate low-velocity product categories led to stockouts in high-demand zones and excess inventory buffers in lagging territories.
- **Reporting Inefficiencies:** Manual spreadsheet collation introduced analytical delays of 4–5 business days for monthly review cycles.

---

## ⚙️ Data Pipeline & Transformation (ETL)

Data ingestion and cleaning workflows were executed inside **Power Query (M Engine)**:

* **Type Normalization:** Handled inconsistent date formatting (`YYYY-MM-DD` vs `DD-MM-YYYY`), standardized customer phone numbers, and enforced strict currency decimal precisions.
* **Missing Value Imputation:** Handled `NULL` and empty territory records via relational key lookup mapping rather than row drops to maintain revenue totals.
* **Custom Conditional Columns:** Engineered flags for high-value orders (`Order_Amount >= 5000`), regional categorization tiers, and customer longevity brackets.
* **Performance Tuning:** Filtered redundant attributes and applied table indexing upstream to optimize VertiPaq compression inside Power BI.

---

## 🏗️ Data Modeling & Architecture

The report implements an optimized **Star Schema** data model to minimize memory footprint and maximize DAX evaluation speeds.

```text
               ┌────────────────────────┐
               │     Dim_Customers      │
               ├────────────────────────┤
               │ CustomerID (PK)        │
               │ CustomerName           │
               │ Segment / Region       │
               └───────────┬────────────┘
                           │ 1
                           │
                           │ *
┌──────────────────────┐   │   ┌────────────────────────┐   *   1 ┌────────────────────────┐
│       Dim_Date       │───┴───│       Fact_Sales       │─────────│      Dim_Products      │
├──────────────────────┤ *   * ├────────────────────────┤         ├────────────────────────┤
│ Date (PK)            │       │ TransactionID (PK)     │         │ ProductID (PK)         │
│ Year / Quarter       │       │ OrderDate (FK)         │         │ ProductName            │
│ MonthName / Weekday  │       │ CustomerID (FK)        │         │ Category / SubCategory │
│ FiscalPeriod         │       │ ProductID (FK)         │         │ UnitCost               │
└──────────────────────┘       │ Quantity               │         └────────────────────────┘
                               │ UnitPrice              │
                               │ TotalRevenue           │
                               │ DiscountAmount         │
                               └────────────────────────┘
