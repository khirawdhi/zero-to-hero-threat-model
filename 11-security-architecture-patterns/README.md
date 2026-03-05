# Security Architecture Patterns

This section provides **reusable secure architecture patterns** for common system designs.

While threat models analyze risks in existing systems, **security architecture patterns help engineers design systems with security built in from the beginning**.

Each pattern includes:

* architecture overview
* security design principles
* recommended security controls
* architecture diagrams

These patterns can be used as **reference designs when building new systems**.

---

## Available Architecture Patterns

### Secure API Gateway Pattern

```
secure-api-gateway-pattern
```

A common architecture used in microservices systems where an API gateway provides authentication, authorization, rate limiting, and request validation before traffic reaches backend services.

---

### Zero-Trust Service Communication

```
zero-trust-service-communication
```

Defines secure communication between internal services using identity-based authentication and encrypted communication.

---

### Secure CI/CD Pipeline Pattern

```
secure-ci-cd-pipeline-pattern
```

Describes how to design CI/CD pipelines with secure build environments, artifact integrity, and controlled deployment workflows.

---

### Secure Data Pipeline Pattern

```
secure-data-pipeline-pattern
```

A reference architecture for processing and storing sensitive data securely across ingestion, processing, and storage layers.

---

### Secure AI System Pattern

```
secure-ai-system-pattern
```

Provides a security-focused architecture for AI and LLM systems including prompt validation, model access control, and secure tool integrations.

---

## Why Architecture Patterns Matter

Security is most effective when integrated into **system design**, not added after systems are built.

Using reusable architecture patterns helps teams:

* design secure systems faster
* reduce common security mistakes
* standardize security controls across projects
* improve collaboration between security and engineering teams
