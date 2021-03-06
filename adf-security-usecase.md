# Azure Data Factory Attack Surface

* ADF instance
* ADF Portal
* ADF GitHub repo
* Integration Runtimes
    * Azure IR
    * Self-Hosted IR
    * Azure SSIS-IR
    * IR VMs
    * IR VNETs
        * NSGs
    * IR Auth Keys
* Linked Services
* Data Sources
    * Azure SQL DB
    * Azure Data Lake
    * Azure Storage
    * ...
* Key Management
    * Azure Key Vault

# ADF Use Case Summary Table
Following table summarizes ADF security use cases by ADF components.
| [Data Factory](adf-security-usecase.md#1-data-factory-instance) | [Integration Runtime](adf-security-usecase.md#2-self-hosted-integration-runtime-shir) | [Linked Service](adf-security-usecase.md#3-linked-services) | [Pipeline](adf-security-usecase.md#4-pipelines) |
| --- | --- | --- | --- |
| [Rare ADF Operations](ADF%20Use%20Cases/adf_rare_operations.yaml) | [IR Operations](ADF%20Use%20Cases/adf_ir_operations.yaml) | [Linked Service Operations](ADF%20Use%20Cases/adf_linkedservice_operations.yaml) | [Pipeline Operations](ADF%20Use%20Cases/adf_pipeline_operations.yaml) |
| [Unauthorized ADF Signins](ADF%20Use%20Cases/adf_signins.yaml) | [Too many IR operations](ADF%20Use%20Cases/adf_ir_operations_toomany.yaml) | [Too many Linked Service operations](ADF%20Use%20Cases/adf_linkedservice_toomany.yaml) | - |
| [Failed ADF signins](ADF%20Use%20Cases/adf_signins_failed.yaml) | [IR Auth Keys regenerated](ADF%20Use%20Cases/adf_ir_authkeys_regenerate.yaml) | - | - |
| [ADF Role Assignments](ADF%20Use%20Cases/adf_role_assignments.yaml) | - | - | - |
| [Too many role assignments](ADF%20Use%20Cases/adf_role_assignments_toomany.yaml) | - | - | - |
| [ADF Diagnostic Settings](ADF%20Use%20Cases/adf_diagnostics.yaml) | - | - | - |
| [Anomalous ADF Signins](ADF%20Use%20Cases/adf_signins_anomalous.yaml) | - | - | - |


# Azure Data Factory Use Cases
## 1. Data Factory Instance
* [ ] Ensure that access to Data Factory management plane is monitored. [[3.1](adf-security-baseline.md#31-maintain-an-inventory-of-administrative-accounts)] \
    Operation Name(s):
    * [ ] Create role assignment (RBAC: Data Factory Contributor role) \
    `Microsoft.Authorization/roleAssignments/write`
    * [ ] Delete role assignment (RBAC: Data Factory Contributor role) \
    `Microsoft.Authorization/roleAssignments/delete`
    * [Use Case: ADF Role Assignments](ADF%20Use%20Cases/adf_role_assignments.yaml)
    * [Use Case: Unauthorized ADF Signins](ADF%20Use%20Cases/adf_signins.yaml)
        * Requires a watchlist
* [ ] Ensure that Azure Data Factory Activity Log is monitored. [[2.2](adf-security-baseline.md#22-configure-central-security-log-management)] [[3.7](adf-security-baseline.md#37-log-and-alert-on-suspicious-activities-from-administrative-accounts)] \
    Operation Name(s):
    * [ ] Create or Update any Data Factory. \
    `Microsoft.DataFactory/factories/write`
    * [ ] Delete Data Factory. \
    `Microsoft.DataFactory/factories/delete`
    * [ ] Get DataPlane access \
    `Microsoft.DataFactory/factories/getDataPlaneAccess/action`
    * [ ] Get GitHub access token \
    `Microsoft.DataFactory/factories/getGitHubAccessToken`
    * [Use Case: Rare ADF Operations](ADF%20Use%20Cases/adf_rare_operations.yaml)
* [ ] Ensure that failed Data Factory signin attempts are monitored. [[3.7](adf-security-baseline.md#37-log-and-alert-on-suspicious-activities-from-administrative-accounts)]
    * [Use Case: Failed ADF signins](ADF%20Use%20Cases/adf_signins_failed.yaml)
* [ ] Ensure that Data Factory diagnostic settings are enabled and logs are sent to a Log Analytics Workspace which is connected to Azure Sentinel. [[2.3](adf-security-baseline.md#23-enable-audit-logging-for-azure-resources)]
    * Log categories: ActivityRuns, PiplelineRuns, TriggerRuns
    * Destination table: Resource specific
    * Operation Name: Create or update resource diagnostic setting \
    `microsoft.insights/diagnosticSettings/write`
    * [Use Case: ADF Diagnostic Settings](ADF%20Use%20Cases/adf_diagnostics.yaml)
* [ ] Ensure that Data Factory log retention period is aligned with organization's compliance regulations. [[2.5](adf-security-baseline.md#25-configure-security-log-storage-retention)]  
* [ ] Ensure that network communication to Data Factory Command Channel does not go over public internet. 
* [ ] Ensure that network communication to Data Factory Data Channel does not go over public internet. e.g. ExpressRoute private peering
* [ ] Ensure that network resources related to Data Factory instances are tagged.  [[1.10](adf-security-baseline.md#110-document-traffic-configuration-rules)]
    
## 2. Self-Hosted Integration Runtime (SHIR)

* [ ] Ensure that Integration Runtime operations are monitored. [[2.2](adf-security-baseline.md#22-configure-central-security-log-management)] [[3.7](adf-security-baseline.md#37-log-and-alert-on-suspicious-activities-from-administrative-accounts)] \
Operation Names:
    * [ ] Create or Update any Integration Runtime \
    `Microsoft.DataFactory/factories/integrationruntimes/write`
    * [ ] Delete Integration Runtime \
    `Microsoft.DataFactory/factories/integrationruntimes/delete`
    * [ ] List Integration Runtime Authentication Keys \
    `Microsoft.DataFactory/factories/integrationruntimes/listAuthKeys/action`
    * [ ] Regenerate Integration Runtime Authentication Keys \
    `Microsoft.DataFactory/factories/integrationruntimes/regenerateAuthKey/action`
    * [ ] Create Self hosted Integration Runtime express install link \
    `Microsoft.DataFactory/factories/integrationruntimes/createExpressSHIRInstallLink/action`
    * [Use Case: ADF Integration Runtime Operations](ADF%20Use%20Cases/adf_ir_operations.yaml)
    * [Use Case: Too many Integration Runtime operations per Data Factory](ADF%20Use%20Cases/adf_ir_operations_toomany.yaml)
    * [Use Case: Integration Runtime Authentication Keys regenerated](ADF%20Use%20Cases/adf_ir_authkeys_regenerate.yaml)
* [ ] Ensure that default-allow-RDP Port 3389 is removed from SHIR VM NSG rules. [[1.1](adf-security-baseline.md#11-protect-azure-resources-within-virtual-networks)]
* [ ] Ensure that SHIR hosting VM Network Security Groups (NSG)s are monitored. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that NSG Flow logs v2 are enabled for SHIR VM. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that Traffic Analytics are enabled and sent to Log Analytics Workspace (LAW) for Sentinel. [[1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)]
* [ ] Ensure that SHIR hosting VNET is protected by DDoS Standard. [[1.4](adf-security-baseline.md#14-deny-communications-with-known-malicious-ip-addresses)]
* [ ] Ensure that SHIR hosting VNET's NSG Flow logs are sent to Azure Storage Account for traffic auditing. [[1.5](adf-security-baseline.md#15-record-network-packets)]
* [ ] Ensure that outbound traffic from SHIR is monitored by IDS/IPS. [[1.6](adf-security-baseline.md#16-deploy-network-based-intrusion-detectionintrusion-prevention-systems-idsips)]
* [ ] Ensure that SHIR hosting VNET is utilizing NSG Service Tag `DataFactoryManagement` in NSG rules. [[1.8](adf-security-baseline.md#18-minimize-complexity-and-administrative-overhead-of-network-security-rules)]
* [ ] Ensure that SHIR hosting VNET NSG rule changes are monitored. [[1.11](adf-security-baseline.md#111-use-automated-tools-to-monitor-network-resource-configurations-and-detect-changes)]
* [ ] Ensure that SHIR VMs are accessed through PAWs or Jumpbox VMs, not directly. [[3.6](adf-security-baseline.md#36-use-dedicated-machines-privileged-access-workstations-for-all-administrative-tasks)]
* [ ] Ensure that access to SHIR VMs is only allowed from IPs and countries specified in Conditional Access Named locations. [[3.8](adf-security-baseline.md#38-manage-azure-resources-from-only-approved-locations)]
* [ ] Ensure that SHIR VMs are onboarded to Azure Sentinel. [[2.4](adf-security-baseline.md#24-collect-security-logs-from-operating-systems)] [[3.9](adf-security-baseline.md#39-use-azure-active-directory)]
* [ ] Ensure that default port 8060 used by SHIR for secure communication is changed.
* [ ] Ensure that data store credentials are not stored locally in SHIR.
    
## 3. Linked Services

* [ ] Ensure that Linked Service operations are monitored. [[2.2](adf-security-baseline.md#22-configure-central-security-log-management)] [[3.7](adf-security-baseline.md#37-log-and-alert-on-suspicious-activities-from-administrative-accounts)] \
    Operation Names:
    * [ ] Create or Update any Linked Service. \
    `Microsoft.DataFactory/factories/linkedServices/write`
    * [ ] Delete Linked Service. \
    `Microsoft.DataFactory/factories/linkedServices/delete`
    * [Use Case: ADF Linked Service Operations](ADF%20Use%20Cases/adf_linkedservice_operations.yaml)
    * [Use Case: Too many Linked Service operations](ADF%20Use%20Cases/adf_linkedservice_toomany.yaml)

* [ ] Ensure that Linked Services are using `Managed Identity` as Authentication Method when connecting to other Azure services. [[3.9](adf-security-baseline.md#39-use-azure-active-directory)]

## 4. Pipelines
* [ ] Ensure that Pipeline operations are monitored. [[2.2](adf-security-baseline.md#22-configure-central-security-log-management)] \
Operation Names:
    * [ ] Create or Update any Pipeline. \
    `Microsoft.DataFactory/factories/pipelines/write`
    * [ ] Delete Pipeline \
    `Microsoft.DataFactory/factories/pipelines/delete`
    * [ ] Create or Update Dataset \
    `Microsoft.DataFactory/factories/datasets/write`
    * [Use Case: ADF Pipeline Operations](ADF%20Use%20Cases/adf_pipeline_operations.yaml)

## 5. Identity & Access
* [ ] Ensure that only Data Factory Managed Identity (MI) is used to authenticate to other Azure services and data sources. [[3.9](adf-security-baseline.md#39-use-azure-active-directory)]
    * AADManagedIdentitySignInLogs
* [ ] Ensure that only dedicated administrative accounts can access Data Factory console. [[3.3](adf-security-baseline.md#33-use-dedicated-administrative-accounts)]
    * Requires a watchlist
* [ ] Ensure that  dedicated administrative accounts accessing Data Factory has MFA enabled. [[3.5](adf-security-baseline.md#35-use-multi-factor-authentication-for-all-azure-active-directory-based-access)]
* [ ] Ensure that excessive role assignmets per Data Factory are monitored.
    * [Use Case: Too many role assignments per Data Factory](ADF%20Use%20Cases/adf_role_assignments_toomany.yaml)


# Terminology
The terms "**control**", "**benchmark**", and "**baseline**" are used often in the Azure Security Benchmark documentation and it's important to understand how Azure uses those terms.

* A **control** is a high-level description of a feature or activity that needs to be addressed and is not specific to a technology or implementation.
* A **benchmark** contains security recommendations for a specific technology, such as Azure. The recommendations are categorized by the control to which they belong.
* A **baseline** is the implementation of the benchmark on the individual Azure service. Each organization decides benchmark recommendation and corresponding configurations are needed in the Azure implementation scope.

# References
* [Azure Security Benchmark](https://docs.microsoft.com/en-us/azure/security/benchmarks/)
* [Azure Data Factory Security Baseline](https://docs.microsoft.com/en-us/azure/data-factory/security-baseline)
* [Azure Data Factory Operation Groups](https://docs.microsoft.com/en-us/rest/api/datafactory/v2#rest-operation-groups)
* [Azure Data Factory Operations List](https://docs.microsoft.com/en-us/rest/api/datafactory/operations/list#operations_list) 
