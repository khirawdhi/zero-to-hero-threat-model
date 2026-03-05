# TM-SC-02 — Dependency Management Threat Model

This threat model focuses on **software dependency risks** introduced via:
- public package registries (npm, PyPI, Maven, RubyGems, NuGet)
- internal/private registries and mirrors
- lockfiles and dependency resolution
- CI/CD dependency download + build steps

## Scope
- Dependency resolution and installation (local + CI)
- Source authenticity and integrity
- Registry trust and namespace control
- Transitive dependencies
- Update mechanisms (renovate/dependabot, manual upgrades)

## Out of scope
- Runtime attacks in production (covered in CI/CD and container pipelines)
- Infrastructure threat model for registry hosting (covered separately)

## Key assets
- application source code
- dependency manifests (package.json, requirements.txt, pom.xml, Gemfile, *.csproj)
- lockfiles (package-lock.json, poetry.lock, Gemfile.lock)
- build scripts (Makefile, scripts, CI configs)
- credentials/tokens for private registries
