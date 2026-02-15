# MNC Global Sales Analytics Dashboard

An end-to-end  business intelligence solution analyzing $50M+ in sales across 7 global regions, built with Power BI and MySQL.


---

## Project Overview
This interactive Power BI dashboard provides comprehensive sales analytics for a multinational corporation, enabling data-driven decision-making across executive leadership, product management, and sales teams.

**Key Features :**
- 4-page interactive dashboard with 20+ visualizations
- Real-time filtering and cross-visual interactivity
- Analysis of 200+ transactions across 7 quarters (Q1 2023 - Q3 2024)
- Custom DAX measures for advanced calculations
- Professional UI/UX with warm sunset color theme

---

## Dashboard Screenshots

### Landing Page
Navingation hub with dashboard summary and key statistics
<img width="1880" height="1156" alt="image" src="https://github.com/user-attachments/assets/eb551844-e7da-4544-b18d-f06ba2475543" />

### Executive Overview
KPIs, geographic sales distribution, trend analysis, and top products
<img width="2074" height="1164" alt="image" src="https://github.com/user-attachments/assets/c60f347f-cd6a-43d1-b683-85556c40e9e0" />

### Products & Customer Analysis
Product performance, profit margins, customer segmentation, and top customers
<img width="2076" height="1168" alt="image" src="https://github.com/user-attachments/assets/c1176fa9-2510-47eb-aeaf-c2a660e7a20c" />

### Sales Team Performance
Sales rep rankings, commission tracking, and performance trends
<img width="2076" height="1158" alt="image" src="https://github.com/user-attachments/assets/ab3ccde5-aa88-4c2e-af40-ad82b09321a4" />

---

## Technical Stack

| Component           | Technology           |
| ------------------- | -------------------- |
| **Database**        | **MySQL 9.6**        |
| **BI Platform**     | **Power BI Desktop** |
| **Query Languages** | **SQL, DAX**         |
| **Connectivity**    | **ODBC Driver**      |
| **Data Model**      | **Star Schema**      |

---

## Database Architecture

### Tables (7 Total) :

**Dimension Tables :**
- **Regions** - 7 global regions (USA, UK, Germany, Singapore, India, UAE, Brazil)
- **Branches** - 14 branch locations across 5 continents
- **Products** - 18 products across 5 categories
- **ProductCategories** - Electronics, Software, Hardware, Cloud Services, Consulting
- **Customers** - 50+ customers (Corporate, Retail, Wholesale)
- **SalesReps** - 20 sales representatives

**Fact Table :**
- **SalesTransactions** - 200+ transactions with quantity, price, discount, dates

### Pre-built Views (5) :
- `vw_SalesByRegion` - Aggregated regional performance
- `vw_ProductPerformance` - Product-level profitability
- `vw_SalesRepPerformance` - Sales rep rankings and commissions
- `vw_CustomerAnalysis` - Customer lifetime value and behavior
- `vw_MonthlySalesTrends` - Time-series analysis

---

## Key DAX Measures

### Sales Metrics
```dax
Total Net Sales =
SUMX(
    SalesTransactions,
    SalesTransactions[Quantity] *
    SalesTransactions[UnitPrice] *
    (1 - SalesTransactions[Discount] / 100)
)

Total Orders = COUNTROWS(SalesTransactions)

Total Customers = DISTINCTCOUNT(SalesTransactions[CustomerID])

Average Order Value = DIVIDE([Total Net Sales], [Total Orders], 0)
```

### Profitability Metrics
```dax
Total Cost =
SUMX(
    salestransactions,
    salestransactions[Quantity] * RELATED(products[CostPrice])
)

Total Profit = [Total Net Sales] - [Total Cost]

Profit Margin % = DIVIDE([Total Profit], [Total Net Sales], 0) * 100
```

### Sales Team Metrics
```dax
Total Commission =
SUMX(
    SalesTransactions,
    [Total Net Sales] * RELATED(SalesReps[CommissionRate]) / 100
)
```

---

## Dashboard Features

### Interactive Elements :
- **Dynamic Filtering** - Year, Quarter, Region, ProductCategory, CustomerType slicers
- **Cross-Filtering** - Click any visual to filter all others
- **Drill-Down** - Navigate from global overview to transaction-level detail
- **Conditional Formatting** - Color gradients for profit margins and performance
- **Data Bars** - Visual comparison in tables
- **Navigation System** - Clickable buttons to move between pages

### Visualization Types :
- KPI Cards (12)
- Geographic Map with bubble sizes
- Line Charts (Trend analysis)
- Bar Charts (ranking and comparisons)
- Donut Chart (category breakdown)
- Pie Chart (customer segmentation)
- Tables with conditional formatting (2)

---

## Key Business Insights

**Geographic Performance :**
- North America and South Asia are top-performing regions
- 7 global regions with consistent 15-20% YoY growth
**Revenue Brerakdown :**
- Total Sales : $15.53M (latest quarter)
- Average Order Value : $135.03K
- 115 orders across 43 customers
**Product Analysis :**
- Software category generates highest revenue
- Enterprise Suite Annual License is #1 product ($43.65M)
- Profit margins range from 36-80% across product lines
**Customer Insights :**
- Corporate customers : 33.33% of revenue
- Retail customers : 33.33% of revenue
- Wholesale customers : 33.33% of revenue
- Top customer : Bangalore Tech Solutions ($8.9M)
**Sales Team :**
- 20 sales representatives tracked
- Total commission : $742.20K
- Top performer : Amit Patel ($1.37M in sales)

---

## Setup Instructions

**Prerequisites :**
- MySQL Server 8.0 or higher
- Power BI Desktop (latest version)
- MySQL ODBC Driver 9.6x

### Step 1 - Database Setup
1. Install MySQL Server from mysql.com
2. Open MySQL Workbench and connect to your local instance
3. Run queries. If you already have a SQL file, then run the database script - **source database/MNC_Sales_Dashboard_MySQL.sql** or open the file in Workbench and execute
4. Verify Installation -
          **USE MNC_SalesDB;**
          **SHOW TABLES;**
          **SELECT COUNT(*) FROM SalesTransactions;**

### Step 2 - Power BI Setup
1. Install MySQL ODBC Driver from mysql.com/downloads/connector/odbc
2. Open PowerBI Desktop
3. Get Data -> ODBC -> Create Connection :
     - Server : "localhost"
     - Database : "MNC_SalesDB"
     - Username : "root"
     - Password : [your MySQL password]
4. Open the dashboard files :
     - Navigate to dashboard/MNC_Sales_Dashboard.pbix
     - Refresh data if prompted
