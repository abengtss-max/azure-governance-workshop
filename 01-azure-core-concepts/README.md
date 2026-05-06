# Module 1: Azure Core Concepts

**Time:** 09:30 – 10:30  
**Goal:** Understand how Azure is structured and why it matters for reporting.

---

## 1.1 The Azure Management Hierarchy

Azure resources are organized in a strict hierarchy. Understanding this is key to understanding cost and governance reports.

```
Tenant (Region Stockholm)
└── Management Group (root)
    ├── Management Group (Platform)
    │   ├── Subscription: management
    │   ├── Subscription: connectivity
    │   ├── Subscription: identity
    │   └── Subscription: security
    └── Management Group (Landing Zones)
        └── Subscription: applz-5
```

### Why this matters for reporting
- **Costs** can be aggregated at any level (subscription, resource group, or individual resource)
- **Policies** are inherited downward — compliance reports reflect the full hierarchy
- **Access** is granted at any level and flows down

---

## 1.2 Navigate the Azure Portal

### Step 1 — Open the Portal
1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Sign in with your Region Stockholm credentials

### Step 2 — View All Subscriptions
1. In the top search bar, type **Subscriptions** and press Enter
2. You will see all subscriptions you have access to
3. Note the **Subscription ID** column — this is used in cost exports and queries

### Step 3 — Explore a Resource Group
1. Click on the **applz-5** subscription
2. Click **Resource groups** in the left menu
3. Click into any resource group
4. Observe the list of resources, their types, and locations

### Step 4 — View the Management Group hierarchy
1. In the top search bar, type **Management groups**
2. Click the root management group
3. Expand the tree — observe how subscriptions are organized

---

## 1.3 Naming Conventions

Good naming makes reports readable. Resources follow a convention like:

```
<type>-<workload>-<environment>-<region>-<instance>
Example: rg-payments-prod-swedencentral-001
```

### Why this matters
- In cost reports, you filter and group by resource name/resource group
- Without consistent naming, cost reports become unreadable

---

## 1.4 Tags — The #1 Tool for Cost Allocation

Tags are key-value pairs attached to resources. They are the **primary mechanism** for splitting costs by department, project, or environment.

### Example tags
| Tag Key | Tag Value |
|---|---|
| `department` | `IT` / `HR` / `Finance` |
| `environment` | `prod` / `dev` / `test` |
| `project` | `patient-portal` |
| `cost-center` | `CC-1042` |

### Step-by-Step: View Tags on Resources
1. Navigate to any resource in the portal
2. Click **Tags** in the left menu
3. Observe whether tags exist

> **Live observation for Region Stockholm:** Currently, resources in this environment have **no tags**. This means cost reports cannot be split by department or project. Adding tags is a key recommendation from this workshop.

### Step-by-Step: Add a Tag to a Resource Group
1. Navigate to a Resource Group
2. Click **Tags** in the left menu
3. Enter `environment` = `demo` in the fields
4. Click **Apply**
5. Note: Tags on a resource group do NOT automatically apply to resources inside it — you need Azure Policy to enforce tag inheritance

---

## 1.5 Key Takeaways

- Azure is organized: Tenant → Management Groups → Subscriptions → Resource Groups → Resources
- Subscriptions are the **billing boundary** — costs are tracked per subscription
- Tags are the **reporting tool** for cost allocation by department or project
- Without tags, you cannot split costs meaningfully in reports

---

**Next:** [Module 2 — Cost Management & Analysis](../02-cost-management/README.md)
