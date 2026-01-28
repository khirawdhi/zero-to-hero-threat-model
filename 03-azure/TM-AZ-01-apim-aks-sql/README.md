# TM-AZ-01: API Management → AKS → Azure SQL

## Overview
This threat model covers a cloud-native application deployed on Azure using:
- Azure API Management (APIM) as the public entry point
- Azure Kubernetes Service (AKS) for application workloads
- Azure SQL and Blob Storage for data persistence
- Azure Key Vault for secrets and keys

## Architecture Pattern
- Public API
- Microservices on AKS
- Managed identity-based access
- Private connectivity to data stores

## Goals
- Identify threats across trust boundaries
- Apply STRIDE consistently
- Define minimum baseline security controls
- Produce reusable patterns for other cloud providers

## Out of Scope
- End-user device security
- Physical data center security
- Non-Azure workloads
