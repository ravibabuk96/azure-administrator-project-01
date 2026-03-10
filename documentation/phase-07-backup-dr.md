# Phase 7 — Backup & Disaster Recovery

## Overview

This phase implements **data protection and disaster recovery capabilities** for the Contoso Azure infrastructure environment.

Backup and recovery operations are managed using **Azure Backup** and **Recovery Services Vault**, ensuring workloads can be restored in case of system failures, data corruption, or infrastructure outages.

Primary objectives:

* Protect critical workloads
* Configure automated backup policies
* Validate recovery procedures
* Demonstrate disaster recovery readiness

Service used:

Azure Backup
Recovery Services Vault

---

# Architecture Context

Protected resources:

| Resource           | Backup Method                       |
| ------------------ | ----------------------------------- |
| vm-dev-web-01      | Azure VM Backup                     |
| Azure SQL Database | Built-in automated backup           |
| Azure Storage      | Soft delete / versioning protection |

Central vault:

rsv-contoso-backup

Resource group:

rg-contoso-backup

---

# Step 7.1 — Recovery Services Vault Deployment

## Purpose

The **Recovery Services Vault** acts as the central management system for backups, recovery points, and restore operations.

All backup policies and protected resources are stored and managed inside the vault.

## Configuration

Vault Name:

rsv-contoso-backup

Resource Group:

rg-contoso-backup

Region:

Central India

Tags applied:

Environment = Shared
Project = Contoso-Infrastructure
Owner = AzureAdmin
CostCenter = IT

## Deployment Steps

1. Navigate to Azure Portal.

2. Search for:

Recovery Services vaults

3. Click:

Create

4. Configure the vault:

Resource Group: rg-contoso-backup
Vault Name: rsv-contoso-backup
Region: Central India

5. Add mandatory governance tags.

6. Click:

Review + Create

7. Deploy the vault.

---

## Backup Redundancy Configuration

After deployment:

Navigate to:

Recovery Services Vault → Backup Infrastructure → Backup Configuration

Configure redundancy:

Geo-redundant storage (GRS)

### Reason

GRS replicates backup data to a secondary region, protecting recovery points from regional disasters.

---

# Step 7.2 — Virtual Machine Backup Configuration

## Target VM

vm-dev-web-01

Resource Group:

rg-contoso-dev

## Backup Policy Design

Backup Frequency:

Daily

Backup Time:

02:00 AM

Retention Policy:

| Backup Type    | Retention |
| -------------- | --------- |
| Daily Backup   | 30 Days   |
| Weekly Backup  | 12 Weeks  |
| Monthly Backup | 12 Months |

This policy represents a **typical enterprise backup strategy**.

---

## Backup Configuration Procedure

1. Navigate to:

Recovery Services Vault → rsv-contoso-backup

2. Select:

Backup

3. Configure backup settings:

Workload location: Azure
What do you want to backup: Virtual Machine

4. Select VM:

vm-dev-web-01

5. Create new policy:

Policy Name:

policy-vm-daily-backup

6. Configure schedule:

Daily backup
02:00 AM

7. Configure retention:

30 days

8. Enable backup.

The VM is now protected by the vault.

---

# Step 7.3 — Initial Backup Execution

After enabling backup, an immediate backup was triggered.

## Procedure

1. Navigate to:

Recovery Services Vault → Backup Items

2. Select:

Azure Virtual Machine

3. Open:

vm-dev-web-01

4. Click:

Backup Now

5. Configure retention:

30 days

6. Start backup job.

---

## Outcome

The backup job completed successfully and created the first **recovery point**.

This recovery point allows the VM to be restored if required.

---

# Step 7.4 — Disaster Recovery Restore Test

## Purpose

Backup systems must be validated through **restore testing** to ensure recovery procedures work correctly.

This step simulates a disaster recovery scenario.

---

## Restore Test Configuration

Source VM:

vm-dev-web-01

Recovery Vault:

rsv-contoso-backup

Restore Method:

Create new virtual machine

Restored VM Name:

vm-restore-test

Target Resource Group:

rg-contoso-test

Target Network:

vnet-contoso-dev

---

## Restore Procedure

1. Navigate to:

Recovery Services Vault → Backup Items

2. Select:

Azure Virtual Machine

3. Open protected VM:

vm-dev-web-01

4. Click:

Restore VM

5. Select restore method:

Create new virtual machine

6. Configure restore settings:

Resource Group: rg-contoso-test
Virtual Network: vnet-contoso-dev
VM Name: vm-restore-test

7. Start restore operation.

---

## Restore Validation

The restored VM deployed successfully.

Validation checks performed:

| Check                     | Result      |
| ------------------------- | ----------- |
| VM deployment             | Successful  |
| OS disk restored          | Verified    |
| Network interface created | Verified    |
| VM boot status            | Operational |

This confirms backup integrity and recovery readiness.

---

## Post-Restore Cleanup

The restore VM was removed to avoid unnecessary resource costs.

Deleted resource:

vm-restore-test

---

# Step 7.5 — SQL Database Protection

The deployed SQL database is protected through built-in automated backups.

Service:

Azure SQL Database

## Backup Characteristics

| Backup Type            | Frequency          |
| ---------------------- | ------------------ |
| Full backup            | Weekly             |
| Differential backup    | Every 12–24 hours  |
| Transaction log backup | Every 5–10 minutes |

Retention:

7–35 days (configurable)

This enables **point-in-time restore capability**.

---

# Step 7.6 — Storage Account Protection

Service:

Azure Storage

Recommended protection features:

| Feature           | Purpose                     |
| ----------------- | --------------------------- |
| Soft Delete       | Recover deleted blobs       |
| Blob Versioning   | Recover overwritten data    |
| Immutable Storage | Prevent accidental deletion |

These features ensure data protection against accidental deletion and data corruption.

---

# Disaster Recovery Capabilities Achieved

| Capability              | Status       |
| ----------------------- | ------------ |
| Central backup vault    | Implemented  |
| Automated VM backup     | Enabled      |
| Recovery points         | Created      |
| Restore testing         | Completed    |
| SQL database protection | Built-in     |
| Storage protection      | Configurable |

---

# Recovery Objectives

| Objective | Description                                       |
| --------- | ------------------------------------------------- |
| RPO       | Recovery Point Objective — data loss tolerance    |
| RTO       | Recovery Time Objective — time to restore service |

The implemented architecture supports recovery scenarios using Azure Backup and built-in platform protection mechanisms.

---

# Phase 7 Outcome

The environment now includes a **fully functional backup and disaster recovery system** capable of restoring critical workloads during failure scenarios.

This phase demonstrates operational capabilities expected from an **Azure Administrator managing production infrastructure**.
