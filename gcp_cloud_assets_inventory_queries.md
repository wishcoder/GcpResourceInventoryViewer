# Use Cloud Asset Inventory for asset management and compliance
- Cloud Asset Inventory is **valuable for asset management and compliance**, but not designed for real-time pod status monitoring


### 1. Cloud Asset Inventory to find all RUNNING resources in GKE, along with key considerations and insights:

```
(asset_type="container.googleapis.com/Deployment" OR
 asset_type="container.googleapis.com/ReplicaSet" OR
 asset_type="container.googleapis.com/StatefulSet" OR
 asset_type="container.googleapis.com/DaemonSet")
AND resource.data.status.conditions.state = "RUNNING"
```

##### Key Considerations:
- Inventory Delay: Cloud Asset Inventory might not reflect real-time status. Consider potential delays.
- Pod Status: For individual pod status, access the Kubernetes API directly or use tools like kubectl.

 
### 2. Cloud Asset Inventory query that will return GKE Deployment resources

```
asset_type = "container.googleapis.com/Deployment"
```

##### The query will return a list of GKE Deployments in your project. For each Deployment, you'll see information such as:
- Name
- Namespace
- Status (e.g., Running, Pending)
- Creation time
- Labels and annotations
- Resource references (e.g., pods, services)

### 3. Retrieving Pod-Related Information from Cloud Asset Inventory

```
asset_type="container.googleapis.com/Pod"
```

##### The query will return a list metadata such as:
- name
- namespace
- creation time-
- labels


