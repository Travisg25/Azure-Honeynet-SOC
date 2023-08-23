# Cloud Honeynet and Mini SOC
![Cloud Honeynet / SOC](https://i.imgur.com/mykLnhS.jpg)

## Introduction

In this project, my goal was to enhance my understanding of security dynamics and incident response within cloud environments. I started by creating a mini honeynet in Azure. To monitor activity, I ingested log data from multiple resources into a Log Analytics workspace. Microsoft Sentinel then utilized this information to construct attack maps, activate alerts, and draft incidents.

To demonstrate the effectiveness of security controls, I initially observed the security metrics in a non-hardened environment for 24 hours. Subsequently, I implemented targeted security measures and continued my observation for another day. The comparative results are presented below. By undertaking this project, I've showcased proficiency in Azure platform security, incident analysis, and the application of protective measures in real-time environments. Metrics highlighted include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Alerts generated in Log Analytics)
- SecurityIncident (Cases defined by Sentinel)
- AzureNetworkAnalytics_CL (Undesirable traffic directed at our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/ElQilzN.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/9lYHtUO.jpg)
 
In Azure, I designed a mini honeynet with a specific architectural blueprint. The components integral to this design include:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (Including 2 Windows and 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For our initial observations, denoted as "BEFORE" metrics, each resource was deliberately vulnerable:

The Virtual Machines had both their Network Security Groups and intrinsic firewalls entirely unrestricted.
All resources were made easily accessible from the internet, showcasing public endpoints without any utilization of Private Endpoints.
Contrastingly, for the "AFTER" metrics, substantial security enhancements were applied:

Network Security Groups underwent meticulous hardening, allowing traffic exclusively from my admin workstation.
Other resources were fortified using their inherent firewalls, complemented with the additional protection layer of Private Endpoints.
This architectural layout and the consequent modifications enabled me to gauge the efficacy of various security measures within a controlled cloud environment.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/v472XNc.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/PKIcT5O.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/FN4iLaj.png)<br>

## Metrics Overview - Before & After



Prior to Security Enhancements:
During a 24-hour observation period (from 2023-08-08 22:21:50 to 2023-08-09 22:21:50), the following metrics were recorded in the unprotected environment:


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 29,698
| Syslog                   | 2,463
| SecurityAlert            | 8
| SecurityIncident         | 269
| AzureNetworkAnalytics_CL | 843


Attack maps Analysis pre-security application:
Notably, there were many recorded attempted attacks across all metrics.

## Attack Maps Before Hardening / Security Controls

```All map queries  returned no results due to NO instances of higher threat malicious activity for the 24 hour period after hardening.```

There was a 70% reduction in the Windows VM's attack/events; and nearly 100% reduction across the rest of the metrics recorded.

## Metrics After Hardening / Security Controls

After applying robust security measures, metrics for another 24 hours (from 2023-08-08 22:21:50 to 2023-08-09 22:21:50) were as follows:

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8,947
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

These results underscore the efficacy of the applied security controls in drastically reducing potential security threats and incidents.

## Conclusion

This project entailed the meticulous design and oversight of a mini honeynet within Microsoft Azure. By integrating diverse log sources into a Log Analytics workspace, a foundation was established for Microsoft Sentinel to interpret and act, triggering alerts and formulating incidents. A core aspect of this initiative was observing the contrast in security metrics pre and post the implementation of robust security controls. The tangible decline in security events and incidents post-intervention underscores the potent efficacy of these measures.

However, an essential caveat to consider is the network's utilization. With higher user traffic and activities, it's conceivable that the subsequent 24 hours post-hardening might have yielded more security events and alerts.

Tackling such a project provides profound insights into the intricate dynamics of cybersecurity within cloud platforms. Not only does it spotlight the immediate impacts of security measures, but it also unravels the layered challenges posed by real-world user interactions. For anyone aspiring to excel in a cybersecurity role within cloud environments, mastering such complexities is paramount. This endeavor serves as a testament to the multifaceted nature of cloud security and the need for adaptive, vigilant strategies in an ever-evolving digital landscape.
