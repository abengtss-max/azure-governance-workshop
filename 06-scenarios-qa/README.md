# Module 6: Practical Scenarios & Q&A

**Time:** 15:45 – 16:15  
**Goal:** Walk through real-world questions that management typically asks and show exactly how to answer them in Azure.

---

## Scenario 1: "How much did we spend last month per department?"

**Current state:** Not yet possible without tags. Here is the workaround and the fix.

### Workaround (today — no tags)
1. Open **Cost Management** → **Cost Analysis**
2. Set scope to root management group
3. Set time to **Last month**
4. Group by **Subscription** — if each department owns a subscription, this approximates department spend
5. Export to Excel and add a manual "Department" column mapping subscriptions to departments

### Proper Solution (after tags are applied)
1. Ensure all resource groups have a `department` tag
2. Enable **tag inheritance** via Azure Policy (tags from resource group apply to child resources)
3. Open Cost Analysis → Group by **Tag: department**
4. Instant cost breakdown per department — no manual work

---

## Scenario 2: "What resources were created or deleted this week?"

1. Navigate to any subscription or the root management group
2. Click **Activity log** in the left menu
3. Set time range: **Last 7 days**
4. Add filter: **Status = Succeeded**
5. Add filter: **Operation = starts with 'Create'** (for new resources)
6. Or: **Operation = starts with 'Delete'** (for removed resources)
7. Export to CSV for a weekly audit report

**For cross-subscription view, use Resource Graph:**
```kql
resourcequeries
| where TimeGenerated > ago(7d)
| where OperationName startswith "Microsoft.Resources/deployments/write"
| project TimeGenerated, Caller, ResourceGroup, SubscriptionId
| order by TimeGenerated desc
```

---

## Scenario 3: "Are we compliant with our security policies?"

1. Open **Defender for Cloud** → **Secure score**
   - Current score tells you overall posture (aim for >70%)
2. Open **Policy** → **Compliance**
   - Filter by **Non-compliant** resources
   - Export the non-compliance report: click **Download report** at the top
3. Share the downloaded PDF/Excel with leadership or auditors

### Monthly Compliance Reporting Routine
1. First Monday of each month:
   - Download Policy compliance report
   - Screenshot Secure Score
   - Export Cost Analysis for previous month
   - Combine into a monthly governance report

---

## Scenario 4: "Someone deleted a resource — who did it?"

1. Go to the subscription where the resource was
2. Click **Activity log**
3. Filter: **Operation = Delete**, **Status = Succeeded**
4. Set time range to when the deletion occurred
5. Click the event row
6. Open the **JSON** tab — the `caller` field shows the exact user or service principal that performed the deletion

---

## Scenario 5: "We're approaching our budget limit — who is spending the most?"

1. You should already have a budget alert email (set up in Module 2)
2. Open **Cost Management** → **Cost Analysis**
3. Set scope to the subscription or management group hitting the limit
4. Group by **Resource** and sort by **Cost (descending)**
5. Identify the top 3–5 most expensive resources
6. For each resource, note the **Resource Group** and the **Owner** tag (if it exists)
7. Contact the resource owner and review whether the resource is still needed

---

## Scenario 6: "Can I see who has access to our production subscription?"

1. Navigate to the production subscription
2. Click **Access control (IAM)** → **Role assignments**
3. Filter by **Role = Owner** and **Role = Contributor**
4. Review the list — any unexpected users or service principals?
5. Click **Download role assignments** → CSV for your access audit documentation

---

## Open Q&A (15 minutes)

Common questions from previous workshops:

**Q: Can we set a hard spending limit so Azure stops provisioning when we hit the budget?**  
A: Budgets only send alerts — they do not stop spending. To enforce limits, you need Azure Policy to deny resource creation in certain subscriptions, which requires IT involvement.

**Q: How far back does cost history go?**  
A: Azure retains cost data for 13 months in Cost Management by default. For longer retention, use scheduled exports to a Storage Account.

**Q: Can we get cost reports by project instead of by subscription?**  
A: Yes — once resources are tagged with a `project` tag, Cost Management lets you group and filter by that tag.

**Q: Who should be responsible for maintaining tags?**  
A: Ideally the team deploying resources. Azure Policy can enforce that resources without required tags cannot be created.

---

**Workshop complete!** See the [cheatsheet](../cheatsheet.md) for a quick reference to take back with you.
