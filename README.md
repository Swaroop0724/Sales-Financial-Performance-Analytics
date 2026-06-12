# 📊 Sales & Financial Performance Analytics — AtliQ Hardwares

> **Excel · Power Query · Power Pivot · DAX | Sales Analytics · Finance Analytics**

An end-to-end business intelligence project for **AtliQ Hardwares**, a global hardware manufacturer selling PCs, peripherals, networking & storage products across 23 countries. The project transforms raw transactional data into automated **Sales** and **Finance** reports using Excel's Power Query and Power Pivot to support strategic decision-making.

---

## 🗂️ Project Structure

```
sales-finance-analytics/
│
├── Sales_report.xlsx              ← Main Sales Analytics workbook
├── Finance_Analytics.xlsx         ← Main Finance Analytics workbook
│
├── reports/
│   ├── Customer_Net_sales_Performance.pdf    ← Sales Report 1
│   ├── Market_Performance_VS_Target.pdf      ← Sales Report 2
│   ├── P_L_By_Fisical_Years.pdf              ← Finance Report 1
│   └── P_L_By_Months.pdf                     ← Finance Report 2
│
├── data/
│   ├── dim_customer.csv                      ← Customer master (189 customers)
│   ├── dim_market.csv                        ← Market/Region mapping (23 markets)
│   ├── dim_product.csv                       ← Product master (298 products)
│   ├── fact_sales_monthly.csv                ← Monthly sales transactions (799,962 rows)
│   ├── fact_sales_monthly_with_cost.csv      ← Sales + freight + manufacturing cost
│   ├── ns_targets_2021.csv                   ← Net sales targets by market (FY2021)
│   └── Sales.zip                             ← Archived raw sales data
│
├── images/
│   ├── atliq_logo.png
│   └── bg.jpg
│
└── README.md
```

---

## 🏢 About AtliQ Hardwares

AtliQ Hardwares is a fictional global hardware company selling products across **23 countries** through **3 channels** (Direct, Distributor, Retailer) and **2 platforms** (Brick & Mortar, E-Commerce). Products span **3 divisions** — PC, N&S (Networking & Storage), P&A (Peripherals & Accessories) — covering **6 segments** and **13 product categories**.

---

## 🗃️ Data Model — Star Schema

```
dim_customer ──────────────── fact_sales_monthly
  (customer_code)               (customer_code)

dim_product ───────────────── fact_sales_monthly
  (product_code)                (product_code)

dim_market ─────────────────── dim_customer
  (market)                      (market)

ns_targets_2021 ─────────────── dim_market
  (market)                       (market)

fact_sales_monthly_with_cost  ← fact_sales_monthly + freight + manufacturing cost
```

### Dimension Tables

| Table | Rows | Key Columns |
|---|---|---|
| `dim_customer` | 189 | customer_code, customer, market, platform, channel |
| `dim_market` | 23 | market, sub_zone, region |
| `dim_product` | 298 | product_code, division, segment, category, product, variant |

### Fact Tables

| Table | Rows | Description |
|---|---|---|
| `fact_sales_monthly` | 799,962 | Monthly qty sold + net sales amount per customer-product |
| `fact_sales_monthly_with_cost` | 799,962 | Above + freight_cost + manufacturing_cost |
| `ns_targets_2021` | 276 | Monthly net sales target by market for FY2021 |

---

## 📈 Part 1 — Sales Analytics

### Report 1: Customer Net Sales Performance

![Customer Net Sales Performance](reports/Customer_Net_sales_Performance.pdf)

Tracks **Net Sales by Customer** across FY2019, FY2020, FY2021 with year-over-year growth %.

| Metric | 2019 | 2020 | 2021 | 21 vs 20 |
|---|---|---|---|---|
| **Grand Total** | 87.5M | 196.7M | 598.9M | **+304.5%** |

**Top Customers by 2021 Net Sales:**
| Customer | 2021 Net Sales | Growth (21 vs 20) |
|---|---|---|
| Amazon | 82.1M | 218.9% |
| AtliQ Exclusive | 61.1M | 345.8% |
| Atliq e Store | 53.0M | 223.8% |
| Sage | 20.7M | 321.5% |
| Leader | 18.8M | 314.8% |

**Highest Growth Customers (2021):**
| Customer | Growth |
|---|---|
| Nova | 2664.9% |
| Integration Stores | 887.2% |
| Chiptec | 722.0% |

---

### Report 2: Market Performance VS Target

Compares **2021 Actual Net Sales vs Target** across all 23 markets.

| Metric | Value |
|---|---|
| Grand Total Net Sales (2021) | 598.9M |
| Grand Total Target (2021) | 653.8M |
| **Total Shortfall** | **-54.9M (-8.4%)** |

**All markets missed their 2021 targets.** Key observations:

| Country | 2021 Sales | vs Target | Target % |
|---|---|---|---|
| India | 161.3M | -9.6M | -5.6% ✅ Best |
| Japan | 7.9M | -0.3M | -4.0% ✅ Best |
| Portugal | 11.8M | -0.5M | -4.1% |
| Poland | 5.2M | -0.9M | **-15.3% ❌ Worst** |
| Canada | 35.1M | -5.1M | -12.6% ❌ |
| Spain | 12.6M | -1.8M | -12.4% ❌ |
| USA | 87.8M | -10.2M | -10.4% |

---

## 💰 Part 2 — Finance Analytics

### Report 3: P&L by Fiscal Years

