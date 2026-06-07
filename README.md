# JIRA Defect Remediation & Tracking — Expedia Group BI Initiative

**Tools:** Python · Pandas · Google Colab · Tableau · Miro  
**Data:** Fully synthetic (simulated JIRA + HR datasets)  
**Completed:** May 2026

---

## Project Overview

This end-to-end business intelligence project simulates a real-world defect remediation initiative for a large technology company. Starting from two raw synthetic datasets — a JIRA export of 6,500 tickets and an employee org chart of 10,500 employees — the project delivers a fully classified, costed, and leadership-ready analysis of an open bug backlog spanning 16 years.

The goal: give executive leadership a clear, actionable picture of how many bugs exist, who owns them, how much remediation will cost, and what it will take to resolve them.

---

## Key Findings

| Metric | Value |
|---|---|
| Open bug-tier tickets identified | **1,820** |
| Oldest unresolved ticket | **16.0 years** (5,836 days) |
| Estimated remediation cost (base) | **$2,337,500** at $125/hr blended rate |
| Tickets in Blocked status | **353** |
| % of all JIRA tickets open/unresolved | **43.2%** |
| Engineering hours remaining | **18,700 hrs** |
| Top team by open ticket count | **Expedia Feature Flags (31 tickets)** |

---

## Architecture & Pipeline

```
jira.csv (6,500 tickets)  ──┐
                             ├──▶  Python ETL Pipeline (Google Colab)
employees.csv (10,500)    ──┘         │
                                      ├── Bug Taxonomy Classification (17 types → 4 tiers)
                                      ├── Status Filter (Open / Unresolved only)
                                      ├── Ticket Aging Calculation
                                      ├── Employee Hierarchy Self-Join
                                      ├── JIRA ↔ Employee Name Match
                                      └── ROI / Cost Estimation
                                               │
                              ┌────────────────┴───────────────────┐
                              ▼                                     ▼
                      Clean CSV Exports                    Tableau Dashboard
              jira_enriched.csv (6,500 rows)          Leadership Accountability
              open_bugs_with_cost.csv (1,820)          Priority & Aging Views
              team_summary.csv                         Ticket Volume Trend
              manager_accountability.csv               Cost & ROI Estimates
              employee_hierarchy.csv (10,500)
```

---

## Bug Taxonomy

One of the core design decisions was consolidating 17 inconsistent JIRA issue type labels into a clean 4-tier classification aligned with Atlassian best practices:

| Tier | Category | Description |
|---|---|---|
| Tier 1 | Direct Bugs | Core software defects |
| Tier 2 | Customer Problems | Customer-reported issues |
| Tier 3 | Adjacent Issues | Related operational issues |
| Tier 4 | Non-Bug Work | Out of scope — excluded from analysis |

---

## Dashboard Preview

![Pipeline Architecture](visuals/pipeline_architecture.png)

![Tableau Dashboard](visuals/tableau_dashboard.png)

> The Tableau workbook (`.twbx`) is included in the `/tableau` folder. All data is fully synthetic — no real Expedia or employee data is present.

---

## Priority Breakdown

Of the 1,820 open bug-tier tickets:

- 🔴 **Critical:** 614
- 🟠 **Highest:** 282
- 🟡 **High:** 448
- 🟢 **Medium:** 560
- 🔵 **Low:** 258

425 Critical/Highest tickets must be resolved before ROI recovery begins.

---

## Remediation Cost Scenarios

| Scenario | Rate | Total Estimate |
|---|---|---|
| Optimistic | $75/hr (junior engineers) | $1,402,500 |
| Base Case | $125/hr (mid-level engineers) | $2,337,500 |
| Conservative | $175/hr (senior engineers) | $3,272,500 |

**Timeline:** 18,700 engineering hours remaining
- 10 engineers @ 30 hrs/week ≈ **14 months**
- 20 engineers @ 30 hrs/week ≈ **7 months**

---

## Deliverables

| # | Deliverable | Description |
|---|---|---|
| 1 | Python Notebook | Full ETL pipeline: taxonomy, aging, org join, cost estimate, CSV export |
| 2 | Clean Datasets (5 CSVs) | Analysis-ready outputs feeding all charts and the dashboard |
| 3 | Miro Process Map | End-to-end data flow diagram (5-lane architecture map) |
| 4 | Tableau Dashboard | Interactive leadership dashboard with 6 chart views |
| 5 | Project Plan | 11-section PM document: scope, stakeholders, WBS, risks, budget, comms |

---

## Project Plan Highlights

- **Stakeholders:** CIO, President of Technology, VP of Product, Engineering VPs, JIRA Admin
- **Risks addressed:** No accountability structure, inconsistent naming schema, 353 blocked tickets, unassigned/orphaned tickets
- **Communication plan:** Weekly executive summaries → bi-weekly VP reports → monthly all-stakeholder digest
- **Change control:** 72-hour review cycle with CIO/President of Technology final approval authority

---

## Repo Structure

```
├── README.md
├── notebooks/
│   └── BUS_266_JIRA_Bug_Project.ipynb
├── docs/
│   └── Project_Plan_Ardenvale-Wood_Consulting.pdf
├── visuals/
│   ├── pipeline_architecture.png
│   └── tableau_dashboard.png
└── tableau/
    └── JIRA_Defect_Remediation.twbx
```

---

*Prepared by Ardenvale-Wood Consulting | Synthetic data only — no proprietary or personally identifiable information.*
