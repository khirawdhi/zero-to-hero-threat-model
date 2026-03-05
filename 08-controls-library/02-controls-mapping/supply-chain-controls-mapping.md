# Software Supply Chain Controls Mapping

This document maps common **software supply chain threats** to recommended security controls.

The mapping applies to systems involved in the **software delivery lifecycle**, including:

* dependency management
* CI/CD pipelines
* container build pipelines
* artifact repositories
* deployment systems

---

## Dependency Security

| Threat                  | Control                      |
| ----------------------- | ---------------------------- |
| Dependency confusion    | Internal package namespaces  |
| Malicious packages      | Dependency scanning          |
| Vulnerable dependencies | Automated dependency updates |

---

## CI/CD Pipeline Security

| Threat                          | Control                         |
| ------------------------------- | ------------------------------- |
| Pipeline compromise             | Restricted pipeline permissions |
| Secret exposure                 | Secure secret storage           |
| Unauthorized pipeline execution | Pipeline access controls        |

---

## Build Integrity

| Threat                  | Control                     |
| ----------------------- | --------------------------- |
| Build tampering         | Reproducible builds         |
| Build system compromise | Isolated build environments |
| Artifact manipulation   | Build verification          |

---

## Artifact Security

| Threat                       | Control                         |
| ---------------------------- | ------------------------------- |
| Artifact tampering           | Artifact signing                |
| Unauthorized artifact access | Access control policies         |
| Malicious artifact injection | Artifact integrity verification |

---

## Deployment Security

| Threat                           | Control                     |
| -------------------------------- | --------------------------- |
| Malicious deployment             | Deployment approvals        |
| Unauthorized environment changes | Environment access controls |
| Production compromise            | Deployment monitoring       |
