# Kloud Kart – Situation Diagnosis

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** Abigail Arthur  
**Date:** 13 November 2026

## 1. Executive Summary

Kloud Kart's main challenge is not a lack of advanced technology. It is the absence of a reliable, controlled process for managing, reporting and protecting business data.

The company currently uses one MySQL database for orders, inventory, customer accounts and reporting activities. Reporting exports have slowed the live website twice in the past month. Operations and Finance also produce different figures, while Nana manually prepares the Monday management report.

In addition, Marketing manages a customer list of approximately 300,000 people, but exported copies are not centrally tracked. The company also needs a documented process for handling customer-data requests and demonstrating what action has been taken.

These issues create operational, financial, reporting and data-protection risks. The immediate priority should be to protect the live system, improve reporting consistency and establish better customer-data controls before investing in a complex data platform.

## 2. Business Context

| Area | Current position |
|---|---|
| Business | Three-year-old e-commerce company based in Accra, Ghana |
| Daily operations | Approximately 4,000 orders per day |
| Database | MySQL, approximately 40 GB |
| Database usage | Orders, inventory, customer accounts and reporting |
| Reporting | Monday CSV exports containing a few hundred thousand rows |
| Marketing data | Customer list of approximately 300,000 people |
| Growth | Approximately 15–20% year-on-year |
| Expansion | Nigeria pilot |
| Technical team | One PHP/MySQL developer; no dedicated data engineer or professional Python operator |
| Hiring limit | Two additional data hires |
| Infrastructure constraint | Live MySQL database must remain operational; a second server/read replica is pre-approved |
| Data freshness | Stock information must remain current; other reporting can refresh daily |

## 3. Root Causes, Risk Ranking and Cost Assessment

The following assessment ranks the issues by their potential effect on business operations, customer trust and management decisions.

Cost estimates are expressed as measurable impacts and calculation methods where actual financial information was not supplied. They are not confirmed financial losses.

| ID | Root cause and business impact | Risk ranking | Cost or impact estimate |
|---|---|---|---|
| F-01 | **Shared production database:** The live website and reporting activities use the same MySQL database. Reporting exports have slowed the website twice in the past month, creating a risk of delayed orders and poor customer experience. | Critical | Approximately 4,000 orders are processed daily. Revenue exposure can be estimated as affected orders × average order value. Actual lost revenue requires incident duration, affected-order records and evidence of cancelled or permanently lost orders. |
| F-02 | **Inconsistent reporting definitions and manual reconciliation:** Operations and Finance produce different figures, while Nana manually rebuilds the Monday report. | High | Planning assumption: two staff members spending three hours each per week on reconciliation would use 312 staff-hours annually (2 × 3 × 52). Labour cost = 312 × average loaded hourly staff cost. Actual time spent must be measured. |
| F-03 | **Untracked customer-data exports:** Marketing manages approximately 300,000 customer records, but the company does not have a central record of exported copies, their locations or access. | Critical | Exposure includes time spent identifying copies, reviewing access, responding to requests and correcting unauthorised or unnecessary retention. Estimated cost = staff hours × loaded hourly cost, plus technical and legal support where required. The number of copies is unknown. |
| F-04 | **No evidenced end-to-end customer-data request process:** The company needs to locate customer information, assign responsibility, document decisions and retain evidence of actions taken. | Critical | The brief identifies a 90-day period for responding to a Data Protection Commission complaint. Poor records could increase investigation, legal and remediation costs. Actual exposure requires a review of current processes and records. |
| F-05 | **Limited internal data-management capacity:** The company relies on one PHP/MySQL developer and has no dedicated data engineer or governance specialist. | High | Additional work may delay website development and reporting improvements or require external support. Estimate the impact using additional staff or contractor hours × their loaded hourly rate. |

### 3.1 Costing assumptions and limitations

The available information does not support a reliable total GHS cost for these problems. No supplier quotations, salary figures, incident logs, average order values, contribution margins or actual staff time records were provided.

The following methods should be used to establish the actual financial impact:

- **Website slowdowns:** Identify affected orders, incident duration, cancelled orders and average contribution margin. Distinguish delayed orders from permanently lost sales.
- **Manual reporting:** Record the time each person spends exporting, cleaning, comparing and preparing reports. Multiply the total hours by the relevant loaded hourly cost.
- **Customer-data management:** Record the number of exported copies, investigation hours, access reviews and request-handling effort.
- **Technical capacity:** Track developer time diverted from core website work and any external support required.
- **Infrastructure:** Obtain supplier quotations for the second server, storage, backups, monitoring and maintenance.

