# Situation Diagnosis-Kloud Kart


Kloud Kart's main problem is not a lack of advanced technology. It is the lack of a controlled process for collecting, protecting, reconciling and reporting business data.

Three issues need urgent attention:

1. Reporting extracts are slowing the live website because reporting and customer transactions use the same database server.
2. Operations and Finance produce different figures because reporting is manual and shared definitions are not established.
3. Customer information is copied into marketing lists without a clear record of where copies are stored, who controls them or when they should be deleted.

The company also needs a documented process for handling customer deletion requests under Ghana's Data Protection Act, 2012 (Act 843).

The recommended first step is to protect the live database, establish trusted daily reporting and introduce proper customer-data controls. A large analytics platform and general real-time reporting are not immediate priorities.

## Reconciliation

No actual reconciliation was performed because the company did not provide database exports or report files.

1. **Source database**
   - Rows: Not verified
   - Delta: Not calculated
   - Reason: No database export supplied.

2. **Reporting extract**
   - Rows: Not verified
   - Delta: Not calculated
   - Reason: No reporting extract supplied.

3. **Operations report**
   - Rows: Not verified
   - Delta: Not calculated
   - Reason: No Operations report supplied.

4. **Finance report**
   - Rows: Not verified
   - Delta: Not calculated
   - Reason: No Finance report supplied.

**Reconciliation status:** Not performed. The brief confirms that Operations and Finance report different figures, but it does not provide the underlying records needed to calculate the difference.

## Findings, ranked by risk

### F-01: Reporting affects the live website — Severity: Critical

- **What it is:** The live website and reporting activities use the same MySQL server. Large exports have slowed the website twice in the past month.
- **How I detected it:** The company brief confirms that orders, inventory and customer accounts share one database server. It also reports two incidents involving slow exports.
- **Scale:** Approximately 4,000 orders per day and a database of about 40 GB. The company is growing by 15–20% annually.
- **Effect on the client's number:** Slow reporting queries compete with customer transactions for server resources. This can delay orders, affect customer experience and reduce the reliability of business operations. The number of lost orders or amount of lost revenue is not known.
- **Cost exposure:** If the website is affected, the financial exposure depends on the duration of the slowdown, the number of customers affected, conversion rates and average order value. These figures were not supplied. The business should measure incident duration and affected orders before assigning a monetary loss.
- **What I did about it:** Recommend a second server, using a read replica for reporting. Reporting extracts should run against the replica rather than the live database. Monitor replication delays and server capacity.
- **Residual risk:** The second server introduces additional hosting, storage, backup and monitoring costs. Poor configuration or replication delays could still affect reporting accuracy.

### F-02: Operations and Finance report different figures — Severity: High

- **What it is:** Nana manually rebuilds the Monday figures, while Finance produces a different spreadsheet.
- **How I detected it:** The brief explicitly identifies differences between Operations and Finance reports.
- **Scale:** The exact number of affected reports, transactions and disputed figures is unknown.
- **Effect on the client's number:** Management may make decisions using different versions of revenue, orders or other business measures. This reduces confidence in board reports and makes performance comparisons unreliable.
- **Cost exposure:** Staff time is spent rebuilding, checking and explaining reports. A useful annual estimate is:

  `People involved × hours spent per week × 52 × hourly staff cost`

  For illustration only, two people spending three hours each week would use 312 staff-hours per year. This is not a confirmed Kloud Kart figure; actual staff time must be measured.
- **What I did about it:** Recommend a shared list of business measures, agreed calculation rules and one daily reporting process used by both departments.
- **Residual risk:** Shared reports will not solve disagreements unless each measure has an agreed definition and a named owner.

### F-03: Customer information is copied without clear control — Severity: Critical

- **What it is:** Marketing exports customer lists, but copies are not properly tracked.
- **How I detected it:** The brief identifies a marketing list of approximately 300,000 people and says copies are not tracked.
- **Scale:** Approximately 300,000 people may be represented in the marketing list. The number of copies, storage locations, users and external recipients is unknown.
- **Effect on the client's number:** Uncontrolled copies can lead to inaccurate customer records, unwanted contact, unauthorised access and difficulty responding to deletion requests.
- **Cost exposure:** Exposure includes investigation time, corrective work, possible legal and regulatory costs, and damage to customer trust. The actual financial impact cannot be calculated without knowing the number and location of copies, access arrangements and any incidents.
- **What I did about it:** Recommend an inventory of customer-data copies, named owners, approved access, a record of exports and a retention schedule. New exports should have a business purpose and an expiry or review date.
- **Residual risk:** Existing copies may remain undiscovered. A register must be maintained and checked regularly.

### F-04: Customer deletion requests are not evidenced — Severity: Critical

