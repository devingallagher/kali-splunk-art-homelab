
# 📘 Atomic Red Team Notes

**Purpose**: Atomic Red Team (ART) is a library of simple, flexible tests mapped to the MITRE ATT\&CK framework to simulate adversary behavior in a controlled way.

---

## 🛠️ Setup

1. **Install Atomic Red Team repo**:

```bash
git clone https://github.com/redcanaryco/atomic-red-team.git
cd atomic-red-team
```

2. **Install Prerequisites (Windows Target)**:

* PowerShell 5.0+
* Execution Policy set to allow scripts:

```powershell
Set-ExecutionPolicy Bypass -Scope Process
```

* Import `Invoke-AtomicRedTeam.ps1` script:

```powershell
Import-Module .\atomics\Invoke-AtomicRedTeam.ps1
```

---

## 🧪 Running a Test

Each test is linked to a specific MITRE ATT\&CK technique. To execute:

```powershell
Invoke-AtomicTest T1059.001 -TestNumbers 1 -Verbose
```

To see test details:

```powershell
Get-AtomicTechnique -TechniqueID T1059.001
```

---

## 🔍 Detection in Splunk

1. Ensure your Windows target machine is running:

   * Sysmon
   * Winlogbeat or Splunk Universal Forwarder
   * Proper EventCode ingestion into Splunk (Sysmon IDs, 4688, 1, etc.)

2. Example Splunk search for command execution:

```splunk
index=endpoint EventCode=4688
| stats count by CommandLine, ParentImage, Image
```

---

## ✅ Example Test: T1059.001 (PowerShell)

**Atomic Test**: Executes PowerShell command to simulate execution

**Expected Result**:

* Process creation event (EventCode 4688)
* PowerShell launch from cmd.exe or explorer.exe

**Splunk Detection Query**:

```splunk
index=endpoint EventCode=4688 Image=*powershell.exe*
```

---

## 💡 Tips

* Always revert test changes where needed
* Some tests require cleanup scripts
* Use a safe, isolated lab environment

---

## 📸 Screenshots

1. ART GitHub clone:
2. PowerShell test in action:
3. Detection in Splunk (EventCode 4688):
4. Mapping to MITRE technique in ATT\&CK Navigator:
