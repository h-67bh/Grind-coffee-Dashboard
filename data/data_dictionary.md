# Data Dictionary – Grind Coffee Sales Data

## File: `coffee_sales_data.csv`

This file contains monthly sales records for all Grind Coffee products from **January 2023 to December 2025**.

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Date` | Date (`YYYY-MM-DD`) | First day of the reporting month | `2023-06-01` |
| `Year` | Integer | Calendar year | `2023`, `2024`, `2025` |
| `Month_Num` | Integer (1–12) | Month number | `6` |
| `Month_Name` | Text | Abbreviated month name | `Jun` |
| `Product` | Text | Product name | `Latte` |
| `Category` | Text | Product category | `Hot Drinks`, `Cold Drinks`, `Retail` |
| `Units_Sold` | Integer | Number of units sold in the month | `780` |
| `Unit_Price` | Decimal | Selling price per unit (USD) | `5.00` |
| `Unit_Cost` | Decimal | Cost of goods per unit (USD) | `1.30` |
| `Revenue` | Decimal | `Units_Sold × Unit_Price` (USD) | `3900.00` |
| `COGS` | Decimal | Cost of Goods Sold = `Units_Sold × Unit_Cost` (USD) | `1014.00` |
| `Gross_Margin` | Decimal | `Revenue − COGS` (USD) | `2886.00` |
| `Margin_Pct` | Decimal | `Gross_Margin / Revenue × 100` (%) | `74.0` |

---

## Product Reference

| Product | Category | Unit Price (USD) | Unit Cost (USD) | Gross Margin % |
|---------|----------|-----------------|-----------------|----------------|
| Espresso | Hot Drinks | $3.50 | $0.70 | 80.0% |
| Americano | Hot Drinks | $4.00 | $0.80 | 80.0% |
| Flat White | Hot Drinks | $4.50 | $1.20 | 73.3% |
| Latte | Hot Drinks | $5.00 | $1.30 | 74.0% |
| Cappuccino | Hot Drinks | $4.75 | $1.25 | 73.7% |
| Mocha | Hot Drinks | $5.50 | $1.50 | 72.7% |
| Cold Brew | Cold Drinks | $5.00 | $1.00 | 80.0% |
| Iced Latte | Cold Drinks | $5.25 | $1.35 | 74.3% |
| Frappuccino | Cold Drinks | $5.75 | $1.60 | 72.2% |
| Coffee Beans | Retail | $18.00 | $7.00 | 61.1% |
| Merchandise | Retail | $25.00 | $10.00 | 60.0% |

---

## Categories

| Category | Description |
|----------|-------------|
| Hot Drinks | Espresso-based hot beverages; peak sales in winter months |
| Cold Drinks | Chilled/iced coffee beverages; peak sales in summer months |
| Retail | Packaged coffee beans and branded merchandise |

---

## Key Metrics Used in the Dashboard

| Metric | Formula |
|--------|---------|
| **Total Revenue** | `SUM(Revenue)` |
| **Total Units Sold** | `SUM(Units_Sold)` |
| **Total Gross Margin** | `SUM(Gross_Margin)` |
| **Overall Margin %** | `SUM(Gross_Margin) / SUM(Revenue) × 100` |
| **YoY Revenue Growth** | `(Revenue_CurrentYear − Revenue_PriorYear) / Revenue_PriorYear × 100` |
