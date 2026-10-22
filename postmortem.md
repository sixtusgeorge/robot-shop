# Incident Postmortem: Catalogue Service Outage

## Incident Overview
- **Date:** 2026-10-22
- **Author:** DevOps Engineer
- **Severity:** Critical
- **Impact:** The `catalogue` service experienced backend failure, violating the 99.9% availability SLO and consuming a portion of the error budget.
- **Detection:** Prometheus alert `CatalogueHighErrorRate` fired successfully.

## Timeline
- **14:00 UTC** – MongoDB deployment scaled down to 0 replicas as part of an incident drill simulation.
- **14:01 UTC** – Automated traffic tests hit the `catalogue` service.
- **14:02 UTC** – Prometheus alert `CatalogueHighErrorRate` triggered due to error rate exceeding the threshold.
- **14:05 UTC** – Mitigation executed by scaling MongoDB back to 1 replica.
- **14:06 UTC** – Service health restored and error rate returned to normal.

## Root Cause
The root cause of the outage was an upstream database dependency failure (MongoDB deployment scaled to 0), causing backend connection failures for the catalogue service.

## Action Items / Preventive Measures
1. Improve database high availability by ensuring pod disruption budgets (PDBs) are enforced.
2. Add automated recovery hooks or self-healing strategies for critical stateful dependencies.
