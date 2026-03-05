# Lessons Learned

The Codecov incident demonstrates the risks associated with third-party integrations in CI/CD pipelines.

## Third-Party Dependency Risk

External scripts and tools used in build pipelines must be treated as untrusted components.

Organizations should verify the integrity of external pipeline dependencies.

## Secret Management

Sensitive credentials should not be exposed as plain environment variables in build pipelines.

Use secure secret management systems and minimize secret exposure.

## Pipeline Isolation

Build environments should be isolated and use short-lived credentials where possible.

This limits the impact of credential compromise.

## Monitoring and Detection

Organizations should monitor CI/CD pipeline activity and detect unusual outbound network traffic from build systems.

## Supply Chain Security

Software delivery pipelines must implement strong controls for:

- dependency integrity
- artifact verification
- pipeline access control
