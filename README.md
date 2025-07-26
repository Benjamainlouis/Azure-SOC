Building a SOC + Honeynet in Azure (Live Traffic)

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/f0aadc2f-9a71-4534-87c4-6f552240ea71" />

Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 72 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

  - SecurityEvent (Windows Event Logs)
  - Syslog (Linux Event Logs)
  - SecurityAlert (Log Analytics Alerts Triggered)
  - SecurityIncident (Incidents created by Sentinel)
  - AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

Architecture Before Hardening / Security Controls

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/e7111fa8-38f7-49ab-9f37-7d9793207393" />

Architecture After Hardening / Security Controls

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/0596ec79-d16a-4b77-95a5-17a7734f3d62" />

The architecture of the mini honeynet in Azure consists of the following components:

  - Virtual Network (VNet)
  - Network Security Group (NSG)
  - Virtual Machines (2 windows, 1 linux)
  - Log Analytics Workspace
  - Azure Key Vault
  - Azure Storage Account
  - Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

Attack Maps Before Hardening / Security Controls

<img width="1139" height="634" alt="image" src="https://github.com/user-attachments/assets/f4be4941-fac0-41c8-ac8d-4ec0209f5983" />
<img width="1108" height="643" alt="image" src="https://github.com/user-attachments/assets/63e09186-35b0-4303-a3fd-2542be9f247b" />
<img width="1216" height="680" alt="image" src="https://github.com/user-attachments/assets/3296e70f-4cc9-4e9a-8325-5642de2a2f94" />

Metrics Before Hardening / Security Controls
The following table shows the metrics we measured in our insecure environment for 72 hours: Start Time 2025-07-17 17:04:29 Stop Time 2025-07-21 17:04:29

|   Metrics                | Count 
| ------------------------ | -----
| SecurityEvent            | 24935
| Syslog                   | 32042
| SecurityAlert            | 511
| SecurityIncident         | 512
| AzureNetworkAnalytics_CL | 257951

Attack Maps Before Hardening / Security Controls

All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.
Metrics After Hardening / Security Controls
The following table shows the metrics we measured in our environment for another 72 hours, but after we have applied security controls: Start Time 2025-07-22 15:37 Stop Time 2025-07-25 15:37


|   Metrics                | Count 
| ------------------------ | -----
| SecurityEvent            | 1341
| Syslog                   | 6
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 103904

Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 72-hour period following the implementation of the security controls.

This project helped me get in the mindset of a network and security engineer. Although all the incidents were controlled, it allowed me the oppurtuniuty to see how real world threats would attack my network. If this were a real attack, this data would give me the oppuritunity to refect on policies and changes that may be inacted to mitigate this sort of attacks from occuring in the future,
This project helped me get in the mindset of a network and security engineer. Although all the incidents were controlled, it allowed me the oppurtuniuty to see how real world threats would attack my network. If this were a real attack, this data would give me the oppuritunity to refect on policies and changes that may be inacted to mitigate this sort of attacks from occuring in the future,
