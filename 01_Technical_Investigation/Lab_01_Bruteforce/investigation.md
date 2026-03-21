# 🛡️ SOC Technical Investigation: Bruteforce
**Lead Investigator:** Harvey R
**Academy:** LearnCyber Academy - Intermediate Capstone  

---

## 1. Executive Attack Summary
The organization's Windows environment was targeted by a high-intensity RDP (Remote Desktop Protocol) bruteforce attack originating from the external IP address 113.161.192.227. Over 3,100 Audit Failure events (Event ID 4625) were recorded as the threat actor attempted to compromise the local 'administrator' account. The attack utilized a wide range of source ports, suggesting an automated tool was used to cycle through login attempts.
---

## 2. Incident Timeline (UTC)
| Timestamp | Event Description | Source Log / Evidence |
| :--- | :--- | :--- |
| **07:22:00 AM** | Latest Recorded Failure: The last captured attempt in the log. | `Event ID 4625` |
| **Various** | High-Intensity Spraying: Thousands of attempts in rapid succession. | `Security Log` |
| **Ongoing** | Credential Access Attempt: Continuous NTLM authentication failures. | `NTLM / NtLmSsp`|

---

## 3. The Attack Chain Breakdown

### 🟢 Entry Point
* **Identification:** External-facing RDP (Remote Desktop Protocol) session request.
* **Technical Detail:** The attacker targeted the built-in local 'administrator' account using a Network Logon (Type 3).
* **Visual Evidence:** ![Entry Point Screenshot](./screenshots/entry_point.png)

### 🟡 Lateral Movement
* **Identification:** Potential account takeover.
* **Technical Detail:** The repeated use of NtLmSsp indicates an attempt to crack the local administrator password to gain an initial foothold. If successful, this would lead to administrative access over the network.
* **Visual Evidence:** ![Lateral Movement Screenshot](./screenshots/lateral.png)

### 🔴 Data Exfiltration
* **Identification:** Post-compromise objective
* **Technical Detail:** While the logs provided focus on the authentication failures, the ultimate goal of such an attack is typically data theft or ransomware deployment following a successful administrative login.
* **Visual Evidence:** ![Exfiltration Screenshot](./screenshots/exfil.png)

---

## 4. Extracted Indicators of Compromise (IOCs)

| Type | Value | Description / Context |
| :--- | :--- | :--- |
| **IP Address** | `113.161.192.227` | Command & Control / Attacker Source |
| **Account Name** | `administrator` | Targeted local administrative account |
| **Event ID** | `4625` | Windows Audit Failure (Logon) |
| **Logon Type**| `3` | Network Logon attempt |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)

* **TA0006 - Credential Access:** [T1110.001 - Brute Force: Password Guessing]
* **TA0001 - Initial Access:** [T1133 - External Remote Services]

---

## 6. Tools Utilized

* **Analysis:** Microsoft Excel (CSV analysis), Notepad++
* **Network:** Wireshark, IP Geolocation
* **Endpoint:** Windows Event Viewer (EVTX analysis)

---

## 7. Lab Completion Evidence

![Lab Completion](./screenshots/lab_finish.png)

---
**Note:** *This technical data has been shared with the GRC Lead for Control Mapping and Risk Impact analysis.*
