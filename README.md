# app-template-complete

Reusable **App Management Starter Pack** for running mobile/web/backend products with clear governance, security, release control, and operations, now with a **Supabase-first integration blueprint**.

## What was added
- Product + architecture + security + governance templates under `docs/`
- Supabase integration architecture with secure patterns for Auth, Postgres, Storage, Realtime, and Edge Functions
- Reusable Mermaid diagrams and prompt pack
- Azure DevOps multi-stage pipeline scaffold in `.azuredevops/pipelines/`
- Incident runbook starter set in `docs/RUNBOOKS/`

## Folder structure
- `docs/PRD.md`
- `docs/NFR.md`
- `docs/ARCHITECTURE.md`
- `docs/SUPABASE_ARCHITECTURE.md`
- `docs/THREAT_MODEL.md`
- `docs/DATA_GOVERNANCE.md`
- `docs/RELEASE_STRATEGY.md`
- `docs/OBSERVABILITY.md`
- `docs/DR_PLAN.md`
- `docs/DIAGRAMS.md`
- `docs/RUNBOOKS/`
- `.azuredevops/pipelines/app-management-starter.yml`

## Final Go/No-Go checklist
1. SLOs defined and measurable
2. Bad release mitigation (kill switch + phased rollout)
3. PII map + retention + deletion workflow
4. Threat model with validation evidence
5. Restore tested against RPO/RTO
6. Performance budgets + test matrix
7. Cost budgets + abuse controls
8. On-call ownership + top runbooks
