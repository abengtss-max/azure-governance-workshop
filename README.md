# Azure Governance & Reporting Workshop

**Customer:** Region Stockholm  
**Duration:** Full Day (09:00 – 16:30)  
**Audience:** Non-technical stakeholders  
**Focus:** Cost Analysis, Resource Inventory, Governance Reporting

---

## Workshop Agenda

| Time | Module | Topics |
|---|---|---|
| 09:00 – 09:30 | Welcome | Azure structure, portal orientation |
| 09:30 – 10:30 | [Module 1: Azure Core Concepts](./01-azure-core-concepts/README.md) | Hierarchy, naming, tagging |
| 10:30 – 10:45 | *Coffee Break* | |
| 10:45 – 12:00 | [Module 2: Cost Management & Analysis](./02-cost-management/README.md) | Billing, cost analysis, budgets, exports |
| 12:00 – 13:00 | *Lunch* | |
| 13:00 – 14:00 | [Module 3: Resource Inventory & Visibility](./03-resource-inventory/README.md) | Resource Graph, health, activity log |
| 14:00 – 14:45 | [Module 4: Governance & Compliance](./04-governance-compliance/README.md) | Azure Policy, Defender, RBAC |
| 14:45 – 15:00 | *Coffee Break* | |
| 15:00 – 15:45 | [Module 5: Dashboards & Reporting](./05-dashboards-reporting/README.md) | Dashboards, Workbooks, Power BI |
| 15:45 – 16:15 | [Module 6: Scenarios & Q&A](./06-scenarios-qa/README.md) | Real-world walkthroughs |
| 16:15 – 16:30 | Wrap-Up | Takeaways, cheat sheet, feedback |

---

## Prerequisites & Setup

See [setup/README.md](./setup/README.md) for:
- Required Azure roles for attendees
- Optional resource deployment for richer cost demos

## Quick Reference

See [cheatsheet.md](./cheatsheet.md) for portal links, KQL queries, and tips.

---

## Environment Context (Region Stockholm)

The workshop uses a real Azure Landing Zone with 10 subscriptions:

| Subscription | Purpose |
|---|---|
| `management` | Monitoring, Log Analytics |
| `connectivity` / `connectivity-2` | Hub networking |
| `identity` / `identity-2` | Entra ID |
| `security` / `security-2` | Defender for Cloud |
| `bootstrap` | Platform automation |
| `subcription-vending` | Subscription vending |
| `applz-5` | Application workload |

> **Note:** Resources currently have no tags. This is intentional — used as a live teaching example in Module 1 and Module 2.
