# Data Flow Diagram (DFD)

## External Entities
- End User
- Admin / Operator
- Azure Entra ID

## Processes
- Azure API Management
- Application services running in AKS

## Data Stores
- Azure SQL Database
- Azure Blob Storage
- Azure Key Vault

## Data Flows
1. User sends HTTPS request to APIM
2. APIM validates authentication token
3. APIM forwards request to AKS service
4. AKS service queries Azure SQL
5. AKS service reads/writes blobs
6. AKS service retrieves secrets from Key Vault
7. Admin accesses management plane
