# VPC Flow Logs:

## Purpose: Capture information about the traffic flowing through your Virtual Private Cloud (VPC) networks.

### Use Cases:
- Network monitoring and troubleshooting
- Security analysis and threat detection
- Resource optimization and cost management
- Compliance and auditing
- 

### Functionality: Logs details of accepted and rejected traffic, including:
- Source and destination IP addresses
- Protocols and ports
- Packet and byte counts
- Time stamps
- Traffic actions (accepted, rejected, dropped)

### Key Points:
- Activation: Enabled for specific subnetworks or entire VPCs.
- Destinations: Exported to Cloud Logging, Cloud Storage, BigQuery, or Pub/Sub for analysis and storage.
- Filtering and Sampling: Customize logs to capture specific traffic patterns and reduce log volume.

### Common Tasks:

#### Enabling Flow Logs:
- Using the Google Cloud Console
- Using the gcloud CLI
- Using the Compute Engine API
- 
#### Viewing Flow Logs:
- In Cloud Logging
- In Cloud Storage
- In BigQuery
- In Pub/Sub
  
#### Filtering and Analyzing Flow Logs:
- Using Cloud Logging filters and queries
- Using BigQuery for complex analysis
    
#### Managing Flow Logs:
- Adjusting settings
- Deleting logs


# Query for VPC Flow Logs to identify traffic from resources in 'us-central1' accessing resources in 'us-east1':

## In Cloud Logging:

```
resource.type="gce_subnetwork"
logName:"projects/YOUR_PROJECT_ID/logs/compute.googleapis.com%2Fvpc_flows"
protoPayload.vpcFlow.srcVpc="projects/YOUR_PROJECT_ID/global/networks/YOUR_VPC_NAME"
protoPayload.vpcFlow.srcRegion="us-central1"
protoPayload.vpcFlow.destVpc="projects/YOUR_PROJECT_ID/global/networks/YOUR_VPC_NAME"
protoPayload.vpcFlow.destRegion="us-east1"
```

## Breakdown:
- resource.type="gce_subnetwork": Focuses on logs from subnetworks.
- logName: Specifies the VPC Flow Logs log name.
- protoPayload.vpcFlow.srcVpc: Filters for traffic originating from a specific VPC.
- protoPayload.vpcFlow.srcRegion: Narrows down to traffic from the 'us-central1' region.
- protoPayload.vpcFlow.destVpc: Filters for traffic destined for a specific VPC.
- protoPayload.vpcFlow.destRegion: Restricts to traffic going to the 'us-east1' region.

## Key Points:
- **Replace placeholders:** Ensure you replace YOUR_PROJECT_ID and YOUR_VPC_NAME with the appropriate values.
- **Time range:** Adjust the time range in Cloud Logging to cover your desired analysis period.
- **Further filtering:** Add more filters as needed to refine results (e.g., specific IP addresses, protocols, ports).
- **BigQuery:** For complex analysis, export Flow Logs to BigQuery and use its SQL capabilities for advanced queries.
