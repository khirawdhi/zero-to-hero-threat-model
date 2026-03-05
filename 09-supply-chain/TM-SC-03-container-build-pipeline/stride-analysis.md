# STRIDE Threat Analysis — Container Build Pipeline

| STRIDE Category | Threat |
|---|---|
| Spoofing | attacker impersonates registry or pushes malicious image |
| Tampering | Dockerfile or build configuration modified to introduce backdoor |
| Repudiation | lack of image signing prevents traceability of builds |
| Information Disclosure | secrets leaked during image build process |
| Denial of Service | malicious base image breaks build pipeline |
| Elevation of Privilege | malicious container build step executes privileged operations |
