# Lessons Learned

The Log4Shell incident revealed critical weaknesses in dependency management practices.

## Dependency Visibility

Organizations often lacked visibility into which libraries were used in their applications.

Maintaining a **Software Bill of Materials (SBOM)** can help track dependencies.

## Secure Defaults

Libraries should avoid enabling dangerous features such as remote code loading by default.

## Dependency Monitoring

Teams should regularly monitor vulnerabilities affecting dependencies.

Automated dependency scanning tools can help detect known vulnerabilities.

## Defense in Depth

Even when a vulnerability exists, additional controls can reduce impact:

- input validation
- network egress controls
- runtime monitoring
- application sandboxing
