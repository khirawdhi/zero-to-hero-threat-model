# TM-GCP-01: Cloud Armor / Apigee → GKE → Cloud SQL

## Overview
This threat model covers a cloud-native application deployed on Google Cloud using:
- Cloud Armor as the internet-facing protection layer
- Apigee (or GCP API Gateway) for API management
- Google Kubernetes Engine (GKE) for application workloads
- Cloud SQL and Google Cloud Storage for data persistence
- Secret Manager for secrets
- Cloud Logging and Monitoring for observability

## Architecture Pattern
- Public API
- Microservices on GKE
- Workload Identity for service authentication
- Private connectivity to managed data stores

## Goals
- Apply STRIDE consistently across clouds
- Identify GCP-specific threat vectors
- Compare security primitives across providers

## Out of Scope
- End-user device security
- Physical infrastructure
- Non-GCP workloads
