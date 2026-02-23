# NET-01: Outbound Egress Control

## Control Goal

Restrict outbound network traffic to approved destinations.

---

## Threats Mitigated

- Data Exfiltration
- Command & Control callbacks
- Supply chain compromise
- LLM prompt exfiltration

---

## Control Description

All workloads must:

- Deny outbound traffic by default
- Allow only explicit destinations
- Route internet access via inspection point
- Log outbound connections

---

## Implementation Guidance

- Use private endpoints where possible.
- Restrict metadata service access.
- Enforce DNS filtering.
- Block arbitrary external APIs.

---

## Validation / Test Cases

- Attempt outbound call to unauthorized domain → must fail.
- Attempt metadata service access → must fail (unless required).
- Monitor outbound DNS queries.

---

## Evidence Artifacts

- Firewall rules
- NSG / Security group configs
- VPC flow logs
- Egress gateway configuration

---

## Common Failure Modes

- Default allow outbound
- Hardcoded IP exceptions
- Forgotten test environments
- No DNS monitoring

---

## Cloud Mapping

Azure: NSGs + Firewall + Private Endpoints  
AWS: Security Groups + NAT + VPC endpoints  
GCP: VPC Firewall + Private Service Connect
