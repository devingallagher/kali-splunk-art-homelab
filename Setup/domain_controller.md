# 🛡️ Domain Controller Setup (Windows Server 2019)

This guide explains how the Windows Server 2019 VM was configured to act as the Domain Controller (DC) and DNS server for the Kali + Splunk + Atomic Red Team (ART) home lab.

---

## 🧱 Role of the Domain Controller

The domain controller (AD01) manages:

- Centralized user authentication
- DNS resolution for all machines in the network
- Domain membership for Windows clients
- Support for group policies and administrative control

---

## ⚙️ Step-by-Step Setup

### 1. Install Active Directory Domain Services (AD DS)

1. Open **Server Manager**
2. Go to **Manage > Add Roles and Features**
3. Select **Role-Based or Feature-Based Installation**
4. Choose the local server
5. Select **Active Directory Domain Services**
6. Accept the defaults and install
7. Wait for installation to complete

📸 Example:  
![Install AD Role](../screenshots/install%20ad%20ds%20and%20promoted%20server%20to%20domain%20controller.PNG)

---

### 2. Promote the Server to Domain Controller

1. In **Server Manager**, click the yellow flag (post-installation tasks)
2. Choose **Promote this server to a domain controller**
3. Select **Add a new forest**
4. Set the root domain name: `crazy1wins.local`
5. Set a **Directory Services Restore Mode (DSRM) password**
6. Accept all default paths
7. Allow the system to reboot

📸 Example:  
![Domain Name](../screenshots/domain%20name.PNG)

---

### 3. Configure DNS

- The AD DS installation automatically configures DNS
- You can verify under **DNS Manager** that forward and reverse zones are set
- The server IP (`192.168.10.7`) should now act as the DNS server for the network

---

### 4. Create Domain Users

1. Open **Active Directory Users and Computers**
2. Right-click the Users container > **New > User**
3. Create accounts like `tsmith`, `jsmith`, etc.
4. Assign temporary passwords
5. (Optional) Add users to the **Remote Desktop Users** group to allow RDP

📸 Example:  
![Add Users](../screenshots/add%20users.PNG)  
![Add User to Group](../screenshots/add%20user%20to%20group.PNG)

---

## 🧠 Why It Matters

- Enables centralized login and policy management
- DNS integration supports Splunk forwarding and detection logic
- Required for simulating real-world AD attacks (e.g., account creation, RDP abuse)
