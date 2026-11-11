# Data Architecture Recommendation-Kloud Kart

**Prepared:** 11 November 2026  
**Prepared for:** Kloud Kart Leadership Team  
**Decision:** Protect the live database first, establish trusted daily reporting and defer a larger analytics platform.

## 1. Executive recommendation

Kloud Kart should begin with a second server that receives a read-only copy of the production database. Reporting and analytical queries will run against this copy instead of competing with customer transactions on the live server.

The company should use daily batch processing for general business reporting. Stock availability will remain connected to the live operational database because stock counts must not become stale.

I do not recommend building a large data warehouse, data lake or lakehouse immediately. The company needs reliable reporting and better data control before investing in a more complex platform.

This approach addresses the problems already affecting the business while keeping the initial design manageable for a small team.

## 2. Proposed architecture

### How data will flow

1. **Live operational database:** The existing database continues to support website orders, customer accounts and inventory transactions.
2. **Second server:** A read replica receives changes from the live database.
3. **Daily reporting process:** Scheduled jobs read the replica and prepare reporting tables.
4. **Shared reporting:** Operations and Finance use the same agreed measures and reporting tables.
5. **Management reports:** Nana receives a consistent daily reporting view and a Monday management report.

**Stock availability is an exception.** The website must continue checking current stock against the live operational data. It must not depend on a daily reporting copy.

### Architecture overview

```text
Customers and website
         |
         v
Production MySQL database
         |
         | Database replication
         v
Second server / Read replica
         |
         | Daily reporting process
         v
Shared reporting tables
         |
         +------------------+
         |                  |
         v                  v
    Operations           Finance
         |                  |
         +--------+---------+
                  |
                  v
           Management reports
```

The website continues to use the production database for transactions and current stock. Reporting workloads are moved away from that server.

## 3. Architecture options considered

| Option | Advantages | Disadvantages | Decision |
|---|---|---|---|
| Read replica with daily reporting | Uses existing database knowledge, protects live transactions and has a manageable starting cost | Requires a second server and replication monitoring | **Recommended now** |
| Full data warehouse | Provides a structured environment for business reporting and future analysis | Adds migration, hosting and maintenance costs before the company has established trusted reporting | Reconsider when reporting needs outgrow the initial setup |
| Data lake | Can store large volumes of raw and varied data for future analysis | More storage and data-management complexity than current needs justify | Defer |
| Lakehouse | Combines analytical reporting and flexible data storage | More complex to operate and requires skills the current team does not have | Defer |

A read replica is not a complete replacement for a future warehouse. It is the practical first step because Kloud Kart's immediate problem is the effect of reporting on its live database.

## 4. Processing recommendation: Batch versus streaming

**Use daily batch processing for general reporting.**

Daily batch processing means collecting and preparing data at scheduled times rather than processing every change immediately.

This is appropriate for:
- Daily sales summaries.
- Revenue and order reports.
- Marketing performance reports.
- Finance and Operations management reports.
- General business dashboards.

**Keep stock availability real time.**

Stock counts are different because a customer must not purchase an item that has already been sold. The website should continue using current operational inventory data.

I would not introduce streaming for every business measure. It would increase operating complexity and monitoring requirements without a confirmed business need.

I would reconsider streaming if the company demonstrates that a specific decision must be made within seconds or minutes and daily updates create measurable financial or operational harm.

## 5. Team and hiring plan

The company has budget for two data hires. I recommend hiring in this order.

### Hire 1: Data Engineer — First priority

The Data Engineer should:

- Assess the existing database and reporting workload.
- Set up and test the second server.
- Configure and monitor database replication.
- Move reporting extracts away from the production database.
- Build the daily reporting process.
- Establish backups, monitoring and recovery procedures.

**First 90-day outcome:** Reporting runs from the second server, production database pressure is measured, and replication health is monitored.

### Hire 2: BI and Data Governance Analyst — Second priority

This person should:

- Agree on common definitions for business measures.
- Reconcile Operations and Finance reports.
- Build shared management reports.
- Introduce data-quality checks.
- Maintain a register of customer-data exports and access.
- Coordinate the customer-data request and deletion process with the appropriate privacy lead.

