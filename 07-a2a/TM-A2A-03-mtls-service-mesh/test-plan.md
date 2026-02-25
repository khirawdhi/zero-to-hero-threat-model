# Test Plan — TM-A2A-03 (mTLS Service Mesh)

This test plan validates identity, authorization, certificate lifecycle,
and mesh enforcement.

---

# 1. Certificate & Identity Testing

## T1 — Certificate Expiry Validation
- Deploy workload with expired cert.
- Expected: connection fails.
- Verify alert generated.

## T2 — Identity Spoof Attempt
- Attempt to use cert from Service A as Service B.
- Expected: connection rejected.

## T3 — CSR Misbinding Test
- Modify CSR to request higher-privileged identity.
- Expected: CA rejects request.

---

# 2. Policy Enforcement Testing

## T4 — Unauthorized Service Call
- Attempt Service A → Service C where policy denies.
- Expected: mTLS connection established but request denied (403/deny).

## T5 — Namespace Wildcard Detection
- Introduce wildcard policy in staging.
- Verify policy linting blocks deployment.

---

# 3. DoS & Resilience Testing

## T6 — Handshake Flood Simulation
- Simulate repeated TLS handshakes.
- Verify rate limiting and no proxy crash.

## T7 — Renewal Storm Simulation
- Trigger simultaneous certificate renewal.
- Verify CA availability and jitter handling.

---

# 4. CI/CD Security Testing

## T8 — Tampered Config Deployment
- Modify mesh config without approval.
- Expected: pipeline blocks promotion.

## T9 — Unsigned Image Deployment
- Attempt deployment of unsigned container image.
- Expected: admission controller rejects.

---

# 5. Observability Validation

## T10 — Log Redaction Verification
- Send sensitive headers in request.
- Verify logs do NOT contain secrets.

## T11 — Policy Change Audit Trail
- Modify authorization rule.
- Verify audit log records user + timestamp + diff.

---

# Pass Criteria

System is considered compliant when:

- All identity validation tests pass.
- Unauthorized lateral movement attempts fail.
- Certificate lifecycle is automated and monitored.
- Policy changes are auditable.
- No sensitive material appears in logs.
