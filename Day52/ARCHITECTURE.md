# RegionPulse — Architecture

## 1. Tech Stack

| Layer | Choice | Why |
|---|---|---|
| Frontend | Streamlit (built-in UI) | No separate frontend code needed; matches zero HTML/CSS/JS experience |
| Backend | None — Streamlit is the backend | Runs Python logic and serves UI in one process |
| Database | None — flat CSV file | PRD non-goal; data is static and small |
| Authentication | None | PRD non-goal; public portfolio dashboard |
| AI Model/API | None | Forecast is local linear regression, not an external AI call |
| Charting | Plotly (plotly.express) | Interactive, integrates natively with Streamlit |
| Data processing | pandas, numpy | Matches existing skills; industry standard |
| Forecasting | numpy.polyfit or sklearn LinearRegression | Simple, explainable, beginner-appropriate |
| Hosting | Streamlit Community Cloud | Free, deploys directly from GitHub, zero server config |
| Version control | Git + GitHub | Required for repo deliverable and Streamlit Cloud deployment |

## 2. Component Overview

The app is a single Python process with no client-server split. Components:

- **app.py** — entry point; page config, filter widgets, layout, orchestrates other modules
- **data_loader.py** — loads and cleans `sales.csv`, returns a pandas DataFrame
- **charts.py** — builds the trend chart and regional comparison chart (Plotly figures)
- **forecast.py** — computes a 3-month linear trend forecast
- **sales.csv** — static data file, the only "external" data source

See the interactive architecture diagram shared in chat for the full component map.

## 3. Data Flow

1. Browser requests the app → Streamlit Cloud runs `app.py`
2. `data_loader.py` reads and cleans `sales.csv` into a DataFrame
3. User's filter selections (region, date range) narrow the DataFrame
4. `charts.py` builds the trend and comparison charts from filtered data
5. `forecast.py` extends the trend chart with a 3-month projection
6. The rendered page (charts + insights panel) streams back to the browser

Because Streamlit reruns the script top-to-bottom on every interaction, there is no separate request/response cycle with routes — every filter change is a fresh, fast re-execution of `app.py`.

## 4. AI Interaction

None. The forecast is a local statistical calculation (linear trend), not an external AI service call.

## 5. External Services

- **GitHub** — stores source code, triggers redeploys on push
- **Streamlit Community Cloud** — hosts the live app (free tier)

No third-party APIs, payment processors, or email services are used.

## 6. Design Rationale

This architecture deliberately avoids a database, backend server, and authentication layer because the PRD explicitly excludes them as non-goals for v1.0. Streamlit was chosen specifically because it lets a Python-only developer (no prior web dev experience) ship an interactive web app without learning a separate frontend stack.
