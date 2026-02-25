# Controls — TM-A2A-03 (mTLS Service Mesh)

This document defines the minimum control baseline for secure mTLS-based
Application-to-Application (A2A) communication using a service mesh.

---

# 1. Identity & Certificate Controls

## MTLS-C01 — Short-Lived Certificates
- Certificates MUST have short TTL (e.g., <24h).
- Automated rotation required.
- Expiry alerts configured.

## MTLS-C02 — Secure Private Key Storage
- Private keys stored in memory or secure volume only.
- No environment variable exposure.
- No plaintext logging of key material.

## MTLS-C03 — Strict CSR Validation
- CSR identity MUST match workload identity.
- SAN/SPIFFE ID strictly validated.
- No wildcard identities.

## MTLS-C04 — Trust Bundle Integrity
- Trust bundles MUST be signed.
- Only trusted CA root accepted.
- Changes require approval and audit.

---

# 2. Mesh Policy Controls

## MTLS-C05 — Least-Privilege Authorization
- Explicit allow rules.
- No namespace-wide wildcards.
- Default deny posture.

## MTLS-C06 — Policy Change Governance
- RBAC-restricted policy editing.
- Peer review required.
- All changes logged.

---

# 3. Runtime & Network Controls

## MTLS-C07 — Sidecar Enforcement Only
- No direct pod-to-pod communication bypassing mesh.
- Network policies prevent bypass traffic.

## MTLS-C08 — Rate Limiting & Circuit Breakers
- Protect against handshake flood.
- Protect against request amplification.

---

# 4. CI/CD & Supply Chain Controls

## MTLS-C09 — Signed Artifacts & Config
- Images signed.
- Mesh configs version-controlled.
- Protected branches enforced.

## MTLS-C10 — OIDC-Based Pipeline Identity
- No static credentials in CI/CD.
- Federated identity for deployments.

---

# 5. Observability Controls

## MTLS-C11 — Log Redaction
- No sensitive headers or payloads logged.
- Certificate/private key material never logged.

## MTLS-C12 — Immutable Audit Logs
- Policy changes logged.
- Certificate issuance logged.
- Logs retained per compliance requirements.

---

# Critical Control Dependencies

The following controls are considered HIGH IMPACT:

- MTLS-C01 (Short-lived certificates)
- MTLS-C03 (Strict CSR validation)
- MTLS-C05 (Least-privilege policies)
- MTLS-C09 (Signed pipeline artifacts)
