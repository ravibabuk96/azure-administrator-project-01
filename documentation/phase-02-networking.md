# Phase 2 — Networking

In enterprise design:
Hub = shared services
Spokes = workload environments (Dev / Prod)

## Step 2.1 — Hub Virtual Network

VNet Name: vnet-contoso-hub  
Resource Group: rg-contoso-prod  
Region: Central India  
Address Space: 10.0.0.0/16  

Subnets:
- AzureBastionSubnet: 10.0.0.0/24

Purpose:
Central hub network for shared connectivity services.

## Step 2.2 — Dev Spoke Virtual Network

VNet Name: vnet-contoso-dev  
Resource Group: rg-contoso-dev  
Region: Central India  
Address Space: 10.1.0.0/16  

Subnets:
- snet-web-dev : 10.1.1.0/24
- snet-app-dev : 10.1.2.0/24
- snet-db-dev  : 10.1.3.0/24

Purpose:
Dedicated development workload network segmented into web, application, and database tiers.

## Step 2.3 — Prod Spoke Virtual Network

VNet Name: vnet-contoso-prod  
Resource Group: rg-contoso-prod  
Region: Central India  
Address Space: 10.2.0.0/16  

Subnets:
- snet-web-prod : 10.2.1.0/24
- snet-app-prod : 10.2.2.0/24
- snet-db-prod  : 10.2.3.0/24

Tags Applied:
- Environment : Prod
- Project : Contoso-Infrastructure
- Owner : AzureAdmin
- CostCenter : IT

Purpose:
Dedicated production workload network segmented into web, application, and database tiers with strict environment isolation.

## Step 2.4 — VNet Peering Configuration

Hub ↔ Dev Peering:
- peer-hub-to-dev
- peer-dev-to-hub

Hub ↔ Prod Peering:
- peer-hub-to-prod
- peer-prod-to-hub

Configuration:
- Allow virtual network access: Enabled
- Forwarded traffic: Disabled
- Gateway transit: Disabled
- Remote gateway: Disabled

Purpose:
Enable centralized hub connectivity while maintaining Dev and Prod isolation.


✅ Phase 2 Completed

- Hub VNet (10.0.0.0/16)
- Dev VNet (10.1.0.0/16)
- Prod VNet (10.2.0.0/16)
- Proper subnet segmentation
- Bidirectional VNet peering
- Governance-compliant tagging

