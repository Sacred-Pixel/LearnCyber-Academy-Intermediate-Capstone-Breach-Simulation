# 🛡️ GRC Risk Assessment: Enterprise Breach Simulation
**Lead Investigator:** Student B (GRC Lead)

## 1. Incident 01: Shiba Insider (Insider Threat)
A premeditated internal exfiltration event where a trusted user used steganography to conceal sensitive data.

| Category | Assessment Details |
| :--- | :--- |
| **Affected Assets** | User identifier (ID: 0726ba87...), insider credentials (fakeblue:redforever), internal infrastructure (Python HTTP server), and carrier files (ssdog1.jpeg). |
| **Business Impact** | **Critical:** Exfiltration of personal data constitutes a major GDPR risk; loss of intellectual property and internal trust; premeditated nature indicates high intent to evade controls. |
| **Likelihood vs. Impact** | **Likelihood:** Medium (requires trusted access) / **Impact:** High (data exfiltration). |
| **Overall Risk Level** | **CRITICAL**. |

---

## 2. Incident 02: RDP Bruteforce (External Threat)
An automated high-volume authentication attack originating from a Vietnamese IP address targeting the administrative perimeter.

| Category | Assessment Details |
| :--- | :--- |
| **Affected Assets** | Public-facing Windows systems (RDP-exposed), the local 'administrator' account, and system security event logs. |
| **Business Impact** | **Critical:** Potential for full administrative takeover leading to ransomware deployment or use of the system as a network pivot; high log volume may impact storage/monitoring. |
| **Likelihood vs. Impact** | **Likelihood:** Very High (automated scanning, no lockout) / **Impact:** Very High (admin access). |
| **Overall Risk Level** | **CRITICAL**. |

---

## 3. Incident 03: Phishing Analysis 2 (Social Engineering)
A brand impersonation campaign designed to harvest user credentials through urgency and typosquatted domains.

| Category | Assessment Details |
| :--- | :--- |
| **Affected Assets** | User email accounts, user credentials, email security gateways (Office 365), and internal network integrity. |
| **Business Impact** | **High:** Successful inbox delivery represents a failure of the security perimeter; risk of financial fraud and unauthorized authenticated access to business integrated services. |
| **Likelihood vs. Impact** | **Likelihood:** High (bypassed filters, social engineering) / **Impact:** High (account compromise). |
| **Overall Risk Level** | **HIGH**. |

---

## 4. Summary of Overall Risk Posture
The organization currently faces a **Critical** risk posture due to systemic failures across all three vectors.
*   **Identity Management:** The total absence of **Multi-Factor Authentication (MFA)** and **Account Lockout Policies** leaves the organization vulnerable to both automated external and manual internal attacks.
*   **Monitoring Gaps:** The lack of real-time **SIEM alerting** and **Deep Packet Inspection (DPI)** meant that these incidents were only discovered through manual forensic review after the attacks reached completion.
*   **Perimeter Vulnerabilities:** Directly exposing management protocols (RDP) to the internet without VPN or IP filtering presents a high-likelihood entry point for threat actors.
