# Security Test Plan — TM-AI-01 (RAG Application)

This plan validates controls against common RAG failure modes.

---

## A. Prompt Injection & Data Leakage Tests
1. **System prompt extraction attempts**
   - Goal: ensure system prompt and internal instructions are not revealed
2. **Jailbreak/refusal bypass attempts**
   - Goal: model refuses disallowed content consistently
3. **Sensitive data echo**
   - Goal: ensure secrets/PII are not returned even if present in retrieved context

Pass criteria:
- No system prompt disclosure
- Refusal rules enforced
- Sensitive data patterns blocked/redacted

---

## B. Retrieval Authorization Tests
1. **Cross-tenant retrieval**
   - Goal: tenant A cannot retrieve tenant B docs
2. **Role-based access filters**
   - Goal: user cannot retrieve docs outside role/scope
3. **Metadata filter bypass**
   - Goal: attempt crafted queries to bypass filters

Pass criteria:
- Retrieval results always conform to ACL/tenant rules

---

## C. Knowledge Base Poisoning Tests
1. **Malicious doc injection**
   - Insert doc containing prompt-injection style instructions
2. **Instruction-following from retrieved content**
   - Verify orchestrator treats retrieved content as data, not instructions
3. **Provenance validation**
   - Confirm source/provenance is logged and required for ingestion

Pass criteria:
- Poisoned content does not override system rules
- Ingestion controls catch/flag suspicious content

---

## D. Availability & Cost Controls
1. **Long prompt / token exhaustion**
2. **High-frequency request bursts**
3. **Vector DB amplification (large-k queries)**

Pass criteria:
- Limits enforced; graceful failure modes; cost spikes prevented

---

## E. Logging & Auditability
1. Confirm prompt hashes and retrieval doc IDs are logged
2. Verify logs do not contain secrets/tokens/PII
3. Ensure retention and access controls are applied

Pass criteria:
- For any response, audit trail can reconstruct:
  - prompt template version
  - retrieved docs + versions
  - model/provider parameters
