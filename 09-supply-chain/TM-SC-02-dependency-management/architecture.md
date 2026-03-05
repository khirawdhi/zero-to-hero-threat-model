# Dependency Management Architecture

## High-level flow

Developer / CI Runner
  |
  | 1) Read manifest + lockfile
  v
Dependency Manager
(npm / pip / maven / gradle / bundler / nuget)
  |
  | 2) Resolve direct + transitive deps
  v
Registry Sources
  - Public Registry (npm/PyPI/Maven Central/etc.)
  - Private Registry (Artifactory/Nexus/GitHub Packages)
  - Internal Mirror/Proxy
  |
  | 3) Download packages
  v
Local Cache / Build Workspace
  |
  | 4) Build + tests
  v
Build Output (artifact/image)

## Trust boundaries
- Developer workstation (least trusted)
- CI runners (trusted but high-value target)
- Public registries (untrusted)
- Private registries (trusted, but must be hardened)
- Internal mirrors/proxies (trusted, but can be poisoned)

## Assets
- dependency manifests + lockfiles
- registry credentials/tokens
- package integrity metadata (hashes, signatures, checksums)
- build cache
- dependency update configs (dependabot/renovate)
