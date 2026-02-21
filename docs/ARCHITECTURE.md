# Architecture Overview

## 1) C4 Context Diagram (Supabase-Centric)
```mermaid
flowchart LR
  User[End User] --> App[Mobile/Web App]
  Admin[Ops/Admin] --> Portal[Admin Portal]

  App --> Edge[Front Door/CDN + WAF]
  Edge --> BFF[BFF/API Layer]

  App --> SA[Supabase Auth]
  App --> SR[Supabase Realtime]

  BFF --> SPG[(Supabase Postgres)]
  BFF --> SST[Supabase Storage]
  BFF --> SEF[Supabase Edge Functions]
  BFF --> SK[Supabase Secrets/Vault]
  BFF --> Obs[Observability Stack]
```

## 2) C4 Container Diagram
```mermaid
flowchart TB
  subgraph Client
    M[Mobile App]
    W[Web SPA]
  end

  subgraph Public_Zone[Public Zone]
    FD[Front Door + WAF]
    SA[Supabase Auth]
    RT[Supabase Realtime]
  end

  subgraph Private_Zone[Private Zone]
    BFF[BFF Service]
    EF[Supabase Edge Functions]
    DB[(Supabase Postgres)]
    ST[(Supabase Storage)]
    O11Y[Logs/Metrics/Traces]
  end

  M --> FD
  W --> FD
  M --> SA
  W --> SA
  M --> RT
  W --> RT

  FD --> BFF
  BFF --> SA
  BFF --> DB
  BFF --> ST
  BFF --> EF
  EF --> DB
  EF --> ST

  BFF --> O11Y
  EF --> O11Y
```

## 3) Trust Boundaries
- Boundary A: Public internet to edge/auth/realtime endpoints.
- Boundary B: Edge to BFF/Edge functions with strict key isolation.
- Boundary C: Data plane (Postgres + Storage) with RLS and private bucket controls.

## 4) Data Stores and Rationale
- Supabase Postgres: primary relational store with RLS.
- Supabase Storage: secure object storage with signed URL access.
- Realtime: low-latency state/event propagation from Postgres changes.

## 5) Integration Points
- Supabase Auth (OIDC, PKCE, MFA)
- Supabase Edge Functions for event/webhook automation
- External providers (payments, notifications, messaging)

## 6) Companion Document
For deep integration patterns by capability, see `docs/SUPABASE_ARCHITECTURE.md`.
