# 🛡️ Security Policy Recommendations: Strategic Remediation Roadmap
**Lead Investigator:** Student B (GRC Lead)

## 1. New Technical Controls
These controls address the immediate "protective" gaps identified in the organization’s perimeter and internal data handling policies.

*   **Identity and Access Management (MFA):** Enforce **Multi-Factor Authentication (MFA)** for all remote access, administrative accounts, and standard user logins to mitigate the risk of credential theft and brute force success.
*   **Account Lockout Policy:** Implement a "3-strike" or "5–10 strike" **Account Lockout Policy** via Group Policy to prevent high-volume automated password-guessing attacks from proceeding uninterrupted.
*   **Administrative Hardening:** Close **RDP Port 3389** to the public internet and restrict access to a VPN or an IP allowlist. Additionally, rename or disable default accounts like "administrator" to reduce the attack surface.
*   **Data Loss Prevention (DLP):** Deploy a **DLP solution** capable of inspecting outbound HTTP traffic for encoded credentials (Base64) or sensitive identifiers to prevent internal exfiltration.
*   **Advanced Email Filtering:** Implement **DMARC, DKIM, and SPF** to prevent brand impersonation, and deploy **Safe Links/URL detonation** to scan malicious links at the time of click.

## 2. Security Process Improvements
These enhancements focus on the organization's ability to "Detect" and "Respond" to future threats more effectively.

*   **SIEM Threshold Alerting:** Configure the **SIEM** to trigger real-time alerts on high-volume authentication failures (e.g., more than 10 **Event ID 4625** failures within 5 minutes).
*   **Network Traffic Analysis (NTA):** Deploy tools like Zeek or Suricata to monitor for anomalous internal HTTP patterns and the use of non-standard ports.
*   **Credential Scrubbing:** Initiate a site-wide password reset for any accounts identified in cleartext logs (such as the "redforever" password exposed in the Shiba Insider incident).
*   **Vulnerability Management:** Establish a robust patch management process and conduct regular technical security reviews of all internet-facing systems.

## 3. Training and Awareness Needs
These recommendations address the human element of the security posture, focusing on social engineering and internal misuse.

*   **Targeted Phishing Simulations:** Conduct quarterly simulations focusing on **URL typosquatting** and brand impersonation (e.g., Amazon/O365) to train users to identify fake sender domains.
*   **Insider Threat Awareness:** Deliver specialized training on the risks of insider threats, reporting duties for suspicious employee behavior, and secure data handling practices.
*   **Incident Response Tabletops:** Run tabletop exercises for IT and SOC staff to validate **Incident Response Plans (IRPs)** for brute force, phishing, and insider threat scenarios.

## 4. Implementation Timeline

| Phase | Duration | Key Objectives |
| :--- | :--- | :--- |
| **Immediate** | **0–7 Days** | Close RDP Port 3389; implement Account Lockouts; engage DPO for GDPR Article 33 notifications. |
| **Short-term** | **0–30 Days** | Enforce MFA globally; deploy SIEM alerting for failed logons; implement email anti-spoofing (DMARC/SPF). |
| **Medium-term** | **30–90 Days** | Develop and test formal IRPs; deploy steganography detection at the gateway; deliver staff security awareness training. |

***

**Conclusion:** By transitioning from a reactive posture to this layered defense-in-depth model, the organization can significantly reduce its risk exposure and ensure compliance with **GDPR Article 32** requirements.
