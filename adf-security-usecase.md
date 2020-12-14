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
    * [Use Case: Unsafe Azure Data Factory Signins](ADF%20Use%20Cases/adf_signins.yaml)
    * Real-time: Yes
* [ ] Ensure that only Data Factory Managed Identity (MI) is used to authenticate to other Azure services and data sources. 
* [ ] Ensure that network communication to Data Factory Command Channel does not go over public internet. 
* [ ] Ensure that network communication to Data Factory Data Channel does not go over public internet. e.g. ExpressRoute private peering
* [ ] Ensure that ADF Activity Log is monitored. 
Operation Names:
    * [ ] Create or Update any Data Factory
    * [ ] Create or Update any Linked Service
    * [ ] Create or Update any Integration Runtime
    * [ ] Delete Integration Runtime
    * [ ] Get GitHub access token
    * [ ] List Integration Runtime Authentication Keys
    * [ ] Create role assignment
    * [ ] Get DataPlane access
    
## 2. Self-Hosted Integration Runtime (SHIR)
* [ ] Ensure that default port 8060 used by SHIR for secure communication is changed.
* [ ] Ensure that data store credentials are not stored locally in SHIR.
* [ ] Ensure that SHIR hosting VM Network Security Groups (NSG)s are monitored.
* [ ] Ensure that default-allow-RDP Port 3389 is removed from SHIR VM NSG rules.
* [ ] Ensure that NSG Flow logs v2 are enabled for SHIR VM.
* [ ] Ensure that Traffic Analytics are enabled and sent to Log Analytics Workspace (LAW) for Sentinel.

## 3. Linked Services
## 4. Data Access
