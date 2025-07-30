# Active Directory – README

This lab simulates a real-world detection and monitoring environment using Atomic Red Team, Splunk, Sysmon, and common attack tools like Crowbar. It’s designed to help SOC analysts, students, and enthusiasts understand how to detect malicious behavior in enterprise systems.

---

## Lab Components

| Component         | Role                                              |
|------------------|---------------------------------------------------|
| **Kali Linux**    | Attacker VM (Crowbar, Atomic Red Team)           |
| **Windows 10**    | Target VM with Sysmon and Splunk Forwarder       |
| **Windows Server**| Domain Controller (AD01) with Splunk Forwarder   |
| **Ubuntu**        | Splunk Enterprise Indexer (Splunk01)             |

---

## What’s Covered

- Installing Sysmon with a custom config for process/network visibility
- Setting up Splunk on Ubuntu and forwarding logs from Windows
- Simulating PowerShell execution via Atomic Red Team
- Detecting Event ID 1 (process creation) and ID 4625 (failed login)
- Simulating brute-force attacks with Crowbar
- Visualizing events in Splunk

---

## Installations

**Splunk Universal Forwarder**  
→ Installed on:  
- Windows 10 (Target01)  
- Windows Server (AD01)  

**Splunk Enterprise Server**  
→ Installed on:  
- Ubuntu VM (Splunk01)

**Sysmon**  
→ Installed on:  
- Windows 10 (Target01) with XML config for extended logging

---
