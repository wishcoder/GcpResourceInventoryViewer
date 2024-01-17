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




