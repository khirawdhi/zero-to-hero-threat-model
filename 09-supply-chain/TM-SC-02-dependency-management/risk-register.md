# Risk Register

| Threat | Impact | Likelihood | Risk | Notes |
|---|---|---:|---:|---|
| Dependency confusion | Critical | Medium | Critical | common in mixed registry setups |
| Typosquatting | High | Medium | High | increases with manual installs |
| Maintainer takeover | Critical | Medium | Critical | especially popular packages |
| Lockfile tampering | High | Medium | High | PR review controls matter |
| Git deps unpinned | High | Low | Medium | depends on engineering habits |
| Postinstall script abuse | Critical | Medium | Critical | frequent in npm ecosystem |
| Token leakage | Critical | Low/Med | High | depends on CI hygiene |
| Proxy poisoning | Critical | Low | High | org-wide blast radius |
