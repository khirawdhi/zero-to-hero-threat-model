# Threat Model Index

This index provides a quick overview of all threat models, architecture patterns, and case studies available in this repository.

Use this page to quickly navigate to relevant systems.

---

# Cloud Architecture Threat Models

| Platform | Architecture                   | Path                                  |
| -------- | ------------------------------ | ------------------------------------- |
| Azure    | API Management + AKS + SQL     | 03-azure/TM-AZ-01-apim-aks-sql        |
| AWS      | CloudFront + API Gateway + EKS | 04-aws/TM-AWS-01-cloudfront-apigw-eks |
| GCP      | Cloud Armor + Apigee + GKE     | 05-gcp/TM-GCP-01-armor-apigee-gke     |

---

# AI Application Threat Models

| System           | Description                                 | Path               |
| ---------------- | ------------------------------------------- | ------------------ |
| RAG Pipeline     | Retrieval-augmented generation architecture | 06-ai-applications |
| AI Agent Systems | Tool-using AI agents                        | 06-ai-applications |

---

# A2A Integration Threat Models

| System                  | Description                           | Path   |
| ----------------------- | ------------------------------------- | ------ |
| Service-to-Service APIs | mTLS and OAuth service authentication | 07-a2a |
| Webhook Integrations    | External event integrations           | 07-a2a |

---

# Software Supply Chain Threat Models

| Threat Model             | Description                    | Path                                              |
| ------------------------ | ------------------------------ | ------------------------------------------------- |
| CI/CD Pipeline           | Secure build pipeline design   | 09-supply-chain/TM-SC-01-ci-cd-pipeline           |
| Dependency Management    | Dependency ecosystem threats   | 09-supply-chain/TM-SC-02-dependency-management    |
| Container Build Pipeline | Container image build security | 09-supply-chain/TM-SC-03-container-build-pipeline |
| Artifact Repository      | Artifact integrity and storage | 09-supply-chain/TM-SC-04-artifact-repository      |
| Deployment Pipeline      | Secure deployment pipelines    | 09-supply-chain/TM-SC-05-deployment-pipeline      |

---

# Security Architecture Patterns

| Pattern                          | Description                              | Path                                                               |
| -------------------------------- | ---------------------------------------- | ------------------------------------------------------------------ |
| Zero Trust Service Communication | Secure service-to-service authentication | 11-security-architecture-patterns/zero-trust-service-communication |
| Secure CI/CD Pipeline            | Secure software delivery pipelines       | 11-security-architecture-patterns/secure-ci-cd-pipeline-pattern    |
| Secure Data Pipeline             | Secure data processing architectures     | 11-security-architecture-patterns/secure-data-pipeline-pattern     |
| Secure AI System                 | Secure AI system architecture            | 11-security-architecture-patterns/secure-ai-system-pattern         |

---

# Security Case Studies

| Incident                    | Description                             | Path                                                 |
| --------------------------- | --------------------------------------- | ---------------------------------------------------- |
| Log4Shell Dependency Crisis | Dependency ecosystem attack analysis    | 12-security-case-studies/log4shell-dependency-crisis |
| Codecov CI/CD Breach        | Supply chain compromise via CI pipeline | 12-security-case-studies/codecov-ci-cd-breach        |
| Uber CI/CD Breach           | Internal pipeline compromise            | 12-security-case-studies/uber-ci-cd-breach           |
