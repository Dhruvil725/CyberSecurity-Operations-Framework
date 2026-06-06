# Common IoC Reference

---

# 1. Document Control

| Field          | Value                                               |
| -------------- | --------------------------------------------------- |
| Document Name  | Common IoC Reference                                |
| Document ID    | MSSP-TRN-KB-004                                     |
| Version        | 1.0                                                 |
| Effective Date | 30-May-2026                                         |
| Owner          | MSSP Threat Intel Lead / Detection Engineering Lead |
| Approved By    | MSSP CISO                                           |
| Classification | Confidential – MSSP Internal                        |
| Review Cycle   | Quarterly (or upon major threat landscape change)   |

---

# 2. Purpose

This document defines the standardized Common Indicator of Compromise (IoC) Reference providing SOC analysts (L1/L2/L3), IR Team members, Threat Intelligence analysts, and Detection Engineers with a consolidated operational guide for understanding, handling, enriching, actioning, and sharing IoCs across the MSSP multi-tenant environment — enabling rapid, accurate, tenant-safe indicator management during alert triage, investigations, threat hunting, containment, and portfolio defense.

A formal Common IoC Reference is critical because:

- IoCs are the operational currency of SOC and IR operations
- inconsistent IoC handling leads to missed detections, false positives, and incorrect blocking
- new analysts need structured understanding of IoC types, confidence levels, and handling procedures
- L1 analysts frequently encounter IoCs in alerts without context on next steps
- L2/L3 analysts need consistent enrichment methodology for deeper investigations
- IR Team members need IoC-driven containment and eradication workflows
- Detection Engineers need IoC-to-detection rule conversion standards
- Threat Intel analysts need consistent IoC production and sharing standards
- multi-tenant MSSPs need strict IoC handling per tenant segregation policy
- cross-tenant IoC sharing requires sanitization before portfolio-wide defense
- IoC confidence levels drive different operational responses (block vs monitor vs ignore)
- IoC aging and expiry affect detection accuracy over time
- regulatory frameworks (RBI, ISO 27001, NIST CSF) require demonstrable threat intelligence capability
- without consolidated reference, IoC handling is inconsistent across analysts and shifts
- this reference is the operational quick-lookup companion to the TI program

This reference ensures:

- consolidated IoC type definitions and handling procedures
- consistent enrichment methodology across all analysts
- confidence level framework for operational decision-making
- per-IoC-type action guidance (block, monitor, hunt, ignore)
- multi-tenant IoC handling and sanitization guidance
- IoC lifecycle management (creation, enrichment, action, aging, expiry, archival)
- linkage to TI platform, SIEM, EDR, firewall, and playbooks
- audit-ready IoC handling documentation
- quarterly update cycle aligned to threat landscape

Reference alignment:

- 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md
- 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md
- 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md
- 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md

---

# 3. Scope

This reference covers:

| Scope Element               | Coverage                      |
| --------------------------- | ----------------------------- |
| IoC type definitions        | All common types              |
| IoC enrichment methodology  | Standard sources and patterns |
| IoC confidence levels       | Framework for scoring         |
| IoC action guidance         | Per type and confidence       |
| IoC lifecycle management    | Creation to expiry            |
| Multi-tenant IoC handling   | Tenant-scoped and sanitized   |
| IoC sharing standards       | Internal and external         |
| IoC feed management         | Commercial and open-source    |
| IoC detection integration   | SIEM, EDR, firewall, proxy    |
| IoC documentation standards | Per IoC register              |
| Common IoC examples         | Categorized reference         |

Out of scope:

- Specific active IoC values (covered by live TI platform and IoC Output Register)
- Detailed TI platform operations (covered by TI SOPs)
- Malware analysis output (covered by L3 procedures)
- Threat actor profiles (covered by Threat Actor Profile Template)
- Detection rule code (covered by Detection Engineering repository)

---

# 4. Definitions

| Term             | Definition                                                                            |
| ---------------- | ------------------------------------------------------------------------------------- |
| IoC              | Indicator of Compromise — observable artifact indicating potential malicious activity |
| IoA              | Indicator of Attack — behavioral indicator of active attack                           |
| Atomic IoC       | Single observable (IP, domain, hash)                                                  |
| Computed IoC     | Derived from analysis (YARA rule, behavioral pattern)                                 |
| Behavioral IoC   | Pattern of activity rather than single observable                                     |
| Confidence Level | Assessed reliability of IoC                                                           |
| TLP              | Traffic Light Protocol — information sharing classification                           |
| STIX             | Structured Threat Information eXpression                                              |
| TAXII            | Trusted Automated eXchange of Intelligence Information                                |
| Feed             | Continuous stream of IoCs from provider                                               |
| Enrichment       | Adding context to raw IoC                                                             |
| Aging            | IoC relevance decay over time                                                         |
| Expiry           | Point where IoC no longer actionable                                                  |
| Whitelisting     | Excluding benign IoC from detection                                                   |
| False Positive   | Benign activity matching IoC                                                          |
| True Positive    | Malicious activity matching IoC                                                       |
| Sanitization     | Removing client-identifying context from IoC                                          |
| Cross-Tenant IoC | IoC applicable across MSSP portfolio                                                  |

---

# 5. Roles and Responsibilities

