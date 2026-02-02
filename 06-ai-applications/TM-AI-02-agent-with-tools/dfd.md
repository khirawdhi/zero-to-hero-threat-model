# Data Flow Diagram (DFD) — TM-AI-02 (Agent + Tools)

This DFD models an agentic AI system where the LLM can propose tool calls
and the application executes actions via a policy-gated tool executor.

---

## External Entities
- **E1: End User**
- **E2: Admin / Operator**
- **E3: External Tools / APIs** (3rd party or internal services)

---

## Processes
- **P1: API / App** (request handling, auth, rate limiting)
- **P2: Agent Orchestrator** (planning, state mgmt, tool selection logic)
- **P3: Prompt Builder** (system prompt + templates + guardrails)
- **P4: Policy Engine** (authorization, allowlists, constraints, approvals)
- **P5: Tool Adapters** (protocol translation, parameter shaping)
- **P6: Tool Executor** (executes approved calls, handles retries/timeouts)

- **P7: LLM API** (inference / reasoning)

---

## Data Stores
- **D1: Memory / State Store** (conversation state, plans, intermediate results)
- **D2: Vector DB** (optional retrieval)
- **D3: Document Store / Knowledge Base** (optional retrieval)
- **D4: Data Stores** (business data accessed by tools)
- **D5: Secret Manager** (API keys, credentials)
- **D6: Logs / Monitoring Store** (telemetry + audit logs)

---

## Trust Boundaries
- **TB1: Untrusted Input Boundary** (E1)
- **TB2: Application Runtime Boundary** (P1–P4)
- **TB3: AI Model Boundary** (P7)
- **TB4: Tooling Execution Boundary** (P5–P6, E3)
- **TB5: Retrieval/Knowledge Boundary** (D2–D3)
- **TB6: Identity & Secrets Boundary** (D5)
- **TB7: Monitoring Boundary** (D6)
- **TB8: Build → Runtime Boundary** (CI/CD → runtime code/config)

> Critical boundary: **Model Output → Action Decision** happens when P2/P4
> interprets LLM output as a proposed action.

---

## Primary Data Flows

### F1 — User intent
- **E1 → P1**
- Data: *user goal, natural language instruction, context*

### F2 — AuthN/AuthZ
- **P1 → Identity Provider**
- Data: *tokens, claims, scopes/roles*

### F3 — Agent planning prompt
- **P1 → P2 → P3 → P7**
- Data: *system prompt + user intent + relevant context/state*

### F4 — Tool invocation proposal (LLM output)
- **P7 → P2**
- Data: *proposed tool name, parameters, justification*

### F5 — Policy evaluation
- **P2 → P4**
- Data: *proposed action + user identity + constraints*

### F6 — Approved action to executor
- **P4 → P6**
- Data: *approved tool call, validated parameters, limits*

### F7 — Tool execution
- **P6 → P5 → E3**
- Data: *API call / action request*

### F8 — Tool result returned
- **E3 → P5 → P6 → P2**
- Data: *result, status, errors*

### F9 — Agent observation to LLM (optional loop)
- **P2 → P7**
- Data: *tool result + next step prompt*

### F10 — Final response
- **P2 → P1 → E1**
- Data: *response to user (text/structured output)*

### F11 — Memory/state update
- **P2 → D1**
- Data: *conversation state, action traces, summaries*

### F12 — Retrieval (optional RAG)
- **P2 → D2/D3**
- Data: *vector query, retrieved context*

### F13 — Secrets retrieval
- **P1–P6 → D5**
- Data: *credentials, API keys*

### F14 — Logging/audit
- **P1–P6 → D6**
- Data: *request IDs, action approvals, tool calls, outcomes (sanitized)*
