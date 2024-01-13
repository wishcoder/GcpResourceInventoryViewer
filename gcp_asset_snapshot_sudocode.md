## Here's a step-by-step guide to generating a comprehensive snapshot of active and running GCP resources using the google-cloud-asset Java client:

### Prerequisites:
  - A Google Cloud project with billing enabled.
  - Java development environment set up.
  - Google Cloud SDK installed and authenticated.

### Steps:
**1. Enable Cloud Asset Inventory API:**
- Navigate to the Google Cloud Console.
- Go to "APIs & Services" > "Library".
- Search for "Cloud Asset Inventory API".
- Click "Enable".

**2. Assign Required Roles:**
- Go to "IAM & Admin" > "Roles".
- Search for "roles/resourcemanager.viewer" and "roles/cloudasset.viewer".
- Add these roles to the appropriate users or service accounts that will be accessing the inventory data.

**3. Set up Java Project:**
Create a new Java project and add the following dependency to your pom.xml file:

```
<dependency>
  <groupId>com.google.cloud</groupId>
  <artifactId>google-cloud-asset</artifactId>
  <version>4.2.4</version>
</dependency>
```
    
**4. Authenticate:**
- Set up authentication using Application Default Credentials (ADC) or a service account key. Follow Google's documentation for details.
```
GoogleCredential credential = GoogleCredential.getApplicationDefault()
    .createScoped(Lists.newArrayList(
        CloudAssetScopes.CLOUD_ASSET_READONLY,
        "https://www.googleapis.com/auth/compute.readonly",
        "https://www.googleapis.com/auth/container.readonly",
        "https://www.googleapis.com/auth/cloud-platform"));
```
  

**5. Write Java Code:** 

```
import com.google.cloud.asset.v1.AssetServiceClient;
import com.google.cloud.asset.v1.Resource;
import com.google.cloud.asset.v1.SearchAllResourcesRequest;
import com.google.cloud.asset.v1.SearchAllResourcesResponse;
import com.google.api.client.googleapis.auth.oauth2.GoogleCredential;
import com.google.api.client.googleapis.javanet.GoogleNetHttpTransport;
import com.google.api.client.http.HttpRequestInitializer;
import com.google.api.client.json.JsonFactory;
import com.google.api.client.json.jackson2.JacksonFactory;
import com.google.api.services.cloudasset.v1.CloudAsset;
import com.google.api.services.cloudasset.v1.CloudAssetScopes;
import com.google.api.services.cloudasset.v1.model.Resource;
import com.google.api.services.cloudasset.v1.model.SearchAllResourcesRequest;
import com.google.api.services.cloudasset.v1.model.SearchAllResourcesResponse;
import com.google.api.services.compute.Compute;
import com.google.api.services.compute.model.Instance;
import com.google.api.services.container.Container;
import com.google.api.services.container.model.Cluster;
import com.google.api.services.cloudresourcemanager.CloudResourceManager;
import com.google.api.services.cloudresourcemanager.model.Project;

import java.io.IOException;
import java.security.GeneralSecurityException;
import java.util.ArrayList;
import java.util.List;

// Optional API clients
CloudAsset assetServiceClient = new CloudAsset.Builder(
        GoogleNetHttpTransport.newTrustedTransport(),
        JacksonFactory.getDefaultInstance(),
        requestInitializer
).build();
Compute computeServiceClient = new Compute.Builder(
        GoogleNetHttpTransport.newTrustedTransport(),
        JacksonFactory.getDefaultInstance(),
        requestInitializer
).build();
Container containerServiceClient = new Container.Builder(
        GoogleNetHttpTransport.newTrustedTransport(),
        JacksonFactory.getDefaultInstance(),
        requestInitializer
).build();
CloudResourceManager resourceManagerServiceClient = new CloudResourceManager.Builder(
        GoogleNetHttpTransport.newTrustedTransport(),
        JacksonFactory.getDefaultInstance(),
        requestInitializer
).build();

// Create a client
try (AssetServiceClient client = AssetServiceClient.create()) {
    SearchAllResourcesRequest request = SearchAllResourcesRequest.newBuilder()
        .setScope("organizations/YOUR_ORG_ID") // Replace with your organization ID
        .setAssetTypes(
            "compute.googleapis.com/Instance", // Add more asset types as needed
            "container.googleapis.com/Cluster",
            // ...
        )
        .build();

    SearchAllResourcesResponse response = client.searchAllResources(request);

    // Process and filter active/running resources
    for (Resource resource : response.getResultsList()) {
        // Check resource state and extract relevant information

            String assetType = asset.getAssetType();

            if (assetType.equals("compute.googleapis.com/Instance")) {
                String instanceName = asset.getName();
                Instance instance = computeServiceClient.instances().get(ORGANIZATION_ID, instanceName).execute();
                // Process instance details
            } else if (assetType.equals("container.googleapis.com/Cluster")) {
              // Do someting
              // String clusterName = asset.getName();
              // Cluster cluster = containerServiceClient.projects().locations().clusters().get(...)
            }

        // ...
    }
} catch (Exception e) {
    // Handle exceptions
}
```
**7. Supported asset types:**
[https://cloud.google.com/asset-inventory/docs/supported-asset-types](https://cloud.google.com/asset-inventory/docs/supported-asset-types)

**8. Filter Active/Running Resources:**
- Iterate through the **response.getResultsList()** and check the resource.getState() property to filter for active or running resources based on your criteria.
- Extract relevant information from each resource as needed.

**9. Store or Export Data:**
- Choose a suitable format (e.g., CSV, JSON, database) to store or export the list of active/running resources for further analysis or reporting.

