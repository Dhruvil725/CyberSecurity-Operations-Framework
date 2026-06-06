# IoC Output Register (Threat Intelligence Extraction)

---

# 1. Document Control

| Field          | Value                                                                    |
| -------------- | ------------------------------------------------------------------------ |
| Document Name  | Register – IoC Output Register                                           |
| Document ID    | TI-IOC-001                                                               |
| Version        | 1.0                                                                      |
| Effective Date | 30-May-2026                                                              |
| Owner          | Threat Intel Lead / SOC Manager                                          |
| Approved By    | CISO                                                                     |
| Classification | Internal – Confidential (sanitized version may be TLP:WHITE/GREEN/AMBER) |
| Review Cycle   | Monthly                                                                  |

---

# 2. Purpose

This document provides the standardized **IoC (Indicators of Compromise) Output Register** to capture, document, and operationalize all IoCs extracted from incidents, threat hunts, threat intel, and security research conducted by the SOC/IR team.

A formal IoC output register is critical because:

- IoCs extracted from incidents are valuable intelligence assets
- timely operationalization (TI feed integration, detection rules) reduces future incident impact
- NIST CSF Identify (ID.RA) and Detect (DE.CM) functions require IoC management
- ISO 27001 Annex A.5.7 requires threat intelligence as a control
- RBI Cyber Security Framework expects threat intelligence capability
- IoC sharing (CERT-In, ISACs, industry peers) supports collective defense
- audit trail required for IoC lifecycle (extraction, validation, deployment, expiry)
- MSSP operations require tenant-scoped IoC management with cross-tenant intelligence
- IoCs have time-bound validity and must be managed through expiry
- TLP (Traffic Light Protocol) classification governs sharing scope

This register ensures:

- consistent extraction and documentation of IoCs across the SOC/IR team
- TLP-based classification and sharing controls
- traceability from incident/source to IoC
- operationalization across SIEM, EDR, firewall, email, and TI platforms
- lifecycle management (validity, expiry, retirement)
- audit-ready evidence of TI generation and sharing
- linkage to incidents, RCA, threat hunts, and detection improvements

Reference alignment:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

---

# 3. Scope

This register tracks IoCs extracted from:

| Source                 | Examples                                                                 |
| ---------------------- | ------------------------------------------------------------------------ |
| Incident Response      | IoCs from confirmed incidents (malware hashes, C2 IPs, phishing domains) |
| Threat Hunting         | IoCs discovered through hypothesis-based hunting                         |
| Malware Analysis       | Static/dynamic analysis output                                           |
| Forensic Investigation | Disk/memory artifacts                                                    |
| Phishing Analysis      | URLs, sender addresses, attachment hashes                                |
| Threat Intel Research  | Internal research on threat actors/campaigns                             |
| Honeypot/Deception     | Activity from deception infrastructure                                   |
| External Sharing       | IoCs from CERT-In, ISACs, partners (re-shared after validation)          |
| Red/Purple Team        | IoCs from simulated attacks (clearly labeled)                            |
| Vendor Notifications   | IoCs from vendor advisories                                              |

IoC types covered:

| IoC Type       | Examples                                              |
| -------------- | ----------------------------------------------------- |
| Network        | IP addresses, domains, URLs, ASNs                     |
| File           | SHA256/SHA1/MD5 hashes, file names, file paths        |
| Email          | Sender addresses, subject patterns, attachment hashes |
| Registry       | Registry keys, values (Windows)                       |
| Process        | Process names, command lines                          |
| Mutex          | Named mutexes                                         |
| Certificate    | TLS certificate fingerprints                          |
| Cryptocurrency | Wallet addresses (ransomware)                         |
| User Agent     | Suspicious user agent strings                         |
| JARM/JA3       | TLS fingerprints                                      |
| YARA Rules     | Pattern-based detection signatures                    |
| Sigma Rules    | Generic detection patterns                            |

Out of scope:

- general threat intelligence narratives (use TTP report or threat actor profile)
- raw evidence (stored in evidence vault)
- IoCs from public commercial feeds without internal validation

---

# 4. Definitions

