![img](https://i.imgur.com/Zs7vGzn.png)

# Introduction

In this lab, we're going to generate our attack traffic from a few vulnerable VMs that were setup on a honeynet. Once that traffic is generated, we'll analyze and capture logs. We'll also be defining alerts for malicious activity that will trigger security incidents within Sentinel.  Next, We'll remediate and harden our VMs by NIST 800-61 standards. Our vulnerable environment will run for 24 hrs so traffic can be captured. Once we analyze the data, we'll harden our environment and observe the results after another 24 hrs have passed. These are the following metrics we'll be collecting:

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
- Virtual Machines (2 Windows, 1 Linux)
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

The attack map below highlights the consequences of leaving your Network Security Groups open. When NSGs are not properly configured, it's an invitation for malicious traffic to make its way into your organization and compromise your system. 

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


## Security Control Implementation

- <b>Network Security Groups:</b> For this lab, we left all inbound ports open for our honeynet. In a real-world scenario, this would be a huge risk and result in inviting unwanted threats to possibly breach your organization. To help separate the VMs from being overexposed to outside threats, we set our inbound port rules for the Network Security Group for both VMs to only allow incoming traffic from the IP of the host machine. We also enabled a firewall around our subnet fro an added layer of protection. 

- <b>Implementing Regulatory Compliance:</b> Microsoft Defender for Cloud enables organizations to set security benchmarks based off of well-known security controls. In this lab, we enabled security controls based off of NIST 800-53 controls. 

- <b>Boundary Protection (NIST 800-53: SC-7)</b> Private links and private endpoints were implemented on the Azure storage account and key vaults so that the privacy of our data could be preserved and separated from the public internet. Private links within the cloud environment will enable authorized users to access services while restricting intruders. Private endpoints will take the network interface of your cloud environment and its private IP address and create a more secure connection when interacting with your cloud services. 

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured <b>AFTER</b> implementing security controls. 

<b>Start Time</b> 2/3/2024, 8:11:26.180 PM 
<b>Stop Time</b> 2/4/2024, 8:11:26.180 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4752            
| Syslog                   | 1743
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion 

In this lab, we constructed a honeynet within the landscape of Microsoft Azure cloud. We learned how to set up and use the Log Analytics workspace, We learned how to query for security incidents using KQL, establish custom and manual alerts, and deploy essential security controls. This hands-on experience served as a pivotal exercise and bettered my understanding of cloud security. As cloud computing continues to rise, it becomes paramount for security analysts to hone their skills.  This lab was a great exercise in getting to know the Sentinel interface while sharpening my skills in the incident response process.
