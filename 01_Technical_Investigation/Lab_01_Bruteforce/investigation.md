# 🛡️ SOC Technical Investigation: Bruteforce
**Lead Investigator:** [Your Name]  
**Academy:** LearnCyber Academy - Intermediate Capstone  

---

## 1. Executive Attack Summary
> [Provide a 3-5 sentence "TL;DR" of the incident. Describe the threat actor's behavior, the primary exploit used, and the ultimate outcome. Example: "The organization was targeted via a Follina RCE vulnerability which led to unauthorized shell access and credential harvesting."]

---

## 2. Incident Timeline (UTC)
| Timestamp | Event Description | Source Log / Evidence |
| :--- | :--- | :--- |
| **HH:MM** | **Initial Access:** User opens malicious file. | `Sysmon Event ID 1` |
| **HH:MM** | **Exploitation:** Connection to C2 IP [X.X.X.X]. | `Packet Capture / HTTP GET` |
| **HH:MM** | **Persistence:** Registry key or Scheduled Task created. | `Autoruns / Registry Hive` |
| **HH:MM** | **Exfiltration:** Sensitive data sent to external server. | `Network Flow Logs` |

---

## 3. The Attack Chain Breakdown
*This section identifies the "Three Pillars" of the breach.*

### 🟢 Entry Point
* **Identification:** [Describe how the attacker gained the first foothold.]
* **Technical Detail:** [e.g., "Exploited CVE-2022-30190 via remote template injection in 'Invoice.docx'."]
* **Visual Evidence:** ![Entry Point Screenshot](./screenshots/entry_point.png)

### 🟡 Lateral Movement
* **Identification:** [Did the attacker move to other systems or escalate privileges?]
* **Technical Detail:** [e.g., "Attacker utilized 'psexec' to move from Workstation-01 to the Domain Controller."]
* **Visual Evidence:** ![Lateral Movement Screenshot](./screenshots/lateral.png)

### 🔴 Data Exfiltration
* **Identification:** [What was stolen and how was it moved out?]
* **Technical Detail:** [e.g., "A .zip archive of the HR database was uploaded via POST request to a GitHub Gist."]
* **Visual Evidence:** ![Exfiltration Screenshot](./screenshots/exfil.png)

---

## 4. Extracted Indicators of Compromise (IOCs)
*Technical artifacts for the GRC Lead to use in the Risk Assessment.*

| Type | Value | Description / Context |
| :--- | :--- | :--- |
| **IP Address** | `0.0.0.0` | Command & Control (C2) Server |
| **Domain** | `malicious-site.com` | Hosting site for second-stage payload |
| **File Hash** | `SHA256: [Hash]` | Hash of the primary malware sample |
| **Registry Key**| `HKCU\...\Run` | Used for persistence |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)
*Mapping technical findings to the industry-standard framework.*

* **TA0001 - Initial Access:** [T1566.001 - Spearphishing Attachment]
* **TA0002 - Execution:** [T1059.001 - PowerShell]
* **TA0010 - Exfiltration:** [T1041 - Exfiltration Over C2 Channel]

---

## 6. Tools Utilized
*List the forensic toolkit used to solve this lab:*
* **Analysis:** CyberChef, Strings, Exiftool
* **Network:** Wireshark, Network Miner
* **Endpoint:** Event Viewer, Procmon, Volatility

---

## 7. Lab Completion Evidence
> [Insert your final "Challenge Complete" or "Flag" screenshot here to prove the lab is finished.]

![Lab Completion](./screenshots/lab_finish.png)

---
**Note:** *This technical data has been shared with the GRC Lead for Control Mapping and Risk Impact analysis.*
