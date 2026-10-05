# AirPure Innovations — AQI Analytics & Product Market Fit

## 📌 Overview

AirPure Innovations is a startup built around India's air quality crisis, with several Indian cities ranking among the world's most polluted urban centers. Before committing to production and R&D, the company needed a clear, data-backed view of where air quality is worst, how it behaves over time, what health burden it carries, and whether current market trends (like EV adoption) are actually helping.

This repository documents that work: the data cleaning and modeling done in SQL, the interactive dashboard built in Power BI, and the supporting research pulled in from outside the core datasets.

**Context:** built as part of a guided resume project challenge (problem statement and raw datasets were provided). The data cleaning approach, coverage thresholds, DAX logic, and analytical choices documented below are my own work on top of that brief.

---

## 📦 Deliverables

| Dashboard |
|---|
| **[Live Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiY2NhOWEzYTUtOWY0Yy00NzFmLWE3YmUtZjJiMGE4MjkyNDcxIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** |

---

## 🔑 Key Findings

*Figures reflect the dashboard's 2024 view.*

- **Most polluted areas, after applying a minimum-coverage threshold** — an area isn't ranked unless it has at least 90 reporting days in the period under review (in the validated Dec 2024–May 2025 ranking, this excluded 38 of 286 candidate areas) — the worst-ranked areas include Byrnihat, Delhi, Hajipur (Bihar), Gurugram, and Ghaziabad. *Byrnihat is listed under Assam in the dataset; it actually sits in Meghalaya's Ri-Bhoi district, on the Assam–Meghalaya border, and is sometimes reported under either state depending on the source.*
- **PM10 is the dominant pollutant nationally**, showing up as the top pollutant in effectively every state reviewed (e.g. Andhra Pradesh, Assam, Bihar, Chandigarh), with PM2.5 consistently the second most common.
- **Air quality is sharply seasonal** — AQI varies roughly 3x across the year (≈55–65 in Jul–Aug vs. ≈155–180 in Nov–Dec).
- **Weekend vs. weekday AQI differences are small and inconsistent across metro areas** — within roughly ±3–4 AQI points either way (Bengaluru −3.3, Pune −3.0, Ahmedabad −1.7, Chennai +1.9, Kolkata +1.0, Mumbai and Hyderabad barely move) — not large or consistent enough to say weekends are materially cleaner.
- **Goa and Gujarat have the highest case fatality rate among states with a meaningful case volume** (states with fewer than 100 total reported cases are excluded, since a handful of cases can produce a misleadingly extreme rate) — both sit at roughly 2.6%, well above most other states in the ranking; the gap between the two of them is negligible.
- **Kerala has the highest total reported case volume** (~13K), followed by Maharashtra (~11K) and Madhya Pradesh (~9.6K) — case volume and fatality rate don't move together, which is worth noting on its own.
- **EV adoption shows no clear relationship with AQI** even among the states with the highest adoption rates — adoption is still in the low single digits everywhere, so it's too early for it to be moving the needle on air quality.
- **Delhi, Uttar Pradesh, and Maharashtra rank highest on a population-weighted market opportunity score**, making them the clearest early targets for a product launch; Delhi alone also tops the metro-level market-potential ranking (AQI × population) by a wide margin.

---

## 🖥️ Dashboard Preview

**City Risk view** — severity KPIs, seasonal trend with YoY callouts, ranked city table, air quality status distribution
![City Risk](screenshots/city_risk_page.png)

**Health Impact view** — case/death/CFR KPIs, pollutant composition by state, CFR ranking with a minimum-case filter applied
![Health Impact](screenshots/health_impact_page.png)

**Executive / Market view** — weekday vs. weekend comparison, metro market potential, seasonal marketing-intensity recommendation, EV adoption vs. AQI, and the market opportunity score
![Executive](screenshots/executive_page.png)

---

## 💡 Recommendations for AirPure

1. **Launch first in Delhi NCR** — it combines the highest market opportunity score with some of the worst severity readings in the dataset.
2. **Concentrate marketing spend October through January** — AQI consistently peaks in this window, matching the dashboard's seasonal marketing-intensity recommendation.
3. **Don't position the product around the EV trend as a demand driver** — the data shows no relationship between EV adoption and improved AQI yet.
4. **Treat PM10 (and secondarily PM2.5) filtration as the core product requirement**, not an afterthought — it's the dominant pollutant in nearly every state reviewed.

---

## 🗂️ Repository Structure

```
├── Primary Analysis/      → SQL scripts and outputs for the core AQI, disease, and vehicle analysis
├── Secondary Analysis/    → Externally researched findings (health impact, market, policy, awareness), with sources
├── Project Inputs/        → Problem statement, dataset metadata, and supporting source documents
├── screenshots/           → Dashboard page images used in this README
└── README.md
```

---

## 📊 Data Sources & Methodology

- **Source data:** day-wise state/city AQI readings, state-and-district-level disease outbreak reports, state-and-month vehicle registration records by fuel type, and state population projections — provided as part of the project brief, originally sourced from the Dataful platform. *(Raw file redistribution terms haven't been independently confirmed — if the platform doesn't permit redistributing the raw CSVs, this repo should keep only the processed/aggregated outputs and link back to the source instead.)*
- **Cleaning, done in SQL:** duplicate removal, correction of truncated/inconsistent state names, handling of missing values (set to null rather than dropped where the rest of the row was still usable), and exclusion of rows with no usable state or date. SQL scripts in Primary Analysis are numbered in the order they were run (e.g. `01_cleaning.sql`, `02_severity_ranking.sql`), so a given result can be traced back to a specific step.
- **Minimum-coverage threshold:** an area is only included in severity rankings if it has at least 90 reporting days in the selected window — this prevents an area with a handful of readings from outranking one with hundreds. In the validated Dec 2024–May 2025 ranking, this excluded 38 of 286 candidate areas.
- **Minimum-case threshold for CFR:** states with fewer than 100 total reported cases in the selected period are excluded from the case-fatality-rate ranking (shown directly on the Health Impact page), since a small number of deaths out of a small number of cases produces an extreme, unreliable percentage.
- **Market Opportunity Score:** a transparent, equally-weighted composite — 50% normalized average AQI severity + 50% normalized population, both scaled 0–1 across states before combining. This is a stated analytical assumption for prioritization purposes, not a measured quantity, and the weighting is disclosed rather than hidden. *It hasn't yet been stress-tested against alternative weightings (e.g. 60/40) — doing so would either strengthen this ranking or reveal that it's sensitive to the weighting choice.*
- **Metro population figures** used in the market-potential chart came from external city-population data (not part of the original datasets), since the provided population data is state-level only — cited in the Secondary Analysis folder.
- **Disease data is used to compare reported case and death burden across states, alongside average AQI for the same period — it does not establish that air quality caused these cases.** The disease dataset covers general outbreak/infectious-disease surveillance, not a respiratory- or pollution-linked diagnosis category, so any AQI–health connection here is a side-by-side comparison, not a causal claim.

---

## 🛠️ Tools Used

- **SQL** — all data cleaning, validation, and the core calculations; the source of truth for every number on the dashboard
- **Power BI** — data modeling, DAX measures, and the interactive dashboard
- **Excel** — small supporting calculations and sanity checks
- **External research** — used only where the internal datasets couldn't answer a question (health-impact literature, competitor pricing, AQI awareness surveys, policy coverage), and always cited in Secondary Analysis

---

## 🎯 Why This Approach

The dashboard isn't just built to look complete — every number on it is checkable. Thresholds like minimum data coverage and minimum case volume are deliberate, documented choices; exclusions and known gaps (for example, a handful of states with no AQI monitoring coverage at all) are disclosed rather than smoothed over; and anything that couldn't be answered from the internal data was either clearly sourced externally or explicitly marked as unanswered instead of estimated.

---

**Author:** Rahul Dhapodkar
