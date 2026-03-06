# Phase 7 — Backup & Disaster Recovery

## Step 7.1 — Recovery Services Vault

Vault Name: rsv-contoso-backup  
Resource Group: rg-contoso-backup  
Region: Central India  
Redundancy: Geo-redundant storage (GRS)

Purpose:
Central vault for backup policies, recovery points, and restore operations.

## Step 7.2 — VM Backup Configuration

Protected VM:
vm-dev-web-01

Backup Vault:
rsv-contoso-backup

Backup Policy:
policy-vm-daily-backup

Schedule:
Daily backup at 02:00 AM

Retention:
30 days

Purpose:
Protect virtual machine data and enable disaster recovery.

## Step 7.3 — VM Restore Test

Performed disaster recovery validation using Azure Backup.

Source VM:
vm-dev-web-01

Recovery Vault:
rsv-contoso-backup

Restore Method:
Create new virtual machine

Restored VM:
vm-restore-test

Purpose:
Validate backup integrity and recovery capability.

## Step 7.4 — Disaster Recovery Validation

Performed restore test using Azure Backup.

Source VM:
vm-dev-web-01

Restored VM:
vm-restore-test

Outcome:
VM successfully restored and validated.

Additional protections:

SQL Database (built-in protection):
- Automatic backups enabled
- Point-in-time restore capability

Storage Account (built-in protection):
- Recommended protections include soft delete, Immutable storage and versioning.