| Role                            | Responsibilities                                |
| ------------------------------- | ----------------------------------------------- |
| MSSP Threat Intel Lead          | IoC program ownership, feed management, quality |
| MSSP Detection Engineering Lead | IoC-to-detection integration, rule creation     |
| MSSP IR Team Lead               | IoC-driven response actions                     |
| MSSP SOC Manager                | Operational IoC use validation                  |
| MSSP L1 Analysts                | IoC lookup during triage                        |
| MSSP L2 Analysts                | IoC enrichment during investigation             |
| MSSP L3 Analysts                | IoC production from forensics                   |
| MSSP Compliance Lead            | IoC handling audit compliance                   |
| All SOC Personnel               | Apply IoC handling per multi-tenant policy      |

---

# 6. IoC Types (Mandatory)

## 6.1 Network IoCs

| IoC Type               | Description                                                 | Examples                                        | Common Sources                            |
| ---------------------- | ----------------------------------------------------------- | ----------------------------------------------- | ----------------------------------------- |
| IP Address (IPv4/IPv6) | Malicious source or destination                             | C2 server, scanning source, exfil destination   | TI feeds, incident analysis, dark web     |
| Domain Name            | Malicious domain                                            | C2 domain, phishing domain, DGA domain          | TI feeds, DNS analysis, incident analysis |
| URL                    | Specific malicious URL                                      | Phishing URL, malware download URL, C2 callback | Email analysis, proxy logs, TI feeds      |
| CIDR Range             | Network block associated with malicious activity            | Bulletproof hosting ranges, VPN exit nodes      | TI feeds, ASN analysis                    |
| ASN                    | Autonomous System Number associated with malicious activity | Bulletproof hosting ASN                         | TI feeds, network analysis                |
| JA3/JA3S Hash          | TLS client/server fingerprint                               | Malware TLS fingerprint                         | NDR analysis, TI feeds                    |
| User-Agent String      | HTTP user-agent associated with malware                     | Custom C2 user-agent                            | Proxy logs, malware analysis              |
| SSL Certificate Hash   | Certificate thumbprint of malicious infrastructure          | Self-signed cert on C2                          | Certificate transparency, NDR             |

## 6.2 Host IoCs

| IoC Type            | Description                                | Examples                                  | Common Sources                  |
| ------------------- | ------------------------------------------ | ----------------------------------------- | ------------------------------- |
| File Hash (MD5)     | File fingerprint — legacy, collision-prone | Malware hash                              | AV, EDR, malware analysis       |
| File Hash (SHA1)    | File fingerprint — legacy                  | Malware hash                              | AV, EDR, malware analysis       |
| File Hash (SHA256)  | File fingerprint — standard                | Malware hash, tool hash                   | EDR, malware analysis, TI feeds |
| File Name           | Suspicious file name                       | Ransomware note, malware dropper          | EDR, forensics                  |
| File Path           | Suspicious file location                   | Malware persistence path                  | EDR, forensics                  |
| Registry Key/Value  | Suspicious registry modification           | Persistence key, configuration            | EDR, Sysmon, forensics          |
| Mutex Name          | Malware synchronization object             | Named mutex for malware family            | Malware analysis                |
| Service Name        | Suspicious Windows service                 | Persistence service                       | EDR, event logs                 |
| Scheduled Task Name | Suspicious scheduled task                  | Persistence task                          | EDR, event logs                 |
| Process Name        | Suspicious process                         | LOLBin abuse, malware process             | EDR                             |
| Command Line        | Suspicious command-line arguments          | Encoded PowerShell, suspicious parameters | EDR, Sysmon                     |
| YARA Rule           | Pattern-matching rule                      | Malware family detection                  | Malware analysis, TI            |
| Sigma Rule          | Generic detection rule                     | Behavioral detection                      | Detection engineering           |

## 6.3 Email IoCs

| IoC Type             | Description                 | Examples                      | Common Sources                   |
| -------------------- | --------------------------- | ----------------------------- | -------------------------------- |
| Sender Email Address | Malicious sender            | Phishing sender               | Email gateway, incident analysis |
| Sender Domain        | Malicious sender domain     | Spoofed or compromised domain | Email gateway, TI feeds          |
| Subject Line         | Phishing email subject      | Lure subject patterns         | Email gateway, user reports      |
| Attachment Hash      | Malicious attachment hash   | Trojanized document           | Email gateway, malware analysis  |
| Attachment Name      | Suspicious attachment name  | Invoice.exe, document.js      | Email gateway                    |
| Reply-To Address     | Mismatch reply address      | BEC indicator                 | Email header analysis            |
| X-Originating-IP     | Source IP from email header | Phishing infrastructure       | Email header analysis            |
| Email Header Anomaly | Spoofing indicators         | SPF/DKIM/DMARC failures       | Email gateway                    |

## 6.4 Identity IoCs

| IoC Type                | Description                 | Examples                   | Common Sources                |
| ----------------------- | --------------------------- | -------------------------- | ----------------------------- |
| Compromised Username    | Known compromised account   | Leaked credentials         | Dark web monitoring, TI feeds |
| Compromised Email       | Known leaked email          | Credential stuffing target | Dark web monitoring           |
| Suspicious OAuth App ID | Malicious OAuth application | Consent phishing app       | IdP logs, TI                  |
| Suspicious Device ID    | Unknown device registration | Rogue device in IdP        | IdP logs                      |
| Session Token           | Stolen session token        | Token theft for access     | Incident analysis             |

