# 🛡️ GRC Control Mapping: Enterprise Breach Simulation
**Lead Investigator:** Student B (GRC Lead)

## 1. Incident 01: Shiba Insider (Internal Threat)
The following mapping addresses the failure to detect unauthorized internal data exfiltration.

| Failure Identified | NIST CSF Mapping | ISO 27001 Mapping | Mitigation Required |
| :--- | :--- | :--- | :--- |
| **No outbound DLP** | **PR.DS** (Data Security) | **A.13.2** (Information Transfer) | Deploy **Data Loss Prevention (DLP)** to inspect outbound HTTP traffic. |
| **Sensitive Data Exposure** | **ID.AM** (Asset Management) | **A.8.2** (Information Classification) | Implement **Data Classification** for sensitive user identifiers. |
| **Lack of Internal Monitoring** | **DE.AE** (Anomalies and Events) | **A.12.4** (Logging and Monitoring) | Deploy **Network Traffic Analysis (NTA)** to detect anomalous internal HTTP patterns. |

---

## 2. Incident 02: RDP Bruteforce (External Threat)
These controls address the critical vulnerabilities identified in the organization's administrative perimeter.

| Failure Identified | NIST CSF Mapping | ISO 27001 Mapping | Mitigation Required |
| :--- | :--- | :--- | :--- |
| **Exposed RDP Port** | **PR.AC** (Access Control) | **A.13.1** (Network Controls) | Close **Port 3389** and restrict RDP access to **VPN-only**. |
| **No Account Lockout** | **PR.AC** (Identity Management) | **A.9.4** (Access Control) | Enforce **Account Lockout Policies** (e.g., 5–10 attempts) via Group Policy. |
| **No MFA on Remote Access** | **PR.DS** (Data Security) | **A.9.4** (Access Control) | Implement **Multi-Factor Authentication (MFA)** for all remote sessions. |
| **Inadequate SIEM Alerting**| **DE.AE** (Anomalies and Events)| **A.12.4** (Logging and Monitoring)| Configure **SIEM threshold alerts** for high-volume failed logons. |

---

## 3. Incident 03: Phishing Analysis 2 (Social Engineering)
The following controls are required to prevent successful brand impersonation and credential harvesting.

| Failure Identified | NIST CSF Mapping | ISO 27001 Mapping | Mitigation Required |
| :--- | :--- | :--- | :--- |
| **Insufficient Email Filters** | **DE.AE** (Anomalies and Events) | **A.13.2** (Information Transfer) | Implement **advanced phishing filters** and anti-spoofing (DMARC/DKIM/SPF). |
| **No URL Scanning** | **PR.PT** (Protective Tech) | **8.7** (Malware Protection) | Deploy **Safe Links** and URL detonation to scan links at the time of click. |
| **Lack of Awareness Training** | **PR.AT** (Awareness & Training) | **A.7.2.2** (Security Training) | Deliver mandatory **Security Awareness Training** and quarterly phishing simulations. |

---

## 4. Remediation Priority Summary
The organization must prioritize **Immediate (0–7 days)** fixes for failures mapped to **PR.AC** (Access Control) and **A.9.4**, specifically the closure of exposed RDP ports and the implementation of account lockout policies. Longer-term strategic goals include the development of formal **Incident Response Plans (IRPs)** for each mapped threat vector.
