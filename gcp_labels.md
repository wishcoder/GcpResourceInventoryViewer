## 1. Container Labels:
- **Access through GKE API:** You can retrieve container labels using the GKE API, specifically endpoints like:
  - GET /projects/{projectId}/zones/{zone}/clusters/{clusterName}/nodePools/{nodePoolName}/nodes/{nodeName}
  - GET /projects/{projectId}/zones/{zone}/clusters/{clusterName}/pods/{podName}
- Response Structure: The API response includes a metadata field with a labels map containing key-value pairs of labels.

## 2. VM Labels (in GKE Nodes):
- **Access through Compute Engine API:** While GKE nodes are essentially VMs, their labels are managed through the Compute Engine API. Use endpoints like:
  - GET /projects/{project}/zones/{zone}/instances/{instanceName}
- Response Structure: The API response's metadata field includes labels with VM-specific labels.

## 3. Key Points:
- Distinct APIs: Use GKE API for container labels and Compute Engine API for VM labels.
- Response Structure: Labels are found in the metadata.labels field of API responses.
- Integration: Manage both container and VM labels programmatically using GKE and Compute Engine APIs.

## 4. Additional Considerations:
- Label Hierarchies: GKE has separate label systems for clusters, nodes, pods, and containers. Understand their relationships for effective management.
- Label Usage: Labels are crucial for organizing, filtering, and managing resources in GKE.
