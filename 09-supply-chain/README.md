# Supply Chain Threat Modeling

Modern software systems depend heavily on external components including open-source libraries, container images, CI/CD pipelines, artifact repositories, and cloud infrastructure.

This creates a **software supply chain attack surface** that attackers increasingly exploit.

Major incidents such as the SolarWinds compromise and dependency confusion attacks demonstrate how upstream compromises can propagate malicious code into thousands of downstream systems.

This section provides **threat modeling playbooks for common software supply chain architectures**, focusing on:

- CI/CD pipeline security
- dependency management risks
- container build pipeline threats
- artifact integrity
- build system compromise

Each threat model follows the **STRIDE methodology** and includes:

- architecture overview
- assumptions
- threat analysis
- risk register
- mitigation strategies

The goal is to help security engineers systematically identify and mitigate risks in modern software delivery pipelines.