## 6.5 Cloud IoCs

| IoC Type          | Description               | Examples                 | Common Sources            |
| ----------------- | ------------------------- | ------------------------ | ------------------------- |
| Cloud Account ID  | Compromised cloud account | AWS IAM user, Azure AD   | Cloud audit logs          |
| Cloud Resource ID | Malicious cloud resource  | Cryptomining instance    | Cloud audit logs          |
| Cloud Storage URL | Malicious cloud storage   | Exfil destination bucket | NDR, DLP                  |
| API Key           | Compromised API key       | Exposed in code repo     | Secret scanning, incident |

## 6.6 Behavioral IoCs (IoA — Indicators of Attack)

| IoC Type                                                 | Description                         | Examples                         |
| -------------------------------------------------------- | ----------------------------------- | -------------------------------- |
| Beaconing Pattern                                        | Regular interval C2 communication   | 60-second callback pattern       |
| Credential Spraying Pattern                              | Multiple accounts, few passwords    | 1 password against 1000 accounts |
| Mass File Modification                                   | Rapid file changes                  | Ransomware encryption pattern    |
| Impossible Travel                                        | Geographically impossible logons    | India then US within 30 minutes  |
| Privilege Escalation Pattern | Normal user gaining admin           | User added to Domain Admins      |
| Lateral Movement Pattern                                 | Sequential host access              | Host A then Host B then Host C   |
| Data Staging Pattern                                     | Large archive creation before exfil | Zip files in temp folder         |
| Defense Impairment                                       | Security tool disabled              | AV service stopped               |

---

# 7. IoC Confidence Level Framework (Mandatory)

## 7.1 Confidence Levels

| Level         | Score  | Definition                                                          | Operational Action                         |
| ------------- | ------ | ------------------------------------------------------------------- | ------------------------------------------ |
| Confirmed     | 90-100 | Verified through direct analysis or multiple independent sources    | Block immediately, investigate all matches |
| High          | 70-89  | Strong correlation from reliable source, not independently verified | Block with monitoring, investigate matches |
| Medium        | 40-69  | Single source or moderate correlation, requires validation          | Monitor and alert, do not auto-block       |
| Low           | 20-39  | Weak correlation, unverified, or aged indicator                     | Monitor only, no alerting                  |
| Informational | 0-19   | Context only, not actionable                                        | Reference only, no detection               |

## 7.2 Confidence Scoring Factors

| Factor             | Increases Confidence                 | Decreases Confidence               |
| ------------------ | ------------------------------------ | ---------------------------------- |
| Source reliability | Government CERT, premium TI          | Unknown blog, anonymous            |
| Corroboration      | Multiple independent sources confirm | Single unverified source           |
| Recency            | Observed in last 7 days              | Older than 90 days                 |
| Context            | Full attack chain context            | Isolated indicator                 |
| Specificity        | Unique to malicious activity         | Shared infrastructure (CDN, cloud) |
| Validation         | Confirmed in MSSP environment        | Never observed locally             |
| Timeliness         | Real-time feed                       | Delayed publication                |

## 7.3 Confidence Level Assignment

| Step | Action                                | Owner      |
| ---- | ------------------------------------- | ---------- |
| 1    | Receive raw IoC                       | TI Analyst |
| 2    | Assess source reliability             | TI Analyst |
| 3    | Cross-reference with other sources    | TI Analyst |
| 4    | Check age and freshness               | TI Analyst |
| 5    | Check specificity (shared infra risk) | TI Analyst |
| 6    | Assign confidence level               | TI Analyst |
| 7    | Document scoring rationale            | TI Analyst |
| 8    | Review if High or Confirmed           | TI Lead    |

---

# 8. IoC Action Matrix (Mandatory)

## 8.1 Per Confidence Level

| Confidence    | Block                | Alert | Monitor | Hunt        | Reference Only |
| ------------- | -------------------- | ----- | ------- | ----------- | -------------- |
| Confirmed     | Yes                  | Yes   | Yes     | Yes         | No             |
| High          | Yes (with review)    | Yes   | Yes     | Yes         | No             |
| Medium        | No (unless approved) | Yes   | Yes     | Recommended | No             |
| Low           | No                   | No    | Yes     | Optional    | No             |
| Informational | No                   | No    | No      | No          | Yes            |

## 8.2 Per IoC Type

| IoC Type           | Typical Action              | Blocking Method             |
| ------------------ | --------------------------- | --------------------------- |
| IP Address         | Block at firewall/proxy     | Firewall deny rule          |
| Domain             | Block at DNS/proxy          | DNS sinkhole or proxy block |
| URL                | Block at proxy/SWG          | URL category block          |
| File Hash          | Block at EDR/AV             | EDR hash block              |
| Email Sender       | Block at email gateway      | Gateway deny list           |
| Email Domain       | Block at email gateway      | Gateway deny list           |
| Attachment Hash    | Block at email gateway      | Gateway hash block          |
| Registry Key       | Detection rule in EDR       | EDR alert rule              |
| Process/Command    | Detection rule in EDR/SIEM  | SIEM or EDR rule            |
| JA3 Hash           | Detection rule in NDR       | NDR rule                    |
| YARA Rule          | Deploy to EDR/scanning      | EDR or file scanning        |
| Behavioral Pattern | Detection rule in SIEM/UEBA | SIEM correlation rule       |

