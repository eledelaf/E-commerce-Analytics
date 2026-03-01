# E-commerce Analytics

End-to-end data analytics pipeline built with **Python** and **DuckDB**, transforming raw e-commerce order data into KPI tables ready for Power BI reporting.

---

## Objective

Analyse sales and profitability performance across product categories and months, compare actuals against targets, and produce a clean output for dashboard visualisation.

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![DuckDB](https://img.shields.io/badge/DuckDB-FFC832?style=flat&logo=duckdb&logoColor=black)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)

---

## Data Sources

| File | Rows | Description |
|---|---|---|
| `List of Orders.csv` | 560 | Order-level data: customer, location, date |
| `Order Details.csv` | 1,500 | Line-item data: product, category, revenue, profit |
| `Sales Target.csv` | 36 | Monthly sales targets by category |

---

## Pipeline Architecture

```
Raw CSVs
   └── raw schema (DuckDB)
         └── staging schema  ← cleaning, type casting, deduplication
               └── clean schema  ← fact_order_lines (joined fact table)
                     └── KPI aggregations
                           └── pbi_monthly_performance.csv  → Power BI
```

**Staging layer** handles:
- Whitespace trimming across text fields
- Date and decimal type casting
- Duplicate and orphaned record validation (zero issues found)

**Fact table** (`clean.fact_order_lines`) combines order and line-item data, including revenue, profit, quantity, product category, customer, and geography.

---

## Key Outputs

**Monthly category vs. target table** — compares actual revenue and profit to sales targets with variance calculations, exported as `pbi_monthly_performance.csv` for Power BI.

### Dataset Highlights

| Metric | Value |
|---|---|
| Period covered | April 2018 – March 2019 |
| Total revenue | $431,502 |
| Total profit | $23,955 |
| Data quality issues | None |

---

## Repository Structure

```
E-commerce-Analytics/
├── data/                        # Raw CSV source files
├── portfolio_analysis.ipynb     # Full analysis pipeline
├── ecommerce.duckdb             # DuckDB database
└── pbi_monthly_performance.csv  # Power BI-ready output
```

---

## How to Run

1. Clone the repo
2. Install dependencies: `pip install duckdb pandas jupyter`
3. Open and run `portfolio_analysis.ipynb` end to end