These methods provide a baseline for comparing the cost of the recommended solution with the cost of continuing the current approach.

## 4. Detailed Findings

### F-01: Reporting activities threaten live website performance

**What is happening**

Orders, inventory and customer accounts are stored in the same MySQL database that supports the live website. Large reporting exports are also taken from this environment.

The brief confirms that these exports have slowed the website twice in the past month.

**Root cause**

Reporting workloads compete with normal website operations for database resources. There is no separate reporting environment to absorb this workload.

**Business impact**

- Customers may experience delays when placing orders.
- Website performance may deteriorate during large exports.
- The developer may spend time investigating performance problems instead of improving the platform.
- Continued growth of 15–20% annually could increase pressure on the current setup.

**Recommended direction**

Introduce a MySQL read replica on a second server. Use it for reporting queries and exports while keeping normal transactions on the main database.

### F-02: Operations and Finance do not have a consistent reporting process

**What is happening**

Operations and Finance produce different figures. Nana then rebuilds the Monday management report from CSV exports.

**Root cause**

There is no confirmed shared definition of key business measures, standard reporting process or documented reconciliation and sign-off procedure.

**Business impact**

- Management may make decisions using inconsistent figures.
- Staff spend time investigating differences.
- Reporting becomes dependent on manual work.
- It becomes difficult to identify who is responsible for resolving discrepancies.

**Recommended direction**

Introduce a shared metric dictionary, standard daily reporting process, data-quality checks and a weekly reconciliation and sign-off process.

### F-03: Customer-data copies are not centrally controlled

**What is happening**

Marketing manages a customer list of approximately 300,000 people. The brief states that exported copies are not properly tracked.

**Root cause**

There is no evidenced central export register showing who exported customer information, why it was exported, where it was stored, who can access it and when it should be reviewed or deleted.

**Business impact**

- Customer information may remain in unnecessary or forgotten copies.
- It may be difficult to locate all relevant records when a customer makes a request.
- The company may struggle to demonstrate responsible handling of personal information.
- Expansion into Nigeria may introduce additional data-handling and cross-border considerations.

**Recommended direction**

Create a customer-data export register, assign ownership, review access and establish retention and deletion procedures. Obtain appropriate privacy advice before expanding customer-data processing into Nigeria.

### F-04: Customer-data requests need a documented process

**What is happening**

The brief identifies a 90-day period for responding to a Data Protection Commission complaint about deleted customer data.

However, the available information does not confirm whether Kloud Kart has a documented process for receiving, verifying, investigating, completing and recording customer-data requests.

**Root cause**

Responsibility, request tracking, evidence retention and coordination across systems and exported copies have not been demonstrated.

**Business impact**

- Requests may be delayed or overlooked.
- Staff may be unable to confirm where customer information is held.
- The company may struggle to provide evidence of actions taken.
- Poor handling may result in regulatory and reputational exposure.

**Recommended direction**

Introduce a request register that records the request, verification, assigned owner, systems checked, decision, actions taken and completion evidence. The process should be reviewed against Ghana's Data Protection Act, 2012 (Act 843), with legal or privacy advice where necessary.

A deletion request should be assessed against applicable legal obligations and retention requirements rather than treated as an automatic instruction to remove every record.

### F-05: The current team has limited capacity for additional data responsibilities

**What is happening**

Kloud Kart has one PHP/MySQL developer and no dedicated data engineer or professional Python operator.

**Root cause**

Data infrastructure, reporting, data quality and governance responsibilities do not have dedicated owners.

**Business impact**

- Important data-management work may compete with website development.
- There is limited capacity to monitor a second server and maintain reliable data movement.
- Reporting and governance improvements may not be sustained.
- Expansion may increase pressure on the existing developer.

**Recommended direction**

Use the two available hires for complementary responsibilities:

1. **Data Engineer:** Responsible for database infrastructure, the read replica, data movement, backups, monitoring and technical reliability.
2. **BI and Data Governance Analyst:** Responsible for reporting, business definitions, data-quality checks, documentation and customer-data management processes.

## 5. Reconciliation Assessment

Reconciliation means comparing information from different sources to determine whether the figures agree and investigating any differences.

