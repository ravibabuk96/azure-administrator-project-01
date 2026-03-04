# Phase 5 — Security & Identity

## Azure Key Vault

Name: kv-contoso-secure  
Purpose: Secure storage of application secrets and credentials.

---

## Managed Identity

Enabled system-assigned identity for App Service.

Benefit:
Allows secure authentication without storing credentials.

---

## Key Vault Secret

Stored SQL connection string as secret:

Name: sql-connection-string

---

## RBAC Integration

Assigned role:
Key Vault Secrets User

Principal:
App Service Managed Identity

---

## Secure Secret Retrieval

Configured App Service to use Key Vault reference.

Outcome:
Application retrieves secrets securely using identity-based authentication.

## Key Vault Private Endpoint

Private Endpoint: pe-kv-contoso-secure  
Subnet: snet-private-endpoints  
Private DNS Zone: privatelink.vaultcore.azure.net  

Public network access disabled.

Purpose:
Restrict Key Vault access to private network only.


## Security Improvement Achieved

Before:
Key Vault → Public Internet

Now:
App Service
↓
Private VNet
↓
Private Endpoint
↓
Key Vault

This is Zero Trust PaaS architecture.


Application Flow:

Internet
   ↓
Application Gateway (Hub)
   ↓
App Service
   ↓
VNet Integration
   ↓
Private Endpoints
   ↓
SQL Database / Storage / Key Vault
