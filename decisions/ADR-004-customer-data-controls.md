# ADR-004: Introduce controlled customer-data exports and deletion tracking

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Proposed: Kloud Kart leadership, with the BI and Data Governance Analyst coordinating implementation

## Context

Marketing maintains a customer list of approximately 300,000 people, but the company does not have a clear record of where exported copies are stored or who controls them.

The company must also be able to respond to Data Protection Commission complaints within 90 days. The brief does not demonstrate a complete process for locating and handling customer deletion requests.

## Decision

Introduce a customer-data register that records approved exports, their purpose, owners, access and review dates. Establish a tracked customer-data request and deletion process that covers relevant systems, exported copies and external processors.

## Alternatives considered

### Alternative A: Continue using manually managed marketing exports

- **How it would work:** Allow departments to create and share customer lists as needed, relying on individual employees to manage their copies.
- **Why it is attractive:** It is familiar, flexible and requires little initial investment.
- **Why rejected:** The brief already identifies untracked copies. Continuing this approach makes it difficult to establish who holds customer information or whether a deletion request has been handled everywhere.

### Alternative B: Build a complete central customer-data platform immediately

- **How it would work:** Consolidate customer information into a central platform and manage access and customer requests from there.
- **Why it is attractive:** It could provide a more centralised view of customer information and support future customer analytics.
- **Why rejected:** It introduces additional cost and implementation complexity. Moving data into one platform does not automatically remove existing spreadsheets, exports or third-party copies.

### Alternative C: Introduce an export register and tracked request process

- **How it would work:** Record each approved export, its owner, purpose and review date. Log customer requests and record the systems, copies and processors checked, actions taken and completion evidence.
- **Why it is attractive:** It addresses the known control gaps without requiring a large new platform.
- **Why selected:** It is a manageable first step for the current team and creates evidence that customer-data processes are being followed.

## Consequences

- **What this buys:** Better visibility of customer-data copies, clearer responsibilities and a record of how customer requests are handled.
- **What this costs:** Staff time to maintain registers, verify requests, investigate systems and copies, and review retention arrangements. Privacy advice may also be required.
- **What it costs the client if I am wrong:** A register may create a false sense of security if employees do not record exports or if hidden copies and external processors are missed. Incomplete handling could expose the company to regulatory and customer-trust risks.
- **What would make me revisit this:** Evidence that the register cannot control the number of copies, that more advanced access controls are needed, or that a central platform would reduce risk at an affordable cost.

## What this survives

This decision survives pressure to solve the problem by simply centralising all customer information. The immediate problem is that the company does not know enough about its existing copies and processes.

The register and request workflow must be reviewed against Ghana's Data Protection Act, 2012 (Act 843), with qualified privacy advice. The process must also account for lawful retention requirements, backups and external processors. Recording a deletion request does not itself delete data or establish legal compliance.