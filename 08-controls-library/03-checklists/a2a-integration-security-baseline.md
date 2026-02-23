# A2A Integration Security Baseline
## Executive Checklist — OAuth Client Credentials Pattern

This checklist is intended for architecture reviews, design approvals,
and partner onboarding for Application-to-Application (A2A) integrations.

If any item is “No”, the integration requires remediation before production.

---

# 1. Identity & Token Security

- [ ] OAuth 2.0 Client Credentials flow is used (no static API keys).
- [ ] Access tokens are short-lived (≤ 15 minutes recommended).
- [ ] Service validates:
  - [ ] Signature
  - [ ] Issuer (`iss`)
  - [ ] Audience (`aud`)
  - [ ] Expiration (`exp`)
  - [ ] Scope / role claims
- [ ] Token validation occurs before business logic execution.
- [ ] Per-environment client identities are used (dev/stage/prod isolation).
- [ ] Per-partner client IDs are unique (no shared credentials).

Controls: IAM-02

---

# 2. Authorization Discipline

- [ ] Scope definitions follow least privilege.
- [ ] Service performs action-level authorization checks.
- [ ] Cross-tenant access is explicitly denied by default.
- [ ] Sensitive operations require elevated scope.
- [ ] Confused deputy risk has been evaluated.

Controls: IAM-02, A2A-04

---

# 3. Secrets Management

- [ ] Client secrets stored in secure secret manager.
- [ ] No secrets hardcoded in source code.
- [ ] Secrets are rotated periodically.
- [ ] Secrets are masked in logs.
- [ ] CI/CD pipelines use ephemeral credentials (OIDC preferred).

Controls: SC-03

---

# 4. Network Controls

- [ ] Outbound egress is restricted to approved endpoints.
- [ ] Metadata services are restricted.
- [ ] Internal APIs are not publicly exposed.
- [ ] mTLS evaluated for high-sensitivity integrations.

Controls: NET-01

---

# 5. Webhook Security (If Used)

- [ ] Webhook payloads are signed (HMAC or asymmetric).
- [ ] Timestamp validation enforced.
- [ ] Replay detection implemented.
- [ ] Webhook endpoints rate limited.
- [ ] Payload schema validation enforced.

Controls: A2A-02, APP-01, APP-02

---

# 6. Logging & Observability

- [ ] Correlation IDs propagated end-to-end.
- [ ] Token issuance logged.
- [ ] Authorization failures logged.
- [ ] Webhook events logged.
- [ ] Sensitive values redacted in logs.
- [ ] Alerting configured for:
  - [ ] Excessive token minting
  - [ ] Unusual scope usage
  - [ ] Repeated authorization failures

Controls: OBS-01, OBS-02, OBS-04

---

# 7. Build & Deployment Controls

- [ ] OAuth configuration changes require review.
- [ ] Protected branches enforced.
- [ ] Infrastructure as Code changes audited.
- [ ] Build artifacts signed (recommended).

Controls: SC-01, SC-02

---

# 8. Risk Acceptance Review

- [ ] Token replay risk evaluated.
- [ ] Scope creep documented.
- [ ] Webhook exposure risk documented.
- [ ] Partner trust boundary defined.

---

# Minimum Production Requirements

The following are non-negotiable:

- Token validation discipline (IAM-02)
- Secrets handling in CI/CD (SC-03)
- Egress restriction (NET-01)
- Correlation ID propagation (OBS-02)
- Webhook signing (if webhooks are enabled)

---

# Architecture Review Decision

| Decision | Status |
|----------|--------|
| Approved | ☐ |
| Approved with Conditions | ☐ |
| Rejected | ☐ |

Reviewer:
Date:
Environment:
Integration ID:
