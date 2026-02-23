# AI-04: Agent Tool Policy Enforcement

## Control Goal

Ensure LLM agents cannot execute unauthorized or unsafe tools.

---

## Threats Mitigated

- Elevation of Privilege
- Prompt Injection
- Data Exfiltration
- Lateral Movement

---

## Control Description

Tool execution must be gated by explicit policy checks:

- Role-based or scope-based authorization
- Tool-level allowlists
- Argument validation
- Runtime approval layer (if high risk)

The LLM must never directly execute tools.

---

## Implementation Guidance

- Separate reasoning layer from execution layer.
- Use structured tool calls (JSON schema).
- Enforce allowlist of callable tools.
- Log tool invocation decisions.
- Apply least privilege to tool credentials.

---

## Validation / Test Cases

- Prompt injection attempt → tool must not execute.
- User without privilege → tool must be blocked.
- Malformed tool arguments → must fail validation.

---

## Evidence Artifacts

- Tool execution logs
- Policy engine configuration
- Access control rules
- Audit of tool usage

---

## Common Failure Modes

- LLM directly controlling system calls
- No argument validation
- Over-privileged tool credentials
- No logging of tool calls

---

## Cloud Mapping

Azure OpenAI + function calling policy  
AWS Bedrock + Lambda control layer  
GCP Vertex AI + policy enforcement wrapper
