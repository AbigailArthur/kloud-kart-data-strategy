# ADR-003: Keep stock availability on the live operational database

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Proposed: Kloud Kart leadership, with the existing PHP/MySQL developer responsible for website integration

## Context

Kloud Kart's brief states that stock counts cannot become stale. The proposed reporting architecture uses a read replica and daily reporting process, which may introduce delays between a live transaction and its appearance in a report.

Customers need accurate stock availability when placing orders.

## Decision

Keep customer-facing stock availability connected to current operational inventory data. Do not use daily reporting tables or a delayed analytical copy to decide whether a customer can purchase an item.

## Alternatives considered

### Alternative A: Use daily reporting tables for stock availability

- **How it would work:** The website checks the latest daily stock report before confirming whether an item is available.
- **Why it is attractive:** It would make stock information available alongside other reporting data.
- **Why rejected:** Stock could change after the daily report is prepared. Customers might be allowed to purchase items that are no longer available.

### Alternative B: Use the reporting read replica for stock availability

- **How it would work:** The website reads stock counts from the replicated database rather than the production database.
- **Why it is attractive:** It could reduce some reads against the production server.
- **Why rejected:** Replication delay could cause the website to display an outdated stock count. The brief explicitly says stock counts cannot become stale.

### Alternative C: Keep stock checks on the live operational database

- **How it would work:** The website continues checking and updating current stock through the operational database as part of the order process.
- **Why it is attractive:** Stock decisions use current operational records rather than a delayed reporting copy.
- **Why selected:** It protects the accuracy of customer-facing stock availability and respects the business requirement.

## Consequences

- **What this buys:** More reliable stock availability for customers and less risk of selling items that are no longer available.
- **What this costs:** Stock-related reads and updates remain on the production database and must be handled efficiently. The website and database developer must protect transaction integrity.
- **What it costs the client if I am wrong:** If the production database becomes overloaded by stock checks, customer transactions may slow down. If the operational inventory process is incorrect, the website may still show inaccurate availability.
- **What would make me revisit this:** Evidence that a separately designed inventory service can guarantee current stock, preserve transaction integrity and meet the company's availability requirements.

## What this survives

This decision survives pressure to move every data workload away from production. Protecting the live website does not mean moving critical operational decisions to a delayed reporting copy.

Stock availability is a different business requirement from management reporting. It should remain current even when general reports are refreshed daily.