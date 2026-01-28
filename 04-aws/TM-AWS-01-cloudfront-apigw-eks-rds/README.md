# TM-AWS-01: CloudFront / API Gateway → EKS → RDS

## Overview
This threat model covers a cloud-native application deployed on AWS using:
- CloudFront and AWS WAF as the internet-facing edge
- Amazon API Gateway as the API entry point
- Amazon EKS for application workloads
- Amazon RDS and S3 for data storage
- AWS Secrets Manager and KMS for secrets and keys

## Architecture Pattern
- Public API
- Microservices on EKS
- IAM-based workload identity (IRSA)
- Private connectivity to data stores

## Goals
- Reuse STRIDE methodology from Azure model
- Identify AWS-specific threat vectors
- Compare and contrast cloud provider controls

## Out of Scope
- End-user device security
- Physical data center security
- Non-AWS workloads
