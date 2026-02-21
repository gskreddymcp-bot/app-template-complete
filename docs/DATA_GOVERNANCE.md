# Data Governance (Supabase Data Plane)

## 1) Data Inventory
| Field | Classification | Storage | Retention | Notes |
|---|---|---|---|---|
| user_id | Internal | Primary DB | Account lifetime | Non-PII key |
| email | PII | Primary DB | Account lifetime + 30 days | Encrypted at rest |
| phone | PII | Primary DB | Optional, until removed | Mask in logs |
| order_id | Internal | Primary DB | 7 years | Regulatory dependent |
| ip_address | Sensitive | Logs store | 30 days | Truncated/anonymized |

## 2) Deletion Workflow
1. User requests deletion.
2. Verify identity and legal holds.
3. Execute erasure workflow across all stores.
4. Emit deletion audit event.
5. Confirm completion within deletion SLA.

## 3) Audit Logging Policy
- Log actor, action, target, timestamp, result, correlation ID.
- Never log credentials, full tokens, or raw payment data.
- Logs must be immutable and access-controlled.

## 4) Analytics Event Allowlist
- Only approved events may be emitted.
- Event schema must exclude sensitive personal fields.
- New events require privacy review and owner approval.


## 5) Supabase Data Controls
- Enforce RLS on all exposed tables.
- Use private storage buckets unless public access is explicitly approved.
- Apply retention/deletion jobs across Postgres, Storage, and derived analytics sinks.
