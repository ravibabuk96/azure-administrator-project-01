# Phase 4 — Platform Services (PaaS Layer)

## Objective
Implement secure PaaS services including Azure Storage, Azure SQL Database, and Azure App Service, with private connectivity and enterprise-grade networking.

---

# Step 4.1 — Azure Storage Account

Name: stcontosodev01  
Resource Group: rg-contoso-dev  
Region: Central India  
Performance: Standard  
Redundancy: LRS  
Public Access: Disabled  

Tags:
- Environment: Dev
- Project: Contoso-Infrastructure
- Owner: AzureAdmin
- CostCenter: IT

Purpose:
Provide secure storage for application logs and future artifacts without public exposure.

---

# Step 4.2 — Azure SQL Database Deployment

Server: sql-contoso-dev-01  
Database: sqldb-contoso-dev  
Resource Group: rg-contoso-dev  
Region: Central India  
Compute Tier: Basic (DTU-based)  
Authentication: SQL Authentication  
Public Network Access: Disabled  

Tags:
- Environment: Dev
- Project: Contoso-Infrastructure
- Owner: AzureAdmin
- CostCenter: IT

Purpose:
Deploy secure PaaS relational database for backend services.

Security Design:
- No public endpoint
- Access restricted via Private Endpoint only

---

# Step 4.3 — Azure App Service Deployment

App Name: app-contoso-dev-01  
App Service Plan: asp-contoso-dev (B1)  
Runtime: .NET 8 (LTS)  
Application Insights: Enabled  
Resource Group: rg-contoso-dev  

Tags:
- Environment: Dev
- Project: Contoso-Infrastructure
- Owner: AzureAdmin
- CostCenter: IT

Purpose:
Deploy modern PaaS web application platform for secure database integration.

---

# Step 4.4 — SQL Private Endpoint Implementation

Private Endpoint Name: pe-sql-contoso-dev  
Virtual Network: vnet-contoso-dev  
Subnet: snet-private-endpoints (10.1.4.0/24)  
Private DNS Zone: Enabled (auto-created)

Architecture Flow:
App Service (VNet Integrated)
↓
Private DNS Resolution
↓
Private Endpoint (10.1.4.x)
↓
Azure SQL Database

Outcome:
- SQL public access disabled
- Private IP assigned inside Dev VNet
- Automatic private DNS resolution configured

---

# Step 4.5 — App Service VNet Integration

Integration Subnet:
snet-appservice-integration (10.1.5.0/24)

Configuration:
App Service → Networking → VNet Integration → Added vnet-contoso-dev

Purpose:
Enable outbound connectivity from App Service into Dev VNet.

Security Benefit:
App Service can now reach private resources such as SQL Private Endpoint.

---

# Step 4.6 — App Service to SQL Integration

Connection String Configured:
Name: DefaultConnection  
Type: SQLAzure  

Server:
sql-contoso-dev-01.database.windows.net

Important:
Private DNS resolves this FQDN to private IP (10.1.4.x).

Validation:
Used Kudu console:
nslookup sql-contoso-dev-01.database.windows.net

Result:
Resolved to private IP (10.1.4.x)

Outcome:
- Secure PaaS-to-PaaS connectivity
- No public SQL exposure
- Enterprise-grade internal communication established

## Step 4.7 — Storage Private Endpoint

Private Endpoint Name: pe-storage-contoso-dev  
Sub-resource: blob  
Subnet: snet-private-endpoints  
Private DNS: Enabled  

Outcome:
- Public network access disabled
- Storage accessible only via private endpoint
- Private DNS resolution validated

Architecture Now:

App Service
↓
VNet Integration
↓
Private Endpoint (Storage + SQL)
↓
Fully Private PaaS

Now your Storage design matches SQL design.
This is proper enterprise architecture.

---

# Final Phase 4 Architecture

Internet
↓
Application Gateway (Hub)
↓
App Service (Public Endpoint)
↓
VNet Integration
↓
Private Endpoint (SQL)
↓
Azure SQL Database

Security Characteristics:
- No public database access
- No direct VM database access
- Controlled subnet segmentation
- Private DNS integration
- Application Insights enabled

---

# Phase 4 Completion Status

✔ Storage Account (Private)
✔ SQL Database (Private Endpoint)
✔ App Service (VNet Integrated)
✔ Secure Connection String
✔ Private DNS Validation
✔ Enterprise PaaS Architecture

Phase 4 Completed Successfully.