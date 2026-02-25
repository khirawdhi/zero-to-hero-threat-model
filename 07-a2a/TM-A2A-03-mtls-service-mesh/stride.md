# STRIDE — TM-A2A-03 (mTLS Service Mesh)

This STRIDE analysis is applied **per data flow** and **per trust boundary**.
Focus is on identity at transport layer, certificate lifecycle, mesh policy, and CI/CD promotion.

---

## Legend

- **S** Spoofing
- **T** Tampering
- **R** Repudiation
- **I** Information Disclosure
- **D** Denial of Service
- **E** Elevation of Privilege

---

# 1) STRIDE per Data Flow

## F1: App → Sidecar A (Local Request)

- **S:** Untrusted local process impersonates Service A app and sends requests to sidecar.
- **T:** Local request parameters manipulated before reaching proxy (if no app-layer integrity checks).
- **R:** Lack of correlation IDs prevents attribution across hops.
- **I:** Sensitive headers/body exposed via local logs/debug tooling.
- **D:** Local flooding of sidecar causes CPU/memory exhaustion.
- **E:** App abuses sidecar configuration (e.g., bypass egress filters) if sidecar runs overly privileged.

**Primary mitigations:** workload hardening, least-privilege pod security, local authn between app↔sidecar where applicable, rate limiting, correlation IDs.

---

## F2: Sidecar A ↔ Sidecar B (mTLS Handshake)

- **S:** Client identity spoofing using stolen cert/private key; rogue workload presents valid-looking identity.
- **T:** TLS downgrade / weak cipher negotiation if misconfigured; trust bundle tampering leads to accepting wrong CA.
- **R:** No handshake audit logs; cannot prove which identity connected.
- **I:** Certificate/private key leakage; exposure of SPIFFE/SAN identity metadata; handshake metadata leakage (SNI) where applicable.
- **D:** Handshake flood (CPU intensive), exhausting proxies; repeated failed handshakes degrade service.
- **E:** Over-broad identity trust (e.g., namespace-wide trust) allows lateral movement as “authorized” identity.

**Primary mitigations:** strict TLS config, short-lived certs, rotation, trust bundle integrity, handshake rate limits, identity-based allowlists.

---

## F3: Sidecar A → Sidecar B (Encrypted Service Call)

- **S:** Unauthorized service calls if policy allows broader identities than intended.
- **T:** Request tampering inside compromised sidecar (post-encryption/pre-forward) or via malicious filter/plugin.
- **R:** Missing request signing/attribution at app layer for sensitive operations.
- **I:** Data exfiltration over allowed routes; sensitive headers/body logged by proxy.
- **D:** High request rate causes queue saturation; circuit breaker misconfig can amplify outages.
- **E:** Policy bypass via misrouted traffic (wrong cluster/service), or permissive routing rules.

**Primary mitigations:** least-privilege mesh authz policies, egress allowlists, log redaction, circuit breakers, app-level authZ for sensitive actions.

---

## F4: Sidecar B → Sidecar A (Encrypted Response)

- **S:** Response spoofing if routing compromised (traffic steered to attacker-controlled service).
- **T:** Response tampering by compromised proxy/filter.
- **R:** Lack of correlation IDs prevents audit trail of response path.
- **I:** Leakage via logs/telemetry; sensitive response caching in proxies.
- **D:** Response amplification (large payloads) leading to bandwidth/memory exhaustion.
- **E:** Downstream data returned beyond caller authorization (if app-layer authorization missing).

**Primary mitigations:** request/response size limits, routing integrity controls, correlation IDs, app-layer authorization.

---

## F5: Sidecar B → App B (Local Delivery)

- **S:** Local process impersonates sidecar to app (rare, but possible with shared network namespace misuse).
- **T:** Sidecar-to-app data modified by compromised node/pod networking.
- **R:** App logs lack request identity; cannot attribute action to calling workload.
- **I:** Local exposure of sensitive payloads.
- **D:** Sidecar overwhelms app with requests (no backpressure).
- **E:** App assumes mTLS == authorization and performs privileged actions without app checks.

**Primary mitigations:** app-layer authorization, identity propagation (caller identity headers), local network policies, backpressure.

---

## F6: Control Plane → Sidecars (Policy Distribution)

- **S:** Attacker impersonates control plane and pushes malicious policy.
- **T:** Policy tampering in transit or at rest; unauthorized edits to policy store.
- **R:** No audit trail of policy change → cannot prove who changed what.
- **I:** Policy documents reveal internal topology, service names, trust domains.
- **D:** Bad policy push breaks traffic (deny-all) or causes proxy crash (invalid config).
- **E:** Malicious/overly permissive policies allow unauthorized lateral movement.

**Primary mitigations:** strong RBAC for policy authors, signed config, change approvals, policy validation tests, audit logging.

---

## F7: CA → Sidecars (Certificate Issuance/Rotation)

