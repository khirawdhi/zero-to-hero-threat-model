# STRIDE Threat Analysis — TM-AI-02 (Agent + Tools)

Focus: threats where **LLM output can trigger actions**.
Key risk is the **Model Output → Action Decision** boundary.

---

## 1. Spoofing (S)

- **S1: User/session spoofing → actions executed as another user**
  - Attacker reuses tokens/session to trigger tool calls under victim identity.
  - Mitigation: strong auth, token binding, step-up auth for sensitive actions.

- **S2: Tool endpoint spoofing**
  - Tool adapter points to attacker-controlled endpoint (DNS/URL manipulation).
  - Mitigation: strict allowlists, pinned base URLs, egress controls.

- **S3: Service identity spoofing**
  - Compromised workload uses executor credentials to call tools directly.
  - Mitigation: workload identity, scoped credentials, network policies.

---

## 2. Tampering (T)

- **T1: Action parameter tampering**
  - LLM output crafts parameters that exploit tools (SQL injection, command args, SSRF).
  - Mitigation: schema validation, strict parameter allowlists, encoding, safe SDKs.

- **T2: Policy tampering**
  - Policy rules modified or bypassed in runtime/config.
  - Mitigation: policy as code, signed config, protected changes, runtime integrity checks.

- **T3: Memory/state tampering**
  - Attacker poisons memory so future actions are biased or unsafe.
  - Mitigation: access control on memory writes, signed traces, bounded retention, sanitization.

---

## 3. Repudiation (R)

- **R1: No provable action trail**
  - Cannot prove who approved/executed an action or why.
  - Mitigation: immutable audit logs, action IDs, policy decision logs, timestamps.

- **R2: Admin actions untracked**
  - Prompt/policy/tool allowlists changed without attribution.
  - Mitigation: admin RBAC + MFA + audit + approvals.

---

## 4. Information Disclosure (I)

- **I1: Prompt/Tool result leakage**
  - Tool returns sensitive data; model echoes it to user or logs.
  - Mitigation: output filtering, data classification, redaction, least-privileged tools.

- **I2: Secrets exposure to model**
  - Secrets included in prompts/context or returned by tools.
  - Mitigation: never pass secrets to LLM; use token exchange; secret scanners.

- **I3: Cross-tenant leakage via tools**
  - Tool access not scoped per tenant/user.
  - Mitigation: per-tenant credentials, row-level authorization, scoped tokens.

---

## 5. Denial of Service (D)

- **D1: Tool execution amplification**
  - Model loops causing repeated tool calls (expensive, rate-limited APIs).
  - Mitigation: max tool calls per request, time budgets, circuit breakers.

- **D2: Token/compute exhaustion**
  - Long conversations + tool results inflate prompt size.
  - Mitigation: truncation, summarization, quotas, caching.

- **D3: Dependency failure cascades**
  - Tool outage triggers retries and agent loops.
  - Mitigation: bounded retries, fallback paths, graceful degradation.

---

## 6. Elevation of Privi
