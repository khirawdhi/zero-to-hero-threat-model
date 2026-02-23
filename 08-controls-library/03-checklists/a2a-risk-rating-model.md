# A2A Integration Risk Rating Model
## OAuth / Service-to-Service Security Classification Framework

This model provides a structured method to classify Application-to-Application (A2A) integrations as **Low, Medium, or High Risk**.

It is intended for:
- Architecture reviews
- Partner onboarding
- Production approval decisions
- Security exception handling

---

# 1. Risk Scoring Method

Each category is scored:

- **1 = Low Risk**
- **2 = Moderate Risk**
- **3 = High Risk**

Add all category scores to determine overall classification.

---

# 2. Risk Categories

## A. Identity & Token Risk

| Condition | Score |
|------------|-------|
| Short-lived JWT, strict validation (iss, aud, exp, scope) | 1 |
| JWT validation present but scopes broad | 2 |
| Static API keys or long-lived tokens | 3 |

---

## B. Authorization Complexity

| Condition | Score |
|------------|-------|
| Fine-grained, least-privilege scopes | 1 |
| Broad role-based access | 2 |
| Single global scope or no action-level enforcement | 3 |

---

## C. Data Sensitivity

| Condition | Score |
|------------|-------|
| Non-sensitive metadata | 1 |
| Business-sensitive data | 2 |
| PII, financial, healthcare, or regulated data | 3 |

---

## D. Network Exposure

| Condition | Score |
|------------|-------|
| Private network only | 1 |
| Public endpoint with strict controls | 2 |
| Public endpoint without strong restrictions | 3 |

---

## E. Webhook Exposure (If Applicable)

| Condition | Score |
|------------|-------|
| Signed + replay-protected | 1 |
| Signed but no replay detection | 2 |
| Unsigned or unverified | 3 |

If webhooks are not used → score 1.

---

## F. Egress Controls

| Condition | Score |
|------------|-------|
| Strict outbound allowlist | 1 |
| Partial outbound filtering | 2 |
| Default allow outbound | 3 |

---

## G. Partner Trust Level

| Condition | Score |
|------------|-------|
| Internal service | 1 |
| Known partner with contractual controls | 2 |
| External unknown or multi-tenant third party | 3 |

---

## H. Operational Maturity

| Condition | Score |
|------------|-------|
| Correlation IDs + monitoring + alerting | 1 |
| Logging present but weak alerting | 2 |
| Minimal logging | 3 |

---

# 3. Risk Classification

Add all category scores.

| Total Score | Risk Level | Required Action |
|-------------|-----------|----------------|
| 8–12 | Low | Standard baseline controls sufficient |
| 13–17 | Medium | Additional controls required + review |
| 18–24 | High | Security architecture approval required |

---

# 4. Mandatory Escalation Conditions

Regardless of total score, automatic escalation required if:

- Regulated data involved
- Cross-tenant access enabled
- High-value financial transactions
- Write access to production systems
- Third-party webhook ingestion without replay protection

---

# 5. Required Controls by Risk Tier

## Low Risk

Minimum required:
- IAM-02 (Token Validation Discipline)
- NET-01 (Egress Control)
- SC-03 (Secrets Handling in CI/CD)
- OBS-02 (Correlation ID Propagation)

---

## Medium Risk

All Low controls plus:
- A2A-02 (Webhook Signing & Replay Protection)
- OBS-01 (Audit Logging)
- Tenant isolation controls
- Scope restriction review

---

## High Risk

All Medium controls plus:
- mTLS or token binding (DPoP/mTLS-bound tokens)
- Per-tenant scoped tokens
- Anomaly detection on token issuance
- Manual approval workflow for sensitive operations
- Security architecture board review

---

# 6. Review Record

Integration Name:
Environment:
Partner:
Total Score:
Risk Tier:
Compensating Controls:
Reviewer:
Approval Date:

---

# 7. Design Principle

Risk classification ensures that **control depth matches integration impact**.

The objective is proportional security — not maximum friction.
