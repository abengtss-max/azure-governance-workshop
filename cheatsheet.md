# Azure Governance Workshop — Cheat Sheet

**Region Stockholm | Quick Reference**

---

## Key Portal Links

| What | URL |
|---|---|
| Azure Portal | https://portal.azure.com |
| Cost Management | https://portal.azure.com/#blade/Microsoft_Azure_CostManagement/Menu/costanalysis |
| Resource Graph Explorer | https://portal.azure.com/#blade/HubsExtension/ArgQueryBlade |
| Azure Policy | https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/Overview |
| Defender for Cloud | https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/Overview |
| Azure Monitor | https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview |
| Service Health | https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade |
| Activity Log | https://portal.azure.com/#blade/Microsoft_Azure_ActivityLog/ActivityLogBlade |
| Dashboards | https://portal.azure.com/#dashboard |

---

## Region Stockholm Subscriptions

| Subscription Name | Subscription ID |
|---|---|
| management | d775d3cc-7245-4744-aa69-bee03036114b |
| connectivity | 1722f280-2f89-42c1-a80f-9a4773491727 |
| connectivity-2 | 029039e3-76a6-4c2e-b3c0-1473059b0193 |
| identity | 57bdcaf9-eabe-4565-a3e4-d2c1557ce700 |
| identity-2 | f96403ae-7ef3-4e36-81a7-cb74a12ce667 |
| security | c001a7f8-e371-42c4-89b9-1a23848a72a0 |
| security-2 | 63aea3b5-e43a-4274-89e3-a06bdd5a77b4 |
| bootstrap | b9794400-1ef6-405c-be7f-2e24ba8bfa1b |
| subcription-vending | f8f58886-bc68-4061-ae1c-a84c15637234 |
| applz-5 | 08436ef1-79fc-4f99-a8c3-1ea611f64196 |

---

## Essential Resource Graph Queries

### Count all resources per subscription
```kql
resources
| summarize count() by subscriptionId
```

### All resources with no tags
```kql
resources
| where isnull(tags) or tags == "{}"
| project name, type, resourceGroup, subscriptionId
```

### All resources with location and type
```kql
resources
| project name, type, resourceGroup, location, subscriptionId
| order by type asc
```

### Count resources by type
```kql
resources
| summarize count() by type
| order by count_ desc
```

### Find all storage accounts
```kql
resources
| where type == "microsoft.storage/storageaccounts"
| project name, resourceGroup, location, subscriptionId
```

---

## Common Cost Management Actions

| Task | Steps |
|---|---|
| View total spend | Cost Management → Cost Analysis → Scope: root MG |
| Spend by department | Cost Analysis → Group by: Tag (department) |
| Export to Excel | Cost Analysis → Download → Excel |
| Create a budget | Cost Management → Budgets → + Add |
| Schedule monthly export | Cost Management → Exports → + Add |
| View forecast | Cost Analysis → set end date to next month |

---

## Required Azure Roles for This Workshop

| Role | Scope | Purpose |
|---|---|---|
| **Reader** | Root management group | View all resources |
| **Billing Reader** | Billing account | View invoices |
| **Cost Management Reader** | Root management group | View cost data |
| **Security Reader** | Root management group | View Defender & Policy |

---

## Monthly Governance Reporting Checklist

- [ ] Export last month's cost data from Cost Management
- [ ] Screenshot or download Policy compliance report
- [ ] Note Defender Secure Score (track trend)
- [ ] Run "resources with no tags" query and review
- [ ] Review Owner/Contributor role assignments
- [ ] Check Service Health for any past incidents
- [ ] Verify budget alerts are still configured

---

## Tagging Standard (Recommended)

| Tag Key | Example Values | Purpose |
|---|---|---|
| `environment` | prod, dev, test, staging | Environment separation |
| `department` | IT, HR, Finance, Clinical | Cost allocation |
| `project` | patient-portal, hr-system | Project cost tracking |
| `cost-center` | CC-1042 | Finance cost code |
| `owner` | ali.bengtsson@region.se | Accountability |
| `managed-by` | terraform, portal, bicep | Deployment tracking |