## 8.3 Blocking Authorization Matrix

| Scope                                   | Authorization Required                       |
| --------------------------------------- | -------------------------------------------- |
| Single-tenant IoC block (per client)    | L2 plus per-client authority                 |
| Multi-tenant IoC block (MSSP perimeter) | Detection Eng Lead plus TI Lead              |
| Portfolio-wide IoC block (all clients)  | Detection Eng Lead plus SOC Manager approval |
| Emergency IoC block (active attack)     | SOC Lead plus documented justification       |
| Reverse block (unblock)                 | TI Lead review plus Detection Eng            |

---

# 9. IoC Enrichment Methodology (Mandatory)

## 9.1 Standard Enrichment Steps

| Step | Action                                 | Sources                                       |
| ---- | -------------------------------------- | --------------------------------------------- |
| 1    | Lookup IoC reputation                  | VirusTotal, AbuseIPDB, GreyNoise, TI platform |
| 2    | Check age and first-seen date          | WHOIS, passive DNS, TI platform               |
| 3    | Check associated malware families      | VirusTotal, hybrid-analysis, TI platform      |
| 4    | Check associated threat actors         | TI platform, MITRE ATT&CK                     |
| 5    | Check associated campaigns             | TI platform, vendor reports                   |
| 6    | Check geographic context               | GeoIP, ASN lookup                             |
| 7    | Check shared infrastructure risk       | CDN check, cloud provider check               |
| 8    | Check MSSP historical hits             | SIEM historical search per tenant             |
| 9    | Cross-reference with other active IoCs | TI platform correlation                       |
| 10   | Assign confidence level                | Per Section 7                                 |
| 11   | Document enrichment results            | TI platform or ticket                         |

## 9.2 Enrichment Sources

| Source                 | Type            | Use Case                         |
| ---------------------- | --------------- | -------------------------------- |
| VirusTotal             | Commercial/Free | Hash, IP, domain, URL reputation |
| AbuseIPDB              | Free/Commercial | IP reputation                    |
| GreyNoise              | Commercial      | Internet noise vs targeted       |
| URLScan                | Free            | URL analysis                     |
| Shodan                 | Commercial      | IP exposure and services         |
| WHOIS                  | Free            | Domain registration              |
| PassiveTotal           | Commercial      | Passive DNS, WHOIS               |
| AlienVault OTX         | Free            | Community threat intel           |
| MISP                   | Open-source     | IoC sharing platform             |
| TI Platform (internal) | Commercial      | Primary enrichment source        |
| Hybrid-Analysis        | Free/Commercial | Sandbox analysis results         |
| ANY.RUN                | Commercial      | Interactive sandbox              |
| PhishTank              | Free            | Phishing URL database            |
| EmailRep               | Free/Commercial | Email address reputation         |
| NVD                    | Free            | CVE information                  |

## 9.3 Enrichment Quality Standards

| Standard                                        | Requirement |
| ----------------------------------------------- | ----------- |
| Minimum 2 sources for High/Confirmed            | Mandatory   |
| Shared infrastructure check for all IPs/domains | Mandatory   |
| Age check for all IoCs                          | Mandatory   |
| MSSP historical check                           | Mandatory   |
| Document all enrichment steps                   | Mandatory   |
| Confidence level assigned                       | Mandatory   |

---

# 10. IoC Lifecycle Management (Mandatory)

## 10.1 IoC Lifecycle Stages

Stage 1 CREATION: IoC identified from incident, TI feed, analysis, or external report

Stage 2 ENRICHMENT: Context added per enrichment methodology (Section 9)

Stage 3 VALIDATION: Confidence level assigned, shared infra risk checked

Stage 4 ACTION: Block, alert, monitor, hunt, or reference per action matrix

Stage 5 DEPLOYMENT: Pushed to SIEM, EDR, firewall, proxy, DNS per action

Stage 6 MONITORING: Active monitoring for matches across tenant portfolio

Stage 7 AGING: Confidence decays over time without re-validation

Stage 8 REVIEW: Periodic review of active IoCs for continued relevance

Stage 9 EXPIRY: IoC no longer actionable, removed from active detection

Stage 10 ARCHIVAL: Retained in IoC Output Register for historical reference

## 10.2 IoC Aging Schedule

| IoC Type           | Initial Active Period | Review Cycle  | Maximum Active Period (without re-validation) |
| ------------------ | --------------------- | ------------- | --------------------------------------------- |
| IP Address         | 30 days               | Every 30 days | 90 days                                       |
| Domain             | 60 days               | Every 30 days | 180 days                                      |
| URL                | 14 days               | Every 14 days | 60 days                                       |
| File Hash          | 365 days              | Every 90 days | Indefinite (if malware confirmed)             |
| Email Sender       | 30 days               | Every 30 days | 90 days                                       |
| JA3 Hash           | 60 days               | Every 30 days | 180 days                                      |
| YARA Rule          | 365 days              | Every 90 days | Indefinite (if malware family active)         |
| Behavioral Pattern | 180 days              | Every 90 days | Indefinite (if technique active)              |

