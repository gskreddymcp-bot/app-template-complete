# Release Strategy

## 1) Environments and Promotion Rules
- Dev -> QA -> PreProd -> Prod
- Promotion requires: green tests, security gate pass, approval record.

## 2) Mobile Distribution
- iOS: TestFlight for internal/external testers
- Android: Play Console Internal Testing track
- Signing keys managed with strict RBAC and rotation schedule

## 3) Feature Flags and Kill Switch
- All high-risk functionality must be behind remote flags.
- Global kill switch to disable critical features without store redeploy.
- Compatibility policy for N-2 app versions.

## 4) Phased Rollout
- Default ramp: 5% -> 25% -> 50% -> 100%
- Advance only when crash-free and latency thresholds are healthy.

## 5) Rollback and Mitigation
- Backend rollback: blue/green or slot swap with health-gated automation.
- Mobile mitigation: server-side disablement + fallback UI/flows.

## 6) Exit Criteria for Release
- No Sev-1/Sev-2 open defects.
- SLO/SLI and crash-free thresholds met.
- Runbook links included in release notes.

## 7) Note on App Center
App Center distribution is retired; use TestFlight and Play internal tracks.
Reference: https://learn.microsoft.com/en-us/appcenter/retirement
