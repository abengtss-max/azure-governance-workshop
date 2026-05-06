# Module 3: Resource Inventory and Visibility

Goal: Get a full resource inventory and track operational activity.

## Step-by-step: Resource Graph

1. Open Resource Graph Explorer.
2. Run query:

```kql
resources
| summarize count() by subscriptionId
```

3. Run query:

```kql
resources
| project name, type, resourceGroup, location, subscriptionId
| order by type asc
```

4. Run query:

```kql
resources
| where isnull(tags) or tags == "{}"
| project name, type, resourceGroup, subscriptionId
```

5. Export results to CSV.

## Step-by-step: Activity Log

1. Open a subscription.
2. Open Activity log.
3. Filter by operation (Create/Delete) and time range.
4. Export results for audit reporting.

## Step-by-step: Health

1. Open Service Health for platform incidents.
2. Open Resource health on critical resources.
