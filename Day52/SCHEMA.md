# RegionPulse — Data Schema

## 1. Why No Database

The PRD explicitly excludes database setup as a non-goal for v1.0. The dataset is:
- Static (a public dataset, not user-generated)
- Small enough to fit comfortably in memory
- Not in need of persistence between sessions

A flat CSV file, loaded into a pandas DataFrame at runtime, replaces a database for this project.

## 2. File Locations

- `data/raw/sales.csv` — original downloaded dataset, untouched
- `data/processed/clean_sales.csv` — cleaned, analysis-ready output (produced Day 3)

## 3. Schema (Cleaned Data)

| Column | Type | Description | Constraints |
|---|---|---|---|
| `region` | string | Sales region name | Non-null; standardized casing/whitespace |
| `order_date` | datetime | Date of the sale | Non-null; parsed to datetime64 |
| `month` | period (derived) | Order date truncated to month, for aggregation | Derived column, not in raw source |
| `revenue` | float | Sale revenue amount | Non-null; assumed >= 0 |

## 4. Relationships

None — this is a single flat table, not a relational schema. No foreign keys, no joins.

## 5. Validation Against PRD User Stories

| PRD Feature | Requires | Present in schema? |
|---|---|---|
| Region filter | `region` column | ✅ |
| Date range filter | `order_date` column | ✅ |
| Revenue trend chart | `order_date` (or `month`) + `revenue` | ✅ |
| Regional comparison chart | `region` + `revenue` | ✅ |
| Forecast feature | `month` + `revenue` (monthly aggregation) | ✅ |
| Key insights panel | `region` + `revenue` + `month` | ✅ |

Every column maps directly to a stated PRD feature. No unused columns, no missing columns.

## 6. Cleaning Rules (Applied Day 3)

- Drop or flag rows with null `region`, `order_date`, or `revenue`
- Convert `order_date` to datetime; standardize format
- Trim whitespace and standardize casing on `region` (e.g. `.str.strip().str.title()`)
- Derive `month` as a monthly period from `order_date`
- Aggregate to monthly revenue per region for chart/forecast inputs
