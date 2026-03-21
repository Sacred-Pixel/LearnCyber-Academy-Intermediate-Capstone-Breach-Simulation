# 🛡️ SOC Technical Investigation: Phishing Analysis 2
**Lead Investigator:** Harvey R
**Academy:** LearnCyber Academy - Intermediate Capstone  

---

## 1. Executive Attack Summary
A targeted spear-phishing attack was identified, impersonating Amazon brand communications to harvest user credentials. The email, sent from `amazon@zyevantoby.cn`, utilized urgency-based social engineering ("Your Account has been locked") to pressure the recipient into clicking a malicious link. The attack was sophisticated enough to use Base64 encoding for the body content and leveraged a legitimate Squarespace CDN to host the brand's logo, increasing the appearance of legitimacy.

---

## 2. Incident Timeline (UTC)
| Timestamp | Event Description | Source Log / Evidence |
| :--- | :--- | :--- |
| **01:40:32** | **Email Sent:** Malicious email dispatched from attacker domain. | `Date: Wed, 14 Jul 2021` |
| **N/A** | **Initial Delivery:** Phishing email lands in `saintington73@outlook.com`. | `SMTP Headers / To: Field` |
| **N/A** | **Triaging:** Forensic analysis of email headers and body initiated. | `Sublime Text / Thunderbird` |

---

## 3. The Attack Chain Breakdown

### 🟢 Entry Point
* **Identification:** External Email originating from an unauthorized domain (`zyevantoby.cn`).
* **Technical Detail:** The attacker utilized a "Safelinks" protected URL to mask the final destination. The actual malicious endpoint was `amaozn.zzyuchengzhika.cn`.
* **Visual Evidence:** ![Entry Point Screenshot](./screenshots/phishing_headers.png)

### 🟡 Lateral Movement
* **Identification:** Credential Harvesting / Account Takeover.
* **Technical Detail:** The call-to-action button led to a spoofed Amazon login page. A successful click and login would provide the attacker with cleartext credentials, enabling them to bypass authentication and move laterally into any integrated Amazon services (AWS, Business accounts).
* **Visual Evidence:** ![Lateral Movement Screenshot](./screenshots/malicious_url_decode.png)

### 🔴 Data Exfiltration
* **Identification:** Tracking and Reconnaissance.
* **Technical Detail:** The presence of a `mailtoken` in the URL suggests that the attacker was tracking the specific victim. Additionally, a hidden Facebook profile link (`amir.boyka.7`) was found in the footer, likely a remnant of the phishing kit used to build the email.
* **Visual Evidence:** ![Exfiltration Screenshot](./screenshots/facebook_artifact.png)

---

## 4. Extracted Indicators of Compromise (IOCs)
*Technical artifacts identified during forensic analysis.*

| Type | Value | Description / Context |
| :--- | :--- | :--- |
| **Sender IP/Domain**| `amazon@zyevantoby.cn` | Spoofed sender address |
| **Malicious URL** | `amaozn.zzyuchengzhika.cn`| Typosquatted phishing landing page |
| **CDN URL** | `images.squarespace-cdn.com/...`| Used to pull legitimate Amazon logo |
| **Artifact** | `amir.boyka.7` | Facebook profile found in email code |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)
* **TA0001 - Initial Access:** T1566.002 (Phishing: Spearphishing Link)
* **TA0007 - Discovery:** T1589.002 (Gather Victim Identity Information: Email Addresses)
* **TA0005 - Defense Evasion:** T1132.001 (Data Encoding: Standard Encoding - Base64)

---

## 6. Tools Utilized
* **Forensics:** Sublime Text (Header analysis), Mozilla Thunderbird (Email client)
* **De-obfuscation:** CyberChef (Base64 decoding of the email body)
* **Reputation:** URL2PNG (Safe viewing of the landing page)

---

## 7. Lab Completion Evidence
> **Subject:** Your Account has been locked  
> **Body Encoding:** Base64  

![Lab Completion](./screenshots/lab_finish_phishing.png)

---
**Note:** *This technical data has been shared with the GRC Lead. High-risk finding: The use of Safelinks indicates the attack successfully traversed standard email filtering.*
