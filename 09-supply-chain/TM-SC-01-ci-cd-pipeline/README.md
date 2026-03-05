# TM-SC-01 — CI/CD Pipeline Threat Model

This threat model focuses on **security risks within Continuous Integration and Continuous Deployment (CI/CD) pipelines**, which are critical components of modern software delivery systems.

CI/CD pipelines automate the process of building, testing, packaging, and deploying software. Because they interact with **source code, build systems, dependency registries, artifact repositories, and production environments**, they represent a high-value target in the **software supply chain**.

This model examines risks introduced through:

* source code repositories and commit workflows
* automated build and test pipelines
* dependency retrieval during builds
* artifact storage and container registries
* automated deployment to runtime environments

---

## Scope

* Source code commits triggering pipeline execution
* CI/CD pipeline configuration and execution environments
* Build systems and dependency resolution during builds
* Artifact repositories and container registries
* Automated deployment mechanisms to staging or production environments

---

## Out of scope

* Runtime application vulnerabilities in deployed services
* Infrastructure threat models for underlying cloud platforms
* Detailed dependency security risks (covered in **TM-SC-02 — Dependency Management Threat Model**)

---

## Key assets

* source code repositories
* CI/CD pipeline configurations and workflow definitions
* build scripts and automation tools
* dependency manifests and build dependencies
* build artifacts and container images
* secrets and credentials used by pipelines
* deployment configurations and environment variables

---

## Typical CI/CD Pipeline Flow

A simplified CI/CD pipeline architecture typically includes:

```
Developer
   ↓
Git Repository
   ↓
CI/CD Pipeline
   ↓
Build System
   ↓
Artifact Repository
   ↓
Container Registry
   ↓
Production Environment
```

External package registries may also be accessed during the build phase for dependency resolution.

---

## Security Objectives

The CI/CD pipeline must ensure:

* integrity of source code and build artifacts
* authenticity of dependencies used during builds
* protection of secrets and credentials within pipelines
* controlled deployment of trusted artifacts
* traceability and auditability of pipeline actions

---

## Related Threat Model

This threat model complements:

```
TM-SC-02 — Dependency Management Threat Model
```

which focuses specifically on risks introduced through **third-party software dependencies and package registries**.

Together, these models address key areas of **software supply chain security** within modern development pipelines.