The brief confirms that Operations and Finance produce different figures. However, the actual database exports and reports were not supplied.

Therefore, reconciliation was not performed. Actual row counts, differences and financial variances could not be calculated or verified.

This is an important evidence limitation. Kloud Kart should begin by collecting the relevant Operations and Finance reports, agreeing on reporting periods and metric definitions, and comparing the figures using a consistent process.

The proposed Monday Reporting Reconciliation and Sign-off Template provides a starting point for this process.

## 6. What May Look Like a Problem but Is Not Necessarily One

Some observations should not automatically lead to unnecessary investment.

| Observation | Diagnosis |
|---|---|
| The company wants real-time analytics. | Not every business measure needs real-time updates. Stock availability requires current information, while most management reports can refresh daily. |
| The database is approximately 40 GB. | Database size alone does not justify a data warehouse. Performance, workload, data sources and analytical requirements should determine the architecture. |
| The company has approximately 300,000 customer records. | The size of the list is not itself evidence of poor data quality or non-compliance. The main concern is whether copies, access, retention and requests are properly controlled. |
| The company is expanding into Nigeria. | Expansion does not automatically require a new data platform. Data flows, applicable legal obligations and operational needs should be assessed before deciding on additional infrastructure. |

## 7. Evidence Gaps: What Could Not Be Verified

The following items require further investigation before final financial or technical conclusions can be made.

| Area | Information unavailable | Evidence needed |
|---|---|---|
| Database performance | CPU, memory, query performance, connection usage and database health | MySQL monitoring, query logs and server metrics |
| Website slowdowns | Duration, affected orders and actual financial losses | Incident records, website logs and order records |
| Reporting differences | Exact differences between Operations and Finance figures | Original CSV exports and reports from both teams |
| Data quality | Duplicate, missing or invalid records | Data profiling and quality checks |
| Customer-data exports | Number, location, ownership and access to exported copies | Export register, storage review and access records |
| Customer-data requests | Existing workflow and evidence of completed requests | Request records, policies and system audit trails |
| Infrastructure costs | Actual cost of a second server and supporting services | Supplier quotations |
| Staffing costs | Recruitment and employment costs for the proposed hires | Salary benchmarks and recruitment estimates |
| Nigeria expansion | Data flows, storage locations and applicable privacy requirements | Business process review and appropriate legal advice |

No unverified figure has been presented as an established business fact.

## 8. Priority Actions

| Priority | Action | Expected business outcome |
|---|---|---|
| 1 – Immediate | Assess database performance and establish a second server for reporting | Reduce reporting pressure on the live website |
| 2 – High | Agree on reporting definitions and introduce reconciliation and quality checks | Improve consistency between Operations and Finance |
| 3 – High | Inventory customer-data exports and establish request-handling procedures | Improve visibility, accountability and protection of customer information |
| 4 – High | Recruit a Data Engineer and a BI and Data Governance Analyst | Establish clear technical and reporting ownership |
| 5 – Medium | Review reporting performance, data growth and Nigeria data flows | Determine when additional platform investment is justified |

## 9. Questions for Further Investigation

The following questions should be addressed during implementation:

1. Which specific reports and database queries caused the two website slowdowns?
2. How long did each slowdown last, and how many orders were affected?
3. Which business measures differ between Operations and Finance, and what definitions does each team currently use?
4. How much staff time is spent preparing the Monday report?
5. How many customer-data exports exist, where are they stored and who can access them?
6. What process currently handles customer requests involving access, correction or deletion of personal information?
7. What are the actual costs of the proposed second server, backups, storage and monitoring?
8. What customer-data flows and privacy obligations will arise from the Nigeria pilot?

## 10. Overall Diagnosis

Kloud Kart's immediate challenge is a combination of shared database workloads, inconsistent reporting practices, untracked customer-data exports and limited internal data-management capacity.

The company should not begin with a complex data warehouse or a full real-time analytics platform. Its immediate needs can be addressed more proportionately by separating reporting from the live database, introducing daily reporting and reconciliation controls, strengthening customer-data management and recruiting two complementary data specialists.

This approach protects the existing business while creating a foundation that can support future growth.

**Evidence position:** Findings are based on the supplied project brief. Financial exposure figures are estimates or calculation methods, not verified losses. Further technical, financial and data-protection evidence is required before final costs and compliance conclusions can be confirmed.