**First 90-day outcome:** Operations and Finance use agreed reporting measures, Nana has a repeatable Monday report, and customer-data copies and responsibilities are documented.

The existing PHP/MySQL developer should support integration with the website, but should not become the only person responsible for the company's data operations.

## 6. Running-cost model

Exact costs cannot be confirmed because server specifications, hosting arrangements, staff salary expectations and supplier quotations were not supplied.

The company should budget for the following:

| Cost area | What drives the cost | Recommendation |
|---|---|---|
| Second server | Compute, memory, storage and network capacity | Obtain quotations based on a workload test |
| Database storage | Database copy, reporting tables and growth | Include capacity for 15–20% annual business growth |
| Backups and recovery | Backup storage and recovery testing | Include in the operating budget |
| Monitoring | Replication delays, server health and failed reporting jobs | Establish alerts and routine checks |
| Staff | Two data hires | Recruit the Data Engineer first |
| Privacy support | Review of customer-data processes and legal obligations | Obtain qualified Ghanaian privacy advice |
| Future analytics platform | Additional hosting, migration and support | Defer until a measured need exists |

**Monthly operating cost formula:**

`Second server + storage + backups + monitoring + staff costs + privacy support`

The first financial decision should be based on quotations for the second server and the cost of the two hires. Do not approve a larger platform until the company has evidence that the initial arrangement cannot meet its reporting needs.

## 7. Risks and safeguards

| Risk | Safeguard |
|---|---|
| Reporting replica falls behind | Monitor replication delay and show the last successful refresh time |
| Reporting still affects production | Test capacity and run reporting workloads only against the replica |
| Different departments calculate measures differently | Maintain one approved definition for each shared measure |
| Customer information remains in old exports | Maintain an export register, access controls and retention rules |
| Deletion requests are missed | Track requests, owners, deadlines and completion evidence |
| Business growth exceeds current capacity | Review server capacity and reporting performance quarterly |

The company should also review its obligations under Ghana's Data Protection Act, 2012 (Act 843), including its customer-data handling and deletion procedures, with a qualified privacy professional.

## 8. When should the company invest in a larger platform?

Reconsider a warehouse or lakehouse when one or more of these conditions is demonstrated:

- The read replica can no longer support reporting workloads reliably.
- Reporting requires combining several additional business systems.
- Daily reporting no longer meets agreed business requirements.
- Data volume and analytical workloads exceed the capacity of the current arrangement.
- Forecasting and advanced analytics have a clear business case and reliable historical data.

**Final position:** Protect the live website, establish consistent daily reporting and control customer information before investing in advanced analytics. This is the most practical starting point for Kloud Kart's current size, team and budget.# Data Architecture Recommendation — Kloud Kart

**Prepared:** 11 November 2026  
**Prepared for:** Kloud Kart Leadership Team  
**Decision:** Protect the live database first, establish trusted daily reporting and defer a larger analytics platform.

## 1. Executive recommendation

Kloud Kart should begin with a second server that receives a read-only copy of the production database. Reporting and analytical queries will run against this copy instead of competing with customer transactions on the live server.

The company should use daily batch processing for general business reporting. Stock availability will remain connected to the live operational database because stock counts must not become stale.

I do not recommend building a large data warehouse, data lake or lakehouse immediately. The company needs reliable reporting and better data control before investing in a more complex platform.

This approach addresses the problems already affecting the business while keeping the initial design manageable for a small team.

## 2. Proposed architecture

### How data will flow

1. **Live operational database:** The existing database continues to support website orders, customer accounts and inventory transactions.
2. **Second server:** A read replica receives changes from the live database.
3. **Daily reporting process:** Scheduled jobs read the replica and prepare reporting tables.
4. **Shared reporting:** Operations and Finance use the same agreed measures and reporting tables.
5. **Management reports:** Nana receives a consistent daily reporting view and a Monday management report.

**Stock availability is an exception.** The website must continue checking current stock against the live operational data. It must not depend on a daily reporting copy.

### Architecture overview

