# ADR-002: Use daily batch processing for general reporting

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Proposed: Kloud Kart leadership, with the Data Engineer responsible for implementation

## Context

The board has requested real-time analytics. However, the business brief states that stock counts cannot become stale while everything else can refresh daily.

Kloud Kart has a small technical team and a limited budget for two data hires. Introducing continuous processing across every business function would add operational complexity.

## Decision

Use scheduled daily batch processing for general business reporting. Do not introduce streaming for all business data unless a specific business requirement demonstrates that daily updates are insufficient.

## Alternatives considered

### Alternative A: Real-time streaming for all business data

- **How it would work:** Process changes continuously as orders, payments, customer activities and other events occur.
- **Why it is attractive:** It can provide fresher information and support rapid operational decisions.
- **Why rejected:** The brief does not establish a need for second-by-second reporting across all departments. Continuous processing would add infrastructure, monitoring and troubleshooting responsibilities to a team that is already small.

### Alternative B: Daily batch processing

- **How it would work:** Collect and prepare reporting data at scheduled times, then make the results available to users.
- **Why it is attractive:** It is simpler to operate, easier to monitor and sufficient for the daily reporting requirements described in the brief.
- **Why selected:** The business explicitly permits daily refreshes for everything except stock counts.

### Alternative C: Frequent scheduled processing throughout the day

- **How it would work:** Run reporting jobs every 15 or 30 minutes instead of once daily.
- **Why it is attractive:** It provides fresher information without requiring a continuous streaming system.
- **Why rejected:** The brief does not show that this additional frequency is needed. It would create more processing and monitoring work without a demonstrated business benefit.

## Consequences

- **What this buys:** Lower operational complexity, predictable reporting schedules and a manageable workload for the new team.
- **What this costs:** Managers will not see every business change immediately in general reports. Reporting must clearly show its last successful refresh time.
- **What it costs the client if I am wrong:** Important decisions may be delayed if a business process genuinely requires more frequent information than daily reporting provides.
- **What would make me revisit this:** Evidence that daily reporting causes measurable financial loss, operational delays or missed business opportunities. Any proposed increase in frequency should identify the exact data flow and required response time.

## What this survives

This decision survives pressure for real-time dashboards simply because the board has requested them. A dashboard updating every second is not automatically more useful if the business does not act on that information.

If the company later identifies a genuine time-sensitive use case, it can introduce faster processing for that specific flow instead of making every report real time.