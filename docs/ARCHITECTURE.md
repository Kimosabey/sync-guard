# Architecture — SyncGuard

## High-Level Design (HLD)
SyncGuard reconciles cache against the database of record, detecting and repairing divergence so read-through/write-aside caching stays correct.

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#ffffff','lineColor':'#2563eb','mainBkg':'#ffffff'}}}%%
graph LR
    A([DB State])
    B([vs. Cache State])
    C([Reconciliation Worker])
    D([Consistent])
    A --> B
    B --> C
    C --> D
    style A fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#1e40af
    style B fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#1e40af
    style C fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#1e40af
    style D fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#1e40af
```

**Flow:** DB State → vs. Cache State → Reconciliation Worker → Consistent

## Low-Level Design (LLD)
- **Components:** `Postgres`, `Redis`
- **Interfaces / contracts:** to be finalized during implementation.
- **Data model:** to be defined per component.

## Decision Log
- **Why this stack:** **Postgres** — relational source of truth; **Redis** — in-memory store / cache / queue.
- **Antigravity constraint:** run logic/state/UI locally; offload heavy reasoning to cloud APIs; target modest hardware.

## Concept Deep Dive
Keeping cache and source of truth consistent under concurrent writes without locking everything.
