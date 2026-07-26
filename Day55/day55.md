## Key Learnings — Day 5: Continue Core Feature Development

1. **Testing is a design activity, not just a bug hunt.** Writing edge cases (missing files, reversed date ranges, empty filters, sparse data) forced a review of every assumption baked into earlier code — several "obviously fine" functions only proved correct once explicitly tested against the inputs that break naive implementations.

2. **The "unhappy path" defines software quality.** Anyone can make an app work with perfect, complete data. Professional-grade software is judged by what happens when a user picks an empty filter, a date range with no results, or triggers a calculation that could divide by zero — today's pass confirmed every one of those cases degrades gracefully instead of crashing.

3. **Temporary tooling shouldn't ship.** `verify.py` was valuable for this pass but was deliberately deleted afterward — a reminder that verification scripts, debug prints, and scratch files are development aids, not production code, and leaving them in a repo signals a lack of intentionality to anyone reviewing it (including recruiters).

4. **A README is a product, not an afterthought.** It's often the *only* thing a recruiter or hiring manager actually reads — the code itself may never be opened. Writing it well (problem, solution, setup, methodology, honest non-goals) is as much a communication skill as pandas or Streamlit is a technical one.

5. **Being explicit about a model's limitations builds trust.** Documenting the forecast as "a simple linear trend, not a guarantee" in both the README and the app itself is a small thing that signals real data literacy — knowing what a model can't do is as important as knowing what it can.

6. **Finishing early is a signal to re-plan, not coast.** Because testing and documentation landed ahead of schedule, the sensible move wasn't to rush into new scope — it was to explicitly decide how to spend the freed-up time (deployment prep vs. polish), keeping the same discipline that avoided scope creep all week.
