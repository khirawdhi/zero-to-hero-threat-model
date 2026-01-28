# Reference Architecture: Cloud-Native API

## Description
A public-facing API protected by an edge layer, backed by
containerized application services and managed data stores.

## Typical Components
- User / Client
- Edge (WAF, CDN, API Gateway)
- Application runtime (Kubernetes / PaaS)
- Identity provider
- Data stores (SQL / Object storage)
- Secrets management
- Observability
- CI/CD system

## Common Trust Boundaries
- Internet → Edge
- Edge → Application
- Application → Identity
- Application → Data
- Build → Runtime

## Typical Threats
- Token theft and replay
- AuthZ bypass
- Injection attacks
- Data exfiltration
- DoS at edge or runtime
- Supply chain compromise

## Used By
- TM-AZ-01
- TM-AWS-01
- TM-GCP-01
