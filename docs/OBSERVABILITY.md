# Observability Plan

## 1) Telemetry Standard
- Use correlation IDs end-to-end (client -> edge -> API -> services).
- Structured logs with consistent keys.
- Metrics and traces aligned to service/version/environment.

## 2) Dashboards
- Release health by app version
- Latency (p50/p95/p99)
- Error rate by endpoint and dependency
- Saturation (CPU/memory/connection pool)
- Cost and ingestion volume

## 3) Alerts and Routing
- Crash-free rate drops below threshold
- API error rate above threshold
- P95 latency budget breach
- Queue depth and dead-letter growth
- Cost anomaly detection

## 4) Incident Readiness
- On-call rota defined
- Severity matrix documented
- Top runbooks linked from alert payloads

## 5) Operational Questions We Must Answer Quickly
- What changed?
- Who is impacted?
- What is the immediate mitigation?
