# Kloud Kart – Data Strategy Recommendation

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** Abigail Arthur  
**Date:** 13 November 2026

## 1. Executive Recommendation

Kloud Kart should establish a reliable reporting environment using a second MySQL server (read replica), introduce standard daily reporting, strengthen customer-data controls and recruit two data specialists.

The immediate priority is to protect the live website and improve confidence in business reports. A full data warehouse or company-wide real-time analytics platform is not justified at this stage.

This recommendation builds on the existing MySQL environment, addresses the problems identified in the brief and respects the board's limit of two additional hires.

## 2. Recommended Architecture

### Introduce a MySQL read replica

Kloud Kart should retain its existing MySQL database as the main operational database and introduce a second server that receives a copy of its data.

The responsibilities should be divided as follows:

**Main operational database**
- Handles customer orders and transactions.
- Manages customer accounts.
- Supports live inventory operations and stock availability.
- Remains the primary system for day-to-day business activities.

**Second server – reporting**
- Receives replicated data from the main database.
- Handles reporting queries and large exports.
- Supports daily management reports.
- Reduces the need to run heavy reporting queries against the live website database.

The Data Engineer should monitor replication delays, server capacity, backups and recovery procedures. Reports should clearly show their last successful refresh time so users understand how current the information is.

Live stock availability must continue using the operational database because stock information cannot become stale. Other management reporting can refresh daily.

### Why a read replica instead of Snowflake or BigQuery?

A cloud data warehouse such as Snowflake or Google BigQuery offers powerful analytical capabilities. However, Kloud Kart's immediate problem is reporting pressure on an existing MySQL database, not an inability to perform advanced analysis across many data sources.

| Consideration | MySQL read replica | Snowflake / BigQuery |
|---|---|---|
| Primary purpose | Separates reporting reads from live operations | Provides a separate analytical data platform |
| Initial complexity | Lower; extends existing MySQL infrastructure | Higher; requires data integration, configuration and platform management |
| Cost areas | Additional server, storage, backups, monitoring and maintenance | Storage, compute or query usage, data movement, integration and administration |
| Skills | Builds on existing MySQL knowledge, supported by a Data Engineer | Requires additional cloud data-platform skills |
| Current suitability | Directly addresses the immediate reporting-performance issue | Provides broader capabilities than the immediate requirements demand |

**Financial justification:** A read replica is expected to have a lower initial implementation and operating burden because it extends the existing MySQL environment instead of introducing a separate analytical platform.

This is a proportionate starting point, not a claim that a read replica will always be cheaper. Actual costs must be compared using supplier quotations.

Finance should evaluate:

- **Read replica:** Server or hosting + storage + backups + monitoring + maintenance.
- **Cloud warehouse:** Storage + compute or query usage + data movement + integration + administration and support.

The company should obtain comparable quotations before approving the final infrastructure budget.

A warehouse should be reconsidered if Kloud Kart begins combining multiple data sources, needs more complex analytics, experiences growing analytical workloads or reaches the limits of the reporting replica.

## 3. Reporting and Data Quality

Introduce a standard daily reporting process using the second server.

The process should include:

1. Agree on definitions for key business measures such as orders, revenue and sales.
2. Document the source and calculation method for each measure.
3. Schedule daily reporting refreshes.
4. Check for missing, duplicate or inconsistent records.
5. Compare Operations and Finance figures using the same reporting definitions.
6. Record unexplained differences and assign responsibility for resolving them.

The Monday management report should use agreed figures rather than relying on separate manual calculations.

The reporting process should also record refresh times and failed jobs so that Nana can identify when information is incomplete or delayed.

## 4. Customer-Data Management and Protection

Kloud Kart should establish a central register of customer-data exports.

The register should record:
- Who exported the information.
- Why it was exported.
- The date of export.
- Where the copy is stored.
- Who can access it.
- Its retention or review date.

The company should also introduce a documented process for customer-data requests. Each request should have an assigned owner, verification record, systems checked, decision, actions taken and completion evidence.

This process should be reviewed against Ghana's Data Protection Act, 2012 (Act 843), with appropriate legal or privacy advice. The Nigeria pilot should also trigger a review of relevant cross-border data flows and applicable obligations.

Not every deletion request should automatically result in every record being erased. Requests must be assessed against applicable data-protection rights and lawful retention requirements.

## 5. People and Responsibilities

The board has approved a limit of two additional data hires. I recommend the following roles:

| Role | Main responsibilities | Why the role is needed |
|---|---|---|
| Data Engineer | Set up and maintain the read replica, manage data movement, monitor performance, backups and technical reliability. | Provides dedicated ownership of the data infrastructure and reduces dependence on the existing developer. |
| BI and Data Governance Analyst | Build reports, define business measures, perform data-quality checks, document reporting processes and support customer-data governance. | Improves reporting consistency, business understanding and accountability for data management. |

The Data Engineer should be recruited first because the reporting environment needs to be established before it can be used reliably. The second role should follow as the reporting and governance processes are introduced.

## 6. Cost, Risks and Controls

Actual GHS costs cannot be confirmed without infrastructure quotations, salary estimates and operational records. The following cost areas should be included in the budget.

| Cost area | What must be priced |
|---|---|
| Infrastructure | Second server or hosting, storage and any required network capacity |
| Reliability | Backups, monitoring, recovery testing and maintenance |
| Staffing | Recruitment and employment costs for both specialists |
| Governance | Staff time, privacy advice and customer-data process reviews |
| Reporting | Initial setup, report development and ongoing support |

### Main implementation risks

| Risk | Control |
|---|---|
| Replication delay or failure | Monitor replication health, display refresh times and investigate failed updates. |
| Second server becomes overloaded | Monitor capacity and review workloads as data volumes grow. |
| Reports still use inconsistent definitions | Maintain an approved metric dictionary and reconciliation process. |
| Customer-data copies remain untracked | Maintain an export register and review access and retention regularly. |
| New responsibilities overwhelm the small team | Assign clear ownership and recruit the two recommended specialists. |

The financial benefits should be measured against an initial baseline. Relevant measures include website performance during reporting, staff time spent preparing Monday reports, reporting discrepancies and successful handling of customer-data requests.

## 7. Decision and Review Conditions

I recommend that the board:

1. Approve a second MySQL server for reporting, subject to supplier quotations and technical assessment.
2. Keep live stock availability and normal transactions on the operational database.
3. Approve recruitment of a Data Engineer and a BI and Data Governance Analyst.
4. Introduce daily reporting, shared business definitions and data-quality checks.
5. Establish customer-data export tracking and a documented request-handling process.
6. Review progress and infrastructure requirements monthly.

The company should reconsider a full data warehouse when the current architecture can no longer support its reporting requirements, when additional data sources need to be combined or when more advanced analytics becomes a clear business requirement.

## Final Decision

Kloud Kart should begin with a MySQL read replica, daily reporting, stronger customer-data controls and two dedicated data specialists.

This approach addresses the immediate business risks while keeping initial complexity and investment proportionate to the company's current size and capabilities. It also provides a clear path to more advanced data infrastructure when business needs justify it.