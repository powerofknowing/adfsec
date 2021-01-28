# Azure Data Factory Attack Surface

* ADF instance
* Integration Runtimes
    * Azure IR
    * Self-Hosted IR
    * Azure SSIS-IR
* ADF Portal
* ADF GitHub repo
* Linked Services
* Data Sources
    * Azure SQL DB
    * Azure Data Lake
    * Azure Storage
* Key Management
    * Azure Key Vault
* VNET isolation
    * NSGs

# Azure Data Factory Use Cases
## 1. Data Factory Instance
* [ ] Ensure that access to Data Factory management plane is monitored.  RBAC: Data Factory Contributor role [ASBv1 3.1]
    * [Use Case: Unsafe ADF Signins](ADF%20Use%20Cases/adf_signins.yaml)
* [ ] Ensure that ADF Activity Log is monitored.
    * [Use Case: Rare ADF Operations](ADF%20Use%20Cases/adf_rare_operations.yaml)  
Operation Names:
    * [ ] Create or Update any Data Factory
    * [ ] Create or Update any Linked Service
    * [ ] Create or Update any Integration Runtime
    * [ ] Delete Integration Runtime
    * [ ] Get GitHub access token
    * [ ] List Integration Runtime Authentication Keys
    * [ ] Create role assignment
    * [ ] Get DataPlane access
    
* [ ] Ensure that only Data Factory Managed Identity (MI) is used to authenticate to other Azure services and data sources. 
* [ ] Ensure that network communication to Data Factory Command Channel does not go over public internet. 
* [ ] Ensure that network communication to Data Factory Data Channel does not go over public internet. e.g. ExpressRoute private peering
    
## 2. Self-Hosted Integration Runtime (SHIR)

* [ ] Ensure that default-allow-RDP Port 3389 is removed from SHIR VM NSG rules. [[1.1](adf-security-baseline.md#11-protect-azure-resources-within-virtual-networks)]
* [ ] Ensure that SHIR hosting VM Network Security Groups (NSG)s are monitored. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that NSG Flow logs v2 are enabled for SHIR VM. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that Traffic Analytics are enabled and sent to Log Analytics Workspace (LAW) for Sentinel. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that SHIR hosting VNET is protected by DDoS Standard. [[1.4](adf-security-baseline.md#14-deny-communications-with-known-malicious-ip-addresses)]
* [ ] Ensure that SHIR hosting VNET's NSG Flow logs are sent to Azure Storage Account for traffic auditing. [[1.5](adf-security-baseline.md#15-record-network-packets)]
* [ ] Ensure that outbound traffic from SHIR is monitored by IDS/IPS. [[1.6](adf-security-baseline.md#16-deploy-network-based-intrusion-detectionintrusion-prevention-systems-idsips)]
* [ ] Ensure that SHIR hosting VNET is utilizing NSG Service Tag `DataFactoryManagement` in NSG rules. [[1.8](adf-security-baseline.md#18-minimize-complexity-and-administrative-overhead-of-network-security-rules)]
* [ ] Ensure that default port 8060 used by SHIR for secure communication is changed.
* [ ] Ensure that data store credentials are not stored locally in SHIR.

## 3. Linked Services
## 4. Data Access
