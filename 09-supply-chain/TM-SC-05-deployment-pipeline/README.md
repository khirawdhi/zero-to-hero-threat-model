# TM-SC-05 — Deployment Pipeline Threat Model

This threat model focuses on **security risks within software deployment pipelines**, which are responsible for delivering built artifacts from repositories to runtime environments such as cloud infrastructure or container orchestration platforms.

Deployment pipelines are the final stage of the **software supply chain**, where previously built and stored artifacts are promoted to staging or production environments.

Because deployment pipelines typically possess **high-privilege credentials and direct access to production systems**, they are an attractive target for attackers seeking to introduce malicious software into operational environments.

---

## Scope

* automated deployment pipelines triggered by CI/CD systems
* artifact retrieval from artifact repositories or container registries
* deployment automation tools and scripts
* infrastructure configuration used for deployments
* credentials used to access runtime environments

Common deployment systems include:

* Kubernetes deployment pipelines
* infrastructure-as-code deployment tools
* automated release pipelines in CI/CD platforms

---

## Out of scope

* build pipeline security (covered in **TM-SC-01**)
* dependency supply chain risks (covered in **TM-SC-02**)
* container build processes (covered in **TM-SC-03**)
* artifact repository security (covered in **TM-SC-04**)

---

## Key assets

* deployment pipeline configurations
* deployment automation scripts
* infrastructure credentials
* container images or deployment artifacts
* environment configuration files

---

## Typical Deployment Flow

A simplified deployment pipeline:

```
Artifact Repository / Container Registry
        ↓
Deployment Pipeline
        ↓
Infrastructure / Orchestrator
        ↓
Runtime Environment
```

Deployment pipelines typically retrieve trusted artifacts and deploy them to infrastructure platforms such as Kubernetes clusters or cloud environments.

---

## Security Objectives

Deployment pipelines must ensure:

* only trusted artifacts are deployed
* deployment credentials are protected
* infrastructure changes are auditable
* unauthorized deployments are prevented
* deployments are traceable and reversible

---

## Related Threat Models

This model complements other supply chain threat models in the repository:

```
TM-SC-01 — CI/CD Pipeline Threat Model
TM-SC-02 — Dependency Management Threat Model
TM-SC-03 — Container Build Pipeline Threat Model
TM-SC-04 — Artifact Repository Threat Model
```

Together these models represent the **end-to-end security of the modern software supply chain**.
