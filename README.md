# AirPure Innovations — AQI Analytics & Product Market Fit

## 📌 Overview

AirPure Innovations is a startup built around India's air quality crisis, with several Indian cities ranking among the world's most polluted urban centers. Before committing to production and R&D, the company needed a clear, data-backed view of where air quality is worst, how it behaves over time, what health burden it carries, and whether current market trends (like EV adoption) are actually helping.

This repository documents that work: the data cleaning and modeling done in SQL, the interactive dashboard built in Power BI, and the supporting research pulled in from outside the core datasets.

---

## 📦 Deliverables

| Dashboard |
|---|
| **[Live Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiY2NhOWEzYTUtOWY0Yy00NzFmLWE3YmUtZjJiMGE4MjkyNDcxIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** |

---

## 🗂️ Repository Structure

```
├── Primary Analysis/      → Core AQI, disease, and vehicle data analysis, built and validated in SQL
├── Secondary Analysis/    → Externally researched findings (health impact, market, policy, awareness)
├── Project Inputs/        → Problem statement, metadata, and supporting source documents
└── README.md
```

---

## 🔎 What the Analysis Covers

- **Air quality severity** across Indian states and cities, with a minimum-coverage threshold applied before any city is ranked, so sparse data never distorts the picture.
- **Pollutant composition** by region — which pollutants actually dominate, not just assumed.
- **Time-based patterns** — weekday vs. weekend behavior in major metros, and which months consistently show the worst air quality.
- **Health burden** — the most frequently reported illnesses by state, alongside average AQI and case fatality rate, to connect pollution exposure to real outcomes.
- **Market signals** — EV adoption versus AQI, and a population-weighted opportunity score to help prioritize where a product launch matters most.

Every number on the dashboard traces back to a specific, documented calculation — thresholds, exclusions, and known data gaps (like states with no AQI monitoring coverage) are tracked and disclosed rather than smoothed over.

---

## 🛠️ Tools Used

- **SQL** — data cleaning, validation, and all core calculations (single source of truth for every number on the dashboard)
- **Power BI** — data modeling, DAX measures, and the interactive dashboard
- **Excel** — small supporting calculations and sanity checks
- **External research** — used only where the internal datasets couldn't answer a question, and always cited

---

## 🎯 Why This Approach

The dashboard isn't built to look impressive — it's built to be checkable. Every threshold (like minimum data coverage before ranking a city) is a deliberate, documented choice, every exclusion is logged, and every external claim is sourced. That's what separates a defensible analysis from one that just looks plausible.

---

## 🏁 Conclusion

This project gives AirPure Innovations a grounded starting point for its air purifier strategy — where the pollution is worst, what's actually in the air, who's affected, and where the market opportunity is strongest — built from real data, not assumptions.
