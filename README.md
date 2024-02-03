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
![img](https://i.imgur.com/5obqPWt.png)

<h3>Network Security Groups Open Ports Map</h3>
![img](https://i.imgur.com/PA55maQ.png)

<h3>Windows RDP/SMB Authentication Failure Map</h3>
![img](https://i.imgur.com/0is25A1.png)
