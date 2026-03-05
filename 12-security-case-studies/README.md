# Security Case Studies

This section analyzes real-world security incidents through the lens of **architecture and threat modeling**.

Rather than focusing only on vulnerabilities, these case studies examine:

* the system architecture involved
* how attackers exploited weaknesses
* which threat modeling techniques could have identified the risks
* security controls that may have prevented the incident

Studying real-world attacks helps security engineers understand how architectural weaknesses can lead to large-scale compromises.

---

## Case Studies Included

### SolarWinds Supply Chain Attack

```text
solarwinds-supply-chain-attack
```

A major supply chain compromise where attackers injected malicious code into a widely distributed software update.

---

### Log4Shell Dependency Crisis

```text
log4shell-dependency-crisis
```

A vulnerability in a widely used logging library that enabled remote code execution across thousands of systems.

---

### Codecov CI/CD Breach

```text
codecov-ci-cd-breach
```

Attackers modified a CI/CD pipeline script, allowing them to extract secrets from downstream build environments.

---

### Uber CI/CD Breach

```text
uber-ci-cd-breach
```

An attacker gained internal access and used CI/CD and administrative tools to escalate privileges across infrastructure.

---

## Why Case Studies Matter

Real-world incidents demonstrate that security failures often result from **architectural weaknesses rather than individual vulnerabilities**.

Analyzing these events helps engineers:

* identify systemic security gaps
* improve architecture design
* strengthen threat modeling practices
