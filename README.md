# Kloud Kart Data Strategy

## Project Overview

This project presents a data strategy for Kloud Kart, a growing e-commerce business based in Accra, Ghana.

Kloud Kart processes approximately 4,000 orders daily and is preparing for expansion into Nigeria. Its current reporting process relies heavily on manual database exports, while its website, orders and inventory share one MySQL database.

These practices have created challenges involving website performance, inconsistent business reports and customer data management.

The goal of this project is to recommend a practical, cost-conscious data strategy that supports business growth without putting the live website at risk.

## Project Objectives

- Identify the main challenges affecting Kloud Kart's data operations.
- Recommend an architecture that separates reporting activities from the live website.
- Determine which data processes require daily updates and which require live updates.
- Improve reporting consistency between Operations and Finance.
- Strengthen customer data management and deletion procedures.
- Develop a practical 12-month implementation roadmap.

## Key Recommendations

1. Introduce a second server to handle reporting workloads.
2. Use daily batch processing for general business reporting.
3. Keep stock availability connected to the live operational system.
4. Recruit a Data Engineer first, followed by a BI and Data Governance Analyst.
5. Establish consistent business reporting definitions.
6. Introduce a controlled process for tracking customer data requests and deletions.

## Repository Structure

```text
kloud-kart-data-strategy/
│
├── decisions/
│   ├── ADR-001-reporting-read-replica.md
│   ├── ADR-002-daily-batch-reporting.md
│   ├── ADR-003-live-stock-availability.md
│   ├── ADR-004-customer-data-controls.md
│   └── ADR-005-hiring-priority.md
│
├── 04-board-presentation/
│   └── [Final board presentation]
│
├── 05-improvement/
│   ├── improvement.md
│   └── [Customer data request tracker]
│
├── situation_diagnosis.md
├── recommendation.md
├── roadmap.md
├── client_memo.md
├── README.md
```

## Project Deliverables

| Deliverable | Description |
|---|---|
| Situation diagnosis | Identifies the root causes, risks and limitations of the current data environment. |
| Architecture recommendation | Proposes a practical reporting architecture and processing approach. |
| 12-month roadmap | Defines quarterly activities and measurable business outcomes. |
| Architecture Decision Records | Documents five important decisions, alternatives and consequences. |
| Board presentation and improvement | Communicates the strategy to leadership and demonstrates an improvement beyond the original brief. |

## Important Assumptions and Limitations

This strategy was developed using the information supplied in the project brief.

No actual database export, production logs, report samples or infrastructure quotations were provided. Therefore, numerical reconciliation, database performance testing and exact infrastructure costing were not possible.

All assumptions and unverified areas are documented in the relevant deliverables.

The proposed architecture and roadmap should be validated against Kloud Kart's actual environment before implementation.

## Expected Business Benefits

- Reduced reporting pressure on the live website.
- More consistent Operations and Finance reports.
- Better visibility into customer data access and deletion requests.
- Clearer ownership of data responsibilities.
- A scalable foundation for business growth and expansion into Nigeria.

## Author

**Abigail Arthur**

Data Strategy Project  
Kloud Kart  
November 2026