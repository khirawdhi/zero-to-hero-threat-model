# Threat Modeling Assumptions — TM-AI-02 (Agent + Tools)

---

## 1. Architectural Assumptions
- The LLM cannot directly execute tools; all tool calls go through policy + executor
- Tool endpoints and capabilities are allowlisted
- The agent maintains state/memory to support multi-step workflows

---

## 2. Identity & Authorization Assumptions
- Users authenticate through a trusted identity provider
- Authorization is enforced server-side before any tool execution
- High-risk actions require step-up auth or human approval

---

## 3. Tooling Assumptions
- Tools can create real side effects (writes/changes), not just read operations
- Tool executor runs in a restricted network environment with egress controls
- Tool parameters are validated against strict schemas

---

## 4. Operational Assumptions
- All tool actions produce immutable audit logs
- CI/CD is protected and changes to policies/allowlists require review
- Logs are sanitized and access-controlled

---

## 5. Explicit Non-Goals
- Securing model training pipelines or model weights
- Preventing all jailbreak attempts (goal is containment via policy enforcement)
- Fully autonomous self-modifying agents
