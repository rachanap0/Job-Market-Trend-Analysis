# Data Analyst Job Market – 6 US States (Indeed)

**Goal:** Build a reproducible pipeline to scrape, clean, and analyze “Data Analyst” job postings across six states, then publish an interactive Tableau dashboard that answers:
- Where is **demand** strongest?
- Where are **salaries** most attractive?
- Where are **entry-level** opportunities more common?
- Which states are most **remote-friendly**?
- What’s the **overall best market** (composite score) right now?

---

## Live Dashboard
[Open the interactive Tableau dashboard ↗](https://public.tableau.com/app/profile/rachana.pandey5721/viz/DataAnalystJobMarketAnalysis/Dashboard2#1)


---

## Tech & Data
- **Scrape:** `jobspy` (Indeed)  
- **Notebook:** Python (pandas, matplotlib/seaborn)  
- **Viz:** Tableau (Public)  
- **Geography:** Texas, California, New York, Illinois, Florida, Washington  
- **Fields used:** `title, company, location, state, date_posted, job_type, salary (mean of min/max), is_remote, job_url_direct`

> **Ethics note:** scraping respects site ToS/rate limits; for portfolio/demo only.

---

## How to Reproduce

1. **Scrape & clean (Jupyter)**
   - Run `Jobspy.ipynb` to scrape Indeed via `jobspy` for the six states.
   - Cleaning keeps: `title, company, location, state, date_posted, job_type, salary, is_remote, job_url_direct`.
   - Exports helper time series:  
     `jobs_postings_daily.csv` with columns `state, date_posted_dt, postings`.

2. **EDA (Jupyter)**
   - Salary distribution, top titles/locations, average salary by state, remote share, entry-level share.
   - Outputs shown in the notebook.

3. **Tableau model**
   - **Measures**
     - *Postings (Demand):* `COUNT([title])`
     - *Median Salary:* `MEDIAN([salary])`
     - *Entry Share %:* `AVG([Is Entry?])`
     - *Remote Share %:* `AVG([Is Remote?])`
   - **Z-scores** (table calcs over `State`)
     - `Demand Z`, `Salary Z`, `Entry Z`, `Remote Z`
   - **Composite Score**  
     ```
     0.30 * [Demand Z] +
     0.30 * [Salary Z] +
     0.25 * [Entry Z]  +
     0.15 * [Remote Z]
     ```
   - **Dashboard layout**
     - KPI Row: Postings • Median Salary • Entry % • Remote %
     - Composite Score (Use as Filter)
     - 2×2 Detail: Median Salary | Postings • Entry % | Remote %
     - Optional: Posting over Time (7-day rolling avg)

---

## Key Findings (from this scrape)
- **Highest average salary:** *Washington, USA* (~$106k)
- **Highest demand:** *Washington, USA* (≈48 postings)
- **Best entry-level availability:** *Florida, USA* (~2.5% of postings)
- **Most remote-friendly:** *New York, USA* (~26% remote)
- **Overall best market (composite):** *California, USA*

> These will update on new runs; the dashboard recomputes live.

--
## About
Built end-to-end: web scraping → data cleaning → EDA → modeling (Z-scores) → interactive Tableau dashboard. Perfect showcase of the data-analyst lifecycle.