| Term               | Definition                                                                  |
| ------------------ | --------------------------------------------------------------------------- |
| IoC                | Indicator of Compromise – observable artifact indicating malicious activity |
| Atomic IoC         | Single discrete indicator (e.g., IP, hash, domain)                          |
| Composite IoC      | Combination of indicators that together indicate compromise                 |
| Behavioral IoC     | Pattern-based indicator (e.g., process behavior)                            |
| TLP                | Traffic Light Protocol for information sharing classification               |
| Defanged IoC       | IoC formatted to prevent accidental execution (e.g., `hxxp://evil[.]com`)   |
| IoC Validity       | Time period during which IoC is considered actionable                       |
| False Positive IoC | IoC that triggers benign matches                                            |
| Pivot              | Using one IoC to discover related IoCs                                      |
| Operationalization | Deployment of IoC into security tools for detection/blocking                |
| Sigma Rule         | Open standard for SIEM detection rules                                      |
| YARA Rule          | Pattern matching for file/memory artifacts                                  |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                               |
| ------------------------ | -------------------------------------------------------------- |
| Threat Intel Lead        | Owns register; ensures quality; coordinates sharing            |
| Threat Intel Analyst     | Extracts IoCs; validates; enriches; tracks lifecycle           |
| L3 Analyst               | Provides IoCs from forensic investigations                     |
| Malware Analyst          | Provides IoCs from malware analysis                            |
| L2 Analyst               | Provides IoCs from incident investigations                     |
| Threat Hunter            | Provides IoCs from threat hunting                              |
| Detection Engineer       | Operationalizes IoCs into detection rules                      |
| SOC Lead                 | Validates operational deployment                               |
| SOC Manager              | Approves sharing decisions; reviews log monthly                |
| CISO                     | Approves external sharing (TLP:CLEAR/GREEN); reviews quarterly |
| Compliance Lead          | Validates sharing against regulatory requirements              |
| Legal Counsel            | Reviews sharing for legal implications (sensitive cases)       |
| MSSP SDM (if applicable) | Coordinates client-specific IoC handling                       |

---

# 6. TLP (Traffic Light Protocol) Classification (Mandatory)

All IoCs must be classified per TLP v2.0:

| TLP Level                      | Description                                                             | Sharing Scope                                    |
| ------------------------------ | ----------------------------------------------------------------------- | ------------------------------------------------ |
| **TLP:RED**                    | Highly sensitive; not for disclosure                                    | Recipients only; no further sharing              |
| **TLP:AMBER+STRICT**           | Limited disclosure to specific organization | Within recipient organization only               |
| **TLP:AMBER**                  | Limited disclosure                                                      | Recipient organization + clients on need-to-know |
| **TLP:GREEN**                  | Community sharing                                                       | Trusted community (ISACs, peers)                 |
| **TLP:CLEAR (formerly WHITE)** | Public disclosure                                                       | No sharing restrictions                          |

**Default classification:** TLP:AMBER unless explicitly downgraded.

Reference:
`https://www.first.org/tlp/`

---

# 7. IoC Lifecycle (Mandatory)

| Phase                     | Activities                                       | Owner                | Output            |
| ------------------------- | ------------------------------------------------ | -------------------- | ----------------- |
| **1. Extraction**         | IoC identified from source                       | L2/L3/Hunter/Analyst | Raw IoC entry     |
| **2. Validation**         | Confirmed as malicious; false positive check     | Threat Intel Analyst | Validated IoC     |
| **3. Enrichment**         | Context added (WHOIS, VirusTotal, sandbox, etc.) | Threat Intel Analyst | Enriched IoC      |
| **4. Classification**     | TLP assigned; confidence rated                   | Threat Intel Lead    | Classified IoC    |
| **5. Pivoting**           | Related IoCs discovered                          | Threat Intel Analyst | Pivot IoCs        |
| **6. Operationalization** | Deployed to SIEM/EDR/firewall/TI platform        | Detection Engineer   | Active detection  |
| **7. Sharing**            | Shared per TLP (internal/external)               | Threat Intel Lead    | Sharing record    |
| **8. Monitoring**         | Performance tracked (TP/FP)                      | SOC Lead             | Performance data  |
| **9. Tuning**             | False positives addressed                        | Detection Engineer   | Tuned detection   |
| **10. Expiry/Retirement** | Removed when no longer valid                     | Threat Intel Analyst | Retirement record |

---

# 8. Logging Principles (Mandatory)

| Principle              | Requirement                                                           |
| ---------------------- | --------------------------------------------------------------------- |
| Single source of truth | This register is authoritative IoC log                                |
| Defanged IoCs          | All IoCs in register must be defanged to prevent accidental execution |
| TLP classified         | Every IoC has TLP classification                                      |
| Source traceability    | Every IoC links to source (incident, hunt, etc.)                      |
| Confidence rated       | Confidence level (High/Medium/Low) per IoC                            |
| Time-bound             | First/Last seen and expiry tracked                                    |
| Enriched               | Context fields populated where available                              |
| Validated              | No raw, unvalidated IoCs in operationalized register                  |
| MSSP-segregated        | Client-specific IoCs scoped to tenant                                 |

