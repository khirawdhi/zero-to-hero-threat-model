# Data Flow Diagram (DFD) — TM-AI-01 (RAG Application)

This DFD enumerates the primary processes, data stores, and data flows for a
Retrieval-Augmented Generation (RAG) application.

---

## External Entities
- **E1: End User**
- **E2: Admin / Operator** (optional, for management actions)

---

## Processes
- **P1: API / App** (request handling, auth, rate limiting)
- **P2: RAG Orchestrator** (retrieval + context assembly + response handling)
- **P3: Prompt Builder** (template + system instructions + guardrails)

- **P4: Embedding Service** (creates/query embeddings)
- **P5: LLM API** (model inference)

---

## Data Stores
- **D1: Vector Database** (embeddings + indexes)
- **D2: Document Store / Knowledge Base** (source docs, chunks)
- **D3: Secret Manager** (API keys, credentials)
- **D4: Logs / Monitoring Store** (application and audit logs)

---

## Trust Boundaries
- **TB1: Untrusted Input Boundary** (End User)
- **TB2: Application Runtime Boundary** (P1–P3)
- **TB3: AI Model Boundary** (P4–P5)
- **TB4: Retrieval / Knowledge Boundary** (D1–D2)
- **TB5: Identity & Secrets Boundary** (D3)
- **TB6: Monitoring Boundary** (D4)
- **TB7: Build → Runtime Boundary** (CI/CD → runtime config/code)

---

## Primary Data Flows

### F1 — User request / prompt
- **E1 → P1**
- Data: *user prompt, query parameters, session identifiers*

### F2 — AuthN/AuthZ (if applicable)
- **P1 → Identity Provider**
- Data: *tokens, claims, role / scope checks*

### F3 — Prompt assembly
- **P1 → P2 → P3**
- Data: *system prompt, developer instructions, user input*

### F4 — Retrieval query (embedding / vector search)
- **P2 → P4 → D1**
- Data: *embedding vectors, similarity query, filters*

### F5 — Context fetch
- **P2 → D2**
- Data: *documents/chunks, metadata, access constraints*

### F6 — LLM inference call
- **P3/P2 → P5**
- Data: *prompt + retrieved context + conversation history (if any)*

### F7 — Model output handling
- **P5 → P2 → P1 → E1**
- Data: *generated text, citations, structured output (if any)*

### F8 — Secrets retrieval
- **P1/P2/P3/P4/P5 → D3**
- Data: *API keys, credentials, encryption keys*

### F9 — Logging/telemetry
- **P1/P2/P3 → D4**
- Data: *request logs, traces, model outputs (sanitized), errors, audit events*

### F10 — Build/deploy
- **CI/CD → P1/P2/P3**
- Data: *code, prompt templates, configuration, policies*
