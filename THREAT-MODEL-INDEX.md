# Threat Model Index

This index helps readers quickly locate threat models and architecture patterns within the **Zero-to-Hero Threat Modeling Playbook**.

Threat models are organized by **system type and security domain**.

---

# Cloud Platforms

| Section  | Description                                  |
| -------- | -------------------------------------------- |
| 03-azure | Threat models for Azure architectures        |
| 04-aws   | Threat models for AWS systems                |
| 05-gcp   | Threat models for Google Cloud architectures |

---

# AI Systems

| Section            | Description                                                |
| ------------------ | ---------------------------------------------------------- |
| 06-ai-applications | Threat models for AI pipelines, RAG systems, and AI agents |

---

# Application-to-Application Integrations

| Section | Description                                                                    |
| ------- | ------------------------------------------------------------------------------ |
| 07-a2a  | Threat models for service-to-service communication, APIs, and B2B integrations |

---

# Security Controls

| Section             | Description                                      |
| ------------------- | ------------------------------------------------ |
| 08-controls-library | Common security controls mapped to threat models |

---

# Software Supply Chain Security

| Threat Model | Description                           |
| ------------ | ------------------------------------- |
| TM-SC-01     | CI/CD Pipeline Threat Model           |
| TM-SC-02     | Dependency Management Threat Model    |
| TM-SC-03     | Container Build Pipeline Threat Model |
| TM-SC-04     | Artifact Repository Threat Model      |
| TM-SC-05     | Deployment Pipeline Threat Model      |

Location:

```text
09-supply-chain/
```

---

# Security Architecture Patterns

Reusable security design patterns:

| Pattern                          | Description                          |
| -------------------------------- | ------------------------------------ |
| Secure API Gateway Pattern       | Secure microservice entry points     |
| Zero-Trust Service Communication | Identity-based service communication |
| Secure CI/CD Pipeline Pattern    | Secure software delivery pipelines   |
| Secure Data Pipeline Pattern     | Secure data processing architectures |
| Secure AI System Pattern         | Secure architecture for AI systems   |

Location:

```text
11-security-architecture-patterns/
```

---

# Security Case Studies

Real-world security incidents analyzed using threat modeling principles.

| Case Study                     | Description                                        |
| ------------------------------ | -------------------------------------------------- |
| SolarWinds Supply Chain Attack | Build pipeline compromise                          |
| Log4Shell Dependency Crisis    | Dependency vulnerability exploitation              |
| Codecov CI/CD Breach           | Pipeline integration compromise                    |
| Uber CI/CD Breach              | Identity compromise and internal access escalation |

Location:

```text
12-security-case-studies/
```

---

# Methodology

Threat modeling methodology and guides are located in:

```text
10-threat-modeling-methodology/
```

These documents explain:

* how to build threat models
* how to apply STRIDE
* how to evaluate security risks
* how to perform architecture reviews
