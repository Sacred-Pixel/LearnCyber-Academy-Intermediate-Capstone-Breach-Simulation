# 🛡️ SOC Technical Investigation: Shiba Insider
**Lead Investigator:** Harvey R  
**Academy:** LearnCyber Academy - Intermediate Capstone

---

## 1. Executive Attack Summary
This investigation uncovered a deliberate and premeditated **insider threat** involving the unauthorized exfiltration of sensitive data. By analyzing a captured PCAP file, forensic investigators identified a multi-layer concealment chain used to evade standard detection. The attacker utilized an unencrypted HTTP authorization header to transmit a ZIP password (**redforever**) and employed **image steganography** to hide a unique identifier within a JPEG file. The insider was positively identified as BTLO user **bluetiger** (User ID: 0726ba878ea47de571777a).

---

## 2. Incident Timeline (UTC)
The following timeline establishes the sequence of forensic discovery and the attacker's actions.

| Timeframe | Event Description | Source Log / Evidence |
| :--- | :--- | :--- |
| **Detection** | **Initial Flag:** Suspicious internal HTTP traffic identified. | Wireshark / PCAP Analysis |
| **Forensics** | **Traffic Capture:** Client (192.168.176.1) requests file access. | Wireshark / Frame 4 |
| **Forensics** | **Data Leak:** Server responds with "use your own password" hint. | Wireshark / Frame 6 |
| **Forensics** | **Credential Recovery:** Extraction of "redforever" from headers. | Authorization: Basic (Base64) |
| **Analysis** | **Archive Access:** Password successfully used to unlock `file.zip`. | ZIP Encryption |
| **Extraction** | **Artifact Recovery:** Steganographic ID successfully recovered. | Steghide / ID: 0726ba87... |

---

## 3. The Attack Chain Breakdown
The attacker followed a 5-stage attack flow designed to bypass standard Data Loss Prevention (DLP) filters.

| # | Stage | Insider Action | Technical Evidence |
| :--- | :--- | :--- | :--- |
| 1 | **Covert Communication** | Sent HTTP GET request to an internal Python server. | Wireshark Packet 4 (Host: 192.168.176.145) |
| 2 | **Credential Embedding** | ZIP password encoded in the HTTP Authorization header. | Authorization: Basic (Base64: fakeblue:redforever) |
| 3 | **Data Packaging** | Sensitive JPEG stored in a password-protected ZIP archive. | `file.zip` / Password: redforever |
| 4 | **Metadata Manipulation** | XMP fields written into JPEG to declare the tool used. | ExifTool 11.88 / XMP:Technique: Steganography |
| 5 | **Data Exfiltration** | BTLO user ID hidden inside the pixel data of `ssdog1.jpeg`. | Steghide / Hidden ID: 0726ba878ea47de571777a |

### 🟢 Entry Point (Visual Evidence)
> *[Insert Screenshot of Wireshark Frame 4 showing the Base64 Authorization header]*

### 🟡 Lateral Movement (Visual Evidence)
> *[Insert Screenshot of unlocked ZIP contents and ExifTool metadata results]*

### 🔴 Data Exfiltration (Visual Evidence)
> *[Insert Screenshot of Steghide successfully extracting the hidden User ID]*

---

## 4. Extracted Indicators of Compromise (IOCs)
These artifacts have been shared with the GRC Lead for inclusion in the enterprise blocklist.

| Type | Value | Significance |
| :--- | :--- | :--- |
| **Source IP** | 192.168.176.1 | Machine used by the insider to initiate communication. |
| **Dest IP/Port** | 192.168.176.145:8099 | Internal Python server used for covert file hosting. |
| **Credential** | redforever | Password recovered from unencrypted HTTP headers. |
| **Unique ID** | 0726ba878ea47de571777a | Secret identifier exfiltrated from the network. |
| **Username** | bluetiger | Identified Insider Threat actor. |
| **Carrier File** | `ssdog1.jpeg` (82 KB) | Steganographic vessel used to conceal the payload. |

---

## 5. Attack Techniques (MITRE ATT&CK Mapping)
The attacker's behavior aligns with the following industry-standard techniques.

*   **TA0001 - Initial Access:** [T1078.003 - Valid Accounts: Local Accounts]
*   **TA0005 - Defense Evasion:** [T1132.001 - Standard Encoding: Base64]
*   **TA0005 - Defense Evasion:** [T1027.003 - Steganography]
*   **TA0009 - Collection:** [T1005 - Data from Local System]

---

## 6. Tools Utilized
The forensic investigation was completed using the following suite.

*   **Network Forensics:** **Wireshark** (Protocol analysis and Base64 header extraction).
*   **Metadata Analysis:** **ExifTool** (Identification of deliberate XMP metadata manipulation).
*   **Data Recovery:** **Steghide** (Extraction of hidden ASCII payload from the carrier image).
*   **OSINT/Attribution:** **BTLO Platform** (Profile lookup to confirm user identity).

---

## 7. Key Findings & Weakness Summary
*   **Findings:** The investigation confirmed that the insider (**bluetiger**) intentionally used unencrypted internal channels to transmit credentials and bypass security sensors.
*   **Key Weakness:** The organization lacks **Deep Packet Inspection (DPI)** to detect encoded credentials in internal traffic and has no automated controls to flag the use of steganography tools on standard workstations.

---

**Note:** *This technical data has been shared with the GRC Lead.*
