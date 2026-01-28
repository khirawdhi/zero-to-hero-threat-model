# Zero-to-Hero Threat Modeling (Cloud + AI + A2A)

A practical, reusable threat-modeling repository for:
- Cloud-native applications (microservices, event-driven, data pipelines)
- AWS / Azure / GCP architectures
- AI applications (RAG, agents, tool-using systems)
- App-to-app (A2A) integrations (B2B APIs, webhooks, service-to-service)

## Who this is for
- Security engineers and architects who want repeatable threat-modeling artifacts
- Developers who want to design secure cloud systems
- Anyone learning threat modeling and looking for real-world examples

## How to use this repo
### If you're learning
Start here:
1. `00-getting-started/how-to-use-this-repo.md`
2. `00-getting-started/threat-modeling-101.md`
3. Use `01-templates/threat-model-template.md`
4. Pick a model in `/03-azure`, `/04-aws`, `/05-gcp`, `/06-ai-applications`, or `/07-a2a`

### If you're using it at work
- Copy a closest matching threat model folder
- Update assumptions, data flows, and trust boundaries
- Use the Controls Library (`/08-controls-library/`) to standardize mitigations
- Track outcomes in `risk-register.csv`

## Threat model folder standard
Each threat model folder follows the same structure:
- `README.md` summary
- `diagram.drawio` + `diagram.png`
- `dfd.md` (components + flows + trust boundaries)
- `stride.md` (threats + scenarios + mitigations)
- `controls.md` (minimum baseline controls)
- `assumptions.md`
- `risk-register.csv`
- `test-plan.md`

## Learning path (zero → hero)
- Level 0: DFD + trust boundaries + STRIDE basics
- Level 1: Cloud-native microservices
- Level 2: Multi-cloud equivalents (AWS/Azure/GCP)
- Level 3: AI systems (prompt injection, tool abuse, data leakage)
- Level 4: A2A integrations (mTLS, OAuth client credentials, signing, replay defense)

## Disclaimer
This repository is educational and designed for practical reuse, but every system has unique context.
Validate controls with your engineering, platform, and compliance requirements.

## License
MIT (recommended for maximum reuse).
