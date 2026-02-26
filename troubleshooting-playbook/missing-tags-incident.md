# Incident: Missing Tags on Resource

## Incident Summary
A resource was created without mandatory organizational tags, resulting in governance non-compliance and improper cost tracking.

---

## Issue
Developers were able to create Azure resources without required tags such as:

- Environment
- Project
- Owner
- CostCenter

This caused:
- Lack of cost visibility
- Poor resource categorization
- Governance gaps

---

## Root Cause
No Azure Policy enforcement was configured to require mandatory tags during resource creation.

As a result:
- Tagging standards were not enforced
- Compliance relied on manual user input
- No preventive governance control existed

---

## Impact
- Cost allocation could not be accurately tracked
- Resource inventory lacked standardized metadata
- Compliance posture was weakened

---

## Resolution Strategy

Instead of creating multiple separate policies, an Azure Policy **Initiative (Policy Set)** was implemented to centrally enforce mandatory tagging standards at the subscription level.

---

## Governance Implementation Steps

### Step 1 — Created Custom Initiative

Initiative Name:
contoso-mandatory-tagging-initiative

Definition Location:
Subscription level

Category:
Tags

Purpose:
Group multiple mandatory tag policies under a single governance control.

---

### Step 2 — Added Built-in Policy Definitions

Policy Used:
Require a tag on resources (Built-in Azure Policy)

The policy was added 4 times inside the initiative with different parameters:

| Tag Enforced | Effect |
|--------------|--------|
| Environment  | Deny   |
| Project      | Deny   |
| Owner        | Deny   |
| CostCenter   | Deny   |

Configuration Details:
- Parameter Type: Set value
- Effect: Deny
- Configured under Policy Parameters section
- Initiative Parameters were not used (advanced scenario)

---

### Step 3 — Assigned Initiative

Scope:
Subscription level

Reason:
To ensure centralized governance enforcement across project resource groups.

---

### Step 4 — Configured Exclusions

To avoid disrupting existing workloads:

Excluded:
All non-project resource groups containing legacy resources.

Included:
- rg-contoso-dev
- rg-contoso-test
- rg-contoso-prod
- rg-contoso-monitoring
- rg-contoso-backup

Reason:
Enterprise best practice — assign at high level and exclude legacy environments.

---

### Step 5 — Validation Test

Test Performed:
Attempted to create a Storage Account in rg-contoso-dev without required tags.

Result:
Deployment failed with error:
"Request disallowed by policy"

Conclusion:
- Initiative enforcement is active
- Deny effect working correctly
- Governance control successfully implemented

---

## Prevention Implemented

Mandatory tagging is now enforced through:

- Subscription-level Azure Policy Initiative
- Deny effect on missing required tags
- Controlled exclusions for non-project resource groups
- Centralized governance model

---

## Governance Outcome

- Standardized tagging enforcement
- Improved cost tracking readiness
- Enterprise-level governance structure
- Controlled policy rollout strategy
- Compliance validation completed

This implementation reflects real-world Azure Administrator governance practices.
