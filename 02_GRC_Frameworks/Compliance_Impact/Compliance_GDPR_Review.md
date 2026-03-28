# ⚖️ GRC Compliance Impact: GDPR Review
**Lead Investigator:** Student B (GRC Lead)

## 1. Executive Summary
The organization has a legal obligation under **GDPR** to assess every security incident for risks to the rights and freedoms of individuals. Following a forensic review of the three incidents, one has been classified as a **Reportable Breach**, while two have been classified as **Documented Near-Misses**.

---

## 2. Incident Breakdown & Data Exposure

### **Incident 01: Shiba Insider**
*   **Was Sensitive Data Exposed?** **Yes.** A unique identifier (**ID: 0726ba878ea47de571777a**) was successfully exfiltrated via steganography. This ID is linked to a specific user profile (**bluetiger**), making it "identifiable personal data" under **GDPR Article 4(1)**.
*   **Is this a Reportable Breach?** **Yes.** Because the breach was premeditated and resulted in the actual exfiltration of a unique identifier, it poses a risk to the individual.
*   **Action Required:** Notification to the supervisory authority (e.g., the ICO) is mandatory within **72 hours** under **Article 33**.

### **Incident 02: RDP Bruteforce**
*   **Was Sensitive Data Exposed?** **No.** Forensic logs (Event ID 4625) confirm all 3,103 attempts failed. No successful logons (Event ID 4624) from the attacker's IP were recorded.
*   **Is this a Reportable Breach?** **No.** There was no unauthorized access to personal data.
*   **Action Required:** This must be documented internally as a **"Near-Miss"** under **Article 33(5)**, detailing the facts, the impact, and the remedial actions taken (e.g., closing the RDP port).

### **Incident 03: Phishing Analysis 2**
*   **Was Sensitive Data Exposed?** **No.** While the email reached the inbox, there is no confirmed forensic evidence that the user clicked the link or submitted credentials to the harvested landing page.
*   **Is this a Reportable Breach?** **No.**
*   **Action Required:** Must be documented internally under **Article 33(5)**.

---

## 3. Regulatory Violations (GDPR Article 32)
Beyond the notification of breaches, the organization is currently in a state of **non-compliance** regarding **Article 32 (Security of Processing)**. This article requires controllers to implement "appropriate technical and organizational measures" to ensure a level of security appropriate to the risk.

**Identified Failures in Technical Measures:**
*   **Lack of MFA:** Reliance on single-factor authentication across all vectors.
*   **No Access Control Limits:** Absence of an account lockout policy allowed a high-volume brute force to continue uninterrupted.
*   **Insecure Internal Transit:** Transmission of credentials in cleartext over unencrypted HTTP for the Shiba Insider incident.

---

## 4. Required Compliance Actions
| Priority | Action Item | GDPR Context |
| :--- | :--- | :--- |
| **Urgent** | Notify Supervisory Authority of the Shiba Insider breach. | Article 33 (72-hour window) |
| **Urgent** | Document all three incidents in the internal Breach Register. | Article 33(5) |
| **Immediate**| Engage the Data Protection Officer (DPO) for a full **DPIA**. | Article 35 (Data Protection Impact Assessment) |
| **Short-Term**| Implement MFA and Account Lockouts to remediate technical gaps. | Article 32 (Security of Processing) |

---

**Conclusion:** Failure to report the Shiba Insider incident within the 72-hour window or failing to document the "near-misses" could result in significant administrative fines under **Article 83**, reaching up to 4% of annual global turnover.
