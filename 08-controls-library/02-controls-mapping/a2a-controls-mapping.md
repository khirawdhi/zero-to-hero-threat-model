# Control Mapping — A2A (OAuth Client Credentials)

This document maps the TM-A2A-01 threat model risks
to reusable controls from the Controls Library.

---

# 1. Identity & Token Controls

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Token forgery / invalid JWT | IAM-02 | Token Validation Discipline |
| Scope abuse | IAM-02 | Token Validation Discipline |
| Over-privileged service identity | A2A-04 | Confused Deputy Protection |
| Token replay | A2A-03 | JWT Validation (iss/aud/exp enforcement) |
| Stolen client credentials | SC-03 | Secrets Handling in CI/CD |

---

# 2. Authorization & Confused Deputy

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Service acting beyond caller authority | A2A-04 | Confused Deputy Protection |
| Action-level authorization bypass | IAM-02 | Token Validation Discipline |
| Cross-tenant access | DATA-04 | Tenant Isolation |
| Partner privilege escalation | A2A-01 | OAuth Client Credentials Hardening |

---

# 3. Webhook Security (if used)

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Webhook spoofing | A2A-02 | Webhook Signing & Replay Protection |
| Replay attack | A2A-02 | Webhook Signing & Replay Protection |
| Webhook flooding | APP-02 | Rate Limiting |
| Payload tampering | APP-01 | Input Validation |

---

# 4. Network & Exfiltration

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Data exfiltration via outbound calls | NET-01 | Egress Control |
| Calling unauthorized endpoints | NET-01 | Egress Control |
| Metadata abuse | NET-01 | Egress Control |

---

# 5. Logging & Observability

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Lack of traceability | OBS-02 | Correlation ID Propagation |
| Token exposure in logs | OBS-04 | Log Redaction |
| Inability to reconstruct actions | OBS-01 | Audit Logging |

---

# 6. Supply Chain & Configuration

| Threat | Control ID | Control Name |
|--------|------------|--------------|
| Scope drift via config changes | SC-01 | Protected Branches |
| CI/CD credential leakage | SC-03 | Secrets Handling in CI/CD |
| Authorization config tampering | SC-02 | Signed Builds |

---

# 7. Minimum A2A Security Baseline (Required Controls)

For any OAuth-based A2A integration, the following controls are mandatory:

- IAM-02: Token Validation Discipline
- A2A-02: Webhook Signing & Replay Protection (if webhooks used)
- NET-01: Egress Control
- SC-03: Secrets Handling in CI/CD
- OBS-02: Correlation ID Propagation
- OBS-01: Audit Logging

---

# 8. Advanced / Recommended Controls

- Token binding (mTLS / DPoP)
- Per-tenant scoped tokens
- Step-up authentication for sensitive operations
- Behavioral anomaly detection on token minting
- Environment isolation (dev/stage/prod token separation)
