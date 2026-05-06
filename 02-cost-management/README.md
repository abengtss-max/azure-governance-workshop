# Module 2: Cost Management & Analysis

**Time:** 10:45 – 12:00  
**Goal:** Read and analyze Azure costs, set budgets, and export data for reporting.

---

## 2.1 Where to Find Cost Data

### Step 1 — Open Cost Management
1. Go to [https://portal.azure.com](https://portal.azure.com)
2. In the search bar, type **Cost Management** and press Enter
3. You are now in the **Cost Management + Billing** blade

### Step 2 — Select Your Scope
Cost Management works at different scopes. For Region Stockholm:
- **Billing account** — total spend across all subscriptions
- **Management group** — spend across a group of subscriptions
- **Subscription** — spend for one subscription
- **Resource group** — spend for resources in one group

> **Tip:** Start at the **management group root** to see total spend.

---

## 2.2 Cost Analysis — Reading the Numbers

### Step-by-Step: View Cost by Subscription
1. In Cost Management, click **Cost analysis** in the left menu
2. At the top, set the **Scope** to your root management group
3. Set the time range to **Last 3 months**
4. In the **Group by** dropdown, select **Subscription**
5. Observe which subscriptions are spending the most

### Step-by-Step: View Cost by Service
1. Keep the same scope
2. Change **Group by** to **Service name**
3. Identify the top cost-generating services (e.g., Virtual Machines, Storage, Networking)

### Step-by-Step: View Cost by Resource Group
1. Change **Group by** to **Resource group**
2. This shows you which workloads or teams are spending the most

### Step-by-Step: Filter by Tag (After Tags Are Applied)
1. Click **Add filter**
2. Select **Tag**
3. Choose a tag key (e.g., `department`) and a value
4. The chart now shows only costs for that department

> **Note for Region Stockholm:** Tags are not yet applied. This is why filtering by department is not yet possible. See Module 1 for how to add tags.

---

## 2.3 Actual vs. Amortized Cost

| View | What it shows |
|---|---|
| **Actual cost** | What you were charged this month, including one-time reservation purchases |
| **Amortized cost** | Reservation costs spread evenly across the reservation period — better for trend analysis |

### Step-by-Step: Switch Between Views
1. In Cost Analysis, click the **Metric** dropdown (top right area)
2. Switch between **Actual cost** and **Amortized cost**
3. Compare the charts — amortized is smoother and better for forecasting

---

## 2.4 Budgets & Alerts

Budgets let you set a spending limit and receive email alerts before you overspend.

### Step-by-Step: Create a Budget
1. In Cost Management, click **Budgets** in the left menu
2. Click **+ Add**
3. Fill in:
   - **Name:** `monthly-budget-applz5`
   - **Scope:** Select the `applz-5` subscription
   - **Reset period:** Monthly
   - **Amount:** Enter a realistic monthly budget in SEK or your currency
4. Click **Next**
5. Set alert conditions:
   - **80%** of budget — send email to finance team
   - **100%** of budget — send email to IT manager
6. Enter email addresses
7. Click **Create**

> **Result:** You will receive an email when spending approaches the limit. No action is taken automatically — it is informational only.

---

## 2.5 Forecasting

### Step-by-Step: View the Cost Forecast
1. In Cost Analysis, set the time range to **Custom**
2. Set start = first day of current month, end = last day of **next** month
3. The chart shows actual costs (solid line) and forecasted costs (dotted line)
4. This helps predict end-of-month spend

---

## 2.6 Exporting Cost Data

### Option A — Export to Excel (Ad-hoc)
1. In Cost Analysis, configure your desired view
2. Click **Download** (top right)
3. Select **Excel (.xlsx)**
4. Open the file — it contains the same data you see on screen

### Option B — Scheduled Export to Storage Account
1. In Cost Management, click **Exports** in the left menu
2. Click **+ Add**
3. Fill in:
   - **Name:** `monthly-cost-export`
   - **Export type:** Monthly cost for billing month
   - **Storage account:** Select an existing storage account (e.g., in the `management` subscription)
   - **Container:** `cost-exports`
   - **Directory:** `region-stockholm`
4. Click **Create**
5. Azure will automatically drop a CSV file each month into the storage account
6. Power BI or Excel can connect directly to this storage account

---

## 2.7 Power BI Integration

### Step-by-Step: Connect Power BI to Azure Cost Management
1. Open **Power BI Desktop** (download from [https://powerbi.microsoft.com](https://powerbi.microsoft.com) if not installed)
2. Click **Get Data**
3. Search for **Azure Cost Management**
4. Select **Azure Cost Management connector**
5. Choose scope: **Management Group** → enter your management group ID
6. Set date range
7. Click **Connect** and sign in
8. Load the data — you now have a live cost dataset in Power BI
9. Build charts: bar chart by subscription, pie chart by service, trend line over time

---

## 2.8 Key Takeaways

- Cost Management is available at multiple scopes — start at the management group for a full picture
- Use **Group by** to slice costs by subscription, service, or resource group
- Tags enable cost allocation by department/project — prioritize tagging
- Budgets send alerts — they do NOT stop spending
- Export data for custom reporting in Excel or Power BI

---

**Next:** [Module 3 — Resource Inventory & Visibility](../03-resource-inventory/README.md)
