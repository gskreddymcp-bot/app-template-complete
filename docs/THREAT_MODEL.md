# Threat Model (STRIDE) - Supabase Integrated

## 1) Assets
- Supabase Auth tokens and session data
- PII and transactional data in Supabase Postgres
- Objects/files in Supabase Storage
- Service-role keys and edge function secrets

## 2) Entry Points
- Mobile and web clients
- Supabase Auth endpoints
- BFF and public APIs
- Supabase Edge Functions
- CI/CD pipeline and migration workflows

## 3) STRIDE Table
| Threat | Scenario | Impact | Mitigation | Test Evidence |
|---|---|---|---|---|
| Spoofing | Stolen refresh token reused | Account takeover | PKCE, short JWT TTL, rotating refresh, device/risk checks | Auth abuse tests + anomaly alerts |
| Tampering | Malicious SQL path via weak policy | Data integrity loss | Strict parameterization, RLS policies, migration review gates | SQL injection tests + policy tests |
| Repudiation | User disputes privileged action | Compliance failure | Immutable audit logs with actor, role, trace ID | Audit trail validation |
| Information Disclosure | Misconfigured storage bucket exposes PII | Privacy breach | Private buckets, signed URLs, object path authorization | Storage access deny/allow tests |
| Denial of Service | Abuse floods APIs/realtime channels | Outage/cost spike | WAF, API rate limits, connection quotas, backpressure | Load tests + alert simulation |
| Elevation of Privilege | Service-role key leaked in client | Full data compromise | Never ship service keys to clients, rotate keys, secret scanning | Secret scanning + key rotation drills |

## 4) Supabase-Specific Security Baseline
- RLS enabled on all exposed tables.
- Policy-by-policy automated tests in CI.
- Storage access defaults to private with signed URL workflows.
- Edge functions use managed secrets only.
- Realtime channels scoped by role and topic policies.

## 5) MASVS Mapping (Mobile)
- MASVS-AUTH: token/session hardening
- MASVS-STORAGE: secure local storage and no plaintext secrets
- MASVS-NETWORK: TLS + cert trust validation
- MASVS-RESILIENCE: rooted/jailbroken risk policy

Reference: https://mas.owasp.org/MASVS/

## 6) Rooted/Jailbroken Device Policy
- Default: reduced capability mode for sensitive operations.
- Optional stricter posture: block authentication on high-risk detections.
