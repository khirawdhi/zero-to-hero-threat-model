# STRIDE Threat Analysis — TM-AI-01 (RAG Application)

This STRIDE analysis focuses on threats unique to RAG systems:
- prompts as untrusted inputs
- retrieval as a poisoning/exfiltration surface
- model outputs as untrusted generated content

---

## 1. Spoofing (S)

- **S1: User/session spoofing**
  - Attacker impersonates a user/session to access restricted data via retrieval.
  - Mitigation: strong auth, token validation, session binding, rate limits.

- **S2: Service identity spoofing**
  - Rogue workload calls vector DB/document store using stolen credentials.
  - Mitigation: workload identity, scoped secrets, short-lived tokens.

- **S3: Tool/API spoofing (if tools exist)**
  - Model output directs calls to attacker-controlled endpoints.
  - Mitigation: allowlisted tools, strict URL allowlists, outbound egress controls.

---

## 2. Tampering (T)

- **T1: Prompt template tampering**
  - System prompt / templates modified in CI/CD or runtime config.
  - Mitigation: protected branches, approvals, signed artifacts, integrity checks.

- **T2: Knowledge base poisoning**
  - Malicious docs/chunks inserted to influence output or exfiltrate data.
  - Mitigation: ingestion validation, source signing, moderation, review workflows.

- **T3: Vector index tampering**
  - Embeddings or metadata manipulated to bias retrieval.
  - Mitigation: access controls, integrity checks, audit logs, versioning.

---

## 3. Repudiation (R)

- **R1: No auditability of retrieval + output**
  - Cannot prove what context was retrieved or why the model responded.
  - Mitigation: log retrieval IDs, doc versions, prompt hashes, request IDs.

- **R2: Admin actions untracked**
  - Knowledge base edits or prompt changes not attributable.
  - Mitigation: admin audit logs, RBAC, change approvals.

---

## 4. Information Disclosure (I)

- **I1: Prompt injection causes leakage**
  - User instructs model to reveal system prompts, secrets, or hidden context.
  - Mitigation: do not expose secrets to model; prompt hardening; output filters.

- **I2: Retrieval returns unauthorized data**
  - Vector search bypasses access controls or filters.
  - Mitigation: enforce ACLs at retrieval, per-user authorization filters, tenant isolation.

- **I3: Training-data-like leakage via logs**
  - Sensitive prompts/outputs stored in logs or monitoring.
  - Mitigation: log redaction, PII filters, token/secret scrubbing, retention limits.

- **I4: Cross-tenant data leakage**
  - Multi-tenant vector DB or document store mixes tenants.
  - Mitigation: tenant-isolated indexes, separate keys, strong partitioning.

---

## 5. Denial of Service (D)

- **D1: Token/compute exhaustion**
  - Long prompts or adversarial inputs drive high LLM costs/latency.
  - Mitigation: input limits, truncation, quotas, caching, timeouts.

- **D2: Retrieval amplification**
  - Large k-nearest queries or broad filters overload vector DB.
  - Mitigation: query limits, circuit breakers, caching, rate limiting.

- **D3: Dependency outage (LLM provider)**
  - LLM API outage halts functionality.
  - Mitigation: graceful degradation, fallback modes, retries with backoff.

---

## 6. Elevation of Privilege (E)

- **E1: Model output triggers privileged actions**
  - If tools exist, model output leads to actions beyond user authorization.
  - Mitigation: tool calls must be policy-checked server-side; human-in-the-loop for high risk.

- **E2: Retrieval bypass becomes privilege escalation**
  - User gains access to restricted docs by crafting prompts/queries.
  - Mitigation: enforce authorization *before* retrieval and *after* retrieval.

- **E3: CI/CD compromise → prompt/control takeover**
  - Attacker modifies system prompts/guardrails in build pipeline.
  - Mitigation: signed builds, least-privilege CI/CD, secrets isolation.
