# Azure Governance Workshop Cheat Sheet

## Key links

- Azure portal: https://portal.azure.com
- Cost Management
- Resource Graph Explorer
- Azure Policy
- Defender for Cloud
- Azure Monitor
- Activity Log
- Dashboard

## Core queries

```kql
resources
| summarize count() by subscriptionId
```

```kql
resources
| where isnull(tags) or tags == "{}"
| project name, type, resourceGroup, subscriptionId
```

```kql
resources
| summarize count() by type
| order by count_ desc
```

## Monthly checklist

- Export monthly costs
- Review budget threshold alerts
- Review Policy compliance
- Review Defender Secure Score
- Review IAM Owner/Contributor assignments
- Review untagged resources
