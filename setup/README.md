# Workshop Setup Guide

## Required attendee access

Assign at management group scope:

- Reader
- Cost Management Reader
- Security Reader
- Billing Reader

## Optional resource for richer reporting demos

Deploy one Log Analytics Workspace (small footprint) if you want workbook-based reporting examples with live log data.

### Azure CLI steps

```bash
az login
az account set --subscription "<management-subscription-id>"
az group create --name rg-monitoring-workshop --location swedencentral
az monitor log-analytics workspace create \
  --resource-group rg-monitoring-workshop \
  --workspace-name law-workshop \
  --location swedencentral \
  --sku PerGB2018 \
  --retention-time 30
```

## Cleanup

```bash
az group delete --name rg-monitoring-workshop --yes --no-wait
```
