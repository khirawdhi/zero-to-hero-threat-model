# Security Controls Baseline — TM-AZ-01

This document defines the **minimum required security controls** for the
APIM → AKS → Azure SQL architecture.

These controls are intended to be **reusable across similar systems**.

---

## 1. Identity & Access Management

### Controls
- OAuth2/OIDC enforced at Azure APIM
- Strict token validation (issuer, audience, expiry, signature)
- Short-lived access tokens; refresh token rotation
- Per-service managed identities for AKS workloads
- Least-privilege RBAC for:
  - AKS workloads
  - Data plane access
  - CI/CD deployment identities
- MFA enforced for admins
- Privileged access managed via JIT / PIM

### Threats Addressed
- Spoofing
- Elevation of Privilege
- Unauthorized access

---

## 2. Network & Edge Security

### Controls
- Azure WAF enabled with managed + custom rules
- Rate limiting and quotas at APIM
- Only APIM exposed publicly; AKS not directly internet-facing
- Private endpoints for Azure SQL and Blob Storage
- Egress controls to restrict outbound traffic where possible

### Threats Addressed
- Denial of Service
- Information Disclosure
- Lateral movement

---

## 3. Application & Runtime Security (AKS)

### Controls
- Namespace isolation between application and platform components
- Resource requests/limits for pods
- Horizontal Pod Autoscaling for burst protection
- Ingress allowlists and deny-by-default policies
- Defense-in-depth authorization checks inside services
- No secrets in images, configmaps, or source control

### Threats Addressed
- Denial of Service
- Elevation of Privilege
- Tampering

---

## 4. Data Security

### Controls
- Encryption at rest and in transit for SQL and Blob Storage
- Least-privilege access to databases and storage
- SQL auditing and storage access logs enabled
- Tenant isolation (row-level security or equivalent where applicable)
- Input validation and parameterized queries

### Threats Addressed
- Information Disclosure
- Tampering
- Repudiation

---

## 5. Secrets Management

### Controls
- Azure Key Vault used for all secrets and keys
- Access via managed identity only
- Secret versioning enabled
- Alerts on secret access and modifications
- No secrets logged or exposed via environment variables

### Threats Addressed
- Spoofing
- Information Disclosure
- Tampering

---

## 6. Logging, Monitoring & Audit

### Controls
- Centralized logging via Azure Monitor / Log Analytics
- Correlation IDs propagated from APIM through services
- Admin and data access audit logs retained immutably
- Alerts for:
  - Authentication anomalies
  - Excessive errors
  - Access to sensitive data
- Log redaction for PII and tokens

### Threats Addressed
- Repudiation
- Information Disclosure

---

## 7. CI/CD & Supply Chain Security

### Controls
- Protected branches and mandatory reviews
- Dependency scanning (SCA) and static analysis (SAST)
- Image scanning and signing
- SBOM generation and retention
- Least-privilege RBAC for deployment tooling
- Separate build and deploy identities

### Threats Addressed
- Tampering
- Elevation of Privilege
- Supply chain compromise
