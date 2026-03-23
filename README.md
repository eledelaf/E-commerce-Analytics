# E-commerce Analytics

End-to-end data analytics pipeline built with **Python** and **DuckDB**, transforming raw e-commerce order data into KPI tables ready for Power BI reporting.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![DuckDB](https://img.shields.io/badge/DuckDB-FFC832?style=flat&logo=duckdb&logoColor=black)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)

<!-- Add a screenshot of your Power BI dashboard here:
![Dashboard](docs/dashboard_screenshot.png)
-->

---

## Objective

Analyse one year of e-commerce sales (Apr 2018 – Mar 2019) to evaluate category-level performance against targets, identify profitability drivers, and produce a clean dataset for Power BI dashboarding.

---

## Data Sources

| File | Rows | Description |
|---|---|---|
| `List of Orders.csv` | 560 | Order-level data: customer, location, date |
| `Order Details.csv` | 1,500 | Line-item data: product, category, revenue, profit |
| `Sales target.csv` | 36 | Monthly sales targets by category |

---

## Pipeline Architecture

```
Raw CSVs
 └── raw schema (DuckDB)          ← load as-is
       └── staging views           ← cleaning, type casting, trimming
             └── clean schema      ← fact_order_lines (joined fact table)
                   └── KPI tables  ← monthly aggregations + target comparison
                         └── pbi_monthly_performance.csv → Power BI
```

**Staging layer** handles whitespace trimming, date/decimal type casting, and duplicate/orphan validation (zero issues found).

**Fact table** (`clean.fact_order_lines`) joins order headers with line items into a single analytical table with revenue, profit, quantity, category, customer, and geography.

---

## Key Findings

### Overall Performance
| Metric | Value |
|---|---|
| Period | April 2018 – March 2019 |
| Total Revenue | **$431,502** |
| Total Profit | **$23,955** |
| Profit Margin | **5.6%** |
| Data Quality Issues | **None** (0 nulls, 0 duplicates, 0 orphans) |

### Category Performance vs Targets

- **Electronics** is the strongest category — beat its sales target in **9 out of 12 months**, and delivered the highest profit in the final quarter.
- **Clothing** generates the most revenue overall but consistently underperforms its (ambitious) targets, missing them in **9 out of 12 months**.
- **Furniture** struggled early in the year but turned around sharply in Q4 2018 / Q1 2019 — going from -48% variance in June to +85% in January.

### Seasonal Trends

- **January 2019** was the best month across all three categories, with a combined revenue of **$61,439** — nearly double the average month.
- **November 2018** was the second-best, showing a typical Q4 seasonal lift.
- **July 2018** was the weakest month, with all categories missing targets significantly (-79% Clothing, -28% Electronics, -68% Furniture).

### Profitability Warning

Revenue does not always mean profit. Several months show **positive revenue but negative profit** — for example, Electronics in May 2018 brought in $12,807 in revenue but lost **$2,523** in profit, suggesting cost or discounting issues worth investigating.

---

## Repository Structure

```
E-commerce-Analytics/
├── data/                          # Raw CSV source files
│   ├── List of Orders.csv
│   ├── Order Details.csv
│   └── Sales target.csv
├── portfolio_analysis.ipynb       # Full analysis pipeline (notebook)
├── ecommerce.duckdb               # DuckDB database (generated)
├── pbi_monthly_performance.csv    # Power BI-ready output
├── planning_notes.md              # Initial project planning notes
└── requirements.txt               # Python dependencies
```

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/eledelaf/E-commerce-Analytics.git
cd E-commerce-Analytics

# 2. Create a virtual environment and install dependencies
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# 3. Run the notebook
jupyter notebook portfolio_analysis.ipynb
```

The notebook executes end-to-end: it creates the DuckDB database, builds all schemas, and exports the final CSV.
