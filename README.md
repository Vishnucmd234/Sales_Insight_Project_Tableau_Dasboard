
# Sales Insight Data Analysis Tabuler

End-to-end sales analytics build: raw CSV data cleaned and modeled in **PostgreSQL**, then visualized in an interactive **Tableau** dashboard. Built on the widely-used **AtliQ Hardware "Sales Insights"** practice dataset — a hardware distributor operating across Indian markets.

**Live dashboard:** [Tableau Public →](https://public.tableau.com/app/profile/vishnu.suthar8037/viz/SalesInsightProject_17876414266870/Dashboard1)

## Tech Stack
- **PostgreSQL** — raw data storage, cleaning, keys, indexing, reporting views
- **Tableau Desktop / Tableau Public** — data modeling and dashboarding

## Data Model
5 CSV sources loaded into PostgreSQL and connected to Tableau as an **Extract**:

| Table | Role |
|---|---|
| `transactions` | Fact table — individual sales records, links to all dimensions |
| `customers` | Dimension — customer master data |
| `products` | Dimension — product master data |
| `markets` | Dimension — market/city master data |
| `date` | Dimension — calendar table for time intelligence |

## Data Pipeline (PostgreSQL)
1. Created a PostgreSQL database and raw tables matching each CSV source (`customers`, `products`, `markets`, `transactions`, `date`).
2. Loaded each CSV into its table using `COPY ... DELIMITER ',' CSV HEADER`.
3. Validated the load — row counts, null checks, and key uniqueness per table.
4. Added primary/foreign keys linking `transactions` to its four dimension tables.
5. Created indexes on join and filter columns (customer, product, market, and date keys) for query performance.
6. Built and tested cleaned reporting views in SQL — checked for duplicate rows and correct totals before connecting Tableau.
7. Connected Tableau Desktop to PostgreSQL and pulled the cleaned tables in as an Extract.
8. Built calculated fields and worksheets, then combined them into the final dashboard.
9. Published to Tableau Public.

Example load command:
```sql
COPY transactions FROM 'transactions.csv' DELIMITER ',' CSV HEADER;
```

## Dashboard
**Worksheets:** Revenue · Sales Quantity · Revenue by Markets · Sales Quantity by Market · Top 5 Customers · Top 10 Products · Year · Month · Revenue by Year · Dashboard 1

**Visuals on Dashboard 1:**
- KPI cards — Total Revenue, Sales Quantity
- Bar chart — Revenue by Market
- Bar chart — Sales Quantity by Market
- Line chart — Revenue by Month, split by year (2017–2020)
- Bar chart — Top 5 Products
- Bar chart — Top 5 Customers
- Year / Month filters for time-based drill-down

## Key Insights
1. **Delhi NCR drives over half of total revenue** — $520.79M of the $986.64M total (~53%), more than 3× Mumbai, the #2 market at $150.18M.
2. **Revenue peaked in 2018, then declined** — monthly revenue hit a high near $42.52M in 2018 but fell as low as $14.71M by 2020, a clear downward trend in the most recent years of data.
3. **A handful of SKUs drive most of the volume** — the top 5 products each move 15M+ units; the leader, Prod040 (~23.58M), outsells the #2 product, Prod159 (~17.66M), by roughly a third.
4. **Revenue is heavily concentrated in one account** — Electricalsara Stores alone generates $413.91M, more than 8× the next customer, Electricalslytical ($49.64M) — a real concentration risk if that single relationship weakens.
5. **Month-to-month revenue is volatile, not smoothly seasonal** — e.g. a jump to $35.19M in mid-2019 right after a $28.05M dip points to inconsistent order cadence across markets rather than a predictable seasonal curve.

## Author
Tableau Public profile: [vishnu.suthar8037](https://public.tableau.com/app/profile/vishnu.suthar8037)
