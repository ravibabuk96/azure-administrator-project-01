# Phase 6 — Monitoring & Observability
Objective: Centralize logs, metrics, diagnostics, and alerts across all Azure resources.

Resources we will monitor:VM's, Application Gateway, App Service, SQL Database, Storage Account, Key Vault

## Step 6.1 — Log Analytics Workspace

Name: law-contoso-monitoring  
Resource Group: rg-contoso-prod  
Region: Central India  

Purpose:
Centralized log collection for infrastructure and platform services.

Capabilities:
- Query logs using KQL
- Troubleshoot infrastructure issues
- Monitor performance metrics

## Step 6.2 — VM Monitoring

Enabled Azure Monitor Insights for vm-dev-web-01.

Log destination:
law-contoso-monitoring (Log Analytics Workspace)

Metrics collected:
- CPU utilization
- Memory usage
- Disk I/O
- Network traffic

Validation:
Heartbeat logs confirmed VM connectivity with monitoring workspace.

Query Example:
Heartbeat
| where Computer contains "vm-dev-web-01"
| sort by TimeGenerated desc


## Step 6.3 — Application Gateway Monitoring

Enabled diagnostic logs (Monitor-> Diagnostic settings) for agw-contoso-hub.

Log destination:
law-contoso-monitoring (Log Analytics Workspace)

Enabled logs:
- AGW Access logs
- AGW Performance logs
- AGW Firewall (WAF) logs

These logs help troubleshoot issues like:
- 502 / 503 gateway errors
- backend server failures
- high latency
- traffic patterns

Purpose:
Monitor incoming traffic, gateway performance, and backend connectivity.

Query Example:
AzureDiagnostics
| where ResourceType == "APPLICATIONGATEWAYS"
| sort by TimeGenerated desc

## Step 6.4 — App Service Monitoring

Enabled diagnostic logs for app-contoso-dev-01.

Log destination: law-contoso-monitoring

Enabled logs:
- HTTP logs
- Console logs
- Application logs
- Audit logs
- IPSecurity Audit logs
- App Service Platform logs


Enabled Application Insights for app service, validated for real-time telemetry.

Application Insights monitors:

HTTP requests
response time
failed requests
application dependencies
exceptions
live traffic (Incoming request rate, Response time, Failure rate)

Purpose:
Monitor application performance, request failures, and user traffic.

Query Example:
AppServiceHTTPLogs
| sort by TimeGenerated desc


## Step 6.5 — SQL Database Monitoring
This is very useful for: slow queries,database performance,connection failures.

Enabled diagnostic logs for sqldb-contoso-dev.

Destination:
law-contoso-monitoring (Log Analytics Workspace)

Enabled telemetry:
- Query performance logs
- Automatic tuning logs
- Deadlocks
- Connection errors
- Query store statistics

Purpose:
Monitor database performance and troubleshoot application database issues

QueryExample:
AzureDiagnostics
| where ResourceType == "DATABASES"
| sort by TimeGenerated desc

## Step 6.6 — Storage Monitoring

Enabled diagnostic logs for stcontosodev01.

Destination:
law-contoso-monitoring (Log Analytics Workspace)

Enabled logs:
- StorageRead
- StorageWrite
- StorageDelete

Purpose:
Monitor data access operations and detect unauthorized activity.

QueryExample:
StorageBlobLogs
| sort by TimeGenerated desc

## Step 6.7 — Key Vault Monitoring

Enabled diagnostic logs for kv-contoso-secure.

Destination:
law-contoso-monitoring (Log Analytics Workspace)

Enabled logs:
- AuditEvent

Purpose:
These logs are very important for security auditing.

# Event	           Purpose
SecretGet ->	    When a secret is accessed
SecretSet ->	    When a secret is updated
Key operations ->	Encryption/decryption activity
Authentication ->   attempts Who accessed the vault

This helps detect unauthorized secret access.

QueryExample:
StorageBlobLogs
| sort by TimeGenerated desc

## Step 6.8 — Action Group Creation

Created Action Group:

Name: ag-contoso-alerts

Notifications:
- Email alert

Purpose:
Provide notification channel for Azure Monitor alerts.

## Step 6.9 — Alert Rule for VM High CPU 

Alert Name: alert-vm-high-cpu  
Target: vm-dev-web-01  
Metric: Percentage CPU  

Condition:
CPU > 80% for 5 minutes

Action Group:
ag-contoso-alerts

Purpose:
Detect high CPU usage and notify administrators.

## Step 6.10 — Application Gateway Backend Health Alert

Alert Name: alert-appgw-backend-unhealthy  
Target: agw-contoso-hub  

Metric:
Unhealthy Host Count > 0

Severity:
Critical

Action Group:
ag-contoso-alerts

Purpose:
Detect backend server failures behind Application Gateway.

What This Alert Detects

Examples:
Web server down
App Service backend failing
Network connectivity issue
Health probe failure

This is one of the most useful real-world alerts.


## Step 6.11 — SQL Database High DTU Alert

Alert Name: alert-sql-high-dtu  
Target: sqldb-contoso-dev  

Metric:
DTU percentage > 80%

Severity:
Warning

Action Group:
ag-contoso-alerts

Purpose:
Detect database performance issues and high workload.

What This Alert Detects:

Examples:
slow database queries
high application traffic
inefficient indexing
performance bottlenecks

This is a very common production alert.


# Phase 6 — Monitoring & Observability (Completed)

Azure Resources
   │
   │  Diagnostics Logs
   ▼
Log Analytics Workspace
(law-contoso-monitoring)
   │
   │  Azure Monitor
   ▼
Alert Rules
   │
   ▼
Action Group
(ag-contoso-alerts)
   │
   ▼
Email Notification

Central monitoring implemented using Azure Monitor and Log Analytics.

Monitoring coverage includes:

- Virtual Machine monitoring via VM Insights
- Application Gateway diagnostics logs
- App Service application logs
- SQL Database performance monitoring
- Storage account operation logs
- Key Vault audit logs

Alert rules configured:

1. VM High CPU Alert
2. Application Gateway Backend Health Alert
3. SQL Database High DTU Alert

Notifications delivered via Action Group:
ag-contoso-alerts

Outcome:
Full observability platform implemented for infrastructure and PaaS services.