---

# 9. IoC Defanging Standard (Mandatory)

To prevent accidental execution/access, all IoCs must be defanged in documentation:

| Type      | Original                    | Defanged                      |
| --------- | --------------------------- | ----------------------------- |
| URL       | `http://malicious.com/path` | `hxxp://malicious[.]com/path` |
| Domain    | `evil.com`                  | `evil[.]com`                  |
| IP        | `192.168.1.1`               | `192[.]168[.]1[.]1`           |
| Email     | `bad@evil.com`              | `bad[@]evil[.]com`            |
| File path | `C:\Windows\evil.exe`       | `C:\Windows\evil[.]exe`       |

**Note:** Defanging is for human-readable documentation. Tool integrations (SIEM, TI platforms) use re-fanged formats automatically.

---

# 10. IoC Register Template (Copy/Paste)

## 10.1 Register Schema (Mandatory Fields)

| Field                      | Description                                                                            |
| -------------------------- | -------------------------------------------------------------------------------------- |
| IoC ID                     | Unique identifier (`IOC-YYYY-####`)                                                    |
| Date Extracted (UTC)       | When IoC was extracted                                                                 |
| Source Type                | Incident / Hunt / Malware Analysis / Forensics / Phishing / Intel / External           |
| Source Reference           | INC-####, HUNT-####, MA-####, etc.                                                     |
| IoC Type                   | IP / Domain / URL / Hash-SHA256 / Hash-MD5 / Email / Registry / Process / Mutex / etc. |
| IoC Value (Defanged)       | Actual indicator in defanged format                                                    |
| Defanging Format           | Standard defanging applied                                                             |
| Threat Type                | Malware family / Phishing campaign / C2 / Ransomware / etc.                            |
| Threat Actor (if known)    | APT## / FIN## / Named actor / Unknown                                                  |
| Campaign (if known)        | Named campaign                                                                         |
| MITRE Technique            | T#### (if applicable)                                                                  |
| First Seen (UTC)           | First observation                                                                      |
| Last Seen (UTC)            | Most recent observation                                                                |
| Confidence                 | High / Medium / Low                                                                    |
| TLP                        | RED / AMBER+STRICT / AMBER / GREEN / CLEAR                                             |
| Validity Period            | Days/Months/Indefinite                                                                 |
| Expiry Date (UTC)          | When IoC expires                                                                       |
| Enrichment Status          | Enriched / Pending / N/A                                                               |
| VirusTotal Score           | Detection ratio if applicable                                                          |
| Sandbox Analysis           | Reference if applicable                                                                |
| Operationalized?           | Yes / No                                                                               |
| Operationalization Targets | SIEM / EDR / Firewall / Email / TI Platform / Proxy                                    |
| Deployment Date (UTC)      | When deployed                                                                          |
| TP Validated               | Yes / No                                                                               |
| FP Reported                | Count / Status                                                                         |
| Shared Externally?         | Yes / No                                                                               |
| Shared With                | CERT-In / ISAC / Partner / Vendor                                                      |
| Sharing Date (UTC)         | When shared                                                                            |
| Status                     | New / Validated / Operationalized / Shared / Expired / Retired                         |
| Linked RCA                 | RCA-YYYY-####                                                                          |
| Linked Detection Rule      | DET-IMP-YYYY-####                                                                      |
| Owner                      | Assigned analyst                                                                       |
| Notes                      | Additional context                                                                     |

---

## 10.2 Register Table (Copy/Paste)

| IoC ID        | Date Extracted | Source           | Source Ref | IoC Type    | IoC Value (Defanged) | Threat       | Threat Actor | First Seen | Last Seen | Confidence | TLP          | Expiry | Operationalized | Targets        | Shared | Status          | Linked RCA | Owner | Notes |
| ------------- | -------------- | ---------------- | ---------- | ----------- | -------------------- | ------------ | ------------ | ---------- | --------- | ---------- | ------------ | ------ | --------------- | -------------- | ------ | --------------- | ---------- | ----- | ----- |
| IOC-YYYY-0001 |                | Incident         | INC-####   | Hash-SHA256 | `abc123...`          | Ransomware-X |              |            |           | High       | AMBER        |        | Yes             | SIEM, EDR      | No     | Operationalized |            |       |       |
| IOC-YYYY-0002 |                | Hunt             | HUNT-####  | Domain      | `evil[.]com`         | Phishing     |              |            |           | Medium     | GREEN        |        | Yes             | Email, Proxy   | Yes    |                 |            |       |       |
| IOC-YYYY-0003 |                | Malware Analysis | MA-####    | IP          | `1[.]2[.]3[.]4`      | C2           |              |            |           | High       | AMBER+STRICT |        | Yes             | Firewall, SIEM | No     |                 |            |       |       |

