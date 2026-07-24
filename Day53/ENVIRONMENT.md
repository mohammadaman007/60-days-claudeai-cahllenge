# RegionPulse — Environment Configuration

## Runtime

| Tool | Version | Purpose |
|---|---|---|
| Python | 3.11.9 | Language runtime for the entire app |
| pip | (bundled with Python) | Installs Python packages |
| venv | (bundled with Python) | Creates the isolated virtual environment |

## Editor / IDE

| Tool | Purpose |
|---|---|
| VS Code | Code editor |
| Python extension (Microsoft) | Syntax highlighting, linting, run support for Python in VS Code |

## Package Dependencies (see `requirements.txt` for exact pinned versions)

| Package | Purpose |
|---|---|
| streamlit | Web app framework — renders the entire UI |
| pandas | Data loading, cleaning, aggregation |
| plotly | Interactive chart rendering |
| numpy | Forecast calculation (linear trend) |

## Environment Variables / Secrets

**None required for v1.0.** This project has no API keys, no database connection strings, and no authentication tokens — a direct result of the PRD's non-goals (no auth, no database, no external AI API).

If this changes in the future (e.g. adding a real API), secrets would live in `.streamlit/secrets.toml` locally (already excluded via `.gitignore`) and in the "Secrets" section of the Streamlit Cloud app settings for the deployed version — never committed to Git.

## Version Control

| Tool | Purpose |
|---|---|
| Git | Local version control |
| GitHub | Remote repository hosting: `https://github.com/mohammadaman007/regionpulse-sales-dashboard` |

**Branching strategy:** Single `main` branch (trunk-based). Appropriate for a solo 10-day project — no parallel feature branches needed at this scale.

## Hosting (Day 9)

| Tool | Purpose |
|---|---|
| Streamlit Community Cloud | Free hosting, deploys directly from the GitHub `main` branch |

## Local Ports

| Port | Purpose |
|---|---|
| 8501 | Default Streamlit local development server (`http://localhost:8501`) |
