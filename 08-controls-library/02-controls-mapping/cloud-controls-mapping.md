# Cloud Architecture Controls Mapping

This document maps common **cloud architecture threats** to recommended security controls.

These controls apply to cloud platforms such as:

* AWS
* Azure
* GCP

The mapping can be used when performing threat modeling for cloud-native systems.

---

## Identity and Access Management

| Threat                             | Control                                |
| ---------------------------------- | -------------------------------------- |
| Unauthorized service access        | Strong IAM policies                    |
| Overprivileged identities          | Least privilege access                 |
| Credential compromise              | MFA and short-lived credentials        |
| Cross-service privilege escalation | Identity isolation and role separation |

---

## Network Security

| Threat                               | Control                 |
| ------------------------------------ | ----------------------- |
| Unauthorized network access          | VPC / VNet segmentation |
| Lateral movement                     | Network security groups |
| Public exposure of internal services | Private endpoints       |
| Man-in-the-middle attacks            | TLS encryption          |

---

## Secrets Management

| Threat                         | Control                     |
| ------------------------------ | --------------------------- |
| Secrets leakage in code        | Secrets manager             |
| Hardcoded credentials          | Secret injection at runtime |
| Unauthorized access to secrets | RBAC and access policies    |

---

## Logging and Monitoring

| Threat                     | Control             |
| -------------------------- | ------------------- |
| Undetected compromise      | Centralized logging |
| Privileged misuse          | Audit logs          |
| Delayed incident detection | Security monitoring |

---

## Infrastructure Integrity

| Threat                     | Control                            |
| -------------------------- | ---------------------------------- |
| Infrastructure tampering   | Infrastructure-as-code             |
| Misconfiguration           | Automated configuration validation |
| Drift in security settings | Continuous compliance monitoring   |
