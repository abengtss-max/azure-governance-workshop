# Module 4: Governance & Compliance Reporting

**Time:** 14:00 – 14:45  
**Goal:** Understand what policies are in place, view compliance state, and check who has access to what.

---

## 4.1 Azure Policy — Rules That Govern Your Environment

Azure Policy enforces rules across your resources automatically. Compliance reports show whether resources follow those rules.

### Step-by-Step: View Policy Compliance
1. Go to [https://portal.azure.com](https://portal.azure.com)
2. In the search bar, type **Policy** and press Enter
3. Click **Compliance** in the left menu
4. At the top, set the **Scope** to your root management group
5. You will see:
   - **Overall compliance percentage** (e.g., 74% compliant)
   - A list of all policy initiatives and individual policies
   - Red rows = non-compliant policies requiring attention

### Step-by-Step: Drill Into a Non-Compliant Policy
1. Click on any non-compliant policy in the list
2. Click **View resource compliance**
3. You see the exact resources that are failing the policy
4. Each row shows the resource name, subscription, and why it is non-compliant

### Step-by-Step: View an Initiative (Policy Set)
An initiative is a group of related policies. For example, the **Azure Security Benchmark** initiative contains 200+ policies.
1. In Policy, click **Definitions** in the left menu
2. Click **Initiative** in the Definition Type filter
3. Find **Azure Security Benchmark**
4. Click it and explore the policies it contains

### Understanding Compliance Scores
| Score | Meaning |
|---|---|
| 100% | All resources comply with this policy |
| 0–49% | Significant gap — action required |
| 50–79% | Partial compliance — review non-compliant resources |
| 80–100% | Good posture — maintain |

---

## 4.2 Microsoft Defender for Cloud — Security Posture

Defender for Cloud gives a **Secure Score** that measures your security posture as a percentage.

### Step-by-Step: View Secure Score
1. In the search bar, type **Defender for Cloud** and press Enter
2. The **Overview** page shows:
   - **Secure score** (e.g., 65%) — higher is better
   - Active recommendations grouped by severity
   - Coverage across subscriptions
3. Click **Secure score** in the left menu for a detailed breakdown
4. Each **security control** is listed with its score impact

### Step-by-Step: View Recommendations
1. Click **Recommendations** in the left menu
2. Filter by **Severity: High**
3. Each recommendation shows:
   - What the issue is
   - Which resources are affected
   - What to do to fix it
   - How many score points fixing it would add

> **Key point for management:** You do not need to understand the technical details. Focus on the **score trend** (is it going up?) and the **high severity count** (is it decreasing?).

### Step-by-Step: View Coverage by Subscription
1. In Defender for Cloud, click **Environment settings** in the left menu
2. Expand your tenant root
3. You see which Defender plans are enabled per subscription
4. Green checkmark = plan enabled and monitoring
5. Grey = not enabled = no coverage

---

## 4.3 RBAC — Who Has Access to What

Role-Based Access Control (RBAC) controls who can do what in Azure.

### Step-by-Step: View Access Assignments for a Subscription
1. Navigate to a subscription (e.g., `applz-5`)
2. Click **Access control (IAM)** in the left menu
3. Click the **Role assignments** tab
4. You see a list of every user, group, or service principal with access
5. Columns: **Name**, **Type** (User/Group/Service Principal), **Role**, **Scope**

### Common Roles to Know
| Role | What They Can Do |
|---|---|
| **Owner** | Full control including access management |
| **Contributor** | Create and manage resources, cannot manage access |
| **Reader** | View everything, change nothing |
| **Billing Reader** | View cost and billing data only |
| **Cost Management Reader** | View costs and budgets only |

### Step-by-Step: Check Who Has Owner Access
1. In Access control (IAM) → Role assignments
2. In the **Role** filter, type `Owner`
3. Review the list — Owner access should be limited to a small number of people

### Step-by-Step: Download Access Report
1. In Access control (IAM), click **Download role assignments**
2. Select scope: **This subscription and its children**
3. Download the CSV file
4. This is your access inventory report

---

## 4.4 Key Takeaways

- Azure Policy compliance shows which rules are followed and which are not — no technical knowledge needed to read it
- Defender for Cloud Secure Score is the single number to track security health over time
- RBAC access reports show who has access — export regularly for audit purposes
- Review Owner and Contributor assignments — these should be tightly controlled

---

**Next:** [Module 5 — Dashboards & Reporting](../05-dashboards-reporting/README.md)
