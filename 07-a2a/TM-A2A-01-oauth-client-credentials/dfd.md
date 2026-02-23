# Data Flow Diagram (DFD) — TM-A2A-01 (OAuth Client Credentials)

This DFD models service-to-service communication using OAuth 2.0
client credentials.

---

## External Entities
- **E1: Service A (Client Application)**
- **E2: Authorization Server (OAuth / IdP)**
- **E3: Service B (Resource Server / API)**
- **E4: Webhook Receiver (optional)**
- **E5: Monitoring / Logging System**

---

## Processes
- **P1: Client App Logic**
- **P2: Token Request Handler**
- **P3: API Gateway / Middleware (Service B)**
- **P4: Business Logic (Service B)**
- **P5: Webhook Endpoint (optional)**

---

## Data Stores
- **D1: Client Secret Store**
- **D2: Token Cache**
- **D3: Audit Logs**
- **D4: Business Data Store**

---

## Trust Boundaries

- **TB1: Partner Trust Boundary**
  Between Service A and Service B

- **TB2: Token Issuance Boundary**
  Between Service A and Authorization Server

- **TB3: API Trust Boundary**
  Incoming requests into Service B

- **TB4: Webhook Boundary (optional)**
  Incoming events to Service A

- **TB5: Secrets Boundary**
  Client credentials and signing keys

- **TB6: Monitoring Boundary**
  Logs and telemetry systems

- **TB7: Build → Runtime Boundary**
  CI/CD to deployed services

---

## Primary Data Flows

### F1 — Token Request
E1 → E2  
Data: client_id + client_secret

### F2 — Access Token Response
E2 → E1  
Data: access_token + expiry + scope

### F3 — API Call
E1 → E3  
Data: HTTP request + Bearer token

### F4 — Token Validation
E3 → E2 (optional introspection)  
Data: token validation request

### F5 — API Response
E3 → E1  
Data: business response

### F6 — Webhook Event (optional)
E3 → E4  
Data: event payload

### F7 — Webhook Acknowledgement
E4 → E3  
Data: status response

### F8 — Logging
All services → D3  
Data: request ID, token claims, status, timestamps
