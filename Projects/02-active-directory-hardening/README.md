# 🏢 Project 02: Active Directory Enterprise Simulation & GPO Hardening

## 📌 Executive Summary
This project details the deployment, organizational structure, and security hardening of a simulated enterprise Active Directory Domain Services (AD DS) environment hosted on Windows Server 2022. The objective was to create an identity management baseline, enforce least-privilege administrative access, and configure granular Windows Audit Policies alongside Microsoft Sysmon to capture host-based security telemetry for SIEM ingestion.

---

## 🛠️ Environment Architecture & Roles

| Host Name | OS | Domain Role | Key Services / Components |
| :--- | :--- | :--- | :--- |
| **DC01** | Windows Server 2022 | Primary Domain Controller | AD DS, DNS, Group Policy (GPMC), Sysmon Agent |
| **WKSTN01** | Windows 10 Enterprise | Domain-Joined Endpoint | Corporate User Workstation, Sysmon Agent, Local Audit Logging |

---

## ⚙️ Key Implementation & Hardening Steps

### 1. Active Directory & Organizational Unit (OU) Tiering
To prevent credential theft and administrative privilege escalation, the directory structure was designed using an enterprise Tiering Model (`Corp.Lab` domain):

Corp.Lab/
- 📂 Admin         (Privileged accounts separated from standard users)
- 📂 Groups        (Security and distribution groups for access control)
- 📂 Services      (Dedicated service accounts and non-human identities)
- 📂 Users         (Standard corporate employee accounts)
- 📂 Workstations   (Domain-joined client endpoints)


### 2. Group Policy Objects (GPOs) Deployed
Four custom GPOs were linked to enforce baseline security controls across the domain:

1. **`GPO-Advanced-Audit-Policy`**: Enforces granular Windows Event Logging (capturing Event IDs `4624` Logon, `4625` Failed Logon, `4688` Process Creation, `4720` Account Creation).
2. **`GPO-Disable-LLMNR-NetBIOS`**: Disables insecure legacy resolution protocols to prevent NTLM relay and poisoning attacks (e.g., Responder).
3. **`GPO-Sysmon-Deployment`**: Automatically deploys Microsoft Sysmon service and pushes updated XML configuration files across endpoints.
4. **`GPO-Password-Policy`**: Enforces complex password requirements, account lockout thresholds (5 failed attempts), and lockout duration.

### 3. Sysmon & Host Telemetry Integration
* Installed **Microsoft Sysmon** utilizing SwiftOnSecurity's hardened configuration file.
* Configured command-line process creation logging (Event ID 1) with full command-line arguments enabled via Group Policy (`Include command line in process creation events`).

---

## 📊 Verification & Audit Policy Testing

To verify that GPOs applied correctly across endpoints:

1. Ran Resultant Set of Policy on `WKSTN01`:
   ```cmd
   gpresult /r /scope computer
Verified Sysmon service state:

PowerShell
Get-Service -Name "Sysmon"
Generated a test Security Event (4625 - Failed Logon) by attempting an invalid login to confirm local Event Viewer recording before shipping to Wazuh.

---

##💡 Lessons Learned & Technical Challenges
* **Issue:** Default Windows audit settings do not log detailed process execution command-line parameters required for threat hunting.
* **Resolution:** Explicitly enabled Include command line in process creation events under Computer Configuration -> Administrative Templates -> System -> Audit Process Creation.
* **Key Takeaway:** Enterprise identity security relies heavily on proactive auditing policies—if telemetry is not logged locally on the DC, the SIEM cannot detect credential abuse.

---

##📁 Included Artifacts in this Directory
* `ou-structure.png` - Active Directory Users and Computers (ADUC) hierarchy screenshot.
* `GPO-Advanced-Audit-Policy.xml` - Exported Group Policy settings for security auditing.
* `sysmon-config.xml` - Customized Sysmon configuration file applied across the domain.
* `gpresult-output.txt` - Verification log showing active GPOs applied to client nodes
* `telemetry-proof.png` - Sysmon Event ID 1 CommandLine capture verification.
