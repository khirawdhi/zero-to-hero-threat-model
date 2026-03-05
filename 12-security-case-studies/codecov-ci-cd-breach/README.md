# Codecov CI/CD Breach

The **Codecov breach (2021)** was a major software supply chain incident that affected hundreds of organizations using the code coverage platform **Codecov**.

Attackers compromised a script used in CI/CD pipelines and modified it to **exfiltrate sensitive environment variables** from downstream build environments.

Because the script was executed during CI builds across many organizations, attackers were able to collect **secrets, API tokens, and credentials** from affected pipelines.

---

## Impact

* exposure of CI/CD secrets from numerous organizations
* compromise of credentials used for cloud services and repositories
* long-term risk of infrastructure access using stolen secrets

Organizations affected included technology companies relying on automated build pipelines.

---

## Attack Category

* CI/CD pipeline compromise
* software supply chain attack
* credential exfiltration

---

## Incident Timeline

* attackers gained unauthorized access to Codecov infrastructure
* a Bash uploader script was modified to include a malicious payload
* compromised script distributed to CI/CD pipelines globally
* environment variables and secrets were exfiltrated to attacker-controlled servers

---

## Related Threat Models

This incident directly relates to threat models in this repository:

```
TM-SC-01 — CI/CD Pipeline Threat Model
TM-SC-03 — Container Build Pipeline Threat Model
Secure CI/CD Pipeline Pattern
```
