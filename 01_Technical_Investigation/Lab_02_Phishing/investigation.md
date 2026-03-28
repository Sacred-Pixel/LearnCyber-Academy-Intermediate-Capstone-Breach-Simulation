# 🛡️ SOC Technical Investigation: Phishing Analysis 2
**Lead Investigator:** Harvey R  
**Academy:** LearnCyber Academy - Intermediate Capstone

---

## 1. Executive Attack Summary
On 13 July 2021, a sophisticated spear-phishing campaign was identified targeting the user `saintington73@outlook.com`. The attacker impersonated **Amazon Brand Communications**, using urgency-based social engineering ("Your Account has been locked") to pressure the recipient into clicking a malicious link. The attack utilized **Base64 encoding** for the email body to evade signature-based security filters and leveraged a legitimate Squarespace CDN to host the brand's logo, increasing the appearance of legitimacy. While the email successfully reached the recipient's inbox, no confirmed evidence was found that the user submitted credentials to the landing page.

---

## 2. Detailed Incident Timeline (UTC)
The following timeline tracks the email's progression from the attacker's infrastructure through Microsoft’s security layers to the endpoint.

| Time (13 Jul 2021) | Event Description | Technical Evidence |
| :--- | :--- | :--- |
| **19:14:57** | **Initial Delivery:** Email sent from attacker MTA. | `mta0.zyevantoby.cn` (45.156.23.138) |
| **19:14:57** | **Security Bypass:** Email passed through MS Protection server. | `BN1NAM02FT027.mail.protection.outlook.com` |
| **19:14:58** | **Regional Transit:** Email processed by European Exchange server. | `AM7PR06MB6609.eurprd06.prod.outlook.com` |
| **19:14:58** | **Inbox Delivery:** Email delivered to recipient mailbox. | `AM6PR06MB5954.eurprd06.prod.outlook.com` |
| **14 Jul 2021** | **Forensic Triage:** Manual analysis of headers and body initiated. | Sublime Text / Thunderbird |

---

## 3. The Cyber Kill Chain Breakdown
This model tracks the attacker’s progression from reconnaissance to the potential installation of malicious payloads.

| Stage | Observation | Technical Detail |
| :--- | :--- | :--- |
| **1. Reconnaissance** | Targeted Spear-Phishing | Phishing email sent to specific target: `saintington73@outlook.com`. |
| **2. Weaponisation** | Malicious URL Embedding | A typosquatted URL was embedded in a 'Review Account' button. |
| **3. Delivery** | O365 Filter Bypass | Use of Safelinks and Base64 encoding allowed the email to reach the inbox. |
| **4. Exploitation** | Link Redirection | User interaction triggers navigation to the malicious endpoint: `amaozn.zzyuchengzhika.cn`. |
| **5. Installation** | Credential Harvesting | The landing page was designed to capture cleartext Amazon login details. |

---

## 4. Extracted Indicators of Compromise (IOCs)
These technical artifacts were identified during forensic analysis and added to the enterprise blocklist.

| Type | Value | Significance / Context |
| :--- | :--- | :--- |
| **Sender Address** | `amazon@zyevantoby.cn` | Spoofed Amazon sender address (Typosquatted domain). |
| **Source IP** | 45.156.23.138 | Attacker-controlled MTA IP address. |
| **Malicious URL** | `amaozn.zzyuchengzhika.cn` | Typosquatted landing page designed for credential theft. |
| **Sender Domain** | `zyevantoby.cn` | Malicious attacker-controlled domain. |
| **Tracking Token** | `mailtoken=saintington73...` | Used by the attacker to track individual victim interaction. |
| **Code Artifact** | `amir.boyka.7` | Facebook profile found in the phishing kit footer. |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)
*   **TA0001 - Initial Access:** [T1566.002 - Phishing: Spearphishing Link]
*   **TA0007 - Discovery:** [T1589.002 - Gather Victim Identity Information: Email Addresses]
*   **TA0005 - Defense Evasion:** [T1132.001 - Data Encoding: Standard Encoding - Base64]
*   **TA0001 - Initial Access:** [T1566 - Phishing: Brand Impersonation]

---

## 6. Tools Utilized
The following forensic suite was used to analyze the malicious artifacts.

*   **Email Forensics:** **Mozilla Thunderbird** (Triage) and **Sublime Text** (Header/Path Analysis).
*   **De-obfuscation:** **CyberChef** (Decoding Base64 body content).
*   **Reputation Analysis:** **URL2PNG** (Safe rendering of the typosquatted landing page).

---

## 7. Key Findings & Weakness Summary
*   **Findings:** The attack was highly effective due to its use of **Safelinks-protected URLs** to mask the final malicious destination. The inclusion of legitimate Squarespace CDN assets significantly lowered the "suspicion threshold" for the end-user.
*   **Key Weakness:** The organization's email perimeter relied on a **single layer of automated link scanning**, which was successfully bypassed. Furthermore, a lack of **User Awareness Training** on typosquatted domains made the recipient vulnerable to urgent social engineering tactics.

---
