# Zero-to-Hero Threat Modeling Playbook

![License](https://img.shields.io/badge/license-MIT-blue)
![Security Architecture](https://img.shields.io/badge/focus-Security%20Architecture-purple)
![Cloud](https://img.shields.io/badge/cloud-AWS%20|%20Azure%20|%20GCP-blue)
![AI Security](https://img.shields.io/badge/AI-LLM%20Security-green)

A practical, architecture-first threat modeling playbook for modern systems.

> **Security failures happen at trust boundaries, not components.**

---

## What You'll Find

- Cloud-native architectures
- AI / LLM & RAG security
- Service-to-service trust (OAuth, mTLS)
- Software supply chain security
- Reusable threat modeling patterns

Each threat model includes:

- Architecture diagrams
- Trust boundaries
- STRIDE analysis
- Security controls
- Validation test plans

---

## Featured Threat Models

### AI Security
- RAG Applications
- AI Agents with Tools

Covers prompt injection, retrieval poisoning, tool abuse, and data leakage.

### Service-to-Service Security
- OAuth Client Credentials
- mTLS Service Mesh

Covers identity, authentication, and secure communication.

### Software Supply Chain
- CI/CD Pipelines
- Dependency Management
- Container Build Pipelines
- Artifact Repositories
- Deployment Pipelines

Covers dependency trust, artifact integrity, provenance, and pipeline security.

---

## Core Principles

- Architecture before controls
- Threats emerge at trust boundaries
- STRIDE applied to data flows
- Security controls must be testable
- Security is continuous, not a checklist

---

## Repository Structure

```text
00-getting-started
01-templates
02-reference-architectures
03-azure
04-aws
05-gcp
06-ai-applications
07-a2a
08-controls-library
09-supply-chain
10-threat-modeling-methodology
11-security-architecture-patterns
12-security-case-studies
```

---

## Who It's For

- Product Security Engineers
- Security Architects
- Cloud & Platform Engineers
- Developers building distributed systems

---

## License

MIT
