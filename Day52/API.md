# RegionPulse — API Design (Internal Function Contracts)

## Why No REST Endpoints

This project has no backend server — Streamlit does not expose HTTP routes the way a Flask/FastAPI app would. Instead, this document specifies the **internal function contracts** each module exposes. These serve the same purpose as an API spec: documenting what each callable expects and returns, so implementation on Day 3+ requires no further design decisions.

## Function Contracts

### `load_data(filepath: str) -> pd.DataFrame`
- **Purpose:** Load and clean the sales CSV
- **Input:** Path to the CSV file (string)
- **Output:** Clean pandas DataFrame with columns `region`, `order_date`, `month`, `revenue`
- **Validation:** Drops rows with nulls in required columns; standardizes region names
- **Error handling:** Missing file → catch `FileNotFoundError`, show a friendly Streamlit error message (`st.error`)
- **Auth:** None required

### `filter_data(df: pd.DataFrame, regions: list, date_range: tuple) -> pd.DataFrame`
- **Purpose:** Apply the user's region and date filters
- **Input:** Full DataFrame, list of selected region names, (start_date, end_date) tuple
- **Output:** Filtered DataFrame
- **Validation:** If `regions` is empty, treat as "all regions"; if `date_range` is invalid (start > end), swap or reject with a message
- **Error handling:** Empty result → returns an empty DataFrame; calling code checks length before charting
- **Auth:** None required

### `build_trend_chart(df: pd.DataFrame) -> plotly.graph_objects.Figure`
- **Purpose:** Build the revenue-over-time line chart
- **Input:** Filtered DataFrame
- **Output:** Plotly Figure object
- **Validation:** N/A (read-only)
- **Error handling:** Empty DataFrame → returns a placeholder figure with a "no data" annotation
- **Auth:** None required

### `build_comparison_chart(df: pd.DataFrame) -> plotly.graph_objects.Figure`
- **Purpose:** Build the regional comparison bar chart
- **Input:** Filtered DataFrame
- **Output:** Plotly Figure object
- **Validation:** N/A (read-only)
- **Error handling:** Same as `build_trend_chart`
- **Auth:** None required

### `forecast_revenue(df: pd.DataFrame, periods: int = 3) -> pd.DataFrame`
- **Purpose:** Compute a linear trend forecast for future periods
- **Input:** Monthly revenue series DataFrame, number of periods to forecast (default 3)
- **Output:** DataFrame combining historical and forecasted rows, with a `type` column (`"historical"` / `"forecast"`)
- **Validation:** Requires a minimum number of historical months (recommend >= 3) to fit a trend
- **Error handling:** Insufficient data → returns historical data only, with a flag the UI uses to show "forecast unavailable for this selection"
- **Auth:** None required

### `compute_insights(df: pd.DataFrame, forecast_df: pd.DataFrame) -> dict`
- **Purpose:** Compute the key stats shown in the insights panel
- **Input:** Filtered historical DataFrame, forecast DataFrame
- **Output:** dict with keys `top_region`, `growth_pct`, `forecast_change_pct`
- **Validation:** Guards against division by zero in percentage calculations
- **Error handling:** Any calculation that can't be computed (e.g. single data point) returns `None` for that key; UI displays "N/A"
- **Auth:** None required

## Summary

No authentication is required anywhere (no user accounts exist). No request/response bodies in the HTTP sense exist because there is no HTTP layer — this table of function contracts is the equivalent specification for this architecture.
