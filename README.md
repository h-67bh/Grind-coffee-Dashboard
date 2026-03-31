# Grind Coffee Dashboard

A **Power BI** dashboard that tracks **Revenue**, **Gross Margin**, and **Sales** for all Grind Coffee products across **2023 – 2025**.

---

## 📊 Dashboard Overview

The dashboard is built on monthly sales data covering 11 products in 3 categories:

| Category | Products |
|----------|---------|
| Hot Drinks | Espresso, Americano, Flat White, Latte, Cappuccino, Mocha |
| Cold Drinks | Cold Brew, Iced Latte, Frappuccino |
| Retail | Coffee Beans, Merchandise |

### Key Metrics Tracked

| Metric | Description |
|--------|-------------|
| **Revenue** | Total sales income (`Units Sold × Unit Price`) |
| **Gross Margin** | Profit after cost of goods (`Revenue − COGS`) |
| **Margin %** | Gross Margin as a percentage of Revenue |
| **Units Sold** | Number of items sold per period |
| **YoY Growth** | Year-over-year revenue growth percentage |

### Annual Summary (2023 – 2025)

| Year | Revenue | Gross Margin | Margin % | Units Sold |
|------|---------|-------------|---------|-----------|
| 2023 | $314,389 | $230,748 | 73.4% | 60,102 |
| 2024 | $353,739 | $259,868 | 73.5% | 67,851 |
| 2025 | $380,240 | $279,104 | 73.4% | 72,782 |

---

## 📁 Repository Structure

```
Grind-coffee-Dashboard/
├── data/
│   ├── coffee_sales_data.csv   # Monthly sales data (2023–2025, 396 rows)
│   └── data_dictionary.md      # Column definitions and metric formulas
└── README.md
```

---

## 🗂️ Data Model

The dashboard uses a single flat table (`coffee_sales_data.csv`) loaded into Power BI.

### Table: `coffee_sales_data`

| Column | Type | Description |
|--------|------|-------------|
| `Date` | Date | First day of reporting month |
| `Year` | Integer | Calendar year (2023 / 2024 / 2025) |
| `Month_Num` | Integer | Month number (1–12) |
| `Month_Name` | Text | Abbreviated month name |
| `Product` | Text | Product name |
| `Category` | Text | Hot Drinks / Cold Drinks / Retail |
| `Units_Sold` | Integer | Units sold in the month |
| `Unit_Price` | Decimal | Selling price per unit (USD) |
| `Unit_Cost` | Decimal | Cost per unit (USD) |
| `Revenue` | Decimal | Units_Sold × Unit_Price |
| `COGS` | Decimal | Units_Sold × Unit_Cost |
| `Gross_Margin` | Decimal | Revenue − COGS |
| `Margin_Pct` | Decimal | Gross_Margin / Revenue × 100 |

---

## 🔢 DAX Measures (Power BI)

Paste these measures into Power BI's **Modeling > New Measure** after loading the data:

```dax
Total Revenue = SUM(coffee_sales_data[Revenue])

Total Units Sold = SUM(coffee_sales_data[Units_Sold])

Total Gross Margin = SUM(coffee_sales_data[Gross_Margin])

Overall Margin % =
DIVIDE(
    SUM(coffee_sales_data[Gross_Margin]),
    SUM(coffee_sales_data[Revenue])
) * 100

YoY Revenue Growth % =
VAR CurrentYear = MAX(coffee_sales_data[Year])
VAR PriorRevenue =
    CALCULATE(
        SUM(coffee_sales_data[Revenue]),
        coffee_sales_data[Year] = CurrentYear - 1
    )
RETURN
DIVIDE(
    SUM(coffee_sales_data[Revenue]) - PriorRevenue,
    PriorRevenue
) * 100
```

---

## 📐 Recommended Report Pages

### Page 1 – Executive Summary
- **KPI Cards**: Total Revenue, Total Gross Margin, Overall Margin %, Total Units Sold
- **Line Chart**: Monthly Revenue trend (all years on same axis, colored by year)
- **Bar Chart**: Annual Revenue vs Gross Margin (grouped, 2023 / 2024 / 2025)
- **Slicer**: Year

### Page 2 – Product Performance
- **Bar Chart**: Revenue by Product (sorted descending)
- **Bar Chart**: Gross Margin by Product
- **Table**: Product-level breakdown (Units Sold, Revenue, COGS, Gross Margin, Margin %)
- **Slicer**: Year, Category

### Page 3 – Category Breakdown
- **Donut / Pie Chart**: Revenue share by Category
- **Line Chart**: Monthly Units Sold by Category
- **Matrix**: Category → Product → Revenue (drill-down)
- **Slicer**: Year, Month

### Page 4 – Trend Analysis
- **Line Chart**: Revenue, COGS, and Gross Margin over time
- **Waterfall Chart**: Monthly Gross Margin contribution
- **Scatter Plot**: Units Sold vs Margin % per product
- **Slicer**: Year, Category, Product

---

## 🚀 Getting Started

1. **Clone or download** this repository.
2. Open **Power BI Desktop** (free download from [powerbi.microsoft.com](https://powerbi.microsoft.com)).
3. Click **Get Data → Text/CSV** and select `data/coffee_sales_data.csv`.
4. Ensure Power BI detects the `Date` column as **Date** type.
5. Create the DAX measures listed above.
6. Build report pages following the recommended layout, or design your own.

> **Tip:** In Power Query, set `Date` column type to *Date*, `Year` / `Month_Num` / `Units_Sold` to *Whole Number*, and all currency/percentage columns to *Decimal Number*.

---

## 📝 Data Notes

- Data covers **January 2023 – December 2025** (36 months × 11 products = 396 rows).
- **Seasonal patterns** are baked in: hot drinks peak in winter, cold drinks peak in summer.
- **Year-over-year growth** of ~12% (2023→2024) and ~8% (2024→2025) is reflected in the data.
- All prices are in **USD**.
- See [`data/data_dictionary.md`](data/data_dictionary.md) for full column definitions.