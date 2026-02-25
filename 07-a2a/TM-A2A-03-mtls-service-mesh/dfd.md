# Data Flow Diagram (DFD) — TM-A2A-03 (mTLS Service Mesh)

This DFD models service-to-service communication secured via **Mutual TLS (mTLS)**,
typically enforced by a **service mesh** (data plane sidecars + control plane),
with **X.509 certificates** issued by a trusted Certificate Authority (CA).

---

## External Entities

- **E1: Service A Workload (Client)**
  - Application container + sidecar proxy (data plane)
- **E2: Service B Workload (Server)**
  - Application container + sidecar proxy (data plane)
- **E3: Service Mesh Control Plane**
  - Policy distribution, configuration, identity policy (control plane)
- **E4: Certificate Authority (CA) / Issuer**
  - Issues and rotates X.509 certificates for workloads/sidecars
- **E5: CI/CD Pipeline**
  - Deploys images and configuration to runtime
- **E6: Logging & Monitoring System**
  - Receives telemetry, connection logs, policy violations

---

## Processes

- **P1: Service A Application Logic**
  - Creates outbound requests to Service B via local sidecar
- **P2: Sidecar Proxy A (mTLS Client)**
  - Initiates mTLS handshake, enforces egress and identity policies
- **P3: Sidecar Proxy B (mTLS Server)**
  - Terminates mTLS, validates client identity, enforces ingress policies
- **P4: Service B Application Logic**
  - Handles business logic after successful transport authentication/authorization
- **P5: Policy Enforcement Engine (Mesh)**
  - Policy evaluation (allow/deny) based on identity attributes, service names, namespaces
  - Often implemented in sidecars using config distributed by control plane

---

## Data Stores

- **D1: Workload Identity Material**
  - Private keys, certificates, intermediate certs, trust bundles (sidecar/runtime)
- **D2: Mesh Configuration Store**
  - Service discovery, routing rules, authorization policies (control plane)
- **D3: Audit Logs / Telemetry Store**
  - Connection logs, policy decision logs, mesh control plane events
- **D4: Artifact Registry / Deployment Store (CI/CD)**
  - Container images, signed artifacts, configuration manifests

---

## Trust Boundaries

- **TB1: Workload Identity Boundary**
  - Inside each workload runtime (App + Sidecar), where private keys and certs exist
- **TB2: Mesh Policy Boundary**
  - Control plane boundary where policies are authored, stored, and distributed
- **TB3: Certificate Issuance Boundary**
  - CA boundary where trust is anchored and certificates are minted/rotated
- **TB4: Runtime / Cluster Boundary**
  - The execution environment hosting workloads/sidecars
- **TB5: Build → Runtime Boundary**
  - CI/CD boundary where artifacts and config are promoted into runtime
- **TB6: Monitoring Boundary**
  - Boundary around logging/monitoring systems and telemetry pipelines

---

## Data Flows

### Service-to-Service (Data Plane)

- **F1: Service Request (App → Sidecar A)**
  - P1 → P2
  - Local request from Service A app to its sidecar proxy

- **F2: mTLS Handshake (Sidecar A ↔ Sidecar B)**
  - P2 ↔ P3
  - Certificate exchange, mutual authentication, encrypted channel establishment
  - Identity validated via certificate SAN/SPIFFE ID

- **F3: Encrypted Service Call (Sidecar A → Sidecar B)**
  - P2 → P3
  - Application request forwarded over established mTLS session

- **F4: Encrypted Response (Sidecar B → Sidecar A)**
  - P3 → P2
  - Response returned over mTLS session

- **F5: Local Delivery (Sidecar B → App B)**
  - P3 → P4
  - Sidecar forwards request to Service B app after policy decision

---

### Policy & Identity Control Plane

- **F6: Policy Distribution (Control Plane → Sidecars)**
  - E3 → P2 and E3 → P3
  - Authorization policies, routing config, identity rules (D2)

- **F7: Certificate Issuance / Rotation (CA → Sidecars)**
  - E4 → P2 and E4 → P3
  - Issue/rotate certificates + trust bundles (D1)

- **F8: Certificate Renewal / CSR (Sidecars → CA)**
  - P2 → E4 and P3 → E4
  - CSR submission / renewal requests (depends on mesh/PKI design)

---

### Build / Deployment

- **F9: Artifact & Config Promotion (CI/CD → Runtime)**
  - E5 → E1/E2/E3
  - Image deployment, policy config, mesh config, secret/cert config (D4)
  - Crosses TB5 (high-value boundary)

---

### Observability

- **F10: Telemetry & Audit Logs (Workloads/Control Plane → Monitoring)**
  - P2/P3/E3 → E6
  - Connection logs, policy decisions, cert rotation events, errors (D3)

---

## Notes

- mTLS provides **transport-layer authentication**.
- Authorization may be implemented:
  - purely at mesh layer (identity-based allow/deny)
  - or layered with application-level authorization (recommended for sensitive actions).
- The most critical assets are:
  - **Private keys and certificates (D1)**
  - **Policy configuration (D2)**
  - **CI/CD promotion path (TB5)**
