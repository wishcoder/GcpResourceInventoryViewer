# Kubernetes API functions (REST) to retrieve workload information about a pod:

## 1. GET /api/v1/namespaces/{namespace}/pods/{name}:

### Purpose: Retrieves detailed information about a specific pod, including:
- Name
- Namespace
- Status (Running, Pending, Succeeded, Failed, Unknown)
- Containers (including images, resources, and status)
- IP addresses
- Node assignment
- Labels and annotations
  
### Usage:
    Replace {namespace} with the pod's namespace.
    Replace {name} with the pod's name.

## 2. GET /api/v1/pods:

### Purpose: Lists all pods in the current namespace, providing basic information like:
- names
- statuses
- creation times

### Usable for:
- Filtering and sorting results based on various criteria.

## Additional Functions:

- GET /api/v1/namespaces/{namespace}/pods/{name}/log: Retrieves the logs for a specific pod.
- GET /api/v1/namespaces/{namespace}/pods/{name}/exec: Executes a command in a container within a pod.
- PATCH /api/v1/namespaces/{namespace}/pods/{name}: Updates a pod's configuration (e.g., labels, annotations).

# Kubernetes API functions (API) to retrieve workload information about a pod:

## 1. Create a Container API client:
```
Container container = new Container.Builder(
    GoogleNetHttpTransport.newTrustedTransport(),
    JacksonFactory.getDefaultInstance(),
    credential)
    .setApplicationName("your-application-name")
    .build();
```

## 2. Retrieve a specific pod:
- String projectId = "your-project-id";
- String zone = "your-cluster-zone";
- String clusterName = "your-cluster-name";
- String namespace = "your-pod-namespace";
- String podName = "your-pod-name";

```
PodList podList = container.projects().zones().clusters().pods().list(projectId, zone, clusterName).execute();
```

## 3. Documentation:
- Refer to the official documentation for detailed usage instructions and examples: https://cloud.google.com/kubernetes-engine/docs/reference/libraries


# Retrieve GKE Nodes in a given GCP region:

## 1. Create a Compute Engine API client:

```
Compute compute = new Compute.Builder(
    GoogleNetHttpTransport.newTrustedTransport(),
    JacksonFactory.getDefaultInstance(),
    credential)
    .setApplicationName("your-application-name")
    .build();
```

## 2. Node Information Retrieval:

```
String projectId = "your-project-id";
String region = "your-region";

InstanceList instances = compute.instances().list(projectId, region).execute();

// Iterate through the instances and filter for GKE nodes
for (Instance instance : instances.getItems()) {
    String description = instance.getDescription();
    if (description != null && description.startsWith("GKE Node")) {
        // Process the node information
        System.out.println("Node name: " + instance.getName());
        System.out.println("Machine type: " + instance.getMachineType());
        System.out.println("Zone: " + instance.getZone());
        // ... access other node properties as needed
    }
}
```

## 3. Key points:

- **Filtering for GKE Nodes:**
  - The Compute Engine API lists all instances, so filter for those with descriptions starting with "GKE Node."
- **Node Information:**
  - Access various properties like name, machine type, zone, status, and more.



# "GKE Node" in the description of virtual machines (VMs) that are part of a Google Kubernetes Engine (GKE) cluster

Compute Engine typically prepends "GKE Node" to the description of virtual machines (VMs) that are part of a Google Kubernetes Engine (GKE) cluster. This helps differentiate GKE-managed nodes from other Compute Engine instances you might have in your project.

## Here's how you can observe this behavior:

### Google Cloud Console:
- Navigate to Compute Engine > VM instances.
- Examine the Description column for VMs within a GKE cluster. You'll notice "GKE Node" at the beginning of the description.

### Google Cloud CLI:
- Use the gcloud compute instances list command to list instances.
- The output includes a description field, where you'll find "GKE Node" for GKE nodes.

### Compute Engine API:
- When listing instances through the Compute Engine API, the description field will also display "GKE Node" for GKE nodes.

## Purpose:
- **Identification:** This convention aids in easily identifying VMs that are part of GKE clusters within your project.
- **Management:** It's crucial to avoid directly modifying GKE nodes through the Compute Engine API or console, as GKE manages them. Direct modifications could disrupt cluster operations.
- **Visibility:** The description provides visibility into the purpose of these VMs and their association with GKE.

## Additional Considerations:
-- **Custom Descriptions:** While "GKE Node" is the standard prefix, you might encounter custom descriptions in specific cases, such as when nodes are created with unique labels or annotations.

-- **Filtering:** You can leverage this pattern to filter and manage GKE nodes using tools or scripts that interact with the Compute Engine API.
    



