# Disaster Recovery Plan

## 1) Targets
- RPO:
- RTO:
- Critical services in scope:

## 2) Backup Strategy
- Database backups: frequency, retention, encryption
- Object storage backups: replication and retention
- Configuration backups: infra-as-code + secret references

## 3) Restore Procedure
1. Declare incident and assign commander.
2. Restore database to point-in-time target.
3. Restore dependent stores/services.
4. Run smoke and integrity checks.
5. Switch traffic and monitor stabilization.

## 4) Restore Test Evidence
- Last tested date:
- Result summary:
- Evidence links:

## 5) Failover Strategy
- Regional failover model:
- Traffic management approach:
- Communication plan:
