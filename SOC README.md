This project demonstrates my ability to design and deploy a complete Security Operations Center (SOC) monitoring environment using open-source tools. The lab simulates real-world enterprise logging, detection, alerting, and incident response workflows.

I configured a Wazuh SIEM server and deployed a Kali Linux endpoint running Wazuh Agent, Suricata IDS, and Filebeat. Detection pipelines were validated using simulated attacks such as Nmap scanning, brute-force authentication attempts, and file integrity modifications.

This project showcases technical skills required for SOC Analyst Level 1 and 2 roles, including SIEM architecture, log ingestion, IDS tuning, Linux administration, and incident reporting.

            Learning Outcomes

By completing this lab I gained hands-on experience in:

Deploying and configuring Wazuh SIEM

Installing and tuning Suricata Intrusion Detection System

Configuring Filebeat to ship security logs to the SIEM

Understanding log pipelines, ingestion, parsing, and alert generation

Running offensive security tools (Nmap, Hydra, SSH brute-force)

Validating alerts inside a SOC dashboard

Writing professional SOC incident reports

Creating a complete detection engineering project for a portfolio

flowchart LR
    A[Kali Linux VM] -- Wazuh Agent --> B((Wazuh Manager))
    A -- Suricata Alerts --> E[Filebeat]
    E -- JSON Events --> C((Wazuh Indexer))
    B -- Processed Alerts --> D[Wazuh Dashboard]

    subgraph Endpoint
        A
        E
    end

    subgraph SIEM Stack
        B
        C
        D
    end


Environment Setup
🔹 Host Machine

Windows 10/11

VMware Workstation

🔹 Virtual Machines
1. Wazuh SIEM Stack

Role: Manager, Indexer, Dashboard

OS: Ubuntu Server 22.04 or Wazuh OVA

Network: Host-Only or NAT

2. Kali Linux Endpoint

Role: Endpoint generating logs + attacks

Tools: Suricata, Filebeat, Wazuh Agent

Network: Same subnet as Wazuh Manager

Deployment Overview
1. Install Wazuh SIEM

Installed Wazuh Manager, Indexer, Dashboard

Verified web interface

Created admin credentials

Confirmed health of cluster

2. Install & Configure Wazuh Agent on Kali

Installed Wazuh agent package

Registered agent with Manager

Verified heartbeats and logs in dashboard

Confirmed agent is Active

3. Install Suricata on Kali

Configuration included:

Setting the network interface (eth0, ens33, etc.)

Enabling JSON output

Enabling eve.json logging for Filebeat ingestion

Running Suricata as a service

4. Install Filebeat & Enable Suricata Module

Configured:

Suricata module

Filebeat → Wazuh Indexer output settings

SSL verification disabled for localhost

Filebeat systemd service running

Attack Simulations (Detection Validation)
Test 1 — Nmap Scan (Network Reconnaissance)
sudo nmap -A 127.0.0.1


Expected Alert:
ET SCAN Nmap Scripting Engine User-Agent Detected

Test 2 — Failed SSH Login Brute-Force
ssh baduser@127.0.0.1


Attempt several incorrect passwords.

Expected Alert:
sshd: Possible brute-force attack

Test 3 — File Integrity Monitoring (FIM)
echo "#test" | sudo tee -a /etc/passwd


Expected Alert:
File modified: /etc/passwd

Alert Verification in Wazuh Dashboard

Validated alerts in:

Security Events → Suricata

Security Events → Authentication

Security Events → Integrity Monitoring

Agents → Kali Agent (Online)


Security Incident Report Template
1. Executive Summary

Short description of the incident, impact, and resolution.

2. Incident Details
Field	Information
Incident ID	INC-2025-001
Date/Time Detected	
Detected By	Wazuh SIEM
Alert Source	Suricata / Authentication / FIM
Severity	Low / Medium / High
Status	Open / Investigating / Closed
3. Indicators of Compromise (IOCs)
IOC Type	Value	Notes
IP Address	192.168.x.x	
Username	baduser	
File	/etc/passwd	
4. MITRE ATT&CK Mapping
Technique	ID	Description
Network Scanning	T1046	Host & port discovery
Brute-Force	T1110	Multiple failed logins
File Modification	T1059	Unauthorized file edit
5. Timeline of Events

Detailed narrative of the event sequence.

6. Root Cause Analysis

Explain what happened and why.

7. Containment & Eradication

What actions were taken to respond.

8. Recommendations

Hardening steps such as:

Enable multi-factor authentication

Deploy network segmentation

Improve IDS rule tuning

Enforce least privilege access
