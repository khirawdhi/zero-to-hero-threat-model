# Security Controls Baseline — TM-A2A-01 (OAuth Client Credentials)

This baseline applies to service-to-service integrations using OAuth 2.0
client credentials and optional webhook callbacks.

---

## 1. Token Issuance Controls (TB2)
- Use **client credentials** only for non-user service identities
- Store client secrets only in a **Secret Manager/Vault** (no code, no CI vars in plaintext)
- Enforce **secret rotation** and revocation procedures
- Prefer **private_key_jwt** or **mTLS client auth** for token endpoint when possible
- Rate limit token endpoint usage and alert on anomalies (burst token minting)

**Minimum validations (auth server):**
- client authentication required
- strict scope allowlist per client
- short access token TTL

---

## 2. Token Validation Controls (TB3)
Service B must validate tokens strictly at the API entry point (gateway/middleware).

**Required checks:**
- `iss` (issuer)
- `aud` (audience) — must match this API/resource
- `exp` / `nbf` (time)
- signature validation (correct keys, correct algorithm)
- `scope` (or permissions/roles) mapped to API actions
- tenant/environment binding where applicable (prod token must not work in dev)

**Implementation guidance:**
- Prefer locally validated JWTs for availability
- Use introspection for high-risk APIs or when immediate revocation is required

---

## 3. Authorization Controls (Action-Level, not just token-level)
- Do not treat “valid token” as authorization
- Enforce **action-level authorization** inside Service B:
  - map scopes → allowed operations
  - validate object/tenant ownership (prevent cross-tenant access)
  - implement least privilege on every endpoint

**Confused deputy protection:**
- Service B must not perform privileged operations solely because Service A requested them
- Validate intent and constraints server-side (not in client)

---

## 4. Partner Trust Controls (TB1)
- Treat Service A as a **separate security domain**
- Contractually and technically define:
  - allowed scopes
  - allowed endpoints
  - rate limits
  - data classification boundaries
- Apply throttling and anomaly detection per partner/client identity
- Separate environments and credentials per partner and per environment

---

## 5. Secrets & Key Management (TB5)
- Keep client secrets and signing keys in a dedicated secrets boundary
- Enforce:
  - least privilege access to secrets
  - audit logging for secret reads
  - rotation schedules
- Never log secrets or tokens (redaction at source)

---

## 6. Webhook Security Controls (TB4, if used)
Webhooks are inbound A2A and must be treated as internet-facing.

**Required:**
- Verify **HMAC signature** (or asymmetric signature)
- Require **timestamp + nonce** (replay protection)
- Validate payload schema and enforce strict content types
- Enforce idempotency keys for event processing
- Rate limit webhook endpoint and implement backoff
- Allowlist sender IPs only if stable (do not rely solely on IP allowlists)

---

## 7. Logging, Monitoring, and Auditability (TB6)
- Generate and propagate a **correlation ID** across:
  - token issuance
  - API request
  - business action
  - webhook events
- Log (sanitized):
  - client_id / partner ID
  - token `jti` (if present) or token hash (never the full token)
  - `iss`, `aud`, scopes
  - endpoint + action outcome
- Store logs in restricted systems with retention and access controls
- Alert on:
  - repeated auth failures
  - sudden scope increases
  - token minting spikes
  - webhook replay attempts

---

## 8. Availability & Abuse Controls
- Rate limit:
  - token endpoint requests
  - API requests per client
  - webhook deliveries
- Implement caching for valid tokens within TTL
- Add circuit breakers for introspection dependency failures
- Implement retry strategies with exponential backoff

---

## 9. Build → Runtime Integrity (TB7)
- Treat OAuth config as code (scopes, audiences, allowlists)
- Protect config changes with:
  - protected branches
  - code review
  - approvals for scope changes
- Separate CI/CD secrets from runtime secrets
- Maintain SBOM and dependency scanning for gateway/auth middleware
