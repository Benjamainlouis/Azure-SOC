Cloud Honeynet / SOC
Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

    SecurityEvent (Windows Event Logs)
    Syslog (Linux Event Logs)
    SecurityAlert (Log Analytics Alerts Triggered)
    SecurityIncident (Incidents created by Sentinel)

    AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/f0aadc2f-9a71-4534-87c4-6f552240ea71" />

