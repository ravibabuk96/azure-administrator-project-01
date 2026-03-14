# Contoso Azure Enterprise Infrastructure Project

## Project Overview

This project demonstrates the design and implementation of a **production-style Microsoft Azure infrastructure environment** using enterprise architecture practices.

The infrastructure simulates a real cloud platform that includes networking, compute services, platform services, serverless processing, security, monitoring, disaster recovery, and automation.

The goal of this project is to showcase the practical capabilities required for an **Azure Administrator / Cloud Engineer role**.

---

# Architecture Summary

The system follows a **layered enterprise architecture**.

```
Internet
   │
   ▼
Application Gateway
   │
   ▼
App Service
   │
   ▼
Azure Functions (Serverless Processing)
   │
   ▼
Azure SQL Database
```

Supporting infrastructure layers include networking, monitoring, backup, and automation services.

---

# Architecture Diagram

The infrastructure is built using a **Hub-Spoke network topology**.

Hub network hosts shared services such as Application Gateway and Bastion.

Spoke network hosts application workloads.

Key architectural components:

| Layer             | Services                                     |
| ----------------- | -------------------------------------------- |
| Networking        | Hub-Spoke VNet, Application Gateway, Bastion |
| Compute           | Azure Virtual Machine                        |
| Platform Services | App Service, SQL Database, Storage           |
| Serverless        | Azure Functions                              |
| Security          | Key Vault, Managed Identity                  |
| Monitoring        | Azure Monitor, Log Analytics                 |
| Backup            | Recovery Services Vault                      |
| Automation        | Azure Automation                             |

---

# Project Phases

The project was implemented in multiple phases to simulate a real infrastructure deployment lifecycle.

| Phase     | Description                          |
| --------- | ------------------------------------ |
| Phase 1   | Foundation & Governance              |
| Phase 2   | Hub-Spoke Networking                 |
| Phase 3   | Compute Layer                        |
| Phase 4   | Platform Services                    |
| Phase 4.5 | Serverless Compute (Azure Functions) |
| Phase 5   | Security & Identity                  |
| Phase 6   | Monitoring & Observability           |
| Phase 7   | Backup & Disaster Recovery           |
| Phase 8   | Automation & Operations              |
| Phase 9   | Governance Hardening                 |

Detailed implementation documentation is available in the **documentation** folder.

---

# Key Azure Services Used

This project demonstrates the use of multiple Azure services.

| Service                 | Purpose                         |
| ----------------------- | ------------------------------- |
| Azure Virtual Network   | Network segmentation            |
| Application Gateway     | Layer 7 load balancing          |
| Azure Bastion           | Secure VM access                |
| Azure App Service       | Web application hosting         |
| Azure Functions         | Serverless event processing     |
| Azure SQL Database      | Managed relational database     |
| Azure Storage           | Blob storage and event triggers |
| Azure Key Vault         | Secure secret management        |
| Azure Monitor           | Centralized monitoring          |
| Log Analytics Workspace | Log aggregation                 |
| Azure Backup            | Data protection                 |
| Recovery Services Vault | Backup management               |
| Azure Automation        | Operational automation          |

---

# Security Design

The infrastructure follows **zero-trust security principles**.

Security controls implemented:

* Managed Identity authentication
* Private Endpoints for platform services
* Azure Key Vault for secrets
* Network isolation using Hub-Spoke topology

Sensitive services are not exposed to the public internet.

---

# Monitoring & Observability

Centralized monitoring is implemented using Azure Monitor.

Resources send diagnostic logs to a **Log Analytics Workspace**.

Alert rules detect operational issues including:

* VM CPU overload
* Application Gateway backend failures
* SQL database performance issues

Notifications are delivered through Azure Monitor Action Groups.

---

# Backup & Disaster Recovery

Backup architecture is implemented using Azure Backup.

Protected workloads include:

* Virtual Machines
* Azure SQL Database
* Storage services

A restore test was performed to validate disaster recovery capability.

---

# Automation

Operational tasks are automated using Azure Automation.

Example automation:

Daily shutdown of development VM using a scheduled runbook.

This reduces operational costs and demonstrates infrastructure automation.

---

# Skills Demonstrated

This project demonstrates the following Azure capabilities:

* Azure infrastructure architecture design
* Hub-Spoke networking implementation
* Platform service deployment
* Serverless event-driven processing
* Managed identity security
* Private endpoint configuration
* Monitoring and alerting
* Disaster recovery implementation
* Infrastructure automation

---

# Repository Structure

```
architecture/
    architecture-overview.md
    project-visual-flow.md
documentation/
    phase-01-foundation-governance.md
    phase-02-networking.md
    phase-03-compute.md
    phase-04-platform-services.md
    phase-04.1-serverless-compute.md
    phase-05-security-identity.md
    phase-06-monitoring-observability.md
    phase-07-backup-disaster-recovery.md
    phase-08-automation-operations.md
    phase-09-governance-hardening.md

troubleshooting-playbooks/
    
```

---

# Author

Azure Infrastructure Project created as a practical implementation of enterprise cloud architecture.

Technologies used:

Microsoft Azure
Azure Administrator Practices
Cloud Infrastructure Design
