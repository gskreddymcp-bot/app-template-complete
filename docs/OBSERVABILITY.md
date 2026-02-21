# Observability Plan (Supabase + App Stack)

## 1) Telemetry Standard
- Correlation IDs end-to-end (client -> edge -> BFF -> Supabase).
- Structured logs with consistent keys (`trace_id`, `user_id`, `app_version`, `env`).
- Capture function, query, and storage-operation latency metrics.

## 2) Dashboards
- Release health by app version
- Auth success/failure rates (Supabase Auth)
- DB latency and saturation (Supabase Postgres)
- Storage operations and signing failures (Supabase Storage)
- Edge function error rate and timeout rate
- Cost and telemetry volume

## 3) Alerts and Routing
- Auth failure spike
- RLS denial anomaly spike
- P95 latency budget breach
- Storage signed URL generation failures
- Realtime disconnection surge
- Cost anomaly detection

## 4) Incident Readiness
- On-call rotation documented
- Severity matrix and escalation path documented
- Top runbooks linked from alerts

## 5) Fast Incident Questions
- What changed (deploy, migration, policy, key rotation)?
- Who is impacted (which tenants/users/regions)?
- What mitigation can be applied now (flag, rollback, throttling)?