## 10.3 IoC Expiry Criteria

| Criterion                                            | Action               |
| ---------------------------------------------------- | -------------------- |
| No matches in 2x active period                       | Expire and archive   |
| Source retracted IoC                                 | Expire immediately   |
| Confirmed false positive                             | Expire and whitelist |
| Infrastructure confirmed legitimate                  | Expire and whitelist |
| Threat actor infrastructure confirmed decommissioned | Expire and archive   |
| Re-validation confirms continued maliciousness       | Extend active period |

---

# 11. Multi-Tenant IoC Handling (Mandatory)

## 11.1 Tenant-Scoped IoC Handling

| Principle                                           | Requirement   |
| --------------------------------------------------- | ------------- |
| IoCs from client incidents are tenant-scoped        | Mandatory     |
| Tenant-derived IoCs not shared without sanitization | Mandatory     |
| Per-tenant blocking actions                         | Mandatory     |
| Per-tenant SIEM/EDR searches                        | Mandatory     |
| Client-specific IoC enrichment context              | Tenant-scoped |

## 11.2 Cross-Tenant IoC Sharing (Sanitized)

| Scenario                                             | Permitted       | Conditions                                 |
| ---------------------------------------------------- | --------------- | ------------------------------------------ |
| Generic IoC from client incident shared to portfolio | Yes (sanitized) | No client attribution, approved by TI Lead |
| TTP-derived IoC shared to portfolio                  | Yes             | TTPs are generic by nature                 |
| Commercial TI feed IoCs applied to all tenants       | Yes             | Per feed license and agreement             |
| Client-specific compromise evidence IoCs             | No              | Stays in client tenant                     |
| Reporting client incident IoCs to CERT-In            | Yes             | With client approval                       |

## 11.3 Sanitization for Cross-Tenant IoCs

| Element                                          | Sanitization Requirement |
| ------------------------------------------------ | ------------------------ |
| Client name                                      | Removed                  |
| Client identifiers (account IDs, hostnames, IPs) | Removed                  |
| Client-specific context                          | Removed                  |
| Generic IoC value (IP, hash, domain)             | Retained                 |
| Technique context (MITRE ATT&CK)                 | Retained                 |
| Malware family name                              | Retained                 |

## 11.4 Cross-Tenant IoC Sharing Approval

| Step | Action                                         | Owner             |
| ---- | ---------------------------------------------- | ----------------- |
| 1    | Analyst identifies IoC with cross-tenant value | L2/L3/IR          |
| 2    | Sanitization performed                         | TI Analyst        |
| 3    | Peer review of sanitization                    | Second TI Analyst |
| 4    | Approval by TI Lead                            | TI Lead           |
| 5    | Deployment to portfolio feed                   | Detection Eng     |
| 6    | Logged in IoC Output Register                  | TI Analyst        |

Reference:

- 09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md
- 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md

---

# 12. TLP (Traffic Light Protocol) Quick Reference (Mandatory)

## 12.1 TLP Levels

| TLP Level        | Color | Sharing Scope                              |
| ---------------- | ----- | ------------------------------------------ |
| TLP:RED          | Red   | Named recipients only, no further sharing  |
| TLP:AMBER+STRICT | Amber | Organization only, no sharing with clients |
| TLP:AMBER        | Amber | Organization plus clients who need to know |
| TLP:GREEN        | Green | Community sharing (peer organizations)     |
| TLP:CLEAR        | White | Unrestricted public sharing                |

## 12.2 TLP Application in MSSP Context

| TLP Level        | MSSP Application                                    |
| ---------------- | --------------------------------------------------- |
| TLP:RED          | Sensitive IoCs restricted to specific analysts      |
| TLP:AMBER+STRICT | MSSP internal only, not shared with any client      |
| TLP:AMBER        | Shared with affected client(s) on need-to-know      |
| TLP:GREEN        | Shared with MSSP community, sanitized for portfolio |
| TLP:CLEAR        | Public advisories, generic threat intel             |

## 12.3 TLP Handling Rules

| Rule                                                | Requirement      |
| --------------------------------------------------- | ---------------- |
| TLP must be assigned to all shared IoCs             | Mandatory        |
| TLP determines who can receive IoC                  | Strict adherence |
| TLP downgrade requires original source approval     | Mandatory        |
| TLP upgrade is always permitted                     | Self-serve       |
| TLP:RED never forwarded without explicit permission | Strict           |

---

# 13. IoC Feed Management Quick Reference (Mandatory)

## 13.1 Feed Categories

| Category                  | Examples                               | Use                      |
| ------------------------- | -------------------------------------- | ------------------------ |
| Commercial Premium        | Mandiant, Recorded Future, CrowdStrike | Primary enrichment       |
| Open-Source Community     | AlienVault OTX, Abuse.ch, PhishTank    | Supplementary            |
| Government/CERT           | CERT-In, US-CERT, FS-ISAC              | Regulatory and sector    |
| Internal (MSSP-generated) | Incident-derived IoCs, hunt findings   | Portfolio defense        |
| Dark Web Monitoring       | Dark web platforms                     | Leaked credentials, data |

