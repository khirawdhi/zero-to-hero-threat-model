# Security Controls Baseline — TM-AI-01 (RAG Application)

This baseline defines minimum controls to operate a RAG system safely.

---

## 1. Prompt & Output Safety
- Treat **user prompts** and **model outputs** as untrusted
- Never include secrets (API keys, credentials) in prompts or context
- Use prompt hardening: fixed system prompt, explicit refusal rules
- Output filtering for:
  - secrets/tokens
  - PII patterns
  - policy violations
- Constrain maximum prompt size, conversation history, and response length

---

## 2. Retrieval Authorization & Tenant Isolation
- Enforce authZ **at retrieval time** (per-user/tenant filters)
- Apply post-retrieval checks (confirm documents returned are permitted)
- Isolate tenants:
  - separate vector indexes (preferred)
  - separate encryption keys and namespaces
- Prefer deterministic filters over “LLM decides what is allowed”

---

## 3. Knowledge Base Integrity (Anti-Poisoning)
- Ingestion pipeline validates:
  - file type
  - source origin
  - malware scanning (for uploads)
  - content moderation (for policy-sensitive corpora)
- Maintain document versioning and provenance metadata
- Require approvals for high-impact corpus changes

---

## 4. Identity & Secrets
- Use workload identity / short-lived tokens for service-to-service access
- Store secrets only in Secret Manager / Vault equivalents
- Rotate LLM API keys and enforce least privilege
- Protect admin functions behind MFA and RBAC

---

## 5. Rate Limiting & Cost Controls
- Rate limit per user / per tenant / per IP
- Enforce quotas for:
  - requests/min
  - tokens/day
  - retrieval calls/day
- Add circuit breakers for upstream dependency failures (LLM/vector DB)

---

## 6. Logging, Monitoring, and Auditability
- Centralize logs with strict access controls
- Redact prompts/outputs by default; store hashes when possible
- Log:
  - request IDs
  - prompt hash / template version
  - retrieved doc IDs + versions
  - model/provider + parameters
- Alert on anomalies:
  - token spikes
  - repeated refusals
  - retrieval of sensitive doc classes

---

## 7. Build → Runtime Integrity
- Protect prompt templates/guardrails like code:
  - protected branches
  - code review
  - signed artifacts (where possible)
- Separate CI/CD secrets from runtime secrets
- Maintain SBOM and dependency scanning for app/orchestrator components
