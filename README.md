# Zero-to-Hero Threat Modeling Playbook

![License](https://img.shields.io/badge/license-MIT-blue)
![Focus](https://img.shields.io/badge/focus-security--architecture-purple)
![Cloud](https://img.shields.io/badge/cloud-AWS%20%7C%20Azure%20%7C%20GCP-blue)
![AI Security](https://img.shields.io/badge/AI-LLM%20Security-green)
![Supply Chain](https://img.shields.io/badge/security-Supply%20Chain-orange)

---

## Why This Exists

Most modern systems are **insecure by design**.

Not because engineers ignore security —
but because **threat modeling is treated as a checklist instead of an architectural discipline**.

Security failures don’t happen inside components.

> **They happen at trust boundaries.**

This repository exists to fix that.

---

## What This Is

A **pattern-first, architecture-driven threat modeling playbook** for:

* Cloud-native systems (microservices, APIs, data pipelines)
* AI systems (RAG, agents, tool-integrated LLMs)
* Service-to-service systems (A2A, APIs, webhooks)
* Software supply chains (CI/CD, dependencies, artifacts)

This is not theoretical guidance.

This is how **real systems should be designed securely**.

---

## Flagship Threat Models (Start Here)

If you are evaluating this repository, **start here**.

These represent **real-world, system-level security design**.

---

### AI Security — RAG + Agents

[Explore AI Threat Models](./06-ai-applications)

* Prompt injection attack paths
* Tool execution trust boundaries
* Data exfiltration via LLM context
* LLM treated as **untrusted component**

---

### A2A Security — Trust Models (mTLS vs OAuth)

[Explore A2A Threat Models](./07-a2a)

* Service identity and authentication design
* mTLS vs OAuth tradeoffs (when and why)
* Token vs certificate-based trust
* Secure service-to-service communication patterns

---

### Supply Chain Security — CI/CD + Dependencies

[Explore Supply Chain Threat Models](./09-supply-chain)

* Dependency trust and poisoning risks
* Artifact integrity and provenance
* CI/CD pipeline attack surface
* Build → deploy → runtime trust boundaries

---

## What This Is NOT

* Not a checklist
* Not OWASP copy-paste
* Not tool-specific security
* Not “run STRIDE and move on”

If your architecture is wrong,
**no amount of controls will save you.**

---

## Core Philosophy

* **Patterns before platforms**
  Security is architectural — cloud providers are implementation details

* **Trust boundaries define risk**
  Every boundary is a potential failure point

* **Threat modeling is continuous**
  Done during design, not after incidents

* **STRIDE is applied per data flow**
  Context matters more than components

* **Controls must be testable**
  If you can’t validate it, it’s not real

* **Assumptions must be explicit**
  Hidden assumptions break systems

---

## What You’ll Get

Each threat model includes:

* Architecture + trust boundaries
* STRIDE analysis per data flow
* Risk register (prioritized)
* Security controls
* Test plans (validation-focused)

---

## Architecture → Threat Modeling Approach

> **You don’t threat model components.
> You threat model trust transitions.**

Each system is analyzed as:

1. Architecture
2. Data flows
3. Trust boundaries
4. Threats (STRIDE)
5. Controls
6. Validation (test plan)

---

## Security Architecture Decisions (Real-World Thinking)

Security is about **tradeoffs**, not tools.

This repository explores:

* mTLS vs OAuth for service-to-service trust
* API Gateway vs direct service exposure
* LLM as trusted vs untrusted component
* Build-time vs runtime supply chain controls

The goal is not to apply controls. The goal is to **choose the right model**

---

## Coverage Map

```text
                ┌───────────────────────────────┐
                │   Threat Modeling Methodology │
                └──────────────┬────────────────┘
                               │
                               ▼
 ┌──────────────────────────────────────────────────────────┐
 │                Application Architectures                 │
 │                                                          │
 │  Cloud Platforms      AI Systems        A2A Integrations │
 │  (03 / 04 / 05)       (06)              (07)             │
 └───────────────┬─────────────────────────────┬────────────┘
                 │                             │
                 ▼                             ▼
        ┌──────────────────┐           ┌───────────────────┐
        │ Controls Library │           │ Security Patterns │
        │     (08)         │           │      (11)         │
        └─────────┬────────┘           └─────────┬─────────┘
                  │                              │
                  └─────────────┬────────────────┘
                                ▼
                    ┌────────────────────────┐
                    │ Software Supply Chain  │
                    │        (09)            │
                    └────────────┬───────────┘
                                 │
                                 ▼
                        ┌──────────────────┐
                        │  Case Studies    │
                        │      (12)        │
                        └──────────────────┘
```

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

## How to Use This (Practically)

### Designing a System

* Start with a similar architecture
* Copy the threat model structure
* Replace diagrams, trust boundaries, assumptions
* Run STRIDE per data flow
* Apply controls + validate via test plan

---

### Security Engineers / Architects

* Apply reusable patterns from [Security Architecture Patterns](./11-security-architecture-patterns)  
* Map mitigations using the [Controls Library](./08-controls-library)  
* Align threat models with real system designs

---

## Who This Is For

* Product Security Engineers
* Security Architects
* Platform / Cloud Engineers
* Developers building distributed systems

---

## Final Thought

> **If your architecture is insecure,
> your threat model will only document failure — not prevent it.**

---

## License

MIT License
