# E-commerce Analytics

A cute but practical analytics project using **Python** and **DuckDB** to turn raw e-commerce order data into monthly KPI tables for Power BI.

---

## Objective

Explore sales and profit by product category and month, compare actual results against targets, and create a clean output table ready for reporting.

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
|---|---:|---|
| `List of Orders.csv` | 560 | Order-level data with customer, location, and date |
| `Order Details.csv` | 1,500 | Line-level data with product, category, revenue, and profit |
| `Sales Target.csv` | 36 | Monthly sales targets by category |

---

## Pipeline Overview

```text
Raw CSVs
   └── raw schema
         └── staging schema
               └── clean schema
                     └── KPI tables
                           └── pbi_monthly_performance.csv