| Metrics | FY 2019 | FY 2020 | FY 2021 | 21 vs 20 |
|---|---|---|---|---|
| **Net Sales** | 87.5M | 196.7M | **598.9M** | +204% |
| **COGS** | 51.2M | 123.4M | **380.7M** | +209% |
| **Gross Margin** | 36.2M | 73.3M | **218.2M** | +198% |
| **GM%** | 41.4% | 37.3% | **36.4%** | -2% ⚠️ |

> Revenue grew **6.8x from 2019 to 2021**, but Gross Margin % declined from 41.4% → 36.4%, indicating COGS is growing faster than revenue — a cost efficiency concern.

---

### Report 4: P&L by Fiscal Months

AtliQ follows a **September–August fiscal year** (FY starts in September).

**FY2021 Monthly Breakdown (Net Sales):**

| Month | Net Sales | COGS | Gross Margin | GM% |
|---|---|---|---|---|
| Sep (Q1) | 44.8M | 28.4M | 16.4M | 36.7% |
| Oct (Q1) | 54.6M | 34.7M | 19.9M | 36.5% |
| Nov (Q2) | 74.3M | 47.4M | 27.0M | 36.3% |
| Dec (Q2) | **78.1M** | 49.8M | 28.3M | 36.3% |
| Jan (Q3) | 44.8M | 28.4M | 16.4M | 36.7% |
| **Total** | **598.9M** | **380.7M** | **218.2M** | **36.4%** |

**Q2 (Nov–Dec) is consistently the peak season** across all fiscal years.

**Net Sales YoY Comparison:**
| Period | Growth |
|---|---|
| FY20 vs FY19 | +124.8% |
| FY21 vs FY20 | +204.5% |

> Notable: FY2020 saw a -67.1% dip in March — likely COVID-19 impact.

---

## 🔑 Key Business Insights

1. **Revenue exploded 6.8x** from ₹87.5M (2019) to ₹598.9M (2021) — strong growth trajectory
2. **GM% is declining** (41.4% → 36.4%) — COGS growing faster than revenue, needs cost control
3. **All 23 markets missed 2021 targets** — overall shortfall of ₹54.9M (-8.4%)
4. **India is the largest market** at ₹161.3M (27% of global revenue) and closest to target (-5.6%)
5. **Poland worst performer** vs target at -15.3%; **Japan best** at -4.0%
6. **Amazon** is the top customer at ₹82.1M; **Nova** had the highest growth at 2664.9%
7. **Q2 (Nov–Dec)** is the peak season every year — ideal for promotional and inventory planning
8. **COVID-19 impact visible** in FY2020 March data — 67% drop in net sales that month

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Microsoft Excel** | Report building, dashboards, Pivot Tables |
| **Power Query (M Language)** | Data ingestion, cleaning, transformation, merging |
| **Power Pivot** | Data modeling, star schema relationships |
| **DAX** | Calculated measures — Net Sales, COGS, GM, GM%, YoY % |
| **Conditional Formatting** | Heat maps on performance vs target |

---

## ⚙️ ETL & Data Processing Steps

**Power Query transformations applied:**
1. Loaded all 6 source tables into Power Query
2. Cleaned data types, removed nulls, standardized date formats
3. Merged `fact_sales_monthly` with `dim_customer`, `dim_product`, `dim_market`
4. Added `fact_sales_monthly_with_cost` for P&L calculations
5. Created fiscal year and fiscal month columns (FY = Sep–Aug cycle)
6. Loaded cleaned tables into Power Pivot data model

**DAX Measures created:**
```
Net Sales = SUM(fact_sales_monthly[net_sales_amount])
COGS = SUM(fact_sales_monthly_with_cost[manufacturing_cost]) 
       + SUM(fact_sales_monthly_with_cost[freight_cost])
Gross Margin = [Net Sales] - [COGS]
GM% = DIVIDE([Gross Margin], [Net Sales], 0)
Net Sales Target = SUM(ns_targets_2021[ns_target])
NS vs Target = [Net Sales] - [Net Sales Target]
NS vs Target % = DIVIDE([NS vs Target], [Net Sales Target], 0)
YoY Growth % = DIVIDE([Net Sales] - [Net Sales LY], [Net Sales LY], 0)
```

---

## 🚀 How to Use

1. Clone or download the repository:
   ```bash
   git clone https://github.com/Swaroop0724/Sales-Financial-Performance-Analytics.git
   ```

2. Open **`Sales_report.xlsx`** for Sales Analytics reports

3. Open **`Finance_Analytics.xlsx`** for P&L reports

4. If data connections break, go to:
   `Data → Queries & Connections → Edit` → re-point source paths to `/data/` folder

5. Refresh all queries: `Data → Refresh All`

6. Use slicers to filter by **region**, **market**, **division**, **customer**

> **Requirements:** Microsoft Excel 2019 or later (Power Query + Power Pivot must be enabled)

---

## 📁 Reports Summary

| Report | File | Type |
|---|---|---|
| Customer Net Sales Performance | `reports/Customer_Net_sales_Performance.pdf` | Sales |
| Market Performance VS Target | `reports/Market_Performance_VS_Target.pdf` | Sales |
| P&L By Fiscal Years | `reports/P_L_By_Fisical_Years.pdf` | Finance |
| P&L By Fiscal Months | `reports/P_L_By_Months.pdf` | Finance |

---

## 🤝 Acknowledgements

- Project concept and dataset from [Codebasics](https://codebasics.io/) — Excel Data Analytics Course
- AtliQ Hardwares is a fictional company used for educational analytics projects

---

## 📬 Contact

**Jyothi Swaroop Ganapavarapu**  
MS Data Science | University of North Texas  
🔗 [LinkedIn](https://linkedin.com/in/ganapavarapu-jyothi-swaroop) · [GitHub](https://github.com/Swaroop0724)
