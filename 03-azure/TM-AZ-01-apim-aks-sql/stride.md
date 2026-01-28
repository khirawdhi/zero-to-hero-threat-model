# STRIDE Threat Analysis — TM-AZ-01 (APIM → AKS → SQL)

This STRIDE analysis is performed **per data flow / trust boundary**, not just per component.

## Flow 1: User → WAF → APIM (Internet-facing entry)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Stolen/forged tokens used to call APIs (token replay, leaked JWT) | Account takeover, data access | Enforce OIDC validation at APIM (iss/aud/exp), short token TTL, refresh token rotation, MFA for admins, reject unsigned/weak algs |
| T | Request tampering (parameter pollution, header injection) bypasses downstream validation | Unauthorized actions, data corruption | Schema validation at APIM, normalize headers, strict content-type, WAF rules for common bypass patterns |
| R | User denies actions due to weak audit trail | Forensic gaps | Correlation IDs at APIM, structured logs, immutable audit logging, time sync |
| I | Sensitive data exposure via verbose errors, headers, logs | PII leakage | Standard error responses, log redaction, disable debug headers, secure response headers |
| D | L7 DoS (bot floods expensive endpoints) | Outage, cost spike | Rate limiting/quotas at APIM, WAF bot protection, caching where safe, request size limits |
| E | Misconfigured APIM policies allow bypass of authZ (e.g., open backend) | Privilege escalation | Deny-by-default routes, per-operation authZ, separate admin APIs, automated config checks |

## Flow 2: APIM → AKS (Edge → Application Runtime)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Backend service spoofing (wrong upstream allowed) | Data exposure, SSRF-style abuse | Private connectivity, restrict backend to private IP, validate host headers, mTLS (if feasible) |
| T | Payload tampering in transit | Data corruption | TLS everywhere, consider mTLS service mesh, request signing for high-risk operations |
| R | No end-to-end traceability across gateway → service | Forensic gaps | Propagate trace/correlation IDs, OpenTelemetry |
| I | Internal endpoints exposed (misrouted ingress/service) | Data leak | Kubernetes ingress allowlist, namespace isolation, deny public services |
| D | Request storms overwhelm cluster | Outage | Rate limiting, HPA, resource requests/limits, circuit breakers/timeouts |
| E | AuthZ enforced only at gateway; services trust gateway blindly | Privilege escalation | Defense-in-depth: validate scopes/roles in service, fine-grained authZ per endpoint |

## Flow 3: AKS → Entra ID (Identity Provider)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Workload identity misbinding (wrong service account gets access) | Cross-service access | Use workload identity correctly (federation), per-service identity, least privilege |
| T | Token validation bugs (accept wrong audience/issuer) | Auth bypass | Strict iss/aud/exp/nbf checks, clock sync, block `none` alg |
| R | Missing admin/audit logs for identity events | Forensic gaps | Entra audit logs, alerting on risky sign-ins and consent grants |
| I | Tokens/leaked secrets in logs or env vars | Lateral movement | Never log tokens, redact, use Key Vault/CSI, short-lived creds |
| D | Identity provider outage impacts auth flows | Availability | Caching JWKS, graceful degradation strategy, retries with backoff |
| E | Over-privileged app registration / consent grants | Tenant compromise | Restrict app consent, privileged access workflows, periodic review |

## Flow 4: AKS → Azure SQL / Blob (Application → Data Plane)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Stolen managed identity used to access data plane | Data breach | Least privilege RBAC, scoped identities per service, rotate credentials where applicable |
| T | Unauthorized writes / data tampering | Integrity loss | DB roles least privilege, row-level security/tenant isolation where relevant, input validation |
| R | No audit trails for data access | Forensic gaps | SQL auditing, storage access logs, immutable log retention |
| I | Data exfil via overly permissive network/IAM | PII leakage | Private endpoints, deny public access, egress controls, storage firewall, DLP/log scrubbing |
| D | DB connection exhaustion / hot partitions | Outage | Connection pooling, throttling, caching, backpressure |
| E | SQL injection / SSRF → metadata → creds → data | Full compromise | Parameterized queries, WAF rules, block link-local egress, IMDS protections, secretless patterns |

## Flow 5: AKS → Key Vault (Secrets Management)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Unauthorized pod gets secret access via shared identity | Secret theft | Per-service identity, separate Key Vault access policies, least privilege |
| T | Secret value tampering (malicious rotation) | Compromise | RBAC + approval workflows, secret versioning, alerts on secret changes |
| R | No audit on secret reads/changes | Forensic gaps | Key Vault diagnostics logs + SIEM alerts |
| I | Secrets exposed via env vars, configmaps, logs | Secret leak | CSI driver/secret mounts, no secrets in Git/images, redaction |
| D | Key Vault throttling/outage breaks app | Availability | Caching where safe, retries/backoff, design for degraded mode |
| E | Vault admin privilege abused | Full compromise | Privileged access management, just-in-time access, break-glass controls |

## Flow 6: CI/CD → AKS (Build → Runtime)
| STRIDE | Threat scenario | Impact | Recommended mitigation |
|---|---|---|---|
| S | Compromised CI identity pushes deployments | Full compromise | Strong CI identity, short-lived creds, restrict who can deploy to prod |
| T | Supply chain tampering (poisoned dependency/image) | Backdoor | SBOM, image signing (cosign), provenance checks, SCA/SAST gates |
| R | No traceability from commit → artifact → deploy | Forensic gaps | Signed releases, build attestation, deployment logs |
| I | Secrets leak in pipeline logs/artifacts | Secret theft | Secret scanning, masked vars, separate build vs deploy creds |
| D | Pipeline abuse causes rapid redeploys | Instability | Approval gates, rate-limit deploys, change management |
| E | Over-privileged cluster role for deployment tooling | Cluster takeover | Least privilege RBAC for deployer, separate namespaces, no cluster-admin |
