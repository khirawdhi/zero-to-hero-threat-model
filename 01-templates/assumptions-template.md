# Threat Modeling Assumptions

Document all assumptions clearly.  
Threat models are only as good as their assumptions.

## Assumptions
- Authentication provider is correctly configured and maintained
- Secrets are not hard-coded in source control
- Network segmentation is enforced as designed
- Logging and monitoring are operational

## Non-Goals
- Physical security
- Insider threats (unless explicitly included)
- Legacy systems outside defined scope