## 13.2 Feed Quality Metrics

| Metric                                   | Target                         |
| ---------------------------------------- | ------------------------------ |
| False positive rate                      | Less than 5%                   |
| Freshness (IoC age at ingestion)         | Less than 24 hours for premium |
| Coverage (threat types covered)          | All major categories           |
| Uniqueness (not duplicated across feeds) | Deduplicated at ingestion      |
| Format compliance (STIX/TAXII)           | Preferred                      |

## 13.3 Feed Integration Points

| Integration             | Tool                  |
| ----------------------- | --------------------- |
| SIEM threat matching    | SIEM IoC watch lists  |
| EDR hash blocking       | EDR deny lists        |
| Firewall/Proxy blocking | Firewall IoC feeds    |
| DNS blocking            | DNS sinkhole          |
| Email gateway           | Email IoC block lists |
| TI platform aggregation | Central correlation   |
| SOAR enrichment         | Automated enrichment  |

Reference:

- 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md
- 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md
- 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md

---

# 14. Common IoC Patterns by Incident Type (Mandatory)

## 14.1 Ransomware IoCs

| IoC Type        | What to Look For                                            |
| --------------- | ----------------------------------------------------------- |
| File hashes     | Ransomware executable, dropper, Cobalt Strike beacon        |
| File names      | Ransom note filenames (README.txt, DECRYPT_FILES.html)      |
| File extensions | New encrypted extensions (.locked, .crypt, actor-specific)  |
| IP addresses    | C2 servers, exfiltration destinations                       |
| Domains         | C2 domains, TOR exit nodes                                  |
| Registry keys   | Persistence keys                                            |
| Scheduled tasks | Persistence tasks                                           |
| Process names   | Encryption process, PsExec, LOLBins                         |
| Command lines   | Encoded PowerShell, vssadmin delete shadows, wbadmin delete |
| Behavioral      | Mass file modification, shadow copy deletion, service stop  |

## 14.2 Phishing/BEC IoCs

| IoC Type          | What to Look For                           |
| ----------------- | ------------------------------------------ |
| Sender email      | Spoofed or compromised sender              |
| Sender domain     | Lookalike domain, recently registered      |
| Subject line      | Urgency, invoice, action required patterns |
| Attachment hash   | Macro-enabled document, executable         |
| Attachment name   | Invoice.docm, payment.exe                  |
| URL in body       | Credential harvesting, malware download    |
| Reply-To mismatch | Different from sender                      |
| X-Originating-IP  | Unusual origin                             |
| SPF/DKIM/DMARC    | Failure indicators                         |
| Behavioral        | Multiple recipients, bulk sending pattern  |

## 14.3 APT IoCs

| IoC Type              | What to Look For                                                |
| --------------------- | --------------------------------------------------------------- |
| Custom malware hashes | Actor-specific tooling                                          |
| C2 infrastructure     | Long-lived domains, fast-flux DNS, compromised legitimate sites |
| JA3/JA3S              | Custom TLS fingerprints                                         |
| YARA rules            | Actor-specific malware families                                 |
| Registry persistence  | WMI, services, scheduled tasks                                  |
| Credential dumping    | LSASS access, DCSync, NTDS.dit                                  |
| Lateral movement      | RDP, SMB, WMI, WinRM from unusual sources                       |
| Exfiltration          | Encrypted uploads to cloud, staged archives                     |
| Behavioral            | Long dwell time, low-and-slow C2, OPSEC discipline              |

## 14.4 Insider Threat IoCs

| IoC Type              | What to Look For                                  |
| --------------------- | ------------------------------------------------- |
| USB device usage      | New USB device on sensitive host                  |
| Cloud storage uploads | Personal Dropbox, Google Drive                    |
| Email forwarding      | Auto-forward to external address                  |
| Bulk file access      | Unusual volume of file downloads                  |
| After-hours access    | Access spikes outside business hours              |
| Printing anomalies    | Bulk printing of sensitive documents              |
| Behavioral            | Performance issues, resignation, financial stress |

## 14.5 Data Breach IoCs

| IoC Type                 | What to Look For                               |
| ------------------------ | ---------------------------------------------- |
| Dark web listings        | Data matching client format                    |
| Large outbound transfers | Volume anomalies                               |
| Cloud storage access     | Misconfigured bucket access                    |
| Database query anomalies | Bulk SELECT statements                         |
| Vendor credential usage  | Third-party credential access                  |
| Behavioral               | Data staging, archive creation, unusual export |

## 14.6 Cloud Security IoCs

| IoC Type                | What to Look For                                            |
| ----------------------- | ----------------------------------------------------------- |
| Unusual API calls       | CreateUser, AttachPolicy, RunInstances from unusual context |
| New regions             | Activity in previously unused cloud regions                 |
| Storage bucket access   | Public bucket access, bulk download                         |
| IAM changes             | New users, role changes, access key creation                |
| Cryptomining indicators | High CPU instances, mining pool connections                 |
| Behavioral              | Impossible travel for cloud accounts, privilege escalation  |

---

# 15. IoC Documentation Standards (Mandatory)

## 15.1 IoC Record Fields

