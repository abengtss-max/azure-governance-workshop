# Module 3: Resource Inventory & Visibility

**Time:** 13:00 – 14:00  
**Goal:** Know exactly what resources exist, where they are, who changed them, and whether they are healthy.

---

## 3.1 The Challenge of Visibility

With 10 subscriptions, it is hard to get a complete picture of what resources exist just by clicking through the portal. **Azure Resource Graph** solves this — it lets you query all resources across all subscriptions at once.

---

## 3.2 Azure Resource Graph Explorer

Resource Graph lets you run queries across your entire Azure environment.

### Step 1 — Open Resource Graph Explorer
1. Go to [https://portal.azure.com](https://portal.azure.com)
2. In the search bar, type **Resource Graph Explorer**
3. Press Enter

### Step 2 — Run Your First Query: Count All Resources
```kql
resources
| summarize count() by subscriptionId
```
1. Paste the query above into the query window
2. Click **Run query**
3. You will see a row per subscription with the resource count

> **For Region Stockholm:** This will show counts across all 10 subscriptions in one view.

### Step 3 — List All Resources with Type and Location
```kql
resources
| project name, type, resourceGroup, subscriptionId, location
| order by type asc
```

### Step 4 — Find Resources With No Tags
```kql
resources
| where isnull(tags) or tags == "{}"
| project name, type, resourceGroup, subscriptionId
| order by subscriptionId asc
```
> **Expected result for Region Stockholm:** Most or all resources will appear — confirming the tagging gap identified in Module 1.

### Step 5 — Count Resources by Type
```kql
resources
| summarize count() by type
| order by count_ desc
```

### Step 6 — Export Results to CSV
1. After running any query, click **Download as CSV**
2. This gives you a full inventory spreadsheet

---

## 3.3 Resource Health

Resource Health shows whether individual resources are running, degraded, or unavailable.

### Step-by-Step: Check Resource Health
1. Navigate to any resource (e.g., a Storage Account in the `management` subscription)
2. In the left menu, scroll down and click **Resource health**
3. View the current status and the health history
4. Green = Available, Yellow = Degraded, Red = Unavailable

### Step-by-Step: View Service Health (Platform-Wide)
1. In the search bar, type **Service Health**
2. Press Enter
3. Set the **Region** filter to **Sweden Central** (your primary region)
4. View any active incidents or planned maintenance
5. Click **Health history** to see past events
6. Click **Health alerts** → **+ Add service health alert** to get notified of future incidents

---

## 3.4 Activity Log — Who Did What, When

The Activity Log records every control-plane action in Azure: who created, modified, or deleted a resource.

### Step-by-Step: View the Subscription Activity Log
1. Navigate to a subscription (e.g., `applz-5`)
2. In the left menu, click **Activity log**
3. Set the time range to **Last 7 days**
4. Browse the events — each row shows:
   - **Operation** — what was done (e.g., "Create or Update Storage Account")
   - **Status** — Succeeded / Failed
   - **Time** — when it happened
   - **Initiated by** — the user or service principal that made the change

### Step-by-Step: Filter by Operation
1. Click **Add filter**
2. Select **Operation**
3. Type `delete` and press Enter
4. View all deletion events — useful for investigating incidents

### Step-by-Step: Export Activity Log
1. In Activity Log, click **Export Activity Logs** (top menu)
2. Configure a diagnostic setting to send logs to:
   - A **Log Analytics Workspace** (for querying later)
   - A **Storage Account** (for long-term archiving)
   - An **Event Hub** (for streaming to a SIEM)

---

## 3.5 Azure Monitor — Environment Overview

### Step-by-Step: Open Azure Monitor
1. In the search bar, type **Monitor** and press Enter
2. The **Overview** page shows alerts, service health, and activity across all subscriptions
3. Click **Alerts** — see all active alerts
4. Click **Activity log** — cross-subscription view

---

## 3.6 Key Takeaways

- Resource Graph gives a complete, cross-subscription inventory in seconds
- Use the "no tags" query regularly to identify resources that need tagging
- Activity Log answers "who changed this?" — keep it for at least 90 days (default)
- Service Health alerts notify you of Azure platform incidents affecting your region

---

**Next:** [Module 4 — Governance & Compliance](../04-governance-compliance/README.md)
