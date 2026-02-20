# Architecture Overview

## 1) C4 Context Diagram
```mermaid
flowchart LR
  User[End User] --> App[Mobile/Web App]
  Admin[Ops/Admin] --> Portal[Admin Portal]
  App --> Edge[Front Door/CDN + WAF]
  Edge --> APIM[API Management]
  APIM --> BFF[BFF/API Layer]
  BFF --> Services[Domain Services]
  Services --> DB[(Primary Database)]
  Services --> Bus[(Event Bus)]
  BFF --> KV[Secrets/Key Vault]
  Services --> Obs[Observability Stack]
```

## 2) C4 Container Diagram
```mermaid
flowchart TB
  subgraph Client
    M[Mobile App]
    W[Web SPA]
  end

  subgraph Azure_Public[Public Zone]
    FD[Front Door + WAF]
    APIM[API Management]
  end

  subgraph Azure_Private[Private Zone]
    BFF[BFF Service]
    SVC1[Service A]
    SVC2[Service B]
    DB[(Postgres/SQL)]
    CACHE[(Redis Cache)]
    BUS[(Queue/Event Bus)]
    KV[Key Vault]
    MON[Logs/Metrics/Traces]
  end

  M --> FD
  W --> FD
  FD --> APIM --> BFF
  BFF --> SVC1
  BFF --> SVC2
  SVC1 --> DB
  SVC2 --> CACHE
  SVC2 --> BUS
  BFF --> KV
  BFF --> MON
  SVC1 --> MON
  SVC2 --> MON
```

## 3) Trust Boundaries
- Boundary A: Public internet to edge (WAF enforced)
- Boundary B: Edge to API layer (authenticated traffic only)
- Boundary C: App services to data plane (private networking only)

## 4) Data Stores and Rationale
- Primary relational DB: transactional consistency
- Cache: low-latency reads
- Event bus: async workflows and resilience

## 5) Integration Points
- Identity provider (OIDC)
- Payment/provider APIs
- Messaging/notification provider
