# ACE Technical Overview

ACE (Application for Conversation Escape) is a platform for **time-boxed conversations** between an **Ambassador** and a **Guest**, coordinated by a **Guide**.
This document is the technical “north star” for engineering and agents.

---

## System Context

```mermaid
flowchart LR
  Guide[Guide (Controller)] -->|configures topics & limits| Web[Web Dashboard]
  Ambassador[Ambassador (Talk Lead)] --> Mobile[Mobile App]
  Guest[Guest (Participant)] --> Mobile
  Web --> API[FastAPI Backend]
  Mobile --> API
  API --> PG[(PostgreSQL)]
  API --> Redis[(Redis)]
  API --> Notify[Notification Service]
  Notify --> Guide
```

---

## Core Conversation Flow

```mermaid
sequenceDiagram
  participant G as Guide (Web)
  participant A as Ambassador (Mobile)
  participant B as Backend (FastAPI)
  participant R as Redis (Timers)
  participant N as Notifier

  G->>B: Create/Update Topics
  A->>B: Fetch Topics
  A->>B: Start Session(topic_id, duration)
  B->>R: Schedule timer(duration)
  B-->>A: Session Started(session_id)
  Note over A: Ambassador leads conversation

  R-->>B: Timer Expired(session_id)
  B->>N: send_session_ended(guide_id, session_id)
  N-->>G: Notify Guide to check-in
  B-->>A: Session Ended
```

---

## Clean Architecture (Practical)

```mermaid
flowchart TB
  subgraph Clients
    MobileUI[Mobile UI]
    WebUI[Web UI]
  end

  subgraph Backend
    Routers[FastAPI Routers]
    Services[Services Layer]
    Domain[Domain Models]
    Repos[Repositories]
  end

  subgraph Data
    PG[(PostgreSQL)]
    Redis[(Redis)]
  end

  MobileUI --> Routers
  WebUI --> Routers
  Routers --> Services
  Services --> Domain
  Services --> Repos
  Repos --> PG
  Services --> Redis
```

---

## Testing Strategy (Saturday-Style)

### E2E Site-Centric Facade
```mermaid
classDiagram
  class Site {
    +pages
    +flows
    +services
  }
  class Pages {
    +locators
    +uiActions()
  }
  class Flows {
    +businessSteps()
  }
  class Services {
    +apiCalls()
  }
  Site --> Pages
  Site --> Flows
  Site --> Services
```

### Test Pyramid
```mermaid
flowchart TB
  Unit[Unit Tests (Vitest/Pytest)] --> Component[Component Tests (Vitest)]
  Component --> Integration[Integration Tests (API/DB)]
  Integration --> E2E[E2E (Playwright)]
```

---

## ML / Visual Validation Roadmap

```mermaid
flowchart TD
  A[Test Run] --> B[Capture Screenshot]
  B --> C[Write Metadata]
  C --> D[Preprocess]
  D --> E[Train Model]
  E --> F[Register Model (versioned)]
  B --> G[Detection]
  F --> G
  G --> H[Validation Result]
  H --> I[Dashboard Insights]
```

---

## Conventions

- All artifacts written to:
  - `reports/screenshots/...`
  - `reports/ml/metadata/...`
  - `ml-models/<detector>/<version>/...`

- All major decisions tracked in `docs/ADRs/`.

