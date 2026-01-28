# Security Test Plan — TM-AZ-01

This test plan validates that the defined security controls are correctly
implemented and effective.

---

## 1. Identity & Access Tests
- Verify APIM rejects tokens with:
  - Wrong issuer
  - Wrong audience
  - Expired signatures
- Verify AKS workloads cannot access resources outside assigned identity
- Verify admin access requires MFA and JIT approval

---

## 2. Edge & API Tests
- Send malformed and oversized requests to APIM and confirm rejection
- Verify rate limits trigger under load
- Validate WAF blocks common injection and traversal patterns

---

## 3. Runtime & Authorization Tests
- Attempt to access protected endpoints without required roles/scopes
- Verify services enforce authorization independently of APIM
- Test resource exhaustion scenarios and confirm autoscaling

---

## 4. Data Security Tests
- Verify SQL and Blob are inaccessible from public internet
- Attempt unauthorized data access and confirm denial
- Validate SQL auditing and storage access logs are generated

---

## 5. Secrets Management Tests
- Verify secrets are not present in pod environment variables
- Confirm only authorized workloads can access Key Vault secrets
- Rotate a secret and confirm application behavior

---

## 6. Logging & Audit Tests
- Confirm correlation IDs appear across APIM, AKS, and data logs
- Verify sensitive data is redacted from logs
- Validate alerts trigger on suspicious access patterns

---

## 7. CI/CD & Supply Chain Tests
- Attempt unauthorized deployment and confirm failure
- Verify only signed images are deployable
- Confirm SBOM and scan reports are generated per build
