# Service Level Objective (SLO) & Error Budget Policy: Robot Shop Catalogue

## Overview
This policy defines the reliability targets for the Robot Shop `catalogue` service to ensure a dependable user experience.

## 1. Definitions
* **SLI (Service Level Indicator):** Percentage of successful HTTP requests (`< 500` status codes) handled by the `catalogue` service.
* **SLO (Service Level Target):** 99.9% success rate over a rolling 30-day window[cite: 10].
* **Error Budget:** 0.1% of total requests allowed to fail over a rolling 30-day window[cite: 10].

## 2. Error Budget Exhaustion Rules
* If 100% of the error budget is consumed within a 7-day period, all feature deployments are frozen until stability is restored.
* Incident reviews and postmortems are mandatory if the error budget is breached.

## 3. Alerting & Escalation
* Alerts fire to Slack when burn rates exceed critical thresholds.
* Runbooks must be linked directly from all alerting channels.
