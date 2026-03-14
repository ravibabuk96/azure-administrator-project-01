# Contoso Azure Enterprise Infrastructure

## Architecture Overview

## Introduction

This project demonstrates a **production-style Azure cloud infrastructure architecture** designed using enterprise best practices.

The environment simulates a real-world cloud platform that includes networking, compute resources, platform services, serverless processing, security controls, monitoring, backup, and operational automation.

The architecture is structured in multiple layers to ensure **scalability, security, and operational reliability**.

---

# Architecture Design Principles

The infrastructure was designed using the following cloud architecture principles:

| Principle     | Description                                           |
| ------------- | ----------------------------------------------------- |
| Scalability   | Services automatically scale based on demand          |
| Security      | Zero-trust access using identity-based authentication |
| Reliability   | Backup and disaster recovery implemented              |
| Observability | Centralized monitoring and alerting                   |
| Automation    | Operational tasks automated using runbooks            |

These principles align with the **Azure Well-Architected Framework**.

---

# High-Level Architecture

The infrastructure follows a **layered architecture model**.

Internet
   │
   ▼
Application Gateway
   │
   ▼
App Service
   │
   ▼
Azure Functions
   │
   ▼
Azure SQL Database


Supporting infrastructure layers include networking, monitoring, security, and automation services.

---

# Network Architecture

The environment uses a **Hub-Spoke network topology**.

Hub-Spoke networking is commonly used in enterprise Azure environments to centralize shared services and isolate application workloads.

## Hub Network

The hub network hosts shared infrastructure services.

| Service                   | Purpose                        |
| ------------------------- | ------------------------------ |
| Application Gateway       | Layer 7 load balancing         |
| Azure Bastion             | Secure VM access               |
| Network security controls | Centralized traffic management |

---

## Spoke Network

The spoke network hosts application workloads.

| Service           | Purpose                            |
| ----------------- | ---------------------------------- |
| Virtual Machine   | Web workload                       |
| App Service       | Web application hosting            |
| Azure Functions   | Event-driven processing            |
| Private Endpoints | Secure access to platform services |

This separation improves security and operational control.

---

# Compute Layer

The architecture uses two compute models:

## Virtual Machines

A Linux virtual machine simulates traditional infrastructure workloads.

Example resource:

vm-dev-web-01

This VM is protected using Azure Backup and monitored using Azure Monitor.

---

## Platform Compute

Application workloads run on **Azure App Service**, which provides managed web hosting.

Benefits include:

* automatic scaling
* platform patching
* built-in monitoring
* high availability

---

# Serverless Processing Layer

The architecture includes **Azure Functions** to enable event-driven serverless computing.

Azure Functions automatically execute code when triggered by events such as blob uploads.

Workflow:

File Upload
↓
Azure Storage Blob
↓
Blob Trigger Event
↓
Azure Function
↓
SQL Database Update

This design eliminates the need for continuously running servers.

---

# Data Layer

Two primary data services are used.

## Azure SQL Database

Azure SQL Database stores application data.

Features include:

* automated backups
* high availability
* built-in performance monitoring
* point-in-time restore capability

---

## Azure Storage

Azure Storage is used for file storage and event triggering.

Capabilities include:

* blob storage
* event-driven processing
* scalable object storage

---

# Security Architecture

Security is implemented using identity-based access and private networking.

## Identity-Based Access

All services authenticate using:

Microsoft Entra ID
Managed Identity

This removes the need for storing credentials in application code.

---

## Secret Management

Sensitive secrets are stored in:

Azure Key Vault

Secrets include:

* database connection strings
* application configuration values

Applications retrieve secrets securely through managed identity authentication.

---

## Network Security

Sensitive services are secured using **Private Endpoints**.

Protected services:

| Service         | Access Method    |
| --------------- | ---------------- |
| SQL Database    | Private Endpoint |
| Storage Account | Private Endpoint |
| Key Vault       | Private Endpoint |

This prevents public internet access to critical resources.

---

# Monitoring and Observability

Centralized monitoring is implemented using Azure Monitor.

## Monitoring Architecture

```text
Azure Resources
   │
   ▼
Diagnostic Logs
   │
   ▼
Log Analytics Workspace
   │
   ▼
Azure Monitor Alerts
   │
   ▼
Action Group Notifications
```

---

## Monitored Services

Monitoring is enabled for the following components:

| Service             | Monitoring Method      |
| ------------------- | ---------------------- |
| Virtual Machine     | VM Insights            |
| Application Gateway | Access logs            |
| App Service         | Application logs       |
| SQL Database        | Query performance logs |
| Storage             | Operation logs         |
| Key Vault           | Audit logs             |

---

# Backup and Disaster Recovery

The architecture includes a full backup strategy using Azure Backup.

## Backup Infrastructure

Backup vault:

rsv-contoso-backup

Protected resources:

| Resource        | Backup Type              |
| --------------- | ------------------------ |
| Virtual Machine | Azure VM Backup          |
| SQL Database    | Automatic backups        |
| Storage         | Data protection features |

---

## Disaster Recovery Validation

A restore test was performed to validate backup integrity.

Test scenario:

Restore VM from recovery point
↓
Deploy restored VM in test resource group
↓
Verify functionality

This confirms recovery readiness.

---

# Automation and Operations

Operational automation is implemented using Azure Automation.

Automation account:

aa-contoso-automation

Example automation task:

Daily shutdown of development VM.

Workflow:

```text
Automation Schedule
      │
      ▼
Runbook Execution
      │
      ▼
Stop Virtual Machine
```

This reduces operational costs and manual administration.

---

# Governance Model

Governance practices ensure consistent resource management.

## Resource Organization

Resources are separated by environment.

| Resource Group        | Purpose                   |
| --------------------- | ------------------------- |
| rg-contoso-dev        | Development workloads     |
| rg-contoso-test       | Testing environment       |
| rg-contoso-prod       | Production infrastructure |
| rg-contoso-monitoring | Monitoring services       |
| rg-contoso-backup     | Backup resources          |

---

## Tagging Framework

Mandatory tags applied to all resources.

| Tag         | Purpose                          |
| ----------- | -------------------------------- |
| Environment | Identify deployment stage        |
| Project     | Associate resources with project |
| Owner       | Responsible administrator        |
| CostCenter  | Cost tracking                    |

These tags enable governance enforcement through Azure Policy.

---

# Enterprise Architecture Capabilities

This infrastructure demonstrates key Azure cloud capabilities.

| Capability                | Implementation |
| ------------------------- | -------------- |
| Hub-Spoke Networking      | Implemented    |
| Serverless Processing     | Implemented    |
| Managed Identity Security | Implemented    |
| Private Endpoint Security | Implemented    |
| Centralized Monitoring    | Implemented    |
| Disaster Recovery         | Implemented    |
| Operational Automation    | Implemented    |

---

# Conclusion

This project demonstrates a **complete enterprise-style Azure infrastructure environment** that incorporates networking, platform services, serverless computing, monitoring, security, backup, and automation.

The architecture follows modern cloud design patterns and reflects real-world operational practices expected from Azure administrators and cloud engineers.

This implementation showcases the ability to design, deploy, secure, monitor, and operate scalable Azure environments.