```text
Customers and website
         |
         v
Production MySQL database
         |
         | Database replication
         v
Second server / Read replica
         |
         | Daily reporting process
         v
Shared reporting tables
         |
         +------------------+
         |                  |
         v                  v
    Operations           Finance
         |                  |
         +--------+---------+
                  |
                  v
           Management reports
```

The website continues to use the production database for transactions and current stock. Reporting workloads are moved away from that server.

## 3. Architecture options considered

| Option | Advantages | Disadvantages | Decision |
|---|---|---|---|
| Read replica with daily reporting | Uses existing database knowledge, protects live transactions and has a manageable starting cost | Requires a second server and replication monitoring | **Recommended now** |
| Full data warehouse | Provides a structured environment for business reporting and future analysis | Adds migration, hosting and maintenance costs before the company has established trusted reporting | Reconsider when reporting needs outgrow the initial setup |
| Data lake | Can store large volumes of raw and varied data for future analysis | More storage and data-management complexity than current needs justify | Defer |
| Lakehouse | Combines analytical reporting and flexible data storage | More complex to operate and requires skills the current team does not have | Defer |

A read replica is not a complete replacement for a future warehouse. It is the practical first step because Kloud Kart's immediate problem is the effect of reporting on its live database.

## 4. Processing recommendation: Batch versus streaming

**Use daily batch processing for general reporting.**

Daily batch processing means collecting and preparing data at scheduled times rather than processing every change immediately.

This is appropriate for:
- Daily sales summaries.
- Revenue and order reports.
- Marketing performance reports.
- Finance and Operations management reports.
- General business dashboards.

**Keep stock availability real time.**

Stock counts are different because a customer must not purchase an item that has already been sold. The website should continue using current operational inventory data.

I would not introduce streaming for every business measure. It would increase operating complexity and monitoring requirements without a confirmed business need.

I would reconsider streaming if the company demonstrates that a specific decision must be made within seconds or minutes and daily updates create measurable financial or operational harm.

## 5. Team and hiring plan

The company has budget for two data hires. I recommend hiring in this order.

### Hire 1: Data Engineer — First priority

The Data Engineer should:

- Assess the existing database and reporting workload.
- Set up and test the second server.
- Configure and monitor database replication.
- Move reporting extracts away from the production database.
- Build the daily reporting process.
- Establish backups, monitoring and recovery procedures.

**First 90-day outcome:** Reporting runs from the second server, production database pressure is measured, and replication health is monitored.

### Hire 2: BI and Data Governance Analyst — Second priority

This person should:

- Agree on common definitions for business measures.
- Reconcile Operations and Finance reports.
- Build shared management reports.
- Introduce data-quality checks.
- Maintain a register of customer-data exports and access.
- Coordinate the customer-data request and deletion process with the appropriate privacy lead.

**First 90-day outcome:** Operations and Finance use agreed reporting measures, Nana has a repeatable Monday report, and customer-data copies and responsibilities are documented.

The existing PHP/MySQL developer should support integration with the website, but should not become the only person responsible for the company's data operations.

## 6. Running-cost model

Exact costs cannot be confirmed because server specifications, hosting arrangements, staff salary expectations and supplier quotations were not supplied.

The company should budget for the following:

| Cost area | What drives the cost | Recommendation |
|---|---|---|
| Second server | Compute, memory, storage and network capacity | Obtain quotations based on a workload test |
| Database storage | Database copy, reporting tables and growth | Include capacity for 15–20% annual business growth |
| Backups and recovery | Backup storage and recovery testing | Include in the operating budget |
| Monitoring | Replication delays, server health and failed reporting jobs | Establish alerts and routine checks |
| Staff | Two data hires | Recruit the Data Engineer first |
| Privacy support | Review of customer-data processes and legal obligations | Obtain qualified Ghanaian privacy advice |
| Future analytics platform | Additional hosting, migration and support | Defer until a measured need exists |

**Monthly operating cost formula:**

`Second server + storage + backups + monitoring + staff costs + privacy support`

