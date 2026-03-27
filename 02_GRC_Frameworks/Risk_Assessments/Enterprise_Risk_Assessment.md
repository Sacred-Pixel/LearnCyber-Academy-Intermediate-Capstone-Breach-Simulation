# Enterprise Risk Assessment

## 1. Affected Assets
The following organizational assets were either targeted, compromised, or placed at significant risk during the investigative period:

*   **Identity & Access Assets:** 
    *   **Local Administrative Account:** Targeted by over 3,100 automated login attempts via RDP.
    *   **User Credentials:** Specifically `saintington73@outlook.com` and integrated cloud service accounts (AWS/Business) targeted via phishing.
    *   **Insider Account:** The `bluetiger` local account used for unauthorized data movement.
*   **Data & Intellectual Property:**
    *   **Internal ZIP Archives:** Secured with weak, cleartext credentials ("redforever").
    *   **Sensitive Identifiers:** A unique ID (0726ba878ea47de571777a) exfiltrated via steganography.
*   **Infrastructure:**
    *   **RDP Service:** Exposed publicly on Port 3389, serving as a primary entry point for external threats.
    *   **Email Security Gateway:** Bypassed by sophisticated typosquatted domains despite Safelinks protection.

## 2. Business Impact Analysis
| Incident | Primary Risk | Potential Business Consequence |
| :--- | :--- | :--- |
| **RDP Bruteforce** | Account Takeover (ATO) | A successful breach of the administrator account could lead to full system compromise, lateral movement across the network, and the deployment of **ransomware**. |
| **Phishing Campaign** | Credential Theft | Successful harvesting of credentials allows attackers to impersonate legitimate users, accessing sensitive business communications and **integrated cloud environments**. |
| **Insider Threat** | Data Exfiltration | The use of steganography allows for the removal of intellectual property without triggering standard **Data Loss Prevention (DLP)** alerts, leading to long-term undetected data loss. |

## 3. Likelihood vs. Impact Assessment
Following the analysis of the threat landscape, the incidents are categorized as follows:

### **Phishing Campaign:** **High Likelihood / High Impact**
*  This is the most critical risk. The likelihood is high because the attack successfully bypassed automated technical filters (Safelinks). The impact is high due to the direct path to harvesting high-value administrative or business credentials.

### **Insider Threat:** **Moderate Likelihood / High Impact**
*  While the frequency of insider incidents may be lower than automated external attacks, the impact is extreme. The `bluetiger` incident demonstrated that internal users with valid accounts can exfiltrate data using methods currently undetectable by organizational sensors (e.g., steganography).

### **RDP Bruteforce:** **High Likelihood / Medium Impact**
*  The likelihood of this attack recurring is very high as long as Port 3389 remains publicly exposed. However, the impact is currently rated as "Medium" because the attacks were largely unsuccessful and the affected systems remained isolated from the core production environment.

---

**Note:** *This risk assessment serves as the foundation for the **Control Mapping** and **Strategic Recommendations** provided in the final Executive Incident Summary Report.*
