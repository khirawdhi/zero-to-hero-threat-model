# Mitigations

## Registry & Resolution Controls
- enforce **scoped packages** and internal namespaces
- configure registry priority: private first (with explicit allow-list for public)
- block unknown registries and direct download URLs

## Integrity & Provenance
- use lockfiles and enable integrity checks (hash verification)
- generate and store **SBOM** for builds
- require provenance attestation for critical builds

## Dependency Governance
- allow-list critical dependencies
- enforce review for dependency changes (CODEOWNERS)
- restrict postinstall scripts or run in sandbox

## CI Hardening
- isolate runners; minimal permissions; short-lived tokens
- secrets scanning in pipelines and repos
- network egress policies for runners

## Monitoring & Response
- monitor for new package publishes matching internal names
- alert on unexpected dependency graph changes
- rapid rollback mechanism for compromised dependency versions
