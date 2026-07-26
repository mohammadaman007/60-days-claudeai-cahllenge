## Key Learnings — Day 4: Core Feature Implementation

1. **Separation of concerns in a data app** — splitting logic into `data_loader.py`, `charts.py`, and `forecast.py` (rather than one large script) meant each module could be built, tested, and debugged independently. This is a core software engineering principle: isolate responsibilities so a bug in one area can't silently break another.

2. **Defensive data handling** — every function was built to handle the "unhappy path" first: missing files, empty filter results, insufficient data for forecasting. Professional data applications are judged less by how they perform on clean data and more by how gracefully they degrade on messy or edge-case input.

3. **Reactive UI architecture** — Streamlit's rerun-on-interaction model (rather than explicit event handlers or API routes) demonstrated a different paradigm from traditional web development: state is recomputed from scratch on every interaction, which simplifies the mental model at the cost of needing careful guards against expensive recomputation as apps scale.

4. **Statistical modeling with intellectual honesty** — the forecast uses a simple linear regression, deliberately chosen over a "black box" model, and is labeled as an estimate rather than a prediction. This reflects a real industry practice: simpler, explainable models are often preferred in business contexts where stakeholders need to trust and interpret the output, not just consume a number.

5. **Building against a contract, not from scratch** — every function signature had already been specified in `API.md` on Day 2. Implementing against a pre-agreed contract (inputs, outputs, error cases) rather than designing on the fly is standard practice in team environments, and it's why today's implementation had zero redesign decisions or blocked moments.

6. **Incremental verification over batch building** — testing after every milestone (charts, then filters, then forecast, then insights) rather than writing all the code first and debugging at the end caught issues early, when they were cheap to fix and easy to isolate to a single recent change.
