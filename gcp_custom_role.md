## Role Name: Resource Inventory Viewer

### Permissions:
- **Kubernetes Engine API:** 
  - container.clusters.list 
  - container.clusters.get
  - container.deployments.list
  - container.nodes.list
  - container.nodes.get
  - container.pods.list
  - container.pods.get
    
- **Resource Manager API:** 
  - resourcemanager.folders.get
  - resourcemanager.folders.list
  - resourcemanager.projects.get
  - resourcemanager.projects.list

- **Cloud Asset Inventory API:** 
  - cloudasset.assets.searchAllResources
  - cloudasset.assets.listResource
  - cloudasset.assets.listOSInventories

- **Compute Engine API:** 
  - compute.instances.list 
  - compute.instances.get
