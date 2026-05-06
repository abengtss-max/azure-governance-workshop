# Module 5: Dashboards & Self-Service Reporting

**Time:** 15:00 – 15:45  
**Goal:** Build reusable dashboards and reporting views that can be checked daily without technical knowledge.

---

## 5.1 Azure Portal Dashboards

Dashboards let you pin charts, metrics, and resource counts to a single page that loads every time you open the portal.

### Step-by-Step: Create a New Dashboard
1. Go to [https://portal.azure.com](https://portal.azure.com)
2. Click the **Dashboard** icon in the left sidebar (or search for **Dashboard**)
3. Click **+ New dashboard**
4. Select **Blank dashboard**
5. Give it a name: `Region Stockholm – Governance Overview`
6. Click **Save**

### Step-by-Step: Pin a Cost Chart
1. Open **Cost Management** → **Cost Analysis**
2. Configure the view you want (e.g., last 3 months, grouped by subscription)
3. Click the **pin icon** (top right of the chart)
4. Select your dashboard: `Region Stockholm – Governance Overview`
5. Click **Pin**
6. Navigate back to your dashboard — the chart now appears

### Step-by-Step: Pin a Resource Count
1. Open **Resource Graph Explorer**
2. Run this query:
```kql
resources
| summarize count()
```
3. Click **Pin to dashboard**
4. Select your dashboard
5. Click **Pin**

### Step-by-Step: Pin Defender Secure Score
1. Open **Defender for Cloud** → **Secure score**
2. Find the score tile
3. Click the **pin icon** in the top right
4. Pin to your dashboard

### Step-by-Step: Pin Policy Compliance
1. Open **Policy** → **Compliance**
2. Click the **pin icon** on the compliance overview chart
3. Pin to your dashboard

### Sharing a Dashboard
1. Open your dashboard
2. Click **Share** in the top menu
3. Select **Publish dashboard**
4. Choose the scope (subscription) to publish to
5. Other users with Reader access can now see and use this dashboard

---

## 5.2 Azure Workbooks — Recurring Operational Reports

Workbooks are interactive reports inside Azure Monitor. They combine text, charts, tables, and queries into a single document.

### Step-by-Step: Open a Built-in Workbook
1. In the search bar, type **Monitor** and press Enter
2. Click **Workbooks** in the left menu
3. You will see a gallery of pre-built workbooks
4. Click **Cost Optimization** (if available) or **Azure Activity**
5. Explore the workbook — it runs live queries automatically

### Step-by-Step: Open the Activity Log Workbook
1. In Workbooks gallery, find **Azure Activity Logs**
2. Click to open it
3. Set the subscription filter to all subscriptions
4. Set the time range to **Last 30 days**
5. The workbook shows: operations by category, failed operations, operations by user

### Step-by-Step: Save and Share a Workbook
1. Open any workbook
2. Click **Edit** → then **Save**
3. Give it a name and select a **Log Analytics workspace** to save it to
4. Share the URL with colleagues — they will see live-refreshed data every time they open it

---

## 5.3 Power BI — Executive Reporting

For scheduled reports shared with leadership, Power BI provides the richest experience.

### Step-by-Step: Build a Simple Cost Report in Power BI
1. Open **Power BI Desktop**
2. Click **Get Data** → search **Azure Cost Management**
3. Connect to your management group (scope)
4. Load the **UsageDetails** and **Budgets** tables
5. Build these visuals:
   - **Card**: Total spend this month
   - **Bar chart**: Spend by subscription
   - **Line chart**: Monthly spend trend (last 6 months)
   - **Table**: Top 10 most expensive resources
6. Click **Publish** → publish to Power BI Service
7. Set a **scheduled refresh** (daily)
8. Share the report link with stakeholders

### Recommended Dashboard Tiles for Management Reporting

| Tile | Data Source | Refresh |
|---|---|---|
| Total monthly cost | Azure Cost Management | Daily |
| Cost vs budget | Azure Cost Management | Daily |
| Top 5 spending subscriptions | Azure Cost Management | Daily |
| Secure Score | Defender for Cloud | Daily |
| Policy compliance % | Azure Policy | Daily |
| Total resource count | Resource Graph | On demand |
| Active high-severity alerts | Azure Monitor | Real-time |

---

## 5.4 Key Takeaways

- Portal dashboards are free, easy to build, and shareable — start here
- Workbooks provide richer operational reports with live data — great for daily checks
- Power BI is best for scheduled reports shared with leadership who don't have portal access
- Pin the 4 most important tiles: Cost, Secure Score, Policy Compliance, Resource Count

---

**Next:** [Module 6 — Scenarios & Q&A](../06-scenarios-qa/README.md)