- **What it is:** The brief does not demonstrate a complete process for finding and handling customer deletion requests across the company's systems and exported copies.
- **How I detected it:** The company must respond to a Data Protection Commission complaint within 90 days, but no documented deletion workflow or evidence of testing was provided.
- **Scale:** The number of outstanding requests and the number of systems or copies containing customer information are unknown.
- **Effect on the client's number:** If a request cannot be traced and handled properly, the company may be unable to demonstrate that it has followed its data-protection responsibilities. Deleting a record from one location may leave other copies untouched.
- **Cost exposure:** The company may incur investigation, legal advice, corrective-action and regulatory-response costs. The amount depends on the circumstances and cannot be estimated from the brief alone.
- **What I did about it:** Recommend a tracked request process recording the date received, identity checks, responsible owner, systems and copies checked, actions taken, completion evidence and any lawful reason for retaining information. Obtain a Ghana privacy-law review before approving the process.
- **Residual risk:** A tracker does not itself delete information or prove legal compliance. The company must identify all relevant systems, processors, backups and retention obligations.

### F-05: Data responsibilities are unclear — Severity: High

- **What it is:** Reporting depends heavily on Nana and one PHP/MySQL developer, with no dedicated data engineering or reporting role.
- **How I detected it:** The brief describes Nana manually rebuilding reports and confirms that the company has no professional data engineer or warehouse operator.
- **Scale:** The company handles approximately 4,000 orders per day and is preparing to expand into Nigeria, while having a budget for only two data hires.
- **Effect on the client's number:** Important processes depend on individual knowledge. This increases the chance of delays, inconsistent calculations and undocumented changes.
- **Cost exposure:** Time spent manually preparing reports and correcting errors reduces the time available for operational work. The business also faces delays when only one person understands a critical process. Staff time and the cost of delayed decisions should be measured.
- **What I did about it:** Recommend hiring a Data Engineer first to protect and organise data flows, followed by a BI and Data Governance Analyst to improve reporting, definitions and customer-data controls.
- **Residual risk:** Two hires cannot immediately cover every data responsibility. Department heads must still own their business measures and processes.

## Looked wrong, is not wrong

| Apparent problem | Why it looks wrong | Why it is actually fine |
|---|---|---|
| Not every dashboard updates in real time | The board has asked for real-time analytics | Only stock counts must not become stale. Daily updates are acceptable for other reporting under the brief. |
| Stock remains in the live operational database | It is not part of a separate analytics platform | Live stock availability must reflect current transactions. A daily reporting copy is not suitable for customer-facing stock availability. |
| The database is only about 40 GB | It may seem too small to justify a separate reporting environment | Database size alone does not determine the architecture. The confirmed production impact of reporting is the stronger reason for separating reporting workloads. |
| Marketing has a list of 300,000 customers | A large list may appear to indicate a data-quality problem | List size alone does not prove poor quality. The actual issue is the lack of control over copies, access, purpose and retention. |
| The company has no machine-learning forecasting system | Forecasting may seem necessary for a growing retailer | Forecasting should follow reliable sales and inventory records. Building it before fixing data quality could produce misleading predictions. |

## Could not verify

The following items require evidence before the company can claim that its data environment is reliable or compliant:

- **Database health:** MySQL version, server capacity, storage growth, query performance, backups, recovery tests and current access permissions.
- **Reporting differences:** Actual Operations and Finance reports, metric definitions, source queries and the size of their differences.
- **Data quality:** Duplicate orders, missing values, invalid customer details, cancelled orders and inconsistent product or inventory records.
- **Customer-data copies:** Where the marketing lists are stored, who can access them, who receives them and whether old copies are deleted.
- **Deletion process:** Whether requests are logged, verified, assigned, completed and checked across systems and external processors.
- **Legal compliance:** Current registration and compliance position, privacy notices, lawful processing arrangements, processor contracts and the responsibilities of the relevant privacy officer or supervisor. These require review by a qualified Ghanaian privacy professional.
- **Nigeria expansion:** Whether the pilot involves transferring or processing personal data across borders and what additional requirements apply.
- **Financial impact:** Average order value, gross margin, website incident duration, affected orders, staff time spent on reporting and the cost of the proposed second server.

### Questions I would ask Nana

Nana is unavailable for follow-up, so these questions remain open for the next discovery session:

1. Which figures differ most often between Operations and Finance?
2. How long does the Monday report take to prepare, check and correct?
3. How long did the two website slowdowns last, and were customers unable to complete orders?
4. Where are marketing customer lists stored, and who receives them?
5. Who currently receives and handles customer deletion requests?
6. Which business reports must be ready before Monday management meetings?

**Overall conclusion:** Kloud Kart should first protect its live website, establish consistent daily reporting and control customer information. These steps address confirmed business problems without introducing the cost and complexity of a large analytics platform before the company is ready.