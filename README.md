![img](https://i.imgur.com/B1YCDiQ.png)

# Introduction

In this lab, we're going to generate our attack traffic from a few vulnerable VMs. Once that traffic is generated, we'll analyze and capture logs. We'll also be defining alerts for malicious activity that will trigger security incidents within Sentinel.  Next, We'll remediate and harden our VMs by NIST 800-61 standards. Our vulnerable environment will run for 24 hrs so traffic can be captured. Once we analyze the data, we'll harden our environment and observe the results after another 24 hrs have passed. These are the following metrics we'll be collecting:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet

# Objective

The goal of this project will be to observe the attack traffic, observe the alerts and incidents triggered, and then remediate those incidents using the incident life cycle. 

# Archtectural Components

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

# Cloud Architecture Before and After Hardening 

Our before metrics will showcase what our environment looks like when we intentionally expose it to the public internet. Leaving it vulnerable to cyber attacks outside of our environment. To do this, we intentionally opened up all ports in the Network Security Groups, making endpoints easily detected and unprotected. Our "After" metrics will be the result of blocking ALL traffic in our Network Security Group, thus separating our cloud environment from the internet. 

![Cloud archetecture before and after](https://i.imgur.com/MwVBr9z.png)

# Attack Maps BEFORE Hardening / Security Controls

<h3>SSH Authentication Failure Map</h3>

The attack map below highlights a handful of attackers attempting to brute force their way into our Linux virtual machine 
resulting in failed syslog authentications.  

![img](https://i.imgur.com/5obqPWt.png)


<h3>Network Security Groups Open Ports Map</h3>

The attack map below highlights the consequences of leaving your Network Security Groups open. When NSG's are not properly configured, it's an invitation for malicious traffic to make its way into your organization and compromise your system. 

![img](https://i.imgur.com/PA55maQ.png)


<h3>Windows RDP/SMB Authentication Failure Map</h3>

The attack map below highlights a handful of attackers attempting to exploit SMB and RDP protocols within our vulnerable Windows machine. 

![img](https://i.imgur.com/0is25A1.png)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

<b>Start Time</b> 2/1/2024, 10:53:52.201 PM
<b>Stop Time</b> 2/2/2024, 10:53:52.201 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 66810
| Syslog                   | 31174
| SecurityAlert            | 3
| SecurityIncident         | 362
| AzureNetworkAnalytics_CL | 1069
