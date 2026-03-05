# CI/CD Pipeline Architecture

Typical CI/CD pipeline architecture:

Developer
↓
Source Code Repository (GitHub / GitLab)
↓
CI/CD Pipeline
↓
Build System
↓
Artifact Repository
↓
Container Registry
↓
Deployment Environment (Kubernetes / Cloud)

## Trust Boundaries

External Contributors  
Internal Development Environment  
CI/CD Infrastructure  
Artifact Storage  
Production Infrastructure

## Assets

- source code
- build artifacts
- container images
- secrets
- CI/CD credentials
- deployment configurations