| Field                   | Required                              |
| ----------------------- | ------------------------------------- |
| IoC Value               | Yes                                   |
| IoC Type                | Yes (per Section 6 categories)        |
| Source                  | Yes (feed name, incident ID, analyst) |
| First Seen              | Yes (UTC)                             |
| Last Seen               | Yes (UTC)                             |
| Confidence Level        | Yes (per Section 7)                   |
| TLP                     | Yes (per Section 12)                  |
| Associated Malware      | If known                              |
| Associated Threat Actor | If known                              |
| Associated Campaign     | If known                              |
| MITRE ATT&CK Technique  | If applicable                         |
| Action Taken            | Block, alert, monitor, reference      |
| Deployment Status       | Where deployed (SIEM, EDR, FW, etc.)  |
| Tenant Scope            | Per-tenant or portfolio-wide          |
| Enrichment Notes        | Summary of enrichment findings        |
| Expiry Date             | Per aging schedule                    |
| Created By              | Analyst name                          |
| Approved By             | TI Lead (for High/Confirmed)          |

## 15.2 IoC Register

All IoCs documented in:

- 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md

---

# 16. IoC False Positive Handling (Mandatory)

## 16.1 FP Identification

| Indicator of FP                                          | Action                                |
| -------------------------------------------------------- | ------------------------------------- |
| IoC matches legitimate infrastructure (CDN, cloud, SaaS) | Investigate and potentially whitelist |
| Multiple independent benign matches                      | Investigate and potentially whitelist |
| Source retracted or corrected IoC                        | Remove from active detection          |
| IoC is shared IP/domain (hosting, cloud)                 | Reduce confidence or whitelist        |
| No corroborating evidence in environment                 | Reduce confidence to Low              |

## 16.2 FP Resolution Process

| Step | Action                                              | Owner         |
| ---- | --------------------------------------------------- | ------------- |
| 1    | FP identified by analyst                            | L1/L2/L3      |
| 2    | FP documented with evidence                         | Analyst       |
| 3    | TI Lead reviews                                     | TI Lead       |
| 4    | Decision: whitelist, reduce confidence, or maintain | TI Lead       |
| 5    | If whitelist: documented with justification         | TI Lead       |
| 6    | Detection updated                                   | Detection Eng |
| 7    | Feedback to source (if commercial feed)             | TI Lead       |

## 16.3 FP Documentation

| Field              | Required                                  |
| ------------------ | ----------------------------------------- |
| Original IoC       | Yes                                       |
| FP evidence        | Yes                                       |
| Decision           | Whitelist, reduce confidence, or maintain |
| Decision rationale | Yes                                       |
| Approved by        | TI Lead                                   |
| Date               | Yes                                       |

---

# 17. IoC Sharing Standards (Mandatory)

## 17.1 Internal Sharing (Within MSSP)

| Sharing Context                | TLP                   | Method                |
| ------------------------------ | --------------------- | --------------------- |
| SOC operational sharing        | TLP:AMBER+STRICT      | TI platform, SIEM     |
| Cross-tenant portfolio defense | TLP:GREEN (sanitized) | Sanitized feed        |
| Detection engineering          | TLP:AMBER+STRICT      | Detection Eng channel |
| IR Team active incident        | TLP:AMBER             | Incident channel      |

## 17.2 External Sharing (Outside MSSP)

| Sharing Context     | TLP                    | Authorization                        |
| ------------------- | ---------------------- | ------------------------------------ |
| Client notification | TLP:AMBER              | Per-client SDM                       |
| CERT-In reporting   | Per CERT-In guidelines | Compliance Lead plus client approval |
| ISAC sharing        | TLP:GREEN              | TI Lead plus CISO                    |
| Vendor coordination | TLP:AMBER              | TI Lead plus Legal                   |
| Public advisory     | TLP:CLEAR              | CISO approval                        |

## 17.3 Sharing Format Standards

| Format             | Use                             |
| ------------------ | ------------------------------- |
| STIX 2.1           | Preferred for automated sharing |
| TAXII 2.1          | Preferred for feed transport    |
| CSV                | Simple bulk sharing             |
| JSON               | API-based sharing               |
| PDF (report)       | Human-readable sharing          |
| Email (structured) | Ad-hoc sharing with context     |

---

# 18. Operational Use Patterns (Mandatory)

## 18.1 L1 Analyst Usage

| Situation                     | Action                                                                |
| ----------------------------- | --------------------------------------------------------------------- |
| Alert contains IoC            | Look up IoC type, check TI platform for reputation, note confidence   |
| IoC not in TI platform        | Enrich via VirusTotal and AbuseIPDB, document, escalate if suspicious |
| Multiple IoCs in single alert | Correlate IoCs, escalate to L2 with enrichment                        |

## 18.2 L2 Analyst Usage

| Situation                               | Action                                                  |
| --------------------------------------- | ------------------------------------------------------- |
| Investigation requires enrichment       | Follow enrichment methodology (Section 9)               |
| New IoC discovered during investigation | Document in incident ticket, escalate to TI Lead        |
| IoC matches across multiple alerts      | Correlate, build timeline, escalate if campaign pattern |

## 18.3 L3 Analyst Usage

| Situation                           | Action                                        |
| ----------------------------------- | --------------------------------------------- |
| Forensic analysis produces new IoCs | Document per IoC standards, submit to TI Lead |
| Malware analysis produces IoCs      | Hash, C2, persistence artifacts documented    |
| Attribution analysis uses IoCs      | Cross-reference with TI actor profiles        |

