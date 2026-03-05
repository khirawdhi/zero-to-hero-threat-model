# STRIDE Threat Analysis — Dependency Management

| STRIDE | Threat |
|---|---|
| Spoofing | attacker spoofs internal package identity (dependency confusion) |
| Tampering | lockfile or manifest altered to pull malicious versions |
| Repudiation | lack of signed commits / weak audit trail on dependency changes |
| Information Disclosure | tokens leaked; private package metadata exposed |
| Denial of Service | dependency resolution poisoning / registry outage blocks builds |
| Elevation of Privilege | install scripts lead to RCE in CI runner or dev machine |
