0. Definition of the bussiness case 
    - Are we meeting the targets?
    - Which are the products that are more profitable? 
    - Time series of the revenue, and why it changes?
    - Which are the most loyal customers?(which city? New customers are the returning? High spending vs low spending?)

1. Understand what data do I have
    a. Sales Target:
    Each line is a target for a month and a Category
        - Month of Order Data: Month + Year, "Apr-18, May-18"
        - Category: str, {Furniture, Clothing, Electronics}
        - Target: float 
    
    b. Order Details
    each row is basically a line item inside an order
        - Order ID: B-00000, order id
        - Amount: float, the total sales value (Amount ≈ Quantity × unit selling price)
        - Profit: float, Amount minus cost
        - Quantity: int, how many units were sold 
        - Category: str, self explanatorio
        - Sub-Category: str, self explinatorio 

    c. List of Orders
        - Order ID: B-00000, order id
        - Order Date: Date
        - CustomerName: Str
        - State: str
        - City: str 

2. Structure of the repository 
    a. Data folder with raw and processed data
    b. sql folder with queries and scripts for data processing and analysis
    c. docs folder with documentation and reports, definitiosn of KPI
    d. README file with project overview and instructions

3. Do I need to clean the data?
    Import the csv files
    Normalise column names, check for missing values, and handle inconsistencies.
    Create clean views for each dataset.

    Data cleaning here is not “fixing everything until it looks nice”. It is:
    1. Preserving the raw data
    Never overwrite raw CSVs.
    Load them into raw.* tables exactly as-is.

    2. Making a staging layer (stg.*)
    This is where we do the “mechanical” cleaning:
    standardise names (snake_case)
    trim text (remove hidden spaces)
    parse dates properly
    cast types (numbers as numbers)
    drop truly empty rows (e.g., missing order_id)

    3. Building a clean analytics layer (clean.*)
    This is where we model for analysis / Power BI:
    reliable keys (order_id, customer_id, product/category)
    fact table(s) + dimensions (star schema)
    final business rules documented (what is revenue, what is churn, etc.)

4. Define the KPIs (Key Performance Indicators) for the business
    (inside the docs folder)
    - Revenue (gross vs net si aplica)
    - Profit / margin
    - AOV = revenue / nº pedidos
    - Customers (distinct), new vs returning
    - Retention rate
    - Churn (definición operativa en e-commerce: “no compra en X días”)

5. Create view helpers (tablar metricas)
    - customer_first_order (primera compra por cliente)
    - orders_enriched (pedido con métricas: revenue, items, etc.)
    - monthly_customer_activity (cliente x mes: compró o no)
    - cohorts (cohort = mes de primera compra)

6. Queries that answer business questions
    1. Revenue y profit por mes (trend + MoM con LAG)
    2. AOV y nº pedidos por mes
    3. New vs returning customers por mes
    4. Cohort retention mensual (tabla cohort)
    5. Churn rate (X días sin compra) por mes/cohort
    6. Top categorías por crecimiento (rank con window)
    7. Productos “héroes” vs “villanos” (profit vs volumen)
    8. Basket size: items por pedido (distribución básica)
    9. Concentración: % revenue top 10% clientes (pareto)
    10. Tiempo entre compras (avg days between orders con LAG)
    11. Target vs actual (si tienes targets)
    12. “At risk” customers (no compra en 60–90 días) y tamaño del problema

7. README: “preguntas → queries → conclusiones → decisiones”
    Estructure of the README FILE:
    Contexto (2–3 líneas)
    Dataset + schema (mini diagrama o bullets)
    Definiciones de KPI
    Tabla “Question → SQL file → Key finding → Decision”
    5–8 insights con bullets (con números)
    “How to run” (DuckDB + comandos) 