# Security Policy Recommendations

## 1. New Controls (Short-Term Remediation)
These controls are designed for immediate implementation to address the critical failures identified in the **Bruteforce** and **Shiba Insider** investigations.

*   **RDP & Remote Access Hardening Policy:**
    *   **Control:** All Remote Desktop Protocol (RDP) access must be removed from the public-facing internet (Port 3389).
    *   **Implementation:** Transition all remote access behind a Corporate VPN or a Remote Desktop Gateway that requires **Multi-Factor Authentication (MFA)**.
*   **Identity Management & Account Lockout Policy:**
    *   **Control:** Implement a standardized "3-strike" account lockout policy for all local and domain accounts.
    *   **Justification:** This directly mitigates automated password-guessing attacks, such as the 3,103 login attempts identified from IP 113.161.192.227.
*   **Mandatory Credential Scrubbing:**
    *   **Control:** Enforce an immediate, site-wide password reset for any account identified in cleartext authorization headers.
    *   **Specific Action:** Target the "redforever" password and any associated accounts discovered in the **Shiba Insider** forensic analysis.

## 2. Security Improvements (Long-Term Strategy)
These strategic improvements focus on enhancing the organization's detection capabilities against sophisticated evasion techniques like steganography.

*   **Endpoint Detection & Response (EDR) Deployment:**
    *   **Improvement:** Invest in an EDR solution capable of monitoring suspicious process trees and identifying abnormal file metadata.
    *   **Goal:** Detect "living-off-the-land" techniques (e.g., msdt.exe) and the tools used for data concealment.
*   **Insider Threat Program (ITP):**
    *   **Improvement:** Establish a behavioral baseline for "normal" user activity to flag unauthorized file archiving or unusual network traffic patterns.
    *   **Focus:** Monitor internal movement of ZIP archives and the use of forensic tools like `steghide` or `exiftool` on standard workstations.
*   **Network Visibility Enhancement:**
    *   **Improvement:** Implement **Deep Packet Inspection (DPI)** to inspect unencrypted HTTP headers and identify non-standard traffic patterns used for data exfiltration.

## 3. Training Needs
To address the human element exploited in the **Phishing Analysis** and **Shiba Insider** labs, the following training programs are required:

*   **Targeted Phishing Simulations:**
    *   **Need:** Deploy quarterly phishing simulations that specifically test for "URL Typosquatting" (e.g., `amaozn.zzyuchengzhika.cn`) and brand impersonation.
    *   **Focus:** Training users to verify sender domains and avoid high-pressure social engineering lures.
*   **Security awareness for Technical Staff:**
    *   **Need:** Specialized training for the SOC team on header analysis and de-obfuscation techniques.
    *   **Focus:** Ensuring faster triaging of Base64 encoded payloads and identification of "Safelinks" bypasses in future campaigns.

---

**Note:** *Implementation of these recommendations will transition the organization from a reactive security posture to a proactive defense-in-depth model.*
