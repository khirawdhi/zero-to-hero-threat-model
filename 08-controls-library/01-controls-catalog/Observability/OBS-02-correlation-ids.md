# OBS-02: Correlation ID Propagation

## Control Goal

Enable traceability across distributed services.

---

## Threats Mitigated

- Repudiation
- Delayed incident detection
- Blind forensic gaps

---

## Control Description

All inbound requests must:

- Generate or accept correlation ID
- Propagate ID downstream
- Include ID in logs and events

---

## Implementation Guidance

- Use standard headers (e.g., X-Request-ID)
- Enforce propagation in middleware
- Log correlation ID in structured logs
- Monitor missing ID anomalies

---

## Validation / Test Cases

- Confirm ID appears across service logs.
- Confirm webhook events include correlation ID.
- Confirm monitoring system indexes it.

---

## Evidence Artifacts

- Logging configuration
- Sample trace logs
- Monitoring dashboards

---

## Common Failure Modes

- Generating new ID at each hop
- Not logging ID
- Not propagating to async flows

---

## Cloud Mapping

Azure Monitor / App Insights  
AWS CloudWatch + X-Ray  
GCP Logging + Cloud Trace