The first financial decision should be based on quotations for the second server and the cost of the two hires. Do not approve a larger platform until the company has evidence that the initial arrangement cannot meet its reporting needs.

## 7. Risks and safeguards

| Risk | Safeguard |
|---|---|
| Reporting replica falls behind | Monitor replication delay and show the last successful refresh time |
| Reporting still affects production | Test capacity and run reporting workloads only against the replica |
| Different departments calculate measures differently | Maintain one approved definition for each shared measure |
| Customer information remains in old exports | Maintain an export register, access controls and retention rules |# Data Architecture Recommendation — Kloud Kart

**Prepared:** 11 November 2026  
**Prepared for:** Kloud Kart Leadership Team  
**Decision:** Protect the live database first, establish trusted daily reporting and defer a larger analytics platform.

## 1. Executive recommendation

Kloud Kart should begin with a second server that receives a read-only copy of the production database. Reporting and analytical queries will run against this copy instead of competing with customer transactions on the live server.

The company should use daily batch processing for general business reporting. Stock availability will remain connected to the live operational database because stock counts must not become stale.

I do not recommend building a large data warehouse, data lake or lakehouse immediately. The company needs reliable reporting and better data control before investing in a more complex platform.

This approach addresses the problems already affecting the business while keeping the initial design manageable for a small team.

## 2. Proposed architecture

### How data will flow

1. **Live operational database:** The existing database continues to support website orders, customer accounts and inventory transactions.
2. **Second server:** A read replica receives changes from the live database.
3. **Daily reporting process:** Scheduled jobs read the replica and prepare reporting tables.
4. **Shared reporting:** Operations and Finance use the same agreed measures and reporting tables.
5. **Management reports:** Nana receives a consistent daily reporting view and a Monday management report.

**Stock availability is an exception.** The website must continue checking current stock against the live operational data. It must not depend on a daily reporting copy.

### Architecture overview

```text
Customers and website
         |
         v
Production MySQL database
         |
         | Database replication
         v
Second server / Read replica
         |
         | Daily reporting process
         v
Shared reporting tables
         |
         +------------------+
         |                  |
         v                  v
    Operations           Finance
         |                  |
         +--------+---------+
                  |
                  v
           Management reports
```

The website continues to use the production database for transactions and current stock. Reporting workloads are moved away from that server.

## 3. Architecture options considered

| Option | Advantages | Disadvantages | Decision |
|---|---|---|---|
| Read replica with daily reporting | Uses existing database knowledge, protects live transactions and has a manageable starting cost | Requires a second server and replication monitoring | **Recommended now** |
| Full data warehouse | Provides a structured environment for business reporting and future analysis | Adds migration, hosting and maintenance costs before the company has established trusted reporting | Reconsider when reporting needs outgrow the initial setup |
| Data lake | Can store large volumes of raw and varied data for future analysis | More storage and data-management complexity than current needs justify | Defer |
| Lakehouse | Combines analytical reporting and flexible data storage | More complex to operate and requires skills the current team does not have | Defer |

A read replica is not a complete replacement for a future warehouse. It is the practical first step because Kloud Kart's immediate problem is the effect of reporting on its live database.

## 4. Processing recommendation: Batch versus streaming

**Use daily batch processing for general reporting.**

Daily batch processing means collecting and preparing data at scheduled times rather than processing every change immediately.

This is appropriate for:
- Daily sales summaries.
- Revenue and order reports.
- Marketing performance reports.
- Finance and Operations management reports.
- General business dashboards.

**Keep stock availability real time.**

Stock counts are different because a customer must not purchase an item that has already been sold. The website should continue using current operational inventory data.

I would not introduce streaming for every business measure. It would increase operating complexity and monitoring requirements without a confirmed business need.

I would reconsider streaming if the company demonstrates that a specific decision must be made within seconds or minutes and daily updates create measurable financial or operational harm.

## 5. Team and hiring plan

The company has budget for two data hires. I recommend hiring in this order.

### Hire 1: Data Engineer — First priority

The Data Engineer should:

- Assess the existing database and reporting workload.
- Set up and test the second server.
- Configure and monitor database replication.
- Move reporting extracts away from the production database.
- Build the daily reporting process.
- Establish backups, monitoring and recovery procedures.

