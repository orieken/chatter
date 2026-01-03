# ADR 0006 – ML Artifact Conventions

## Status
Proposed

## Decision
Standardize artifact locations:
- Screenshots: `reports/screenshots/<suite>/<test>/<timestamp>.png`
- Metadata: `reports/ml/metadata/<suite>/<test>/<timestamp>.json`
- Model registry: `ml-models/<detector>/<version>/...` and `ml-models/<detector>/ACTIVE`

## Rationale
- Predictable structure enables automation, training, and dashboards.

## Consequences
- Requires consistent naming across Playwright runs and pipelines.
