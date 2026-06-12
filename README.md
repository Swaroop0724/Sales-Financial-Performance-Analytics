# 📊 Sales & Financial Performance Analytics — AtliQ Hardwares

> **Excel · Power Query · Power Pivot · DAX | Sales Analytics · Finance Analytics**

An end-to-end business intelligence project for **AtliQ Hardwares**, a global hardware manufacturer selling PCs, peripherals, networking & storage products across 23 countries. The project transforms raw transactional data into automated **Sales** and **Finance** reports using Excel's Power Query and Power Pivot to support strategic decision-making.

---

## 📥 Download Data

> Large files are hosted on Google Drive due to GitHub's 25MB file size limit.

| Dataset | Description | Link |
|---|---|---|
| 📂 **Sales Data** | dim_customer, dim_product, fact_sales_monthly, ns_targets | [Download Sales Data](https://drive.google.com/drive/folders/1bpJEy1CuSXNIESuCZyx6RZqRWXYIx9WO?usp=sharing) |
| 📂 **Finance Data** | fact_sales_monthly_with_cost, Finance_Analytics.xlsx | [Download Finance Data](https://drive.google.com/drive/folders/1uymLIxTvgfRRQ7AuBmMmQAN1Cw3bN-aB?usp=sharing) |
| 📊 **Finance_Analytics.xlsx** | Full P&L workbook (Power Pivot + DAX) | [Open in Google Sheets](https://docs.google.com/spreadsheets/d/1NLPdrr_2RkPjdpKXYKVxnqYPaZym-6xP/edit?usp=sharing) |

---

## 🗂️ Project Structure

```
sales-finance-analytics/
│
├── Sales_report.xlsx                  ← Main Sales Analytics workbook
├── Finance_Analytics.xlsx             ← Download from Google Drive (>25MB)
│
├── reports/
│   ├── Customer_Net_sales_Performance.pdf
│   ├── Market_Performance_VS_Target.pdf
│   ├── P_L_By_Fisical_Years.pdf
│   └── P_L_By_Months.pdf
│
├── data/
│   ├── dim_customer.csv               ← 189 customers
│   ├── dim_market.csv                 ← 23 markets
│   ├── dim_product.csv                ← 298 products
│   ├── fact_sales_monthly.csv         ← 799,962 rows
│   ├── fact_sales_monthly_with_cost.csv
│   └── ns_targets_2021.csv            ← FY2021 market targets
│
└── images/reports/                    ← Report screenshots
```

---

## 🗃️ Data Model — Star Schema

```
dim_customer ──────────────── fact_sales_monthly
  (customer_code)               (customer_code)

dim_product ───────────────── fact_sales_monthly
  (product_code)                (product_code)

dim_market ─────────────────── dim_customer
  (market)                      (market)

ns_targets_2021 ────────────── dim_market
  (market)                      (market)

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
| `fact_sales_monthly` | 799,962 | Monthly qty sold + net sales per customer-product |
| `fact_sales_monthly_with_cost` | 799,962 | Above + freight_cost + manufacturing_cost |
| `ns_targets_2021` | 276 | Monthly net sales target by market for FY2021 |

---

## 📈 Part 1 — Sales Analytics

### Report 1: Customer Net Sales Performance

![Customer Net Sales Performance - Page 1](images/reports/Customer_Net_sales_Performance_p1.png)
![Customer Net Sales Performance - Page 2](images/reports/Customer_Net_sales_Performance_p2.png)

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

![Market Performance VS Target](images/reports/Market_Performance_VS_Target_p1.png)

Compares **2021 Actual Net Sales vs Target** across all 23 markets.

| Metric | Value |
|---|---|
| Grand Total Net Sales (2021) | 598.9M |
| **Total Shortfall** | **-54.9M (-8.4%)** |

> ⚠️ **All 23 markets missed their 2021 targets.**

| Country | 2021 Sales | Target % |
|---|---|---|
| India | 161.3M | -5.6% ✅ Best |
| Japan | 7.9M | -4.0% ✅ Best |
| Portugal | 11.8M | -4.1% |
| Poland | 5.2M | **-15.3% ❌ Worst** |
| Canada | 35.1M | -12.6% ❌ |
| USA | 87.8M | -10.4% |

---

## 💰 Part 2 — Finance Analytics

### Report 3: P&L by Fiscal Years

![P&L By Fiscal Years](images/reports/P_L_By_Fiscal_Years_p1.png)

| Metrics | FY 2019 | FY 2020 | FY 2021 | 21 vs 20 |
|---|---|---|---|---|
| **Net Sales** | 87.5M | 196.7M | **598.9M** | +204% |
| **COGS** | 51.2M | 123.4M | **380.7M** | +209% |
| **Gross Margin** | 36.2M | 73.3M | **218.2M** | +198% |
| **GM%** | 41.4% | 37.3% | **36.4%** | -2% ⚠️ |

> Revenue grew **6.8x from 2019 to 2021**, but GM% declined from 41.4% → 36.4% — COGS growing faster than revenue.

---

### Report 4: P&L by Fiscal Months

![P&L By Fiscal Months](images/reports/P_L_By_Months_p1.png)

AtliQ follows a **September–August fiscal year**.

**FY2021 Monthly Snapshot:**

| Quarter | Peak Month | Net Sales | GM% |
|---|---|---|---|
| Q1 | Sep | 44.8M | 36.7% |
| Q2 | **Dec** | **78.1M** | 36.3% |
| Q3 | Jan | 44.8M | 36.7% |
| Q4 | May | 44.4M | 36.6% |
| **Total** | — | **598.9M** | **36.4%** |

> **Q2 (Nov–Dec) is peak season** every year. FY2020 March saw a -67% dip — COVID-19 impact.

**Net Sales YoY:**
| Period | Growth |
|---|---|
| FY20 vs FY19 | +124.8% |
| FY21 vs FY20 | +204.5% |

---

## 🔑 Key Business Insights

1. **Revenue grew 6.8x** from ₹87.5M (2019) to ₹598.9M (2021)
2. **GM% declining** (41.4% → 36.4%) — COGS outpacing revenue growth
3. **All 23 markets missed 2021 targets** — ₹54.9M total shortfall (-8.4%)
4. **India is #1 market** at ₹161.3M (27% of global revenue), closest to target
5. **Poland worst vs target** at -15.3%; **Japan best** at -4.0%
6. **Amazon is top customer** at ₹82.1M; **Nova** had highest growth at 2664.9%
7. **Q2 (Nov–Dec) is peak season** — ideal for promotions and inventory planning
8. **COVID-19 visible** in FY2020 March — 67% month-on-month sales drop

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Microsoft Excel** | Report building, Pivot Tables, dashboards |
| **Power Query (M)** | Data ingestion, cleaning, transformation, merging |
| **Power Pivot** | Star schema data modeling |
| **DAX** | Net Sales, COGS, GM, GM%, YoY %, vs Target measures |
| **Conditional Formatting** | Heat maps on performance vs target |

---

## ⚙️ Key DAX Measures

```dax
Net Sales = SUM(fact_sales_monthly[net_sales_amount])

COGS = SUM(fact_sales_monthly_with_cost[manufacturing_cost])
     + SUM(fact_sales_monthly_with_cost[freight_cost])

Gross Margin = [Net Sales] - [COGS]

GM% = DIVIDE([Gross Margin], [Net Sales], 0)

NS vs Target % = DIVIDE([Net Sales] - SUM(ns_targets_2021[ns_target]),
                         SUM(ns_targets_2021[ns_target]), 0)

YoY Growth % = DIVIDE([Net Sales] - [Net Sales LY], [Net Sales LY], 0)
```

---

## 🚀 How to Use

1. Clone the repository:
   ```bash
   git clone https://github.com/Swaroop0724/Sales-Financial-Performance-Analytics.git
   ```
2. Download data from the Google Drive links above and place in `/data/` folder
3. Open **`Sales_report.xlsx`** for Sales Analytics
4. Open **`Finance_Analytics.xlsx`** (from Google Drive) for P&L reports
5. Go to `Data → Refresh All` to reload all Power Query connections
6. Use slicers to filter by **region**, **market**, **division**, **customer**

> **Requirements:** Microsoft Excel 2019 or later

---

## 🤝 Acknowledgements

Project concept and dataset from [Codebasics](https://codebasics.io/) — Excel Data Analytics Course.

---

## 📬 Contact

**Jyothi Swaroop Ganapavarapu**  
MS Data Science | University of North Texas  
🔗 [LinkedIn](https://linkedin.com/in/ganapavarapu-jyothi-swaroop) · [GitHub](https://github.com/Swaroop0724)