**First 90-day outcome:** Reporting runs from the second server, production database pressure is measured, and replication health is monitored.

### Hire 2: BI and Data Governance Analyst — Second priority

This person should:

- Agree on common definitions for business measures.
- Reconcile Operations and Finance reports.
- Build shared management reports.
- Introduce data-quality checks.
- Maintain a register of customer-data exports and access.
- Coordinate the customer-data request and deletion process with the appropriate privacy lead.

**First 90-day outcome:** Operations and Finance use agreed reporting measures, Nana has a repeatable Monday report, and customer-data copies and responsibilities are documented.

The existing PHP/MySQL developer should support integration with the website, but should not become the only person responsible for the company's data operations.

## 6. Running-cost model

Exact costs cannot be confirmed because server specifications, hosting arrangements, staff salary expectations and supplier quotations were not supplied.

The company should budget for the following:

| Cost area | What drives the cost | Recommendation |
|---|---|---|
| Second server | Compute, memory, storage and network capacity | Obtain quotations based on a workload test |
| Database storage | Database copy, reporting tables and growth | Include capacity for 15–20% annual business growth |
| Backups and recovery | Backup storage and recovery testing | Include in the operating budget |
| Monitoring | Replication delays, server health and failed reporting jobs | Establish alerts and routine checks |
| Staff | Two data hires | Recruit the Data Engineer first |
| Privacy support | Review of customer-data processes and legal obligations | Obtain qualified Ghanaian privacy advice |
| Future analytics platform | Additional hosting, migration and support | Defer until a measured need exists |

**Monthly operating cost formula:**

`Second server + storage + backups + monitoring + staff costs + privacy support`

The first financial decision should be based on quotations for the second server and the cost of the two hires. Do not approve a larger platform until the company has evidence that the initial arrangement cannot meet its reporting needs.

## 7. Risks and safeguards

| Risk | Safeguard |
|---|---|
| Reporting replica falls behind | Monitor replication delay and show the last successful refresh time |
| Reporting still affects production | Test capacity and run reporting workloads only against the replica |
| Different departments calculate measures differently | Maintain one approved definition for each shared measure |
| Customer information remains in old exports | Maintain an export register, access controls and retention rules |
| Deletion requests are missed | Track requests, owners, deadlines and completion evidence |
| Business growth exceeds current capacity | Review server capacity and reporting performance quarterly |

The company should also review its obligations under Ghana's Data Protection Act, 2012 (Act 843), including its customer-data handling and deletion procedures, with a qualified privacy professional.

## 8. When should the company invest in a larger platform?

Reconsider a warehouse or lakehouse when one or more of these conditions is demonstrated:

- The read replica can no longer support reporting workloads reliably.
- Reporting requires combining several additional business systems.
- Daily reporting no longer meets agreed business requirements.
- Data volume and analytical workloads exceed the capacity of the current arrangement.
- Forecasting and advanced analytics have a clear business case and reliable historical data.

**Final position:** Protect the live website, establish consistent daily reporting and control customer information before investing in advanced analytics. This is the most practical starting point for Kloud Kart's current size, team and budget.
| Deletion requests are missed | Track requests, owners, deadlines and completion evidence |
| Business growth exceeds current capacity | Review server capacity and reporting performance quarterly |

The company should also review its obligations under Ghana's Data Protection Act, 2012 (Act 843), including its customer-data handling and deletion procedures, with a qualified privacy professional.

## 8. When should the company invest in a larger platform?

Reconsider a warehouse or lakehouse when one or more of these conditions is demonstrated:

- The read replica can no longer support reporting workloads reliably.
- Reporting requires combining several additional business systems.
- Daily reporting no longer meets agreed business requirements.
- Data volume and analytical workloads exceed the capacity of the current arrangement.
- Forecasting and advanced analytics have a clear business case and reliable historical data.

**Final position:** Protect the live website, establish consistent daily reporting and control customer information before investing in advanced analytics. This is the most practical starting point for Kloud Kart's current size, team and budget.