## 18.4 IR Team Usage

| Situation                                | Action                                          |
| ---------------------------------------- | ----------------------------------------------- |
| Active incident — IoC-driven containment | Block confirmed IoCs per action matrix          |
| Post-incident IoC package                | Compile all IoCs per documentation standards    |
| Cross-client impact assessment           | Sanitized IoC search across portfolio (TI Lead) |

## 18.5 Detection Engineering Usage

| Situation                        | Action                                    |
| -------------------------------- | ----------------------------------------- |
| New IoC feed integration         | Validate feed quality, integrate per tool |
| IoC-to-detection rule conversion | Create alert rule from behavioral IoC     |
| IoC aging review                 | Remove expired IoCs from active detection |

## 18.6 Threat Intel Usage

| Situation                       | Action                                 |
| ------------------------------- | -------------------------------------- |
| IoC production from incident    | Per IoC lifecycle (Section 10)         |
| IoC enrichment request from SOC | Per enrichment methodology (Section 9) |
| Cross-tenant IoC sharing        | Per sanitization process (Section 11)  |
| External IoC sharing            | Per sharing standards (Section 17)     |

---

# 19. Common Pitfalls (Avoid These)

| Pitfall                                        | Correct Behavior                                        |
| ---------------------------------------------- | ------------------------------------------------------- |
| Blocking IoC without confidence assessment     | Always assign confidence before blocking                |
| Blocking shared infrastructure (CDN, cloud IP) | Always check shared infrastructure risk                 |
| Cross-tenant IoC sharing without sanitization  | Always sanitize per Section 11                          |
| IoC never expiring (stale blocklists)          | Follow aging schedule per Section 10                    |
| Single-source confidence (only VirusTotal)     | Minimum 2 sources for High/Confirmed                    |
| Ignoring TLP on received IoCs                  | Always respect TLP                                      |
| Not documenting IoC enrichment                 | Always document per Section 15                          |
| Applying IoC action without authority          | Follow authorization matrix per Section 8.3             |
| Not feeding incident IoCs back to TI           | Always submit per lifecycle                             |
| Treating behavioral IoCs like atomic IoCs      | Behavioral IoCs require detection rules, not blocklists |

---

# 20. Quarterly Update Process (Mandatory)

| Step | Action                               | Owner              | Cadence   |
| ---- | ------------------------------------ | ------------------ | --------- |
| 1    | Review IoC type landscape changes    | Threat Intel Lead  | Quarterly |
| 2    | Review feed quality metrics          | Threat Intel Lead  | Quarterly |
| 3    | Review aging schedule effectiveness  | Threat Intel Lead  | Quarterly |
| 4    | Review FP rates per IoC type         | Detection Eng Lead | Quarterly |
| 5    | Review cross-tenant sharing patterns | Compliance Lead    | Quarterly |
| 6    | Update this reference document       | Threat Intel Lead  | Quarterly |
| 7    | Communicate updates to SOC           | Training Lead      | Quarterly |

---

# 21. Quality Checklist (Per Update)

- [ ] All IoC types current and comprehensive
- [ ] Confidence level framework applied consistently
- [ ] Action matrix current
- [ ] Enrichment sources current
- [ ] Aging schedule reviewed and effective
- [ ] Multi-tenant handling guidelines current
- [ ] TLP guidelines current
- [ ] Feed management current
- [ ] Common IoC patterns per incident type current
- [ ] Documentation standards applied
- [ ] FP handling process current
- [ ] Sharing standards current
- [ ] Version updated
- [ ] CISO plus IR Team Lead approval
- [ ] SOC communication issued

---

# 22. Related Documents

| Document                        | Path                                                                             |
| ------------------------------- | -------------------------------------------------------------------------------- |
| Attack Technique Reference      | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md      |
| MITRE ATT&CK Quick Reference    | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md    |
| Tool Command Reference          | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md          |
| TI IoC Handling SOP             | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md          |
| TI Feed Management              | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md           |
| TI Platform Usage Guide         | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md      |
| TI Integration with SIEM        | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md     |
| TI Integration with EDR         | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md      |
| TI Reporting Template           | 04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md        |
| IoC Output Register             | 08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md                 |
| TTP Intelligence Report         | 08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md             |
| Threat Actor Profile Template   | 08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md       |
| SIEM Query Library              | 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md                          |
| EDR Investigation Queries       | 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md                    |
| Firewall Block Request SOP      | 04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md      |
| Client Data Segregation Policy  | 09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md  |
| Cross-Client Incident Procedure | 09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md |
| L1 Onboarding Program           | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md               |
| L2 Onboarding Program           | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md               |
| L3 Onboarding Program           | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md               |
| Detection Improvement Log       | 08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md          |
| Purple Team Exercise Guide      | 10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md              |
| Red Team IR Integration SOP     | 10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md             |

---

# 23. Revision History

| Version | Date        | Author                                              | Changes         |
| ------- | ----------- | --------------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP Threat Intel Lead / Detection Engineering Lead | Initial version |

---

# 24. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP Threat Intel Lead          |      |           |      |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP IR Team Lead               |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**
