# Threat Modeling Assumptions — TM-AI-01 (RAG Application)

This threat model is valid only under the assumptions below.

---

## 1. Architectural Assumptions
- The application is the only user entry point to the RAG system
- The orchestrator controls prompt construction and retrieval logic
- The LLM is accessed via an API (hosted or third-party)
- Secrets are never embedded directly into prompts or retrieval context

---

## 2. Data & Retrieval Assumptions
- Documents have owners/tenants and enforceable access controls
- Retrieval applies authorization filters for user/tenant access
- Knowledge base ingestion is controlled and auditable

---

## 3. Operational Assumptions
- Logging and monitoring are enabled with restricted access
- CI/CD is secured with protected branches and reviewed changes
- Rate limits and cost controls are implemented and enforced

---

## 4. Explicit Non-Goals
- Securing model training pipelines and model weights
- Defending against advanced hardware-level attacks
- Preventing all possible jailbreak attempts (goal is risk reduction and containment)
