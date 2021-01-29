# Azure Data Factory Security
## Baseline to Use Case mapping
| 1. Network Security | 2. Logging & Monitoring | 3. Identity & Access control | 4. Data Protection | 5. Vulnerability Mgmt | 6. Inventory & Asset Mgmt | 7. Secure config | 8. Malware Defense | 9. Data Recovery | 10. Incident Response |
| ------------------- | ------------------------- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- |
| [1.1](adf-security-baseline.md#11-protect-azure-resources-within-virtual-networks)  | N/A  | [3.1](adf-security-baseline.md#31-maintain-an-inventory-of-administrative-accounts)  | N/A | N/A | N/A  | 7.1  | 8.1 | N/A | N/A |
| [1.2](adf-security-baseline.md#12-monitor-and-log-the-configuration-and-traffic-of-virtual-networks-subnets-and-nics)  | [2.2](adf-security-baseline.md#22-configure-central-security-log-management)  | N/A  | 4.2 | 5.2 | N/A  | N/A  | N/A | N/A | N/A |
| N/A  | [2.3](adf-security-baseline.md#23-enable-audit-logging-for-azure-resources)  | [3.3](adf-security-baseline.md#33-use-dedicated-administrative-accounts)  | N/A | N/A | N/A  | N/A  | N/A | N/A | N/A |
| [1.4](adf-security-baseline.md#14-deny-communications-with-known-malicious-ip-addresses)  | [2.4](adf-security-baseline.md#24-collect-security-logs-from-operating-systems)  | 3.4  | N/A | N/A | N/A  | N/A  | -   | N/A | N/A |
| [1.5](adf-security-baseline.md#15-record-network-packets)  | [2.5](adf-security-baseline.md#25-configure-security-log-storage-retention)  | N/A  | N/A | N/A | N/A  | 7.5  | -   | -   | N/A |
| [1.6](adf-security-baseline.md#16-deploy-network-based-intrusion-detectionintrusion-prevention-systems-idsips)  | [2.6](adf-security-baseline.md#26-monitor-and-review-logs)  | 3.6  | 4.6 | -   | 6.6  | N/A  | -   | -   | N/A |
| N/A  | [2.7](adf-security-baseline.md#27-enable-alerts-for-anomalous-activities)  | 3.7  | N/A | -   | 6.7  | N/A  | -   | -   | -   |
| [1.8](adf-security-baseline.md#18-minimize-complexity-and-administrative-overhead-of-network-security-rules)  | [2.8](adf-security-baseline.md#28-centralize-anti-malware-logging)  | 3.8  | N/A | -   | 6.8  | N/A  | -   | -   | -   |
| N/A  | N/A  | 3.9  | 4.9 | -   | N/A  | 7.9  | -   | -   | -   |
| [1.10](adf-security-baseline.md#110-document-traffic-configuration-rules) | [2.10](adf-security-baseline.md#210-enable-command-line-audit-logging) | 3.10 | -   | -   | 6.10 | N/A  | -   | -   | -   |
| [1.11](adf-security-baseline.md#111-use-automated-tools-to-monitor-network-resource-configurations-and-detect-changes) | -    | 3.11 | -   | -   | 6.11 | 7.11 | -   | -   | -   |
| -    | -    | 3.12 | -   | -   | 6.12 | 7.12 | -   | -   | -   |
| -    | -    | N/A  | -   | -   | N/A  | 7.13 | -   | -   | -   |

## Mapping details
ADF Security Baseline details are [here](adf-security-baseline.md). \
ADF Security Use Cases are [here](adf-security-usecase.md).

```
+----------+      +---------------+      +-------------+      +-------------+      +------------+
| Security |      |   Identify    |      |             |      | Use Case    |      | Develop    |
| Baseline | +--> |   Applicable  | +--> | Team Review | +--> | Definitions | +--> | Use Cases  |
|          |      |   Cases       |      |             |      |             |      |            |
+----------+      +---------------+      +-------------+      +-------------+      +------------+

```