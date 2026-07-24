# RegionPulse — Project Structure

## Status as of Day 3

All folders and files below now exist in the repository. `.py` files are currently placeholders/foundation only (`app.py` has a working "Hello World"; `data_loader.py`, `charts.py`, `forecast.py` are empty, scheduled for Days 3-6 per the Blueprint). `requirements.txt` and `.gitignore` are complete and committed.


```
regionpulse/
│
├── app.py                     # Main entry point — page config, layout, filters, calls other modules
├── data_loader.py              # load_data(): reads + cleans CSV, returns DataFrame
├── charts.py                   # build_trend_chart(), build_comparison_chart(): Plotly figure builders
├── forecast.py                  # forecast_revenue(): linear trend forecast logic
│
├── data/
│   ├── raw/
│   │   └── sales.csv            # Original downloaded dataset (untouched)
│   └── processed/
│       └── clean_sales.csv      # Cleaned, analysis-ready data (output of Day 3)
│
├── requirements.txt            # Pinned dependencies (streamlit, pandas, plotly, numpy) — generated via pip freeze
├── README.md                    # Problem, features, screenshots, setup, live link
├── .gitignore                    # Excludes venv/, __pycache__/, .streamlit/secrets.toml
├── venv/                          # Local virtual environment (not committed to Git)
│
├── ARCHITECTURE.md
├── SCHEMA.md
├── API.md
├── UI-WIREFRAMES.md
├── PROJECT-STRUCTURE.md         # (this file)
├── SETUP.md
├── ENVIRONMENT.md
└── DAY3-SUMMARY.md
```

## Folder Responsibilities

- **Root `.py` files** — each has exactly one responsibility (data, charts, forecasting, orchestration). This keeps `app.py` short and readable; a bug in a chart means you know exactly which file to open.
- **`data/raw/`** — keeps the original download untouched, in case cleaning logic ever needs revisiting.
- **`data/processed/`** — the analysis-ready output that the app actually reads from at runtime.
- **Documentation files** — live at the root for visibility; they are the single source of truth for design decisions made on Day 2.

## Why This Structure

Nothing here is over-engineered for a Streamlit app of this size:
- No `src/` directory — unnecessary for a project this small, and would add import complexity with no benefit.
- No `tests/` folder yet — testing happens inline per the Implementation Blueprint's daily testing tasks, not via a formal test suite, matching the project's intentionally limited scope.
- No `config/` or `utils/` folders — there isn't enough shared configuration or utility code to justify them; adding them now would be premature structure for code that doesn't exist yet.

## Where Future Code Will Live

- Day 3: `data_loader.py` + `data/processed/clean_sales.csv`
- Day 4: `charts.py` (trend + comparison chart functions)
- Day 5: filter logic added directly to `app.py`
- Day 6: `forecast.py`
- Day 7: insights panel + styling, added to `app.py`
- Day 8 onward: no new files — testing, README, deployment, and polish only
