## Cloud Asset Inventory query that will return GKE Deployment resources

```
asset_type = "container.googleapis.com/Deployment"
```

#### The query will return a list of GKE Deployments in your project. For each Deployment, you'll see information such as:
- Name
- Namespace
- Status (e.g., Running, Pending)
- Creation time
- Labels and annotations
- Resource references (e.g., pods, services)
