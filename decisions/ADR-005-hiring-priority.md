# ADR-005: Hire a Data Engineer before a BI and Data Governance Analyst

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Proposed: Kloud Kart leadership

## Context

Kloud Kart has one PHP/MySQL developer, no professional data engineer or warehouse operator, and a budget for two data hires.

The company needs to protect its production database, establish reliable reporting and improve customer-data governance.

The order of recruitment matters because the reporting and data-control work depends on a stable data environment.

## Decision

Recruit a Data Engineer first to establish and maintain the reporting infrastructure. Recruit a BI and Data Governance Analyst second to standardise business reporting, improve data quality and coordinate customer-data controls.

## Alternatives considered

### Alternative A: Hire a BI Analyst first

- **How it would work:** Recruit someone to reconcile reports, build dashboards and define business measures before recruiting an engineer.
- **Why it is attractive:** It could improve management reporting quickly and reduce Nana's manual reporting work.
- **Why rejected:** Reporting would still depend on the production database, which has already experienced slowdowns during exports. The underlying reporting environment needs attention first.

### Alternative B: Hire two Data Engineers

- **How it would work:** Recruit two technical staff to focus on database infrastructure, data pipelines and platform maintenance.
- **Why it is attractive:** It provides more engineering capacity for infrastructure and future platform development.
- **Why rejected:** It leaves no dedicated capacity for agreeing on business measures, reconciling Finance and Operations reports, improving reporting adoption and coordinating customer-data governance.

### Alternative C: Hire a Data Engineer first, then a BI and Data Governance Analyst

- **How it would work:** The first hire establishes the second server, replication, monitoring and daily reporting process. The second hire improves shared reporting, definitions, quality checks and customer-data controls.
- **Why it is attractive:** It addresses infrastructure risk first while ensuring both technical and business reporting responsibilities are covered.
- **Why selected:** It matches the two-hire budget and follows the dependency between reliable data infrastructure and trusted reporting.

## Consequences

- **What this buys:** Clearer responsibility for the data environment, a safer reporting setup and dedicated support for business reporting and governance.
- **What this costs:** Two salaries, recruitment time and onboarding. The company must also allocate time from its existing developer and department representatives.
- **What it costs the client if I am wrong:** If the engineering work is relatively small but reporting problems are the greater immediate cost, delaying the analyst could prolong manual reporting. If the second hire is delayed, customer-data controls may also take longer to mature.
- **What would make me revisit this:** Evidence that the infrastructure can be safely established through a reliable external provider, or that an immediate reporting and governance problem is creating greater measurable business harm than the engineering work.

## What this survives

This decision survives pressure to hire the person who can produce dashboards first. Dashboards built on an unstable or inconsistent data environment may simply make unreliable figures look more professional.

The company should not exceed its two-hire budget by adding a third permanent data role. The existing developer and department representatives should support the work within their responsibilities.