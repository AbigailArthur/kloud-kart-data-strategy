# ADR-001: Use a second server and read replica for reporting

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Proposed: Kloud Kart leadership, with the Data Engineer responsible for implementation

## Context

Kloud Kart runs its website, orders, inventory and customer accounts on one MySQL server. Reporting exports have slowed the live website twice in the past month.

The database is approximately 40 GB and the company processes about 4,000 orders per day. The second server has already been pre-approved.

The company needs to protect customer transactions without immediately introducing a complex analytics platform.

## Decision

Use the approved second server as a read replica of the production database. Run reporting extracts and analytical queries against the replica instead of the live production server.

## Alternatives considered

### Alternative A: Continue running reports on the production database

- **How it would work:** Keep the current setup and schedule reporting queries during quieter periods.
- **Why it is attractive:** It avoids the cost of another server and requires little initial setup.
- **Why rejected:** Two reporting-related slowdowns have already occurred. Scheduling large queries at quieter times does not remove competition for database resources or guarantee that the website remains responsive.

### Alternative B: Build a full data warehouse immediately

- **How it would work:** Copy and transform data into a separate analytical platform for reporting.
- **Why it is attractive:** It provides a dedicated environment for structured reporting and future analytics.
- **Why rejected:** It introduces additional hosting, migration and maintenance costs before the company has established reliable reporting definitions. The current team also lacks a professional data engineer.

### Alternative C: Use a second server with a read replica

- **How it would work:** Replicate production database changes to a second server and direct reporting queries to that server.
- **Why it is attractive:** It separates reporting workloads from live customer transactions while building on the company's existing database skills.
- **Why selected:** It directly addresses the confirmed production impact and uses infrastructure that has already been approved.

## Consequences

- **What this buys:** Less reporting pressure on the live website, a separate place for analytical queries and a practical foundation for future reporting improvements.
- **What this costs:** Additional server, storage, backup, monitoring and maintenance costs. The Data Engineer must configure and monitor replication.
- **What it costs the client if I am wrong:** If reporting needs exceed the replica's capacity, the company may spend money on an arrangement that still needs replacement. If replication is delayed or fails unnoticed, reports may use outdated information.
- **What would make me revisit this:** Repeated capacity problems, unacceptable replication delays, major increases in reporting complexity or evidence that the replica cannot support agreed reporting requirements.

## What this survives

This decision survives pressure to build a large analytics platform immediately. The company has a confirmed production problem and an approved second server, so separating reporting workloads is the more direct first step.

Growth of 15–20% annually does not automatically require a warehouse. However, measured capacity problems or new reporting requirements could justify one later.