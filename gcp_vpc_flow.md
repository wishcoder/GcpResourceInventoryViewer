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