---

## 10.3 Detailed Entry Template (Per Significant IoC Set)

> Use this format for IoC sets related to a specific incident or campaign.

### IoC Set: `IOC-YYYY-####`

**Metadata:**

| Field                | Value                                         |
| -------------------- | --------------------------------------------- |
| IoC Set Name         |                                               |
| Source Type          | Incident / Hunt / Malware / Forensics / Intel |
| Source Reference     |                                               |
| Date Extracted (UTC) |                                               |
| TLP Classification   |                                               |
| Confidence           |                                               |
| Owner                |                                               |

**Threat Context:**

| Field                        | Value                                      |
| ---------------------------- | ------------------------------------------ |
| Threat Type                  | Malware / Phishing / C2 / Ransomware / APT |
| Threat Actor (if attributed) |                                            |
| Malware Family               |                                            |
| Campaign Name                |                                            |
| MITRE Tactic                 |                                            |
| MITRE Techniques             | T####, T####                               |
| Target Industry/Geo          |                                            |

**IoC Inventory:**

### Network IoCs

| Type   | Value (Defanged) | First Seen | Last Seen | Confidence | Notes |
| ------ | ---------------- | ---------- | --------- | ---------- | ----- |
| IP     |                  |            |           |            |       |
| Domain |                  |            |           |            |       |
| URL    |                  |            |           |            |       |
| ASN    |                  |            |           |            |       |

### File IoCs

| Type   | Value | File Name | Size | Confidence | Notes |
| ------ | ----- | --------- | ---- | ---------- | ----- |
| SHA256 |       |           |      |            |       |
| SHA1   |       |           |      |            |       |
| MD5    |       |           |      |            |       |

### Email IoCs

| Type            | Value (Defanged) | Subject Pattern | Confidence | Notes |
| --------------- | ---------------- | --------------- | ---------- | ----- |
| Sender Address  |                  |                 |            |       |
| Attachment Hash |                  |                 |            |       |

### Host-Based IoCs

| Type         | Value | Context | Confidence | Notes |
| ------------ | ----- | ------- | ---------- | ----- |
| Registry Key |       |         |            |       |
| File Path    |       |         |            |       |
| Process Name |       |         |            |       |
| Mutex        |       |         |            |       |
| Service Name |       |         |            |       |

### Other IoCs

| Type                 | Value | Context | Confidence | Notes |
| -------------------- | ----- | ------- | ---------- | ----- |
| User Agent           |       |         |            |       |
| TLS Cert Fingerprint |       |         |            |       |
| JA3/JA3S             |       |         |            |       |
| Crypto Wallet        |       |         |            |       |
| YARA Rule Ref        |       |         |            |       |
| Sigma Rule Ref       |       |         |            |       |

**Enrichment Summary:**

| Enrichment Source                        | Result | Date |
| ---------------------------------------- | ------ | ---- |
| VirusTotal                               |        |      |
| Sandbox Analysis (Cuckoo/Hybrid/ANY.RUN) |        |      |
| WHOIS                                    |        |      |
| Passive DNS                              |        |      |
| Threat Intel Platform                    |        |      |
| Internal correlation                     |        |      |

**Operationalization Plan:**

| Tool                    | Action | Status | Deployed Date | Owner |
| ----------------------- | ------ | ------ | ------------- | ----- |
| SIEM (correlation rule) |        |        |               |       |
| EDR (block/alert)       |        |        |               |       |
| Firewall (block)        |        |        |               |       |
| Email gateway (block)   |        |        |               |       |
| Web proxy (block)       |        |        |               |       |
| TI Platform (feed)      |        |        |               |       |
| DNS (sinkhole)          |        |        |               |       |

**Sharing Plan:**

| Recipient                | TLP   | Format    | Date Shared | Confirmation |
| ------------------------ | ----- | --------- | ----------- | ------------ |
| Internal SOC             | AMBER | STIX/CSV  |             |              |
| MSSP Clients (sanitized) | AMBER |           |             |              |
| CERT-In                  | GREEN | STIX      |             |              |
| ISAC                     | GREEN | STIX/MISP |             |              |
| Vendor (e.g., AV vendor) | AMBER |           |             |              |
| Public (blog/advisory)   | CLEAR |           |             |              |

