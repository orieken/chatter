# ADR 0005 – CI/CD: Makefile as the Source of Truth

## Status
Proposed → Accepted after implementation

## Decision
CI should invoke repository **Makefile targets** (setup/lint/test/e2e/coverage) rather than duplicating logic.

## Rationale
- Prevents drift between local and CI behavior.
- Simplifies onboarding (“run what CI runs”).

## Consequences
- Make targets must stay stable and well-documented.
