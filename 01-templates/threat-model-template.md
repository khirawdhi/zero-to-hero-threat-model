# Threat Model: <System Name>

## 1. Overview
**System description:**  
Briefly describe what this system does and why it exists.

**Business impact:**  
What happens if this system is compromised, unavailable, or leaks data?

**Threat model scope:**
- In scope:
- Out of scope:

---

## 2. Architecture Summary
**Architecture type:**
- Cloud-native / Event-driven / Data pipeline / AI / A2A

**Key components:**
- External users / systems
- Entry points (API, UI, events)
- Core services
- Data stores
- Third-party integrations

---

## 3. Trust Boundaries
List all trust boundaries explicitly.

Examples:
- Internet → Cloud edge
- Edge → Application services
- Service → Data store
- Application → Third-party service
- CI/CD → Production

---

## 4. Data Flow Diagram (DFD)
**Diagram:** `diagram.png`

**Key data flows:**
1. User → API Gateway (auth request)
2. API Gateway → Backend service
3. Service → Database
4. Service → External API
5. Async events (if any)

---

## 5. STRIDE Threat Analysis

| Component / Flow | STRIDE | Threat Scenario | Impact | Existing Controls | Recommended Mitigation |
|------------------|--------|-----------------|--------|-------------------|------------------------|
|                  |        |                 |        |                   |                        |

---

## 6. Abuse Cases (Optional but powerful)
Describe how an attacker might intentionally misuse functionality.

Example:
- Valid partner abuses API scope to extract excessive data
- Authenticated user triggers expensive operations repeatedly

---

## 7. Risk Rating
Define your risk logic (simple is fine).

Example:
- High: Data breach, privilege escalation, cross-tenant impact
- Medium: Single-user impact, partial DoS
- Low: Minor info disclosure, noisy logs

---

## 8. Mitigation Plan
Summarize **top 5–10 actions** that materially reduce risk.

---

## 9. Open Questions
- Unknown assumptions
- Design decisions pending confirmation
- Dependencies on other teams

---

## 10. Review & Ownership
- Threat model owner:
- Reviewers:
- Last updated:
