# Security Controls Baseline — TM-AI-02 (Agent + Tools)

Agent systems must treat model output as **untrusted** and enforce all permissions
server-side before any action is executed.

---

## 1. Model Output → Action Decision Controls
- LLM output must be treated as a **proposal**, never an instruction
- All actions require:
  - tool allowlist match
  - parameter schema validation
  - server-side authorization checks
- Default posture: **deny-by-default**

---

## 2. Policy Engine (Mandatory)
- Policy is enforced outside the LLM and outside prompt text
- Policy evaluates:
  - user identity and role/scopes
  - tenant context
  - action risk class
  - rate and cost budgets
- High-risk actions require:
  - step-up auth (MFA)
  - explicit user confirmation or HITL

---

## 3. Tooling Safety (Adapters + Executor)
- Hard allowlist tool endpoints and methods (no arbitrary URLs)
- Validate tool parameters against strict schemas
- Use safe SDKs and parameterized queries (no raw concatenation)
- Enforce timeouts, retries with backoff, and circuit breakers
- Apply egress controls from executor (network policy / firewall)

---

## 4. Privilege Design (Avoid Confused Deputy)
- Avoid “shared super-user” executor credentials
- Prefer per-user/per-tenant scoped tokens (token exchange)
- If service identity is used:
  - enforce fine-grained permissions per tool
  - restrict to minimal actions required
- Log policy decision and token scope used per action

---

## 5. Memory/State Controls
- Separate:
  - **trusted state** (system decisions, approvals)
  - **untrusted state** (user-provided or model-derived)
- Sanitize memory writes to prevent instruction persistence
- Bound retention; avoid storing sensitive data unless necessary
- Protect memory store with RBAC and audit logs

---

## 6. Logging & Auditability
- Immutable action audit trail:
  - request ID
  - proposed tool call (normalized)
  - policy decision + reason
  - executor identity and scope used
  - tool response (sanitized)
  - user confirmation/HITL evidence (if used)
- Redact secrets/PII by default
- Alert on anomalies:
  - repeated denied actions
  - tool-call bursts
  - unusual endpoints/params

---

## 7. Build → Runtime Integrity
- Treat prompts, policies, allowlists like code:
  - protected branches, reviews
  - signed artifacts where possible
- Separate CI/CD secrets from runtime secrets
- SBOM + dependency scanning for agent/orchestrator/tool adapters
