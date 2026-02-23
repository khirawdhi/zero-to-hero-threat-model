# Security Test Plan — TM-A2A-01 (OAuth Client Credentials)

This plan validates common A2A risks: token theft/replay, scope abuse,
confused deputy, webhook spoofing, and audit gaps.

---

## A. Token Issuance Tests (TB2)
1. **Token minting abuse**
   - Attempt high-rate token requests for a valid client
   - Verify rate limits and anomaly alerts
2. **Invalid client authentication**
   - Wrong secret / wrong assertion
   - Ensure consistent failure behavior (no info leakage)
3. **Scope request enforcement**
   - Request scopes not assigned to client
   - Verify denial and proper logging

Pass criteria:
- Unauthorized scopes are denied
- Token endpoint is rate limited and monitored

---

## B. Token Validation Tests (TB3)
1. **Issuer mismatch**
   - Token signed by different issuer
2. **Audience mismatch**
   - Token with different `aud`
3. **Expired / not-yet-valid token**
4. **Algorithm/key confusion**
   - Attempt `alg=none` or wrong key set usage (as applicable)
5. **Token replay**
   - Reuse a valid token across multiple requests rapidly

Pass criteria:
- Tokens fail on iss/aud/exp/signature checks
- Replay patterns are detected and throttled (where applicable)

---

## C. Authorization & Confused Deputy Tests
1. **Scope → action mismatch**
   - Call write endpoints with read-only scope
2. **Cross-tenant/object access**
   - Use valid token to access another tenant’s resources
3. **Indirect privileged action**
   - Attempt an action that should require additional checks (server-side constraints)

Pass criteria:
- Service B enforces action-level authorization
- Object/tenant access is denied and logged

---

## D. Partner Trust & Environment Isolation Tests (TB1)
1. **Prod token in non-prod**
2. **Non-prod token in prod**
3. **Partner A identity used to reach Partner B resources**
4. **Excessive request volume per partner**

Pass criteria:
- Environment/tenant boundaries are enforced
- Per-partner throttles work as designed

---

## E. Webhook Security Tests (TB4, if used)
1. **Unsigned webhook**
2. **Invalid signature**
3. **Replay attack**
   - Same payload and signature resent (or same nonce) after a delay
4. **Timestamp skew**
   - Old timestamp outside allowed window
5. **Payload tampering**
   - Modify payload after signing (must fail)
6. **Flooding**
   - Burst webhook requests and validate rate limits

Pass criteria:
- Only valid signature + timestamp + nonce are accepted
- Replays are rejected
- Endpoint is rate limited and resilient

---

## F. Logging & Auditability Tests (TB6)
1. Confirm correlation IDs flow end-to-end:
   - token issuance → API call → business action → webhook event (if any)
2. Confirm logs do not store:
   - raw tokens
   - secrets
   - sensitive payloads without redaction
3. Validate audit reconstruction:
   - identify client_id, scopes, endpoint, decision, outcome

Pass criteria:
- Audit trail can reconstruct “who did what, when, and why”
- No secret/token leakage in logs

---

## G. Resilience & Failure Mode Tests
1. Introspection endpoint outage (if used)
2. Authorization server degraded
3. Retry behavior (no infinite retries)
4. Backoff correctness for webhook delivery

Pass criteria:
- System fails safely
- No cascading retries or amplification
