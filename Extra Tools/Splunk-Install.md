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

---

# 📦 Installing Splunk on Ubuntu (Indexer/Server)

This section walks through setting up Splunk Enterprise on the `Splunk01` Ubuntu virtual machine.

## 🖥️ Splunk Role in Lab

* **Splunk01 (Ubuntu)** → Acts as the **indexer/server**
* **Windows Target** → Runs the **Universal Forwarder** to send logs to Splunk

---

## 📥 Step 1: Download Splunk Enterprise

Go to: [https://www.splunk.com/en\_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
Download the `.deb` installer package for Ubuntu.

Example:

```bash
wget -O splunk-9.2.0.1.deb 'https://download.splunk.com/products/splunk/releases/9.2.0.1/linux/splunk-9.2.0.1-xxxxx.deb'
```

---

## ⚙️ Step 2: Install Splunk

Install the downloaded `.deb` package:

```bash
sudo dpkg -i splunk-9.2.0.1.deb
```

Start Splunk and accept the license:

```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

Enable Splunk to start on boot:

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

---

## 🔑 Step 3: Login and Configure Web UI

Access Splunk Web from your browser at:

```
http://[SPLUNK_VM_IP]:8000
```

Login using the admin username and password you created during setup.

---

## 📥 Step 4: Install Splunk Universal Forwarder on Target (Windows)

Download Splunk Universal Forwarder from: [https://www.splunk.com/en\_us/download/universal-forwarder.html](https://www.splunk.com/en_us/download/universal-forwarder.html)

Install on Windows and configure to forward logs to Splunk01’s IP on port `9997`.

---

## 📸 Screenshots

### 1. Splunk01 VM setup (with NAT network):

![Splunk NAT](../screenshots/creating%20nat%20network%20to%20our%20ip,%20than%20putting%20all%20the%20vms%20on%20it%20is%20the%20splunk%20ss.PNG)

### 2. Splunk VM attached to NAT network:

![Splunk Adapter](../screenshots/puytting%20splunk%20to%20nat%20netwrok.PNG)
