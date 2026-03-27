# Control Mapping Analysis (NIST CSF)

## 1. Overview
The purpose of this document is to map the specific control failures identified in the **Enterprise Breach Simulation** to the **NIST Cybersecurity Framework (CSF)**. This ensures the organization can align its remediation efforts with industry-standard security functions: **Identify, Protect, Detect, Respond, and Recover**.

## 2. Consolidated Mapping Table
The following table summarizes the failures identified across the three investigative labs (Bruteforce, Phishing, and Shiba Insider) and their corresponding NIST CSF subcategories.

| Incident Source | Identified Control Failure | NIST CSF Subcategory | Subcategory Description |
| :--- | :--- | :--- | :--- |
| **Bruteforce** | Publicly exposed RDP (Port 3389) | **PR.AC-4** | Access permissions and authorizations are managed, incorporating the principles of least privilege and separation of duties. |
| **Bruteforce** | Absence of account lockout policies | **PR.AC-7** | Users, devices, and other assets are authenticated commensurate with the risk of the transaction (e.g., MFA, lockout). |
| **Phishing** | Insufficient user awareness training | **PR.AT-1** | All users are informed and trained on their roles and responsibilities regarding cybersecurity. |
| **Phishing** | Reliance on single-layer email scanning (Safelinks bypass) | **PR.DS-2** | Data-in-transit is protected (e.g., inadequate multi-layered email filtering). |
| **Shiba Insider** | Transmission of cleartext credentials | **PR.DS-2** | Data-in-transit is protected (e.g., failure to use encryption for authorization headers). |
| **Shiba Insider** | Lack of Deep Packet Inspection (DPI) for steganography | **DE.AE-3** | Event data is collected and correlated from multiple sources and sensors to identify unauthorized activity. |
| **Shiba Insider** | Insufficient logging of internal unauthorized access | **PR.PT-1** | Audit/log records are determined, documented, implemented, and reviewed. |

---

## 3. Detailed Framework Alignment

### 3.1 Protective Technology (PR.PT) & Access Control (PR.AC)
The **Bruteforce** attack succeeded in making 3,103 attempts against the 'administrator' account because the perimeter lacked basic defensive thresholds.
*   **Control Gap:** The organization failed to implement **PR.AC-7**, as the system allowed continuous authentication attempts without triggering a lockout or requiring a second factor (MFA).
*   **Control Gap:** Exposure of RDP to the public internet violates **PR.AC-4**, as administrative access should be restricted to internal or VPN-protected segments.

### 3.2 Awareness and Training (PR.AT)
The **Phishing Analysis** revealed that technical controls (Safelinks) can be bypassed by sophisticated attackers using typosquatted domains.
*   **Control Gap:** This highlights a failure in **PR.AT-1**. When technical filters fail, the "human firewall" is the last line of defense. The success of the "Account Locked" lure indicates users require better training to spot typosquatted URLs and sender address anomalies.

### 3.3 Data Security (PR.DS) & Detection Processes (DE.AE)
The **Shiba Insider** investigation showed that internal users can bypass Data Loss Prevention (DLP) by hiding data in image metadata (steganography).
*   **Control Gap:** The transmission of the "redforever" password in an unencrypted authorization header is a direct failure of **PR.DS-2**, which requires protecting data-in-transit.
*   **Control Gap:** The inability to detect the exfiltration of the unique identifier (ID: 0726ba87...) demonstrates a gap in **DE.AE-3**. The organization lacks the advanced sensors, such as Deep Packet Inspection (DPI), needed to flag non-standard traffic patterns like hidden data in media files.

---

**Note:** *This mapping informs the **Policy Drafts** and **Risk Assessment** documents by identifying the specific regulatory and framework requirements currently being neglected.*
