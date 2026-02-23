# SC-03: Secrets Handling in CI/CD

## Control Goal

Prevent credential exposure via build pipelines.

---

## Threats Mitigated

- Credential leakage
- Privilege escalation
- Supply chain compromise

---

## Control Description

CI/CD pipelines must:

- Use ephemeral credentials
- Avoid static secrets in config files
- Restrict secret scope
- Mask secrets in logs
- Enforce protected branches

---

## Implementation Guidance

- Use OIDC-based federation when possible.
- Restrict pipeline roles.
- Disable secret printing.
- Rotate secrets automatically.

---

## Validation / Test Cases

- Attempt echo secret → should be masked.
- Attempt unauthorized pipeline access → must fail.
- Verify secret rotation schedule.

---

## Evidence Artifacts

- Pipeline configuration
- Secret store config
- Audit logs

---

## Common Failure Modes

- Hardcoded credentials
- Long-lived pipeline tokens
- Shared credentials across environments

---

## Cloud Mapping

Azure DevOps + Managed Identity  
GitHub Actions + OIDC  
AWS CodePipeline + IAM roles  
GCP Cloud Build + Workload Identity
