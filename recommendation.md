# Data Strategy Recommendation – Kloud Kart

**Prepared for:** Kloud Kart Leadership Team  
**Date:** 12 November 2026

## 1. Executive Recommendation

Kloud Kart should first protect its live website, establish reliable business reporting and improve customer data controls.

I recommend introducing a second server with a read replica of the existing MySQL database. Reporting activities will run against this copy instead of competing with live customer transactions.

General business reporting should use daily batch processing. Stock availability must remain live because outdated stock counts could cause overselling.

A full data warehouse, data lake or lakehouse is not necessary at this stage. The immediate problems can be addressed with a simpler solution that fits the company's current team, budget and technical capacity.

## 2. Proposed Architecture

The recommended arrangement is:

1. The existing MySQL database continues to support website orders, customers and inventory.
2. A second server receives a read-only copy of the database.
3. Scheduled reporting processes use the second server to prepare business reports.
4. Operations and Finance use shared reporting definitions and outputs.
5. Nana receives consistent management reports.

The website must continue checking live inventory against the operational database. Stock availability must not depend on the daily reporting copy.

### Why this architecture?

| Option | Advantage | Why it is not the first choice |
|---|---|---|
| Read replica with reporting | Uses existing MySQL knowledge and separates reporting workloads from live transactions | Requires a second server and monitoring |
| Data warehouse | Provides structured reporting and supports advanced analysis | Adds cost and maintenance before reporting processes are trusted |
| Data lake | Stores large amounts of raw data for future analysis | Current needs do not justify the additional storage and management |
| Lakehouse | Supports structured and flexible analytical workloads | Adds complexity and requires skills the current team lacks |

The read replica is a practical first step, not a permanent limit. A larger platform should be considered when actual reporting needs exceed its capabilities.

## 3. Processing Recommendation

**Daily batch processing for general reporting**

Daily updates are sufficient for sales summaries, revenue reports, marketing performance and management dashboards. These reports do not require every transaction to appear immediately.

**Live processing for stock availability**

Stock counts must reflect current transactions to prevent overselling. The website should continue using the live operational inventory data.

I do not recommend streaming every business activity simply because investors have requested real-time analytics. It adds monitoring and operating costs without a demonstrated need.

I would reconsider this decision if evidence shows that delayed information is causing measurable financial or operational harm.

## 4. Hiring Plan

Kloud Kart has funding for two data hires. The recommended order is:

### First: Data Engineer

**First 90 days:**
- Assess the current database and reporting workload.
- Set up the second server and read replica.
- Move reporting queries away from the live database.
- Establish replication monitoring, backups and recovery procedures.
- Introduce the first scheduled reporting process.

**Expected outcome:** Reporting runs separately from the live website database, with monitoring to detect delays and failures.

### Second: BI and Data Governance Analyst

**First 90 days after appointment:**
- Agree on shared definitions for business measures.
- Reconcile Operations and Finance reports.
- Establish consistent management reports.
- Introduce data-quality checks.
- Document customer-data exports, access and ownership.
- Coordinate a documented customer request and deletion process.

**Expected outcome:** Nana receives consistent reports, and the company has clearer responsibility for customer information.

The existing PHP/MySQL developer should support website integration, but should not carry sole responsibility for data operations.

## 5. Running Costs

Exact prices cannot be established without server specifications, supplier quotations and salary information. The company should obtain quotations before approving the operating budget.

| Cost area | What the company must budget for |
|---|---|
| Second server | Computing capacity, memory and storage |
| Database storage | Replicated data and reporting tables |
| Backups and recovery | Backup storage and recovery testing |
| Monitoring | Server health, replication delays and failed reports |
| Staffing | Two data professionals |
| Privacy support | Qualified advice on customer data protection |

**Estimated monthly operating cost structure:**

Second server + storage + backups + monitoring + two salaries + privacy support.

The first investment should cover the second server and the two approved hires. Avoid committing to a larger analytics platform before there is evidence that it is necessary.

## 6. Risks and Safeguards

| Risk | Safeguard |
|---|---|
| Reporting server falls behind | Monitor replication delays and last successful refresh |
| Live website remains under pressure | Run reporting queries only against the second server |
| Departments report different figures | Maintain approved metric definitions |
| Customer data copies remain uncontrolled | Record exports, owners, access and retention dates |
| Deletion requests are missed | Track requests, deadlines, actions and completion evidence |
| Business growth exceeds capacity | Review performance and storage needs quarterly |

The customer-data process must be reviewed against Ghana's Data Protection Act, 2012 (Act 843), with qualified privacy guidance. A tracker alone does not establish compliance.

## 7. When to Reconsider the Recommendation

A larger warehouse or lakehouse should be considered when:
- The reporting server can no longer handle the workload.
- The business needs to combine data from several additional systems.
- Daily reporting no longer meets agreed business needs.
- Reliable historical data supports a clear demand-forecasting business case.

**Final position:** Protect the live website first, make business reporting consistent, and establish customer-data controls. Invest in more advanced analytics only when business evidence justifies the additional cost.