**Validation Tracking:**

| Metric                  | Initial | Week 1 | Month 1 | Current |
| ----------------------- | ------- | ------ | ------- | ------- |
| True positives detected |         |        |         |         |
| False positives         |         |        |         |         |
| FP rate                 |         |        |         |         |
| Tuning iterations       |         |        |         |         |

**Lifecycle:**

| Milestone       | Date | Notes |
| --------------- | ---- | ----- |
| Extracted       |      |       |
| Validated       |      |       |
| Enriched        |      |       |
| Operationalized |      |       |
| Shared          |      |       |
| Reviewed        |      |       |
| Expired         |      |       |
| Retired         |      |       |

---

# 11. Confidence Rating Definitions (Mandatory)

| Confidence | Definition                                      | Criteria                                                             |
| ---------- | ----------------------------------------------- | -------------------------------------------------------------------- |
| **High**   | Strong evidence; multiple corroborating sources | Direct extraction from confirmed incident; sandbox-confirmed malware |
| **Medium** | Moderate evidence; some corroboration           | Extracted from threat hunt; single-source validation                 |
| **Low**    | Weak evidence; requires further validation      | External feed without internal validation; circumstantial            |

---

# 12. IoC Expiry Standards (Mandatory)

Different IoC types have different recommended validity periods:

| IoC Type             | Default Validity             | Rationale                  |
| -------------------- | ---------------------------- | -------------------------- |
| File Hash (SHA256)   | Indefinite                   | Hashes don't change        |
| Domain               | 30–90 days                   | Domains can be repurposed  |
| IP Address           | 7–30 days                    | IPs frequently reused      |
| URL                  | 7–30 days                    | URLs short-lived           |
| Email Sender         | 30 days                      | Domains often spoofed      |
| Registry Key         | 90 days                      | Persistence may be removed |
| YARA Rule            | Indefinite (review annually) | Pattern-based, durable     |
| TLS Cert Fingerprint | 90 days                      | Certs rotate               |
| JA3/JA3S             | 90 days                      | TLS profiles change        |

**Note:** Expiry should be reviewed before retirement; some IoCs may need extension if still active.

---

# 13. Sharing Standards (Mandatory)

## 13.1 Internal Sharing

| Audience                       | Format               | Frequency |
| ------------------------------ | -------------------- | --------- |
| SOC L1/L2/L3                   | TI Platform feed     | Real-time |
| Detection Engineering          | Detection rule input | Real-time |
| MSSP Clients (relevant tenant) | Client TI feed       | Real-time |
| Management                     | Summary report       | Monthly   |

## 13.2 External Sharing

| Recipient              | TLP Limit   | Format           | Approval Required |
| ---------------------- | ----------- | ---------------- | ----------------- |
| CERT-In                | GREEN/CLEAR | STIX 2.x / Email | SOC Manager       |
| ISACs (FS-ISAC, etc.)  | GREEN/AMBER | STIX / MISP      | SOC Manager       |
| Trusted Partners       | AMBER       | STIX / Email     | SOC Manager       |
| Public (blog/advisory) | CLEAR       | Markdown / PDF   | CISO              |
| Law Enforcement        | RED/AMBER   | Per LEA format   | CISO + Legal      |

## 13.3 Sharing Format Standards

| Format   | Use Case                          |
| -------- | --------------------------------- |
| STIX 2.x | Industry standard for IoC sharing |
| MISP     | Open-source TI platform format    |
| CSV      | Simple bulk import                |
| JSON     | API consumption                   |
| YARA     | File/memory pattern matching      |
| Sigma    | SIEM detection rules              |

---

# 14. Status Definitions (Standard)

| Status              | Definition                                      |
| ------------------- | ----------------------------------------------- |
| **New**             | Just extracted, not yet validated               |
| **Validated**       | Confirmed as malicious, not yet operationalized |
| **Enriched**        | Context added (VT, sandbox, etc.)               |
| **Operationalized** | Deployed to detection/blocking tools            |
| **Shared**          | Shared externally per TLP                       |
| **Active**          | In production, generating detections            |
| **Tuning**          | Under tuning to reduce FPs                      |
| **Stable**          | Mature, low FP rate                             |
| **Expired**         | Past validity period                            |
| **Retired**         | Removed from production                         |
| **False Positive**  | Determined to be FP, removed                    |

