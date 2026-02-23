# Security Controls Baseline — TM-A2A-01 (OAuth Client Credentials)

This baseline defines minimum controls for service-to-service OAuth 2.0
(client credentials) integrations, including optional webhook callbacks.

---

## 1. Client Credentials & Secret Hygiene
- Store client secrets only in a secrets manager (never in code or CI logs)
- Rotate secrets on a schedule and on suspicion of exposure
- Prefer private key JWT / mTLS client auth where supported (stronger than shared secrets)
- Separate identities per:
  - environment (dev/stage/prod)
  - integration partner
  - service
- Enforce least privilege on secret access (who/what can read secrets)

---

## 2. Token Issuance Constraints (Authorization Server)
- Issue tokens with strict:
  - `aud` (audience bound to Service B)
  - `iss` (trusted issuer)
  - `exp` (short TTL)
  - `scope` (minimal scopes only)
- Disable wildcard scopes and overly broad scopes (avoid “admin” tokens for automation)
- Prefer short-lived tokens + refresh strategy (if applicable)
- Where possible, use:
  - proof-of-possession (DPoP) or mTLS token binding

---

## 3. Token Validation (Resource Server / API)
- Validate JWTs strictly:
  - signature
  - `iss`
  - `aud`
  - `exp` / `nbf`
  - scopes/permissions
- Reject tokens without required claims
- Do not accept tokens issued for other environments or audiences
- If using introspection:
  - enforce timeouts and caching
  - handle auth server outage safely

---

## 4. Authorization Beyond OAuth (Action-Level Controls)
OAuth proves a client is allowed to call an API; it does not prove the action is safe.

- Enforce authorization at the action level:
  - resource ownership checks
  - tenant scoping
  - partner scoping
- Protect against confused deputy:
  - do not perform privileged actions solely because the caller is authenticated
  - require explicit input validation + intent validation for sensitive operations

---

## 5. Replay & Abuse Resistance
- Rate limit per client ID and per endpoint
- Apply quotas and budgets per partner integration
- Use short token TTLs (reduce replay window)
- Add anomaly detection:
  - token usage spikes
  - unusual IPs/regions
  - repeated 4xx/5xx patterns
- For high-risk operations, require:
  - idempotency keys
  - request timestamps
  - nonce/replay checks (where applicable)

---

## 6. Webhook Security (Optional)
If Service B delivers callbacks to Service A:

- Require webhook signatures (HMAC or asymmetric)
- Validate:
  - signature
  - timestamp
  - replay window (reject old events)
- Use idempotency keys / event IDs to prevent duplicate processing
- Restrict webhook endpoint exposure:
  - allowlist source IPs where possible
  - WAF/rate limits
- Do not trust webhook payload fields for authorization decisions

---

## 7. Logging, Monitoring, and Auditability
- Never log:
  - access tokens
  - client secrets
  - authorization headers
- Log with correlation IDs:
  - token subject/client ID (safe identifiers only)
  - scopes used (not the token)
  - request ID → action mapping
- Maintain immutable audit logs for:
  - token issuance events (auth server)
  - privileged API operations (resource server)
- Alert on:
  - repeated token validation failures
  - unusual client behavior
  - scope escalation attempts

---

## 8. Build → Runtime Integrity
- Protect CI/CD secrets from appearing in build output
- Separate:
  - CI/CD credentials
  - runtime OAuth client credentials
- Require code review for:
  - scope changes
  - token validation logic changes
  - webhook verification changes
- Maintain SBOM + dependency scanning for token libraries and gateway middleware
