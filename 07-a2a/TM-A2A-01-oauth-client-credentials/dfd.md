# Data Flow Diagram (DFD) — TM-A2A-01 (OAuth Client Credentials)

This threat model covers service-to-service authentication using OAuth 2.0
client credentials flow.

---

## External Entities
- **E1: Service A (Client Application)**
- **E2: Service B (Resource Server / API)**
- **E3: Authorization Server (OAuth / IdP)**
- **E4: Webhook Sender/Receiver (Optional Partner System)**

---

## Processes
- **P1: Service A Runtime**
- **P2: Token Endpoint (Auth Server)**
- **P3: Service B API Gateway / Auth Middleware**
- **P4: Service B Business Logic**
- **P5: Webhook Endpoint (Optional)**

---

## Data Stores
- **D1: Client Secrets Store**
- **D2: Token Cache**
- **D3: API Data Store**
- **D4: Audit Logs / Monitoring**

---

## Trust Boundaries
- **TB1: Partner Trust Boundary** (Service A ↔ Service B)
- **TB2: Token Issuance Boundary** (Service A ↔ Auth Server)
- **TB3: API Trust Boundary** (Inbound requests to Service B)
- **TB4: Secrets Boundary** (Client credentials)
- **TB5: Webhook Boundary** (Inbound external callbacks)
- **TB6: Build → Runtime Boundary**

---

## Primary Data Flows

### F1 — Token Request
- **E1 → E3**
- Data: Client ID + Client Secret

### F2 — Access Token Response
- **E3 → E1**
- Data: Access Token (JWT or opaque)

### F3 — API Call
- **E1 → E2**
- Data: API request + Bearer token

### F4 — Token Validation
- **E2 → E3** (optional introspection)
- Data: Token validation request

### F5 — Business Operation
- **E2 → D3**
- Data: Read/Write operation

### F6 — API Response
- **E2 → E1**
- Data: Response payload

### F7 — Webhook Callback (Optional)
- **E2 → E4**
- Data: Event payload

### F8 — Logging
- **E1/E2 → D4**
- Data: Token use, API actions, audit events
