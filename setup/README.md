# Workshop Setup

## Attendee Access Requirements

Each attendee needs the following roles **before the workshop**. Assign these at the **root management group** scope so they apply to all 10 subscriptions.

| Role | Why Needed |
|---|---|
| `Reader` | View all resources across all subscriptions |
| `Cost Management Reader` | View cost analysis, budgets, exports |
| `Security Reader` | View Defender for Cloud and Policy compliance |
| `Billing Reader` | View billing and invoices |

### How to Assign Roles (For Azure Admin)

1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Search for **Management groups** and open the root management group
3. Click **Access control (IAM)** → **Role assignments**
4. Click **+ Add** → **Add role assignment**
5. Select the role (e.g., `Cost Management Reader`)
6. Search for the attendee's name or email
7. Click **Save**
8. Repeat for each role

> Attendees with these roles can **view everything but change nothing**. Safe for workshop use.

---

## Optional: Deploy a Log Analytics Workspace for Richer Demos

This is **optional**. Deploy only if you want live monitoring data in the Workbooks and Monitor demos.

The workspace costs approximately **2–5 USD/month** at minimal ingestion.

### Step-by-Step: Deploy via Azure CLI

```bash
# Login
az login

# Set the management subscription as target
az account set --subscription "d775d3cc-7245-4744-aa69-bee03036114b"

# Create resource group if it doesn't exist
az group create \
  --name rg-monitoring-workshop \
  --location swedencentral

# Create Log Analytics Workspace
az monitor log-analytics workspace create \
  --resource-group rg-monitoring-workshop \
  --workspace-name law-workshop-regionstockholm \
  --location swedencentral \
  --sku PerGB2018 \
  --retention-time 30

echo "Done. Workspace created in the management subscription."
```

### Step-by-Step: Deploy via Azure Portal

1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Search for **Log Analytics workspaces**
3. Click **+ Create**
4. Fill in:
   - **Subscription:** `management`
   - **Resource group:** `rg-monitoring-workshop` (create new)
   - **Name:** `law-workshop-regionstockholm`
   - **Region:** Sweden Central
5. Click **Review + Create** → **Create**
6. Wait ~2 minutes for deployment

### After Deployment: Connect Activity Logs

1. Navigate to any subscription
2. Click **Activity log** → **Export Activity Logs**
3. Click **+ Add diagnostic setting**
4. Check **Send to Log Analytics workspace**
5. Select `law-workshop-regionstockholm`
6. Check: **Administrative**, **Security**, **Policy**
7. Click **Save**
8. Repeat for 2–3 subscriptions

---

## Clean Up After Workshop

To remove the workshop resources:

```bash
az group delete --name rg-monitoring-workshop --yes --no-wait
```

This removes the Log Analytics workspace. All other resources used in the workshop are **read-only views** — nothing else was created.

---

## Pre-Workshop Checklist (Admin)

- [ ] Assign Reader + Cost Management Reader + Security Reader + Billing Reader to all attendees at root MG scope
- [ ] Confirm all attendees can log in to https://portal.azure.com
- [ ] (Optional) Deploy Log Analytics workspace if Workbooks demo is planned
- [ ] (Optional) Connect Activity Logs of 2–3 subscriptions to the workspace
- [ ] Pre-build one example dashboard to show during Module 5
- [ ] Download and print cheatsheet.md for attendees
- [ ] Confirm projector/screen shares portal correctly
