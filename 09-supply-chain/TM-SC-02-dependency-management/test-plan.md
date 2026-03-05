# Test Plan — Dependency Management

## Validation checks
- Attempt dependency confusion by creating an internal-looking package name and ensuring it is blocked
- Introduce typosquatted dependency in a PR and validate policy gate catches it
- Modify lockfile in PR and ensure CODEOWNERS/review is required
- Verify install scripts are blocked or sandboxed in CI
- Ensure registry tokens are scoped read-only where possible
- Confirm dependency scanning runs on PR and main builds

## Evidence artifacts
- CI logs/screenshots
- policy config files
- dependency scan reports
- SBOM output and storage location
