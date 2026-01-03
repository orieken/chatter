# ADR 0004 – Backend Stack: FastAPI + PostgreSQL + Redis

## Status
Accepted

## Decision
Backend is **FastAPI** with **PostgreSQL** for persistence and **Redis** for timers/ephemeral coordination.

## Rationale
- FastAPI is productive and test-friendly.
- PostgreSQL is reliable for core entities (topics, sessions, users).
- Redis is well-suited for TTL/timer patterns and transient state.

## Consequences
- Need clear boundaries between persistent and ephemeral data.
- Local dev requires Docker (compose).
