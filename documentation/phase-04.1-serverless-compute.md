# Phase 4.1 — Serverless Compute Layer

## Overview

This phase introduces **serverless computing** into the Azure infrastructure using Azure Functions.

Serverless architecture allows applications to run code in response to events without provisioning or managing servers. The platform automatically handles scaling, execution, and infrastructure management.

In this project, Azure Functions are used to implement an **event-driven processing pipeline** triggered by file uploads in Azure Storage.

Service used:

Azure Functions

---

# Architecture Context

The serverless component integrates with the existing platform services.

Infrastructure services involved:

| Service              | Purpose                         |
| -------------------- | ------------------------------- |
| Azure Storage        | Blob storage for uploaded files |
| Azure Functions      | Event-driven processing         |
| Azure SQL Database   | Data persistence                |
| Azure Key Vault      | Secure secret retrieval         |
| Application Insights | Function monitoring             |

---

# Event-Driven Architecture

The system follows an **event-driven design pattern**.

When a new file is uploaded to Azure Storage, the Azure Function automatically executes and processes the file.

Architecture flow:

User Upload
↓
Azure Storage Blob Container
↓
Blob Trigger Event
↓
Azure Function Execution
↓
Process File Metadata
↓
Store Results in SQL Database

This architecture removes the need for continuously running servers.

---

# Function App Deployment

A **Function App** acts as the runtime container for serverless functions.

Configuration used:

| Setting           | Value                   |
| ----------------- | ----------------------- |
| Function App Name | func-contoso-processing |
| Resource Group    | rg-contoso-dev          |
| Region            | Central India           |
| Runtime Stack     | Python                  |
| Hosting Plan      | Consumption Plan        |

---

# Hosting Plan Design

Azure Functions supports multiple hosting plans.

The project uses the **Consumption Plan**.

Characteristics:

| Feature                      | Description                     |
| ---------------------------- | ------------------------------- |
| Automatic scaling            | Functions scale based on demand |
| Pay-per-execution            | Billing based on execution time |
| No infrastructure management | Platform-managed runtime        |

This model is ideal for event-driven workloads.

---

# Storage Integration

Azure Functions require a storage account to manage:

* execution state
* trigger events
* function logs
* checkpoints

Storage account used:

stcontosodev01

Blob container example:

uploads

---

# Blob Trigger Configuration

The function uses a **Blob Storage Trigger**.

Trigger behavior:

* When a new file is uploaded to a blob container
* Azure automatically invokes the function
* The function processes the file contents

Example trigger configuration:

Container monitored:

uploads

Event:

BlobCreated

---

# Function Processing Logic

The function performs the following tasks:

1. Detect file upload event
2. Extract metadata from uploaded file
3. Process file content
4. Store metadata in Azure SQL Database

Example processing workflow:

File uploaded
↓
Function triggered
↓
Extract filename and metadata
↓
Insert metadata record into SQL Database

This pattern is commonly used in **data ingestion pipelines**.

---

# Security Architecture

The function follows the same security principles used throughout the environment.

| Component        | Security Method    |
| ---------------- | ------------------ |
| SQL access       | Managed Identity   |
| Secret retrieval | Azure Key Vault    |
| Storage access   | Private Endpoint   |
| Authentication   | Microsoft Entra ID |

Managed Identity eliminates the need for storing database credentials.

---

# Managed Identity Integration

The Function App uses **System Assigned Managed Identity**.

Authentication flow:

Function App
↓
Managed Identity
↓
Microsoft Entra ID
↓
Access Azure resources

This enables secure access to:

* Azure SQL Database
* Azure Key Vault
* Azure Storage

without storing credentials in code.

---

# Secret Management

Sensitive information such as database connection strings are stored in Azure Key Vault.

The function retrieves secrets using Key Vault references.

Example secret:

sql-connection-string

Benefits:

* Centralized secret management
* Secure secret rotation
* No hardcoded credentials

---

# Monitoring and Observability

Function execution is monitored using Application Insights.

Monitoring capabilities include:

| Feature             | Description             |
| ------------------- | ----------------------- |
| Execution logs      | Track function runs     |
| Failure detection   | Identify runtime errors |
| Performance metrics | Measure execution time  |
| Dependency tracking | Monitor SQL calls       |

Application telemetry integrates with Azure Monitor.

---

# Scaling Behavior

Azure Functions automatically scales based on incoming events.

Scaling characteristics:

| Condition             | Behavior                           |
| --------------------- | ---------------------------------- |
| Low workload          | Single instance                    |
| High file upload rate | Multiple instances created         |
| Idle state            | Instances scale down automatically |

This ensures efficient resource utilization.

---

# Enterprise Architecture Insight

Event-driven serverless systems are widely used in modern cloud applications.

Typical enterprise use cases include:

* document processing systems
* image processing pipelines
* log ingestion platforms
* IoT telemetry processing
* data transformation workflows

Serverless computing enables organizations to build scalable applications without managing server infrastructure.

---

# Phase 4.1 Outcome

The infrastructure now supports **event-driven processing using serverless architecture**.

Capabilities implemented:

| Capability                | Status      |
| ------------------------- | ----------- |
| Serverless runtime        | Implemented |
| Blob-triggered execution  | Implemented |
| SQL integration           | Implemented |
| Managed identity security | Implemented |
| Centralized monitoring    | Implemented |

This phase demonstrates the ability to design **modern event-driven Azure architectures used in enterprise cloud environments**.
