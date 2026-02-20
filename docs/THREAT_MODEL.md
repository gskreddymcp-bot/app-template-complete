# Threat Model (STRIDE)

## 1) Assets
- User identity and tokens
- PII and business records
- Payment/order transaction integrity
- Signing keys and deployment credentials

## 2) Entry Points
- Mobile and web clients
- Public API endpoints
- CI/CD pipelines and artifact registry
- Third-party integrations

## 3) STRIDE Table
| Threat | Scenario | Impact | Mitigation | Test Evidence |
|---|---|---|---|---|
| Spoofing | Stolen refresh token used from new device | Account takeover | Short token TTL, secure storage, risk-based auth checks | Auth anomaly test + integration tests |
| Tampering | API payload modified in transit | Fraud/invalid state | TLS 1.2+, request signatures for critical calls, server validation | Security integration tests |
| Repudiation | User disputes admin action | Compliance gap | Immutable audit trail with actor/context/correlation ID | Audit trail verification tests |
| Information Disclosure | PII in logs/analytics | Privacy breach | Redaction middleware + allowlisted analytics schema | Log scanning checks |
| Denial of Service | Bot/API abuse | Service degradation, cost spike | WAF, per-IP/per-user throttling, queue backpressure | Load test + gateway policy tests |
| Elevation of Privilege | Broken role checks | Unauthorized actions | Central policy engine (RBAC/ABAC), deny-by-default | Role matrix test suite |

## 4) OWASP MASVS Mapping (Mobile Baseline)
- MASVS-ARCH: secure architecture, least privilege
- MASVS-AUTH: robust auth/session management
- MASVS-STORAGE: encrypted sensitive storage
- MASVS-NETWORK: TLS, cert validation, no weak ciphers
- MASVS-RESILIENCE: root/jailbreak detection policy

Reference: https://mas.owasp.org/MASVS/

## 5) Rooted/Jailbroken Device Policy
- Default: reduced capability mode (read-only + no sensitive actions)
- Alternate options (choose one): block entirely / warn-only
