# 🛡️ SOC Technical Investigation: Shiba Insider
**Lead Investigator:** Harvey R 
**Academy:** LearnCyber Academy - Intermediate Capstone  

---

## 1. Executive Attack Summary
This investigation uncovered an insider threat involving the unauthorized exfiltration and concealment of data. By analyzing a captured PCAP file, an unencrypted authorization header was discovered containing credentials (`redforever`) used to secure a ZIP archive. Further forensic analysis of the extracted media revealed the use of steganography to hide a unique identifier (ID) and a profile link to the internal threat actor, known as `bluetiger`.

---

## 2. Incident Timeline (UTC)
| Timestamp | Event Description | Source Log / Evidence |
| :--- | :--- | :--- |
| **N/A** | **Traffic Capture:** Client requests "how do I open file". | `Wireshark / Frame 4` |
| **N/A** | **Data Leak:** Server responds with "use your own password". | `Wireshark / Frame 6` |
| **N/A** | **Credential Recovery:** Extraction of "redforever" from headers. | `Authorization: Basic` |
| **N/A** | **Artifact Extraction:** Steganographic ID successfully recovered. | `Steghide / ID: 0726ba87...` |

---

## 3. The Attack Chain Breakdown

### 🟢 Entry Point
* **Identification:** Network Traffic Analysis (PCAP).
* **Technical Detail:** The initial "foothold" was identified via an HTTP GET request. The attacker's credentials were sent in cleartext within the `Authorization` header, formatted as a Base64 encoded string.
* **Visual Evidence:** ![Entry Point Screenshot](./screenshots/wireshark_credentials.png)

### 🟡 Lateral Movement
* **Identification:** Insider Access / Privilege Escalation.
* **Technical Detail:** The attacker (bluetiger) utilized legitimate credentials to access a restricted ZIP file. Within the archive, the attacker attempted to evade detection by hiding data within the metadata and pixel data of an image file (Shiba Dog image).
* **Visual Evidence:** ![Lateral Movement Screenshot](./screenshots/steganography_technique.png)

### 🔴 Data Exfiltration
* **Identification:** Steganographic Data Concealment.
* **Technical Detail:** The attacker embedded a specific unique ID (`0726ba878ea47de571777a`) inside a JPEG file using steganography. This technique was used to pass sensitive identifiers out of the network without triggering standard DLP (Data Loss Prevention) keyword filters.
* **Visual Evidence:** ![Exfiltration Screenshot](./screenshots/steghide_output.png)

---

## 4. Extracted Indicators of Compromise (IOCs)
*Technical artifacts recovered for the GRC Lead's Insider Threat report.*

| Type | Value | Description / Context |
| :--- | :--- | :--- |
| **Credential** | `redforever` | Password used to secure unauthorized ZIP |
| **Unique ID** | `0726ba878ea47de571777a` | Recovered secret identifier |
| **Username** | `bluetiger` | Identified Insider Threat actor |
| **Technique** | `Steganography` | Method used to conceal exfiltrated data |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)
* **TA0001 - Initial Access:** [T1078.003 - Valid Accounts: Local Accounts]
* **TA0009 - Collection:** [T1005 - Data from Local System]
* **TA0005 - Defense Evasion:** [T1027.003 - Steganography]

---

## 6. Tools Utilized
* **Network Forensics:** Wireshark (Protocol analysis and header extraction)
* **Metadata Analysis:** Exiftool (Discovery of hidden steganography tags)
* **Data Recovery:** Steghide (Extraction of hidden text from image files)

---

## 7. Lab Completion Evidence
> **Insider Identified:** bluetiger  
> **Extracted ID:** 0726ba878ea47de571777a

![Lab Completion](./screenshots/lab_finish_shiba.png)

---
**Note:** *This technical data has been shared with the GRC Lead. Focus on "Insider Threat" policies and "Cleartext Credential" transmission risks in the final Executive Report.*
