# TM-SC-01 — CI/CD Pipeline Supply Chain Threat Model

## Overview

Modern software delivery relies heavily on **CI/CD pipelines** to build, test, and deploy applications. While automation increases development velocity, it also introduces a critical **software supply chain attack surface**.

If attackers compromise any stage of the CI/CD pipeline, they may inject malicious code, tamper with build artifacts, or deploy compromised images into production environments.

This threat model analyzes common risks within the CI/CD pipeline and proposes security controls to mitigate them.

---

## Architecture Summary

The modeled CI/CD pipeline includes the following components:

```
Developer
   │
   ▼
Git Repository
   │
   ▼
CI/CD Pipeline
   │
   ▼
Build System
   │
   ▼
Artifact Repository
   │
   ▼
Container Registry
   │
   ▼
Production Environment
```

External dependencies such as **public package registries** may be accessed during the build process.

---

## Key Assets

The following assets must be protected:

* Source code repositories
* CI/CD pipeline configurations
* Build infrastructure
* Dependency packages
* Build artifacts
* Container images
* Deployment configurations
* Secrets and access tokens

Compromise of any of these assets could lead to **supply chain attacks affecting downstream environments**.

---

## Trust Boundaries

The architecture contains several trust boundaries:

**Developer Environment**

Workstations where developers create and commit code.

**Internal CI/CD Infrastructure**

Pipeline runners, build systems, and artifact repositories.

**External Dependency Sources**

Public package registries used during builds.

**Production Environment**

Cloud or container environments where the application is deployed.

Crossing these boundaries introduces additional security risks.

---

## Key Threat Scenarios

### Credential Theft

Attackers steal developer credentials and push malicious commits to the repository.

### Pipeline Trigger Abuse

Unauthorized triggering of pipelines to execute malicious builds.

### Dependency Confusion

Malicious packages published in public registries override internal dependencies.

### Secrets Exposure

Secrets stored in CI/CD configurations or logs are leaked.

### Artifact Tampering

Attackers modify artifacts stored in artifact repositories.

### Malicious Image Deployment

Compromised container images are deployed to production.

---

## Security Controls

The threat model highlights several key security controls.

### Source Code Protection

* Enforce multi-factor authentication for repository access
* Require signed commits
* Enable branch protection and pull request reviews

### CI/CD Pipeline Security

* Restrict pipeline triggers
* Use isolated CI runners
* Limit permissions of pipeline service accounts
* Secure secrets using dedicated secret management systems

### Dependency Security

* Implement dependency scanning
* Generate a Software Bill of Materials (SBOM)
* Pin dependency versions

### Artifact Integrity

* Sign build artifacts
* Verify artifact provenance
* Maintain immutable artifact repositories

### Container Security

* Scan container images for vulnerabilities
* Verify image signatures before deployment
* Implement admission policies in the runtime environment

---

## Diagram

The diagram below illustrates the CI/CD pipeline architecture, attack vectors, and security controls.

![CI/CD Supply Chain Threat Model](diagrams/supply-chain-ci-cd.png)

Legend:

* **Red arrows** represent potential attack vectors
* **Green arrows** represent security controls
* **Dotted boundaries** indicate trust boundaries

---

## Related Standards and Guidance

This threat model aligns with guidance from:

* Open Source Security Foundation
* OWASP Software Supply Chain Security
* Supply-chain Levels for Software Artifacts

---

## Goal

The goal of this threat model is to help security engineers systematically identify and mitigate risks in CI/CD pipelines and protect the integrity of the software supply chain.
