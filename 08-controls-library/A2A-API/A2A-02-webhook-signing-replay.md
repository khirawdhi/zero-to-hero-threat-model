# A2A-02: Webhook Signature & Replay Protection

## Control Goal

Prevent spoofed, replayed, or tampered webhook events.

---

## Threats Mitigated

- Spoofing
- Tampering
- Replay attacks
- DoS via event flooding

---

## Control Description

All incoming webhook requests must:

- Be signed (HMAC or asymmetric signature)
- Include timestamp
- Include nonce or unique event ID
- Enforce expiration window (e.g., 5 minutes)
- Validate payload schema

---

## Implementation Guidance

- Use HMAC SHA-256 with shared secret
- Validate signature before JSON parsing
- Store recent event IDs to prevent replay
- Enforce strict timestamp skew limits
- Rate limit webhook endpoints

---

## Validation / Test Cases

- Modify payload → signature must fail.
- Replay same event ID → must fail.
- Send old timestamp → must fail.
- Send unsigned request → must fail.

---

## Evidence Artifacts

- Signature validation middleware
- Replay cache configuration
- Logs of rejected webhook events
- Rate limit configuration

---

## Common Failure Modes

- Validating signature after parsing
- Not checking timestamp
- Logging secrets in debug mode
- No replay detection

---

## Cloud Mapping

Azure: APIM policies + Function validation  
AWS: Lambda + API Gateway + signature middleware  
GCP: Cloud Run / Cloud Functions + verification layer
