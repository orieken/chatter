# ADR 0002 – Frontend Tooling: Vite + Vitest

## Status
Accepted

## Decision
Use **Vite** for build/dev and **Vitest** for unit/component tests for web and shared frontend logic.

## Rationale
- Fast feedback loops and modern TypeScript ergonomics.
- Consistent tooling across web + (supporting) mobile preview logic.

## Consequences
- React Native runtime tests will also need RN-focused tooling (e.g., Jest/RNTL) when we switch from preview to true RN builds.
