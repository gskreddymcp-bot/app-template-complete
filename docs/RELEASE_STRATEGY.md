# Release Strategy (Supabase-Aware)

## 1) Environments and Promotion Rules
- Dedicated Supabase projects per environment: `dev`, `qa`, `preprod`, `prod`.
- Promotion requires green tests, migration validation, and approval records.

## 2) Supabase Migration Strategy
- All schema changes managed through versioned SQL migrations.
- Each PR validates migration ordering, rollback notes, and RLS policy impacts.
- Production migrations are executed in controlled windows with pre-check backups.

## 3) Mobile Distribution
- iOS: TestFlight for internal/external testers
- Android: Play Console Internal Testing track
- Runtime compatibility policy maintained for N-2 client versions

## 4) Feature Flags and Kill Switch
- High-risk features behind remote flags.
- Kill switch can disable features that depend on unstable integrations.

## 5) Phased Rollout + Health Gates
- Default rollout: 5% -> 25% -> 50% -> 100%.
- Advance only if crash-free %, auth error rate, and DB latency stay within budget.

## 6) Rollback and Mitigation
- Backend rollback via deployment slots/blue-green.
- Supabase mitigation via hotfix migration, feature disablement, or policy rollback.
- Mobile mitigation via server-side kill switch and compatibility fallback.

## 7) Exit Criteria for Release
- No Sev-1/Sev-2 open defects.
- SLO and crash-free thresholds healthy.
- Supabase policy tests and migration checks passed.
- Runbook links included in release artifacts.
