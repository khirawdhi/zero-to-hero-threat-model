# Contributing

Thank you for your interest in contributing to the Zero-to-Hero Threat Modeling Playbook.

This project focuses on practical, reusable threat models for cloud, AI, and distributed systems.

---

## Contribution Principles

- Pattern-first, not cloud-first
- Focus on trust boundaries and data flows
- Keep models practical and reusable
- Controls must be testable

---

## Threat Model Structure

Each threat model must include:

- `diagram.png` — architecture / trust boundaries
- `assumptions.md` — explicit assumptions and scope
- `dfd.md` — data flow description
- `stride.md` — STRIDE analysis (per data flow)
- `risk-register.csv` — prioritized risks
- `controls.md` — recommended controls
- `test-plan.md` — validation steps

---

## Naming Convention

Use the following format:

TM-<DOMAIN>-<NUMBER>-<NAME>

Examples:
- TM-AZ-01-apim-aks-sql
- TM-A2A-01-oauth-client-credentials
- TM-AI-01-rag-system

---

## What Makes a Good Contribution

- Clear trust boundaries
- Realistic threat scenarios
- Actionable controls (not generic)
- Minimal cloud-specific bias unless required
- Consistent structure

---

## How to Contribute

1. Fork the repository
2. Create a new branch
3. Add or update a threat model
4. Follow the structure and naming conventions
5. Submit a pull request with a clear description

---

## Notes

- Keep content concise and practical
- Avoid overly theoretical models
- Ensure consistency with existing patterns

---

Thank you for contributing to making threat modeling more practical and accessible.
