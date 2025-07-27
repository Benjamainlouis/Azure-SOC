Building a SOC + Honeynet in Azure (Live Traffic)

<img width="787" height="397" alt="image" src="https://github.com/user-attachments/assets/7e02bbb0-1cca-4a16-ae66-4e5a661de9bc" />

Introduction

For this project, I created a small honeynet environment in Microsoft Azure. I collected logs from different Azure resources and sent them to a Log Analytics workspace. Microsoft Sentinel then used those logs to build attack maps, generate alerts, and create incidents.

First, I ran the environment without security controls for 72 hours to gather baseline metrics. After that, I applied security measures to strengthen the environment, then collected data for another 72 hours. The results from both phases are compared below. The metrics we’ll focus on include:

  - SecurityEvent (Windows Event Logs)
  - Syslog (Linux Event Logs)
  - SecurityAlert (Log Analytics Alerts Triggered)
  - SecurityIncident (Incidents created by Sentinel)
  - AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

Architecture Before Hardening / Security Controls

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/e7111fa8-38f7-49ab-9f37-7d9793207393" />

Architecture After Hardening / Security Controls

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/0596ec79-d16a-4b77-95a5-17a7734f3d62" />

The architecture of the honeynet in Azure consists of the following components:

  - Virtual Network (VNet)
  - Network Security Group (NSG)
  - Virtual Machines (2 windows, 1 linux)
  - Log Analytics Workspace
  - Azure Key Vault
  - Azure Storage Account
  - Microsoft Sentinel

BEFORE Metrics (Insecure Setup)

  - All resources were deployed with public access, meaning anyone on the internet could try to connect to them.
  - The Virtual Machines had no restrictions in place. Their Network Security Groups (NSGs) allowed all traffic, and their built-in firewalls were not configured to block anything.
  - Other services such as SQL Server were also set up with public endpoints, which made them fully visible and reachable from the internet.
  - No Private Endpoints were used, so there was no protection to limit access to only internal or trusted sources.

AFTER Metrics (Secured Setup)

  - The Network Security Groups were updated to block all incoming traffic except from my admin workstation. This means only I could access the environment remotely.
  - All other resources were protected by enabling their built-in firewalls, which limited who could reach them.
  - Private Endpoints were also added to each resource, which means those services could now only be accessed from inside the virtual network—not from the public internet.
    
Attack Maps Before Hardening / Security Controls

<img width="1139" height="634" alt="image" src="https://github.com/user-attachments/assets/f4be4941-fac0-41c8-ac8d-4ec0209f5983" />
<img width="1108" height="643" alt="image" src="https://github.com/user-attachments/assets/63e09186-35b0-4303-a3fd-2542be9f247b" />
<img width="1216" height="680" alt="image" src="https://github.com/user-attachments/assets/3296e70f-4cc9-4e9a-8325-5642de2a2f94" />

Metrics Before Hardening / Security Controls

The table below shows the security metrics collected from the insecure environment during a 72-hour observation period.
  - Start Time: July 17, 2025, at 5:04 PM
  - End Time: July 20, 2025, at 5:04 PM

|   Metrics                | Count 
| ------------------------ | -----
| SecurityEvent            | 24935
| Syslog                   | 32042
| SecurityAlert            | 511
| SecurityIncident         | 512
| AzureNetworkAnalytics_CL | 257951

Attack Maps Before Hardening / Security Controls

Once I applied the security controls, I continued monitoring the environment for another 72 hours. During that time, none of the attack map queries returned any results, which suggests that the hardening efforts were successful—there were no signs of malicious activity.

Here are the metrics I collected during the secured period:
  - Start Time: July 22, 2025, at 3:37 PM
  - End Time: July 25, 2025, at 3:37 PM

|   Metrics                | Count 
| ------------------------ | -----
| SecurityEvent            | 1341
| Syslog                   | 6
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 103904

Conclusion

In this project, I built a mini honeynet in Microsoft Azure and connected log sources to a Log Analytics workspace. Microsoft Sentinel was used to generate alerts and create incidents based on the collected logs. I measured metrics from the environment before and after applying security controls. The results clearly showed a significant drop in security events and incidents once those controls were in place, highlighting their effectiveness.

It’s also important to note that if the environment had been actively used by real users, it’s likely that more security events and alerts would have been triggered during the 72-hour period following hardening—either from legitimate activity or from new attempted threats.

This project really helped me step into the mindset of a network and security engineer. It gave me the opportunity to observe how real-world threats might target my environment. If this had been a live production system, the data gathered would be valuable for reviewing and adjusting security policies to better defend against similar attacks in the future.

Bellow is a video demonstration of this lab created by me:

https://youtu.be/9aiXfF2uxRk
