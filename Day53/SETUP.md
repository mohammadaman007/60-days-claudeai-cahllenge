# RegionPulse — Setup Guide

This guide lets anyone (including future-you on a new machine) get RegionPulse running locally from scratch.

## Prerequisites

- **Python 3.9+** (developed on 3.11.9)
- **VS Code** with the Microsoft Python extension (recommended, not required)
- **Git**
- A free **GitHub** account

## 1. Clone the repository

```
git clone https://github.com/mohammadaman007/regionpulse-sales-dashboard.git
cd regionpulse-sales-dashboard
```

## 2. Create and activate a virtual environment

**Why:** Keeps this project's Python packages isolated from every other project on your machine.

```
python -m venv venv
```

Activate it:

- **Windows:** `venv\Scripts\activate`
- **Mac/Linux:** `source venv/bin/activate`

You should see `(venv)` appear at the start of your terminal prompt.

## 3. Install dependencies

```
pip install -r requirements.txt
```

This installs Streamlit (the app framework), pandas (data processing), plotly (charts), and numpy (forecast calculation).

## 4. Run the app

```
streamlit run app.py
```

This opens a browser tab automatically at `http://localhost:8501`. If it doesn't open automatically, copy that URL into your browser.

## 5. Verify it's working

You should see the "RegionPulse" title and a confirmation message on the page. No errors should appear in the terminal.

## Project Structure Reference

See `PROJECT-STRUCTURE.md` for the full folder layout and what each file is responsible for.

## Troubleshooting

| Problem | Likely Cause | Fix |
|---|---|---|
| `python: command not found` | Python not installed or not on PATH | Reinstall Python, check "Add to PATH" during install |
| `(venv)` doesn't appear after activating | Wrong activation command for your OS | Use the Windows or Mac/Linux command above, matching your terminal |
| `streamlit: command not found` | Virtual environment not activated, or install failed | Re-activate venv, re-run `pip install -r requirements.txt` |
| Browser doesn't open automatically | Browser auto-launch blocked | Manually visit `http://localhost:8501` |
