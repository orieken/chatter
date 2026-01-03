# ADR 0001 – Architecture Overview

## Status
Accepted

## Decision
Use a monorepo containing:
- Mobile app (React Native / Expo path; current scaffold uses React preview with Vite)
- Web dashboard (Vue 3 + Vite)
- Backend (FastAPI + PostgreSQL + Redis)
- Unified tooling via pnpm workspace, Makefile, Docker Compose, and Invoke.

## Rationale
- One repo simplifies cross-cutting changes, CI, and shared standards.
- Python backend aligns with ML/AI roadmap.
