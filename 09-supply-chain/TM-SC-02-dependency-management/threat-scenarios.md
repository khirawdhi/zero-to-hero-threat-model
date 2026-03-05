# Threat Scenarios (Supply Chain)

## SC-02-01 Dependency Confusion
**Description:** Attacker publishes a package with the same name as an internal dependency on a public registry.
**Prereqs:** Mixed private/public resolution; unscoped package names; misconfigured registry priority.
**Impact:** Remote code execution during install/build; credential theft; backdoor injection.

## SC-02-02 Typosquatting
**Description:** Developer installs a lookalike package (e.g., reqeusts vs requests).
**Prereqs:** Manual install; weak review; permissive dependency policy.
**Impact:** Malicious code execution; data exfiltration.

## SC-02-03 Malicious Maintainer / Account Takeover
**Description:** Maintainer account compromised; attacker ships malicious update.
**Prereqs:** High-trust dependency; auto-updates; weak pinning.
**Impact:** Large blast radius through transitive deps.

## SC-02-04 Transitive Dependency Explosion
**Description:** A “safe” top-level dependency pulls risky transitive deps.
**Prereqs:** No dependency graph visibility; no policy gates.
**Impact:** Hidden vulnerabilities; licensing risk; unexpected binaries.

## SC-02-05 Poisoned Internal Mirror / Proxy
**Description:** Internal proxy caches a malicious version and serves it as “trusted”.
**Prereqs:** Proxy without integrity checks; weak access control.
**Impact:** Organization-wide compromise.

## SC-02-06 Lockfile / Manifest Tampering
**Description:** Attacker modifies lockfile to point to malicious versions or git URLs.
**Prereqs:** PR review bypass; compromised dev credentials.
**Impact:** Silent malicious dependency injection.

## SC-02-07 Git-based Dependencies / Unpinned Refs
**Description:** Dependencies pulled from git by branch/tag (not commit hash).
**Prereqs:** Unpinned refs; weak repo controls.
**Impact:** Non-reproducible builds; supply chain injection.

## SC-02-08 Install Scripts / Postinstall Hooks Abuse
**Description:** Packages execute scripts during install (npm postinstall, setup.py).
**Prereqs:** Allowed scripts; no sandboxing.
**Impact:** RCE in dev/CI; secret theft.

## SC-02-09 Registry Credential Leakage
**Description:** Token leaks via logs/env vars and is used to publish/poison packages.
**Prereqs:** Tokens in CI variables; permissive scopes.
**Impact:** Publish malicious versions; exfiltrate private packages.

## SC-02-10 “Hotfix” Bypass
**Description:** In urgent delivery, engineers bypass policy gates to ship.
**Prereqs:** No enforcement; cultural pressure.
**Impact:** Controls are unreliable in the moments that matter most.
