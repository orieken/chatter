# ADR 0003 – E2E Testing: Playwright with Saturday-Style Site Facade

## Status
Accepted

## Decision
Adopt a **site-centric facade** pattern for E2E testing:
- Sites → Pages → Flows → Services
with Playwright as the driver and optional Cucumber BDD feature files.

## Rationale
- Keeps step definitions thin and reusable.
- Separates UI structure (Pages) from business actions (Flows).
- Mirrors the proven Saturday framework architecture.

## Consequences
- Requires discipline and a small amount of scaffolding up front.