---

# 15. Performance Metrics (Mandatory – Monthly Report)

Track these metrics monthly:

| Metric                             | Calculation                      | Target |
| ---------------------------------- | -------------------------------- | ------ |
| IoCs extracted                     | Count this month                 |        |
| IoCs validated                     | Count validated                  |        |
| IoCs operationalized               | Count deployed                   |        |
| Average time-to-operationalization | Hours from extracted to deployed |        |
| IoCs shared externally             | Count shared                     |        |
| True positive detections from IoCs | Count                            |        |
| False positive rate                | % FP across IoCs                 |        |
| IoCs expired/retired               | Count                            |        |
| Active IoCs in TI platform         | Total count                      |        |
| MITRE coverage from IoCs           | Techniques covered               |        |

---

# 16. Quality Checklist (Per IoC Entry)

Before marking an IoC as "Operationalized":

- [ ] IoC value documented in defanged format
- [ ] Source reference linked
- [ ] TLP classification assigned
- [ ] Confidence rating assigned
- [ ] Enrichment performed (VT, sandbox where applicable)
- [ ] First/last seen timestamps recorded
- [ ] Expiry date set
- [ ] Validated as malicious (not FP)
- [ ] False positive risk assessed
- [ ] Deployed to relevant tools
- [ ] Detection rule created (if applicable)
- [ ] Sharing decision documented
- [ ] Linked to source incident/hunt/intel
- [ ] Owner assigned
- [ ] Approved by Threat Intel Lead
- [ ] MSSP: tenant scoping verified (if applicable)

---

# 17. Review Process (Mandatory)

## 17.1 Daily Review

Threat Intel Analyst reviews:

- New IoCs awaiting validation
- IoCs awaiting enrichment
- Operational deployment status

## 17.2 Weekly Review

Threat Intel Lead reviews:

- IoCs nearing expiry
- IoCs with high FP rates (tuning candidates)
- Sharing backlog
- New campaigns/threat actor activity

## 17.3 Monthly Review

Threat Intel Lead + SOC Manager review:

- IoC extraction and operationalization metrics
- True positive value generated
- False positive analysis
- Coverage gaps
- Sharing program effectiveness

## 17.4 Quarterly Review

CISO + Threat Intel Lead review:

- Strategic threat intelligence priorities
- External sharing partnership effectiveness
- Investment needs (TI platform, feeds)
- Threat landscape changes

---

# 18. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Client-specific IoCs logged in **tenant-scoped registers**
- Cross-client IoCs (generic) tracked in master register
- Client-confidential IoCs (TLP:RED/AMBER+STRICT) must not be shared across tenants
- Common threat IoCs (TLP:AMBER/GREEN) may be operationalized across tenants
- Each client receives **tenant-relevant IoC feed**
- Client approval required for external sharing of client-derived IoCs
- IoCs from one client incident must be **sanitized** before generic sharing
- Monthly **IoC report to client** with their tenant's IoCs and relevant intelligence

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md`

---

# 19. Integration with Other Processes

| Process                | Integration Point                   |
| ---------------------- | ----------------------------------- |
| Incident Response      | IoCs extracted during/post-incident |
| Threat Hunting         | Hunt findings produce IoCs          |
| Malware Analysis       | Static/dynamic analysis output      |
| Detection Engineering  | IoCs feed detection rules           |
| RCA                    | IoCs documented in RCA timeline     |
| Lessons Learned        | IoC-related improvements captured   |
| Threat Intel Reporting | IoCs feed TI reports                |
| External Sharing       | IoCs shared per TLP                 |
| TI Platform            | Operationalization target           |

---

# 20. Related Documents

| Document                      | Path                                                                                     |
| ----------------------------- | ---------------------------------------------------------------------------------------- |
| TTP Intelligence Report       | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`                   |
| Threat Actor Profile Template | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`             |
| TI IoC Handling SOP           | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`                |
| TI Feed Management            | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`                 |
| TI Platform Usage Guide       | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`            |
| TI Integration with SIEM      | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md`           |
| TI Integration with EDR       | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md`            |
| TI Reporting Template         | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md`              |
| L2 Threat Hunting Procedures  | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`              |
| L3 Malware Analysis SOP       | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md`                   |
| Detection Improvement Log     | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                |
| Common IoC Reference          | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`                  |
| CERT-In Reporting SOP         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |

---

# 21. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | Threat Intel Lead / SOC Manager | Initial version |

---

# 22. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
