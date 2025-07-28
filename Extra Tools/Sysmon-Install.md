# 🛠️ Installing Sysmon on Windows 10

This guide shows how to install Sysmon on the Windows 10 target machine and apply a custom configuration to capture detailed event logs for Splunk.

---

## 📥 Step 1: Download Sysmon

Download Sysmon from the official Microsoft Sysinternals page:
🔗 [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

Extract the contents (e.g. `Sysmon64.exe`, `Eula.txt`) into a working directory on your Windows 10 machine.

---

## ⚙️ Step 2: Apply Configuration

Use the provided `sysmon_config.xml` file from this repo (`splunk_config/sysmon_config.xml`).

Place it in the same directory as Sysmon and run the following command in an **elevated PowerShell window** (Run as Administrator):

```powershell
./Sysmon64.exe -i ..\sysmonconfig.xml
```

This command:

* Accepts the license agreement
* Installs Sysmon as a service
* Applies the custom XML config for detailed logging

---

## 🧪 Step 3: Verify Sysmon Is Running

Open **Event Viewer** → `Applications and Services Logs` → `Microsoft` → `Windows` → `Sysmon` → `Operational`

You should now see logs such as:

* Event ID 1: Process creation
* Event ID 3: Network connections
* Event ID 10: Process access

---

## 🔁 Optional: Update Config Later

To update the config without reinstalling:

```powershell
Sysmon64.exe -c sysmon_config.xml
```

To uninstall:

```powershell
Sysmon64.exe -u
```

---

## 📸 Screenshots

### 1. Sysmon installation command:

![Sysmon Install](../screenshots/sysmon%20correctly%20installed.PNG)

### 2. Sysmon logs visible in Event Viewer: *(Add screenshot if available)*
