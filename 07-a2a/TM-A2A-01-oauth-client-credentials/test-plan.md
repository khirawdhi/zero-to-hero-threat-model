# Security Test Plan — TM-A2A-01 (OAuth Client Credentials)

This test plan validates controls for OAuth client credentials flow,
token validation, replay resistance, and optional webhook security.

---

## A. Token Issuance Tests (Auth Server)
1. **Audience enforcement**
   - Request token for wrong audience and verify it is rejected or unusable.
2. **Scope minimization**
   - Attempt to request broader scopes than allowed.
3. **Token TTL**
   - Verify short token lifetime and expiration behavior.

Pass criteria:
- Tokens are audience-bound, least-privileged, short-lived.

---

## B. Token Validation Tests (Resource Server)
1. **Signature validation**
   - Modify JWT payload and verify rejection.
2. **Issuer validation**
   - Use token from untrusted issuer and verify rejection.
3. **Audience validation**
   - Use token minted for another API and verify rejection.
4. **Expiration / nbf**
   - Test expired tokens and not-before tokens are rejected.
5. **Scope enforcement**
   - Use token missing required scope and verify action is denied.

Pass criteria:
- Resource server enforces strict claim validation and scope checks.

---

## C. Replay & Abuse Tests
1. **Token replay**
   - Reuse same token across multiple requests; verify rate limits and anomaly detection.
2. **Burst traffic**
   - Send high-frequency calls with valid tokens and verify quotas per client.
3. **Idempotency for sensitive endpoints**
   - Repeat the same write action and ensure idempotency controls prevent double execution.

Pass criteria:
- Replay window is minimized; abuse is throttled; sensitive actions are idempotent.

---

## D. Confused Deputy / Action-Level Authorization Tests
1. **Cross-tenant access**
   - Use valid token and attempt to access another tenant’s resources.
2. **Resource ownership**
   - Attempt actions on resources not owned by the caller context.
3. **Partner scoping**
   - Validate that partner A cannot operate on partner B’s data.

Pass criteria:
- Authentication does not imply authorization; tenant/partner boundaries hold.

---

## E. Secrets Handling Tests (Client Side)
1. **Secret leakage checks**
   - Verify secrets are not present in:
     - logs
     - CI output
     - crash dumps
2. **Rotation**
   - Rotate secret and verify old credentials no longer mint tokens.
3. **Least privilege**
   - Verify only required services can read OAuth secrets.

Pass criteria:
- Secrets are protected, rotated, and not leaked.

---

## F. Webhook Security Tests (Optional)
1. **Signature validation**
   - Send webhook without signature / invalid signature; must be rejected.
2. **Replay protection**
   - Replay the same event ID; must be ignored.
3. **Timestamp window**
   - Send old timestamp events; must be rejected.
4. **Rate limiting**
   - Flood webhook endpoint; verify throttling and resilience.

Pass criteria:
- Webhooks are authenticated, replay-resistant, and rate-limited.

---

## G. Logging & Auditability Tests
1. Verify tokens are not logged (no Authorization headers stored)
2. Verify correlation IDs link:
   - token subject/client ID → request → action
3. Verify audit logs exist for privileged actions

Pass criteria:
- For any incident, system can reconstruct who did what and why, without sensitive leakage.
