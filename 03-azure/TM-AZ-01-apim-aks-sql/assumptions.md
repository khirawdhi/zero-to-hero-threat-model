# Threat Modeling Assumptions — TM-AZ-01

This threat model is valid only under the assumptions documented below.
If any assumption changes, the threat model must be reviewed and updated.

---

## 1. Architectural Assumptions
- Azure API Management is the **only** public entry point to the application
- Azure WAF is correctly deployed in front of APIM and actively enforced
- AKS is not directly exposed to the public internet
- All communication between components uses TLS
- Azure SQL and Blob Storage are accessed only via private endpoints
- Azure Key Vault is the sole system for secrets and key management
- AKS workloads use managed identity for cloud resource access
- No shared identities are used across unrelated services

---

## 2. Identity & Access Assumptions
- Azure Entra ID is the authoritative identity provider
- OAuth2/OIDC flows are correctly configured and maintained
- Token lifetimes, audiences, and issuers are configured securely
- Admin access is protected by MFA and privileged access workflows
- Service principals and managed identities are reviewed periodically

---

## 3. Operational Assumptions
- CI/CD pipelines are secured and access-controlled
- Only signed and approved artifacts are deployed to production
- Logging, monitoring, and alerting are operational and monitored
- Incident response processes exist and are tested
- Backups for data stores are enabled and regularly tested

---

## 4. Explicit Non-Goals
The following are intentionally out of scope:
- End-user device security
- Physical data center security
- Insider threats beyond privileged access abuse
- Legacy systems not represented in the architecture
- Third-party services outside defined integrations
