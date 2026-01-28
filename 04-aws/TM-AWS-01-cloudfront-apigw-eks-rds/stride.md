# STRIDE Threat Analysis — TM-AWS-01 (Delta from Azure)

This STRIDE analysis focuses on **AWS-specific threats and differences**
relative to the Azure reference model (TM-AZ-01).

Common cloud-native threats (DoS, injection, authZ bypass, data leakage)
are inherited from the Azure model and not repeated here.

---

## AWS-Specific Threat Areas

### 1. Identity & Access (IAM / IRSA)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| S | IRSA misbinding allows wrong Kubernetes service account to assume IAM role | Cross-service data access | Strict OIDC trust conditions, per-service IAM roles, periodic review |
| E | Overly permissive IAM policies (`*`, wildcards) grant excessive access | Account or data compromise | Least-privilege IAM, policy boundaries, SCPs where applicable |
| S | Compromised pod abuses IAM role credentials | Lateral movement | Short session duration, scoped roles, monitor AssumeRole events |
| T | IAM trust policy modified maliciously | Privilege escalation | Change alerts on IAM policies, approvals for trust changes |

---

## 2. Metadata Service (IMDS)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| S | SSRF used to access IMDS credentials | Full IAM role compromise | Enforce IMDSv2, block link-local egress from pods |
| I | Credentials harvested and reused externally | Data breach | Scope IAM roles tightly, monitor anomalous API calls |
| E | Chained SSRF → IMDS → IAM → RDS/S3 | Full environment compromise | Defense-in-depth: WAF rules, egress controls, IRSA |

---

## 3. S3 (Data Plane Differences)

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| I | Public bucket or ACL misconfiguration | Data leakage | Block Public Access at account level, no ACLs |
| T | Object overwrite or deletion by mis-scoped role | Data integrity loss | Versioning, least-privilege IAM, MFA delete (where appropriate) |
| R | Insufficient access logging | Forensic gaps | Enable S3 access logs / CloudTrail data events |

---

## 4. API Gateway & CloudFront

| STRIDE | Threat Scenario | Impact | Recommended Mitigation |
|------|-----------------|--------|------------------------|
| D | API Gateway throttling misconfigured | Service outage | Explicit throttles per stage and per client |
| E | Missing authZ
