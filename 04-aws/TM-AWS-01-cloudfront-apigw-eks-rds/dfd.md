# Data Flow Diagram (DFD)

## External Entities
- End User
- Admin
- IAM

## Processes
- CloudFront / API Gateway
- Application services running in EKS

## Data Stores
- Amazon RDS
- Amazon S3
- AWS Secrets Manager

## Data Flows
1. User sends HTTPS request to CloudFront
2. CloudFront/WAF forwards request to API Gateway
3. API Gateway forwards request to EKS service
4. EKS service queries RDS
5. EKS service reads/writes S3
6. EKS service retrieves secrets from Secrets Manager
7. Admin accesses management plane
