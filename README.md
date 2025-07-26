Cloud Honeynet / SOC
Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

    SecurityEvent (Windows Event Logs)
    Syslog (Linux Event Logs)
    SecurityAlert (Log Analytics Alerts Triggered)
    SecurityIncident (Incidents created by Sentinel)

    AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

    <img width="957" height="541" alt="Screenshot 2025-07-26 at 11 02 06 AM" src="https://github.com/user-attachments/assets/ba4f38ef-b494-4bfb-b085-b8d3a46ae913" />
