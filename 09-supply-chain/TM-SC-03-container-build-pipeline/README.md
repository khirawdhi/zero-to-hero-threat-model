# TM-SC-03 — Container Build Pipeline Threat Model

This threat model focuses on **security risks in container image build pipelines**, which are commonly used to package and deploy applications in modern cloud-native environments.

Container build pipelines typically pull **base images, application code, and dependencies**, then produce container images that are stored in registries and deployed to runtime environments such as Kubernetes clusters.

Because container images are widely reused and distributed, a compromise in the build pipeline can introduce malicious code into **multiple downstream environments**, making this a critical component of the **software supply chain**.

---

## Scope

* Dockerfile and container build configurations
* Base image retrieval from public or private registries
* Container image build processes in CI/CD pipelines
* Container image storage in registries
* Image distribution to deployment environments

---

## Out of scope

* Runtime container security in Kubernetes or container platforms
* Host operating system security for container nodes
* Infrastructure security for registry hosting

---

## Key assets

* Dockerfiles and container build configurations
* base container images
* application source code included in container builds
* container image layers
* container registry credentials
* generated container images stored in registries

---

## Typical Container Build Flow

A simplified container build pipeline:

```
Developer
   ↓
Source Code Repository
   ↓
CI/CD Pipeline
   ↓
Container Build System
   ↓
Container Image
   ↓
Container Registry
   ↓
Deployment Environment
```

During the build process, container images may pull **base images from external registries**, introducing additional supply chain risk.

---

## Security Objectives

The container build pipeline should ensure:

* integrity of container images
* trusted base images
* secure build environments
* protection of secrets used during builds
* verification of container images before deployment

---

## Related Threat Models

This model complements other supply chain threat models in this repository:

```
TM-SC-01 — CI/CD Pipeline Threat Model
TM-SC-02 — Dependency Management Threat Model
```

Together these models cover key risks across **modern software delivery pipelines**.
