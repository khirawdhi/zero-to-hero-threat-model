# IAM-02: Access Token Validation Discipline

## Control Goal

Ensure all access tokens are cryptographically validated and
authorization decisions are not based on trust assumptions.

---

## Threats Mitigated (STRIDE)

- Spoofing (forged tokens)
- Elevation of Privilege (scope abuse)
- Tampering (manipulated claims)
- Repudiation (missing validation logs)

---

## Control Description

All services accepting bearer tokens must validate:

- Signature (correct signing key)
- Issuer (`iss`)
- Audience (`aud`)
- Expiration (`exp`)
- Not-before (`nbf`) if present
- Scope / role claims

Validation must occur before business logic execution.

---

## Implementation Guidance

- Use verified JWT libraries.
- Cache JWKS keys securely.
- Enforce strict audience matching.
- Reject tokens missing required claims.
- Avoid custom token parsing logic.

---

## Validation / Test Cases

- Attempt API call with expired token → must fail.
- Attempt API call with wrong audience → must fail.
- Attempt API call with altered payload → must fail.
- Attempt call with missing scope → must fail.

---

## Evidence Artifacts

- API gateway validation config
- Token validation middleware code
- Security test logs
- Audit logs showing rejected tokens

---

## Common Failure Modes

- Skipping audience validation
- Ignoring scope
- Accepting tokens from multiple issuers without restriction
- Logging full tokens

---

## Cloud Mapping

Azure: Entra ID + API Management policies  
AWS: Cognito / API Gateway JWT authorizers  
GCP: IAP / Cloud Endpoints / JWT middleware
