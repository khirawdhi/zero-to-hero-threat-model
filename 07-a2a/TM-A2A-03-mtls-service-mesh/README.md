# TM-A2A-03: mTLS Service Mesh (Zero Trust A2A)

## Overview

This threat model covers Application-to-Application (A2A) communication
secured using Mutual TLS (mTLS), typically enforced by a service mesh
or transport-layer identity system.

Unlike OAuth-based A2A, identity is verified at the transport layer
using X.509 certificates issued by a trusted Certificate Authority (CA).

---

## Architecture Pattern

- Service A communicates with Service B
- Both workloads authenticate each other via mTLS
- Certificates issued by internal CA
- Optional service mesh (Istio, Linkerd, Consul)
- Authorization policies enforced at mesh or application layer
- No bearer tokens required for authentication

---

## Primary Security Objectives

- Strong workload identity verification
- Eliminate bearer token replay risk
- Prevent unauthorized service communication
- Enforce Zero Trust network principles
- Contain lateral movement inside cluster

---

## Primary Risks Introduced by mTLS

- Certificate theft or key compromise
- CA compromise
- Mesh policy misconfiguration
- Certificate rotation failures
- Identity over-privilege (too-broad trust domains)

---

## Out of Scope

- User authentication flows
- External internet-facing APIs
- Hardware-level attacks
- Physical infrastructure compromise
