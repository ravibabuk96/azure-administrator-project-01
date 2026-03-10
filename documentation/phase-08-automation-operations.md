# Phase 8 — Automation & Operations

## Step 8.1 — Automation Account

Automation Account:
aa-contoso-automation

Resource Group:
rg-contoso-monitoring

Region:
Central India

Identity:
System-assigned managed identity enabled.

Purpose:
Host runbooks to automate operational tasks in the Azure environment.

## Step 8.2 — VM Auto Shutdown Runbook

Runbook Name: stop-dev-vm-runbook  
Automation Account: aa-contoso-automation  

Target VM:
vm-dev-web-01

Script Example:
Connect-AzAccount -Identity

$resourceGroup = "rg-contoso-dev"
$vmName = "vm-dev-web-01"
Stop-AzVM -ResourceGroupName $resourceGroup -Name $vmName -Force

Stops the development VM using managed identity authentication.

Purpose:
Automate cost optimization by shutting down non-production VM resources.

## Step 8.3 — Runbook Schedule

Runbook: stop-dev-vm-runbook  
Schedule: schedule-vm-shutdown  

Execution:
Daily at 7:00 PM (IST)

Every day:

7:00 PM
   ↓
Automation Runbook
   ↓
Managed Identity Authentication
   ↓
Stop vm-dev-web-01

Purpose:
Automate shutdown of development VM to reduce operational cost.

Phase 8 Status:

| Automation Component | Status |
| -------------------- | ------ |
| Automation Account   | ✅      |
| Managed Identity     | ✅      |
| Runbook              | ✅      |
| Runbook Test         | ✅      |
| Scheduled Execution  | ✅      |

