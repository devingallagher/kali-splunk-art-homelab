
## 📦 Installing Splunk on Ubuntu (Indexer/Server)

This section walks through setting up Splunk Enterprise on the `Splunk01` Ubuntu virtual machine.

## 🖥️ Splunk Role in Lab

* **Splunk01 (Ubuntu)** → Acts as the **indexer/server**
* **Windows Target (Windows 10)** → Runs the **Universal Forwarder** to send logs to Splunk

## 🧭 What Gets Installed Where

* **Splunk Enterprise (server/indexer)** is installed on the **Ubuntu Splunk01** VM.
* **Splunk Universal Forwarder** is installed on **both** the **Windows 10 Target** and the **Windows Server (AD01)** machines.

The Universal Forwarder collects logs (including Sysmon and Security logs) and forwards them to the Splunk server for indexing and search.

---

## 📥 Step 1: Download Splunk Enterprise (on Ubuntu)

Go to: [https://www.splunk.com/en\_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
Download the `.deb` installer package for Ubuntu.

Example:

```bash
wget -O splunk-9.2.0.1.deb 'https://download.splunk.com/products/splunk/releases/9.2.0.1/linux/splunk-9.2.0.1-xxxxx.deb'
```

---

## ⚙️ Step 2: Install Splunk on Ubuntu

```bash
sudo dpkg -i splunk-9.2.0.1.deb
sudo /opt/splunk/bin/splunk start --accept-license
sudo /opt/splunk/bin/splunk enable boot-start
```

---

## 🌐 Step 3: Access Splunk Web UI

Visit in browser:

```
http://[SPLUNK_VM_IP]:8000
```

Use credentials created during setup.

---

## 📥 Step 4: Install Universal Forwarder on Windows

Download from: [https://www.splunk.com/en\_us/download/universal-forwarder.html](https://www.splunk.com/en_us/download/universal-forwarder.html)

Install on **Windows Target** and **AD01**, configure each to forward logs to Splunk01 IP on port `9997`.

---
