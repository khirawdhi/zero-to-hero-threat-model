# STRIDE Threat Analysis — TM-GCP-01 (Delta from Azure/AWS)

This STRIDE analysis documents **GCP-specific threats and differences**
relative to the Azure and AWS reference models.

Common cloud-native threats (DoS, injection, generic authZ bypass,
basic data leakage) are inherited and not repeated here.

---

## 1. Identity & Workload Identity (IAM)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| S | Workload Identity misbinding allows GKE service account to impersonate unintended IAM service account | Cross-service or cross-project access | Enforce one-to-one mapping, restrict `iam.serviceAccountTokenCreator`, periodic review |
| E | Use of primitive roles (Owner/Editor) grants excessive privileges | Project or org compromise | Avoid primitive roles, use predefined/custom roles |
| S | Service account key misuse (static keys leaked) | Long-lived credential compromise | Disable service account keys, enforce workload identity |
| T | IAM policy modified without review | Privilege escalation | Org-level policy change alerts, approval workflows |

---

## 2. Data Perimeter & Exfiltration (VPC Service Controls)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| I | Missing VPC Service Controls allows data exfiltration to attacker-controlled projects | Large-scale data breach | Enforce VPC SC around Cloud SQL, GCS, BigQuery |
| E | Privileged identity bypasses perimeter controls | Perimeter collapse | Access levels + context-aware policies, break-glass monitoring |
| R | Insufficient logging on perimeter violations | Forensic gaps | Centralize VPC SC violation logs and alerts |

---

## 3. Cloud Storage (GCS)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| I | Public bucket exposure due to IAM or ACL misconfiguration | Data leakage | Enforce Public Access Prevention, disable ACLs |
| T | Object overwrite or deletion by mis-scoped role | Data integrity loss | Least-privilege IAM, object versioning |
| R | Missing data access logs | Forensic gaps | Enable Cloud Audit Logs (Data Access) |

---

## 4. Apigee / API Gateway

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| E | Missing or inconsistent authZ policies across proxies | Privilege escalation | Centralized authZ policies, deny-by-default |
| D | Rate limits not enforced at proxy or product level | Service degradation | Per-product and per-client quotas |
| I | Sensitive headers or query params logged | Data exposure | Header normalization, log scrubbing |

---

## 5. Observability (Cloud Logging & Monitoring)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| I | Tokens, secrets, or PII logged | Data leakage | Log redaction, never log auth artifacts |
| R | Logs not retained centrally across projects | Forensic gaps | Org-level log sinks and retention policies |
