# T1110 – Brute Force (Crowbar RDP)

**MITRE Technique**: [T1110 – Brute Force](https://attack.mitre.org/techniques/T1110/)

This simulation demonstrates an RDP brute-force attack using the Crowbar tool against a domain-joined Windows 10 target. The purpose is to validate detection capabilities in Windows event logs and Splunk.

---

## 🎯 Objective

* Launch a brute-force attack using Crowbar
* Observe failed login attempts (Event ID 4625) in Windows logs
* Confirm detection in Splunk

---

## 🧪 Attack Method

The Crowbar tool is used with a list of usernames and passwords to perform a brute-force attack over RDP.

```bash
crowbar -b rdp -s 192.168.10.100/32 -u usernames.txt -C passwords.txt -n 3389
```

This command attempts RDP login on the target machine with each credential pair.

---

## 🔍 Detection in Splunk

### Tools Involved:

* Crowbar running on Kali Linux
* Target machine running Windows 10 with RDP enabled
* Sysmon and Windows Event Logging enabled
* Splunk indexing security logs from the Windows host

### Detection Method:

* Windows logs failed login attempts as Event ID **4625**
* Splunk queries identify excessive 4625 events from a single source

### Splunk Detection Query:

```splunk
index=endpoint EventCode=4625
| stats count by Account_Name, host, IpAddress
| where count > 5
```

### What to Look For:

* Numerous Event ID 4625 logs
* Repeated attempts from same IP/usernames
* Spike in authentication failures over short time

> 🔎 **Correlation with Account Lockouts (4740)**:
> A high number of 4625 events may lead to account lockout events (ID 4740). This correlation confirms the brute-force impact.

---

## ✅ Result

* Brute-force attempts logged as multiple 4625 events
* Detection confirmed through Splunk dashboard queries

---

## 📸 Screenshots

### 1. Crowbar tool launched with RDP brute-force settings:

![Crowbar Launch](../screenshots/crowbar%20tool%20bruteforce.PNG)

### 2. RDP brute-force in progress:

![Brute Forcing](../screenshots/crowbar%20bruteforce%20in%20progress.PNG)

### 3. Windows logs show Event ID 4625 for failed attempts:

![Failed Logins](../screenshots/rdp%20failed%20login%20splunk%20event%204625.PNG)

### 4. Splunk detection of brute-force login attempts:

![Splunk Detection](../screenshots/rdp%20attack%20brute%20force%20evidence.PNG)
