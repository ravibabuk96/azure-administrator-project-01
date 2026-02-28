# Phase 3 — Compute Layer

## Step 3.1 — Dev Linux VM Deployment

VM Name: vm-dev-web-01  
Resource Group: rg-contoso-dev  
Image: Ubuntu Server 22.04 LTS  
Size: Standard_B1s  
VNet: vnet-contoso-dev  
Subnet: snet-web-dev  
Public IP: None  

Purpose:
Deploy secure private Linux web server in Dev environment.

## Step 3.2 — Azure Bastion Deployment

Name: bastion-contoso-hub  
VNet: vnet-contoso-hub  
Subnet: AzureBastionSubnet  
Public IP: pip-bastion-contoso  

Purpose:
Provide secure SSH access to private VMs without exposing public IPs.

---

## Step 3.3 — Connectivity Validation

Connected to vm-dev-web-01 via Bastion.

Validation:
- SSH successful
- VM private IP confirmed (10.1.1.x)
- Hub-Spoke peering validated

Outcome:
Secure enterprise connectivity established.

## Step 3.4 — Web Server Installation

Installed Nginx on vm-dev-web-01.

Actions:
- Updated package repository (sudo apt update -y)
- Installed Nginx (sudo apt install nginx -y)
- Started and enabled service (sudo systemctl start nginx, sudo systemctl enable nginx, sudo systemctl status nginx)
- Created custom index.html page: 
  
  sudo nano /var/www/html/index.html

  <h1>Contoso Dev Web Server</h1>
  <p>Azure Administrator Project - Phase 3</p>

  Save: CTRL + X, Y, Enter

Purpose:
Simulate application workload in Dev environment.

## Step 3.5 — Temporary Public Access Test

Actions:
- Assigned temporary Public IP
- Added NSG rule for port 80
- Verified web server access via browser
- Removed Public IP and inbound rule after validation

🚨 Very Important — Security Reminder
Real production systems:
- Do NOT expose VMs directly
- Use Load Balancer or Application Gateway
- Use WAF

Purpose:
Quick functionality validation before implementing enterprise-grade access.

## Step 3.6 — Application Gateway Deployment

Deployed Application Gateway in Hub VNet.

Configuration:
- Public frontend IP
- Backend pool targeting vm-dev-web-01 private IP
- HTTP listener on port 80
- Routing rule configured

Purpose:
Provide enterprise-grade Layer 7 access to web workload without exposing VM publicly.

## Step 3.7 — NSG Configuration (Dev Web Subnet)

Created NSG: nsg-dev-web  
Associated with: snet-web-dev  

Inbound Rule:
- Allow TCP 80 from 10.0.1.0/24 (App Gateway subnet)

Purpose:
Restrict web tier access to only Application Gateway and block direct traffic.

## Step 3.8 — Dev App Subnet Security

Created NSG: nsg-dev-app  
Allowed TCP 8080 only from Web subnet (10.1.1.0/24)  
Associated with snet-app-dev  

---

## Step 3.9 — Dev DB Subnet Security

Created NSG: nsg-dev-db  
Allowed TCP 1433 only from App subnet (10.1.2.0/24)  
Associated with snet-db-dev  

---

## Step 4 — Security Validation

Tested Application Gateway connectivity after NSG restrictions.

Result:
- Web traffic works only via App Gateway
- Direct access blocked
- Subnet-level segmentation confirmed

🔍 Security Model Now Looks Like

- Web tier: Accepts traffic only from App Gateway
- App tier: Accepts traffic only from Web subnet
- DB tier :  Accepts traffic only from App subnet

This is proper 3-tier segmentation.
