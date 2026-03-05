# Uber CI/CD Breach

The **Uber breach (2022)** was a significant security incident in which an attacker gained unauthorized access to internal systems and administrative tools used by **Uber**.

The attacker initially compromised employee credentials through social engineering and then escalated privileges across multiple internal services. This allowed access to engineering tools, source code repositories, and internal dashboards.

Although the breach did not involve a direct vulnerability in application code, it demonstrated how **weak identity controls and insufficient internal access protections can lead to widespread system compromise**.

---

## Impact

* unauthorized access to internal engineering systems
* exposure of internal dashboards and documentation
* access to development and CI/CD tools
* disruption of internal operations

---

## Attack Category

* credential compromise
* social engineering attack
* internal system privilege escalation

---

## Incident Overview

The attacker obtained credentials belonging to an internal contractor and used them to access internal systems.

Once inside the network, the attacker was able to:

* access internal messaging platforms
* retrieve credentials from internal systems
* gain access to administrative tools and development platforms

The attacker then posted messages across internal communication systems to demonstrate the compromise.

---

## Related Threat Models

This incident relates to threat models and architecture patterns in this repository:

```
TM-SC-05 — Deployment Pipeline Threat Model
Secure CI/CD Pipeline Pattern
Zero-Trust Service Communication Pattern
```