- **S:** Rogue workload obtains certificate for another identity (CSR spoofing).
- **T:** Trust bundle tampering; issuance parameters manipulated (long TTL, wrong SAN).
- **R:** No issuance logs; cannot trace cert creation to requester.
- **I:** Certificates/private keys leaked (during delivery, at rest, in logs).
- **D:** CA outage prevents rotation; expired certs cause outage.
- **E:** CA issues overly privileged identities; broad SANs enable escalation across services.

**Primary mitigations:** strict CSR validation, short-lived certs, issuance audit logs, secure secret storage, CA HA, rotation monitoring.

---

## F8: Sidecars → CA (CSR / Renewal)

- **S:** Spoofed CSR requests; attacker requests certs for privileged identities.
- **T:** CSR tampering; replay CSR to extend access.
- **R:** Missing request logs.
- **I:** CSR data leaks identity metadata.
- **D:** Renewal storm (many workloads renew simultaneously) overwhelms CA.
- **E:** Abuse of renewal endpoints to maintain long-term persistence.

**Primary mitigations:** CSR authentication, rate limits, jittered renewals, strict identity binding, replay protection.

---

## F9: CI/CD → Runtime (Artifacts & Config Promotion)

- **S:** Pipeline identity spoofing; attacker triggers deployment as trusted pipeline.
- **T:** Artifact tampering (images, manifests, mesh policies, trust bundles).
- **R:** Lack of provenance; cannot prove what was deployed and by whom.
- **I:** Secrets leaked in pipeline logs; policy files leak topology.
- **D:** Bad rollout causes downtime; repeated deployments cause instability.
- **E:** Malicious config grants broad mesh access, installs permissive policies, or swaps trust anchors.

**Primary mitigations:** protected branches, signed builds, least-privilege pipeline roles, OIDC federation, policy-as-code checks, approval gates.

---

## F10: Telemetry → Monitoring (Logs/Signals)

- **S:** Fake telemetry injected to hide attacks or trigger false alerts.
- **T:** Log tampering to erase evidence; metric manipulation.
- **R:** Logs not immutable; insufficient retention.
- **I:** Sensitive data in logs (payloads, headers, certs, tokens).
- **D:** Telemetry flood overwhelms logging pipeline (drop logs during incident).
- **E:** Over-privileged monitoring access enables reading secrets or modifying policies.

**Primary mitigations:** log redaction, least-privilege access to observability, immutable audit logs, rate limits, retention policy.

---

# 2) STRIDE by Trust Boundary (High-Risk Zones)

## TB1: Workload Identity Boundary (Private Keys & Certs)

- **S/E:** Key theft enables identity spoofing and lateral movement.
- **T:** Trust bundle modification causes accepting malicious CA.
- **I:** Secret leakage via env vars, volume mounts, debug endpoints.
- **D:** Key/cert rotation failure breaks communication.

**Mitigations:** secure secret mounts, short TTL certs, rotation monitoring, least privilege, hardened nodes/pods.

---

## TB2: Mesh Policy Boundary (Control Plane)

- **E:** Misconfig or malicious change grants broad access.
- **T/R:** Unauthorized edits without audit trail.
- **D:** Invalid policy pushes can break cluster traffic.

**Mitigations:** RBAC, approvals, policy linting/tests, signed config, audit logging.

---

## TB3: Certificate Issuance Boundary (CA)

- **E:** CA compromise is catastrophic (issues valid identities).
- **D:** CA outages break rotation and service connectivity.
- **T:** Compromised trust anchor invalidates mesh security.

**Mitigations:** CA hardening/HA, HSM where possible, strict CSR validation, issuance auditing, rapid revocation/rotation plan.

---

## TB4: Runtime / Cluster Boundary

- **E:** Node compromise → access to secrets, sidecars, traffic.
- **I:** Packet capture risk if sidecars compromised (decrypted traffic visible).
- **D:** Cluster-level outages amplify.

**Mitigations:** runtime hardening, segmentation, least privilege, node security, admission controls.

---

## TB5: Build → Runtime Boundary (CI/CD)

- **E:** Supply chain compromise → malicious policy + trust anchor swap.
- **T:** Artifact manipulation.
- **R:** Lack of deployment provenance.

**Mitigations:** signed artifacts, SLSA-style provenance, protected branches, OIDC, approvals.

---

## TB6: Monitoring Boundary

- **I:** Logs contain sensitive data; monitoring becomes data lake of secrets.
- **T/R:** Log integrity issues prevent investigations.
- **D:** Telemetry flood during attacks.

**Mitigations:** redaction, immutable logging, least privilege, rate limits, retention.

---

# 3) High-Priority STRIDE Outcomes (What to put in Risk Register)

1. Certificate/private key compromise → service identity spoofing (TB1, F2/F7)
2. CA compromise or mis-issuance → catastrophic trust failure (TB3, F7/F8)
3. Mesh policy misconfiguration → unintended lateral movement (TB2, F6)
4. CI/CD compromise → push permissive policy or swap trust anchors (TB5, F9)
5. DoS via handshake flood or renewal storm (F2/F8)
6. Sensitive data leakage via logs/telemetry (F10, TB6)
