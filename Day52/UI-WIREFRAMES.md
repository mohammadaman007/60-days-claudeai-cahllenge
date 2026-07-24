# RegionPulse — UI & User Flow

## 1. User Flow

Single-screen, looping interaction — no page navigation:

1. User lands on the page → sees default view (all regions, full date range)
2. User adjusts filters (region multiselect, date range picker)
3. Charts and insights panel update instantly (Streamlit rerun)
4. User sees the forecast extension on the trend chart plus key insights
5. User can re-filter at any time — loops back to step 2, no reload needed

(See the interactive user flow diagram shared in chat for the visual version.)

## 2. Wireframe (Single Screen — This Is the Entire App)

```
┌─────────────────────────────────────────────────────────┐
│  RegionPulse                                    (title)  │
│  Short intro sentence explaining the app                 │
├─────────────────────────────────────────────────────────┤
│  [ Region: multiselect ▾ ]   [ Date range: __ to __ ]    │
├─────────────────────────────────────────────────────────┤
│  ┌───────────┐ ┌───────────┐ ┌───────────┐               │
│  │ Top Region│ │ Growth %  │ │ Forecast %│  ← insights   │
│  └───────────┘ └───────────┘ └───────────┘               │
├─────────────────────────────────────────────────────────┤
│  Revenue Trend + Forecast (line chart, dashed forecast)  │
│                                                            │
├─────────────────────────────────────────────────────────┤
│  Regional Comparison (bar chart)                          │
│                                                            │
└─────────────────────────────────────────────────────────┘
```

## 3. Screen Inventory

| Screen/Section | Purpose | PRD Feature Reference |
|---|---|---|
| Title + intro | Orient the user | N/A (usability) |
| Filter bar | Region + date range control | Feature #2, #3 |
| Insights panel | Top region, growth %, forecasted change | Feature #7 |
| Trend + forecast chart | Historical revenue + 3-month projection | Feature #4, #6 |
| Comparison chart | Cross-region comparison | Feature #5 |

Every section maps to a specific PRD feature — nothing exists without a stated reason.

## 4. Navigation

None. This is a single-page app by design — the PRD explicitly excludes multi-page navigation as a non-goal. All content is visible on one scroll; filters at the top affect every section below them.
