# AI System Controls Mapping

This document maps common **AI and LLM system threats** to recommended security controls.

The controls apply to systems such as:

* Retrieval-Augmented Generation (RAG)
* AI agents
* tool-integrated LLM systems
* model inference APIs

---

## Prompt Injection

| Threat                          | Control                  |
| ------------------------------- | ------------------------ |
| Prompt injection attacks        | Input validation         |
| Malicious instructions to tools | Tool access restrictions |
| Hidden instructions in data     | Context filtering        |

---

## Data Leakage

| Threat                  | Control           |
| ----------------------- | ----------------- |
| Sensitive data exposure | Data redaction    |
| Training data leakage   | Dataset filtering |
| Prompt data exposure    | Context isolation |

---

## Model Abuse

| Threat                  | Control            |
| ----------------------- | ------------------ |
| Unauthorized API access | API authentication |
| Model misuse            | Rate limiting      |
| Resource exhaustion     | Request quotas     |

---

## Tool Abuse

| Threat                      | Control                 |
| --------------------------- | ----------------------- |
| Unauthorized tool execution | Tool allowlist          |
| External API abuse          | Access restrictions     |
| Command injection           | Strict input validation |

---

## Monitoring and Safety

| Threat             | Control           |
| ------------------ | ----------------- |
| Undetected misuse  | Usage monitoring  |
| Abusive prompts    | Prompt monitoring |
| Model exploitation | AI safety filters |
