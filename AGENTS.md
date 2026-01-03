# ACE Agent Instructions (AGENTS.md)

This repository is designed for agent-driven development.

## How to Work
1. Pick exactly **one** TODO from `docs/TODO/`.
2. Implement it end-to-end: code + tests + docs updates.
3. Keep changes in-scope; open a new TODO/PR for out-of-scope improvements.
4. Run `make test` and (when relevant) `make e2e` before submitting.

## Quality Gates (must pass for new/changed code)
- Cyclomatic complexity: **< 7** per function/method
- Max function length: **≤ 30 LOC** (excluding blanks/comments)
- Params per function: **≤ 4** (prefer value objects)
- Duplication: **< 5%** per module/package
- Coverage: **≥ 85%** lines/branches (unit combined) where practical
- Lint: **0 errors**, **0 new warnings**
- Security: **never commit secrets** (tokens, keys, passwords)

## Architecture Rules
- Prefer **clean boundaries**: UI → flows → services → API/data
- Keep stateful logic in hooks/composables/services, not giant components
- Use dependency injection where possible (FastAPI Depends, service factories)
- Keep I/O at the edges; keep domain logic pure

## Testing Rules
- TDD for logic modules; BDD for user behaviors.
- E2E uses the **site-centric** pattern (Saturday-style):
  - Sites → Pages → Flows → Services
- Prefer deterministic tests; avoid sleep where possible.

## Documentation Rules
- Update or add an ADR for any non-trivial architectural decision.
- Keep diagrams in Mermaid in `docs/technical-overview.md`.
