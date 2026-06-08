# 🌍 Global Superstore Sales Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Data](https://img.shields.io/badge/Records-51%2C290-blue?style=for-the-badge)
![Markets](https://img.shields.io/badge/Markets-6%20Global-green?style=for-the-badge)
![Years](https://img.shields.io/badge/Period-2011--2014-orange?style=for-the-badge)

An interactive Power BI dashboard built on the Global Superstore dataset — a multi-year, multi-market retail dataset spanning 147 countries. The dashboard enables slice-and-dice analysis across customer segments, product categories, geographies, and shipping behaviour.

---

## 📸 Dashboard Preview

![Global Store Dashboard](./Screenshot_2026-06-08_160736.png)

---

## 📁 Project Structure

```
global-superstore-dashboard/
│
├── Global_Store_dashboard.pbix     # Power BI report file
├── Global_Superstore.txt           # Raw dataset (tab-separated)
├── Screenshot_2026-06-08_160736.png
└── README.md
```

---

## 📊 Dataset Overview

| Attribute | Detail |
|---|---|
| Source | Global Superstore (Tableau Sample Dataset) |
| Format | Tab-separated (.txt) |
| Total Records | 51,290 transactions |
| Time Period | 2011 – 2014 |
| Countries | 147 |
| Markets | APAC, EU, North America, LATAM, Africa, EMEA |
| Categories | Technology, Office Supplies, Furniture |
| Sub-Categories | 17 (Phones, Chairs, Binders, Copiers, Tables, etc.) |
| Customer Segments | Consumer, Corporate, Home Office |
| Ship Modes | Standard Class, Second Class, First Class, Same Day |

### Key Columns

| Column | Description |
|---|---|
| `Order ID` | Unique transaction identifier |
| `Order Date` / `Ship Date` | Order and fulfilment dates |
| `Customer ID` / `Customer Name` | Customer identifiers |
| `Segment` | Consumer / Corporate / Home Office |
| `Country`, `City`, `State` | Geographic hierarchy |
| `Market` / `Market2` | Region grouping (US, EU, APAC, etc.) |
| `Category` / `Sub-Category` | Product classification |
| `Sales` | Revenue per line item |
| `Profit` | Net profit per line item |
| `Quantity` | Units sold |
| `Discount` | Discount rate applied (0–1) |
| `Shipping Cost` | Cost of shipping per order |
| `Ship Mode` | Delivery class selected |
| `Order Priority` | Critical / High / Medium / Low |

---

## 📈 Dashboard Features

### Visuals Included

| Visual | Description |
|---|---|
| **World Map** | Geographic profit distribution across all markets |
| **Bar Chart — Total Profit by City** | Top 16 cities ranked by profitability |
| **Bar Chart — Total Profit by Category** | Side-by-side category comparison |
| **Line + Bar Combo — Profit & Sales by Segment × Ship Mode** | Dual-axis view of volume vs. profitability |
| **Segment Filter (Top)** | Slicer: Consumer / Corporate / Home Office |
| **Region Filter (Right)** | Slicer: Africa, APAC, Canada, Caribbean, Central, Central Asia, EMEA, EU, North, North Asia, etc. |

### Interactivity

- Cross-filtering between all visuals
- Segment and Region slicers for drill-down
- Bi-directional chart axis toggle on the city bar chart

---

## 🔑 Key Metrics

| KPI | Value |
|---|---|
| Total Sales | $12,642,905 |
| Total Profit | $1,467,457 |
| Overall Profit Margin | 11.6% |
| Total Units Sold | 178,312 |
| Total Transactions | 51,290 |

---

## 💡 Data-Driven Insights

### 1. Technology dominates profitability despite similar sales to Furniture
Technology generated $663K profit on $4.74M in sales — a **14% margin**. Furniture pulled a comparable $4.1M in sales but only returned $285K profit — a **6.9% margin**. Furniture is a capital-heavy, low-return category that warrants either pricing review or portfolio de-emphasis.

### 2. Tables sub-category is consistently loss-making
Among all 17 sub-categories, **Tables is the only one with negative total profit** — a loss of **-$64,083** across the full period. Heavy discounting combined with high shipping costs is the likely driver. This sub-category needs a pricing and discount policy overhaul.

### 3. Discounting above 20% destroys profit
Transactions with no discount averaged **$61 profit per order**. Orders with discounts above 40% averaged **-$90 profit per order** — a complete margin reversal. The data shows a clear inflection point: discounting beyond 20% is unprofitable across every category.

### 4. APAC is the most profitable global market
APAC led all six markets with **$436K profit** on $3.59M in sales (12.2% margin), outpacing EU ($373K) and North America ($304K). Africa and EMEA remain underdeveloped — together under $133K profit on ~$1.6M in combined sales.

### 5. New York City alone accounts for disproportionate profit
NYC generated **$62,037 in profit** — more than double the next city (Los Angeles at $30,441) and more than triple Seattle ($29,156). Concentrated profit in a single city signals both a success story and a concentration risk.

### 6. Standard Class carries the business — efficiently
Standard Class shipping handled **60%+ of all revenue** ($7.58M) and profit ($890K) at an 11.8% margin — barely lower than Same Day (11.4%). Customers are price-sensitive on shipping; speed premiums barely recover their cost.

### 7. Consumer segment leads in volume; Corporate leads in efficiency
Consumer generated the highest profit ($749K) but across the most orders. Corporate achieved $441K profit with significantly fewer transactions — meaning **higher average order value and better efficiency per transaction**.

### 8. Home Office is the smallest but most margin-consistent segment
Home Office delivered $277K profit on $2.31M sales — a 12% margin, the highest of the three segments. Small, high-value B2B-adjacent customers tend to buy less but discount less too.

---

## 🛠 Tools & Technologies

- **Power BI Desktop** — data modelling, DAX measures, report design
- **DAX** — calculated columns and KPI measures (`SUM`, `CALCULATE`, `DIVIDE`, `FILTER`)
- **Power Query (M)** — data cleaning and transformation
- **Global Superstore Dataset** — widely used retail analytics benchmark dataset

---

## 🚀 How to Use

1. Clone or download this repository
2. Open `Global_Store_dashboard.pbix` in **Power BI Desktop**
3. If prompted, update the data source path to point to `Global_Superstore.txt` on your local machine
4. Refresh the data and explore

> **Note:** Power BI Desktop is free to download from [Microsoft](https://powerbi.microsoft.com/desktop/).

---

## 🎯 Interview Questions & Answers

See [`INTERVIEW_QUESTIONS.md`](./INTERVIEW_QUESTIONS.md) for 30+ data analyst interview questions derived from this project, covering Power BI, DAX, data modelling, and business interpretation.

---

## 📝 License

This project uses the publicly available Global Superstore sample dataset for educational and portfolio purposes.

---

## 🙋 About

Built as a portfolio project to demonstrate end-to-end data analytics skills — from raw data ingestion to interactive business dashboard and insight generation.

Connect on [LinkedIn](#) | View more projects on [GitHub](#)
