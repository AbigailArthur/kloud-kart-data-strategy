# Memo to Nana Adjei

**From:** Abigail Arthur  
**Date:** 13 November 2026  
**Subject:** Kloud Kart Data Strategy – Findings, Recommendations and Deliverables

## What I found

Kloud Kart's immediate data challenge is not the absence of advanced technology. It is the need to improve how existing business data is managed, accessed, reported and protected.

The assessment identified five main issues:

1. **Live website performance:** Reporting exports use the same MySQL database as the live website. The brief confirms that these exports slowed the website twice in the past month.
2. **Inconsistent reporting:** Operations and Finance produce different figures, while the Monday management report is manually rebuilt.
3. **Untracked customer-data copies:** Marketing manages approximately 300,000 customer records, but exported copies are not centrally tracked.
4. **Customer-data requests:** A documented process for investigating, handling and recording customer-data requests has not been evidenced.
5. **Limited technical capacity:** The company relies on one PHP/MySQL developer and has no dedicated data engineering or governance specialist.

These issues create operational, reporting and customer-data risks as the business grows and prepares for its Nigeria pilot.

## What I built

| What you asked for | Status | Evidence |
|---|---|---|
| Understand the current data challenges | Completed | `situation_diagnosis.md` |
| Recommend a data architecture | Completed | `recommendation.md` |
| Provide a 12-month implementation plan | Completed | `roadmap.md` |
| Document key technical decisions | Completed | Five ADR files in `decisions/` |
| Provide a board-level presentation | Completed | `04-board-presentation/Kloud_Kart_Board_Presentation_Final.pptx` |
| Deliver an improvement beyond the brief | Completed | `improvement/improvement.md` and `improvement/Monday_Reporting_Reconciliation_Template.docx` |

## What I recommend

I recommend introducing a MySQL read replica on a second server to separate reporting activities from the live website database.

The main database should continue handling orders, customer accounts and live inventory operations. General management reporting should use the second server and refresh daily, while live stock availability should continue using current operational data.

I also recommend recruiting two specialists:

- **Data Engineer:** To manage the database infrastructure, read replica, data movement, monitoring and backups.
- **BI and Data Governance Analyst:** To improve reporting, data quality, business definitions and customer-data management.

The company should introduce a standard reporting process, maintain a register of customer-data exports and establish a documented process for handling customer-data requests.

A full data warehouse should be reconsidered when reporting complexity, data sources or analytical workloads grow beyond what the proposed setup can support.

## What it will cost

The main investment areas are the second server, storage, backups, monitoring, maintenance and recruitment of the two specialists.

Actual GHS costs require supplier quotations and salary estimates. I have not presented unverified prices as confirmed costs.

The business impact of the current problems should also be measured. For example, if two staff members each spend three hours per week reconciling reports, that represents an illustrative 312 staff-hours annually. Actual time and labour costs must be confirmed.

The cost of previous website slowdowns should be calculated using incident duration, affected orders, average order value and contribution margin. The available information does not support a verified loss figure.

## What I could not stand behind

The underlying database exports, Operations and Finance reports, system logs and customer-data records were not provided.

As a result, I could not verify:

- The exact differences between Operations and Finance figures.
- The actual financial losses caused by website slowdowns.
- The number and location of exported customer-data copies.
- The current effectiveness of customer-data request and deletion procedures.
- Actual infrastructure and recruitment costs.

These limitations are documented in the situation diagnosis. They should be investigated before final financial commitments or compliance conclusions are made.

## Closing recommendation

Kloud Kart should first protect its live operations, establish reliable reporting and improve customer-data controls. The proposed second server and two specialist hires provide a practical foundation for growth without introducing unnecessary platform complexity too early.