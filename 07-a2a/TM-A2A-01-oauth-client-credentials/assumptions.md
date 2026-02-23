# Threat Modeling Assumptions — TM-A2A-01 (OAuth Client Credentials)

This document defines the explicit assumptions under which this threat model is valid.

If any assumption changes, the model must be revisited.

---

## 1. Architectural Assumptions

- Service A and Service B are separate security domains.
- Communication occurs over HTTPS with TLS properly configured.
- OAuth 2.0 Client Credentials flow is used for service authentication.
- Tokens are short-lived access tokens (no long-lived bearer tokens).
- Service B validates tokens before executing business logic.
- Optional webhook endpoints are internet-accessible.

---

## 2. Identity & Token Assumptions

- Authorization Server is trusted and securely managed.
- Client credentials are unique per environment and per partner.
- Access tokens include:
  - issuer (`iss`)
  - audience (`aud`)
  - expiration (`exp`)
  - scope or permissions
- Service B validates:
  - signature
  - issuer
  - audience
  - expiration
  - scope
- Tokens are not intentionally reused across environments (dev/prod isolation).

---

## 3. Secrets Management Assumptions

- Client secrets are stored in a dedicated secret manager.
- Secrets are not hardcoded in source code.
- Secret access is logged and restricted.
- Secrets are rotated periodically.
- Tokens and secrets are not logged in plaintext.

---

## 4. Authorization Assumptions

- Token validation is not treated as sufficient authorization.
- Service B performs action-level authorization checks.
- Scope definitions reflect least-privilege access.
- Cross-tenant access is explicitly denied unless designed otherwise.

---

## 5. Webhook Assumptions (if applicable)

- Webhook payloads are signed (HMAC or asymmetric).
- Webhook requests include a timestamp and/or nonce.
- Replay protection is implemented.
- Webhook endpoints enforce rate limits.
- Webhook payload schema is validated before processing.

---

## 6. Operational Assumptions

- Audit logs are generated for:
  - token issuance
  - API calls
  - authorization decisions
  - webhook events
- Correlation IDs are propagated across services.
- Monitoring detects:
  - token minting anomalies
  - excessive API calls
  - scope escalation
  - webhook replay attempts
- CI/CD changes to OAuth config require review and approval.

---

## 7. Environmental Assumptions

- Production, staging, and development environments use separate credentials.
- Partner integrations use isolated client identities.
- Authorization server keys are rotated securely.
- Network infrastructure does not bypass token validation logic.

---

## 8. Explicit Non-Goals

This threat model does NOT cover:

- End-user delegated OAuth flows (authorization code + PKCE).
- Identity federation across multiple IdPs.
- mTLS-only authentication patterns.
- Legacy API key authentication.
- Compromise of the underlying cloud provider.
- Physical security of infrastructure.

---

## 9. Model Validity Condition

This model assumes:

- Bearer tokens are used.
- Proof-of-possession (DPoP/mTLS-bound tokens) is not enforced by default.
- Services trust the authorization server.
- Business logic is correctly implemented.

If tokens become bound, if scopes change to dynamic ABAC policies,
or if zero-trust service mesh is introduced, this model must be updated.
