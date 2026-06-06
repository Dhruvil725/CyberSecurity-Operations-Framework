# CAT-06 – Data Breach and Data Exfiltration Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Data Breach and Data Exfiltration |
| Document ID | IR-CAT-006 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-06 |
| Default Severity | P1 – Critical (confirmed breach/exfiltration of sensitive data) / P2 – High (suspected exfiltration or confirmed unauthorized access to sensitive data) |
| Escalation Priority | Immediate due to regulatory, legal, and reputational impact |
| Attack Goal | Unauthorized access, theft, exposure, or exfiltration of sensitive data |
| Threat Actors | Cybercriminals, APT groups, insiders, compromised vendors |
| Playbook Reference | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |

---

## 3. What is a Data Breach / Data Exfiltration?

### 3.1 Data Breach

A data breach is an incident in which sensitive, protected, or confidential information is accessed, disclosed, altered, or destroyed without authorization. A breach can occur with or without confirmed exfiltration (for example, unauthorized access to a database with sensitive records).

### 3.2 Data Exfiltration

Data exfiltration is the unauthorized transfer of data from an organization to an external destination controlled by an attacker or unauthorized party. Exfiltration may occur via:

- Web uploads (HTTPS, web services, cloud drives)
- Email forwarding or external sharing
- File transfer protocols (SFTP/FTP)
- Remote administration tools
- DNS tunneling or covert channels
- Insider physical transfer (USB)

### 3.3 Why this Category is High Impact

Data breach events frequently trigger:

- Legal and contractual notification requirements
- Regulatory reporting obligations (sector-specific)
- Client notification requirements (MSSP)
- Incident disclosure and audit scrutiny
- Financial penalties, lawsuits, and reputational damage

---

## 4. Common Data Types Involved

| Data Type | Examples |
|----------|----------|
| Customer Personal Data | Names, addresses, phone numbers, IDs, KYC documents |
| Financial Data | Account numbers, card data, transaction history, banking records |
| Credentials | Passwords, hashes, API keys, tokens, private keys |
| Business Confidential | Contracts, pricing, legal documents, strategic plans |
| Intellectual Property | Source code, designs, research, proprietary algorithms |
| HR Data | Payroll, employee personal details, medical info (if applicable) |
| Operational Data | Network diagrams, security configurations, incident artifacts |

Note: Actual classification should align with your organization’s data classification policy.

---

## 5. Common Breach and Exfiltration Scenarios

| Scenario | Description |
|---------|-------------|
| Database Dump | Unauthorized export of database tables or full backups |
| Cloud Storage Exposure | Public access configured on storage buckets or file shares |
| Credential Compromise | Attacker accesses sensitive data using stolen credentials |
| Insider Exfiltration | Employee/contractor exports data to personal storage |
| SaaS Account Takeover | Compromised email or cloud accounts used to access data |
| Web Application Exploit | SQLi/RCE used to access and extract application data |
| Third-Party Exposure | Vendor compromise leading to exposure of your data |
| Backup Exposure | Backups copied or accessed without authorization |

---

## 6. Indicators of Compromise (IoCs) and Observables

### 6.1 Data Access Indicators

| Indicator | Examples |
|----------|----------|
| Unusual Query Volume | Large SQL queries, bulk select, repeated export requests |
| Privileged Data Access | Sensitive tables accessed by non-DBA accounts |
| Mass File Read | Large read volume from file shares or repositories |
| Access Time Anomaly | Sensitive data accessed outside business hours |
| Geographic / Device Anomaly | Sensitive data accessed from new locations or devices |

### 6.2 Data Movement / Exfiltration Indicators

| Indicator | Examples |
|----------|----------|
| Large Outbound Transfers | Sustained outbound data spikes from endpoint/server |
| Uploads to Cloud Drives | OneDrive/Google Drive/Dropbox uploads (not business-approved) |
| Unusual Protocol Usage | SFTP/FTP connections from systems that do not normally use them |
| Encrypted Archives Created | ZIP/RAR/7z files created in bulk prior to transfer |
| DNS Tunneling | High-volume or large DNS queries to single domain |
| Email Forwarding | New rules forwarding mail to external addresses |

### 6.3 Key Log Sources

| Source | What to Look For |
|--------|------------------|
| Proxy / SWG Logs | Upload destinations, large POST requests, new domains |
| Firewall / NetFlow | Data volume, destination IPs/ASNs, uncommon ports |
| DLP (if available) | Sensitive content detection and policy triggers |
| Database Audit Logs | Exports, large queries, login patterns, privilege use |
| File Share Audit Logs | Mass read/write/delete operations, unusual users |
| Cloud Audit Logs | Object downloads, token creation, permission changes |
| Email / M365 Logs | Forwarding rules, external sharing, mailbox exports |
| EDR Telemetry | Archive tools, staging directories, suspicious processes |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed exfiltration of regulated/sensitive data (customer/financial/credentials) | P1 – Critical |
| Confirmed unauthorized access to sensitive data with credible exfiltration indicators | P1 – Critical |
| Confirmed exposure of sensitive data to public (misconfiguration) | P1 – Critical |
| Suspected exfiltration with strong supporting evidence (staging + outbound transfer) | P2 – High |
| Confirmed unauthorized access to sensitive data without exfil proof yet | P2 – High |
| Single-user suspicious access pattern to sensitive data (unconfirmed) | P3 – Medium |
| Policy-level event with no sensitive data and no access confirmation | P4 – Low |

Note: Escalate quickly; downgrade only after verification with SOC Lead and data owners.

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes (Containment and Preservation)

- Create incident ticket and apply initial severity
- Notify SOC Lead immediately for P2 and above
- Preserve volatile evidence (logs and telemetry) immediately
- Identify affected system(s), account(s), and data repository
- If exfiltration is in progress, request immediate containment approval:
  - EDR network containment
  - Blocking destination domains/IPs
  - Disabling compromised accounts or revoking sessions
- Start an incident timeline (who/what/when) in the ticket

### 8.2 First 1 Hour (Scoping and Risk Assessment)

- Determine whether sensitive data was accessed and by which identity
- Identify data classification and data owners (business owners)
- Identify potential exfiltration channels:
  - proxy uploads, email forwarding, cloud sharing, SFTP/FTP
- Check for data staging artifacts (archives, temporary directories)
- Check identity logs for suspicious access patterns and persistence
- Notify GRC/Compliance and Legal for P1 and for P2 cases with likely breach
- Notify MSSP client contacts if client data is impacted (per SLA)

### 8.3 First 4 Hours (Containment Confirmation and Incident Decision)

- Confirm whether exfiltration occurred using:
  - network logs, proxy logs, cloud logs, DLP events, storage access logs
- Confirm scope: which datasets, which records, and how much volume
- Identify the initial access vector (phishing, exploit, insider, vendor)
- Confirm all attacker access paths are closed (tokens, keys, accounts)
- Begin eradication planning (patching, credential reset, hardening)
- Prepare initial management brief (facts, scope, likely exposure)

---

## 9. Containment Guidance (Recommended Controls)

| Containment Action | When | Notes |
|-------------------|------|------|
| Revoke sessions / tokens | Suspected account compromise | Reduces impact with minimal disruption |
| Disable account | Confirmed compromise or malicious insider | Requires approval; document rationale |
| Block destinations | Confirmed exfil destination | Block at firewall/proxy/DNS; document |
| Isolate endpoint/server | Active exfiltration or staging | Prefer EDR containment where available |
| Remove public access | Cloud exposure confirmed | Change permissions; preserve evidence first |
| Rotate keys/secrets | API key/token exposure suspected | Coordinate with app/cloud owners |

Reference: `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 10. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Phishing | T1566 |
| Initial Access | Exploit Public-Facing Application | T1190 |
| Credential Access | Valid Accounts | T1078 |
| Credential Access | OS Credential Dumping | T1003 |
| Discovery | File and Directory Discovery | T1083 |
| Collection | Data from Information Repositories | T1213 |
| Collection | Data from Local System | T1005 |
| Collection | Email Collection | T1114 |
| Exfiltration | Exfiltration Over C2 Channel | T1041 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Exfiltration | Exfiltration to Cloud Storage | T1567.002 |
| Exfiltration | Exfiltration Over Alternative Protocol | T1048 |
| Defense Evasion | Obfuscated Files or Information | T1027 |
| Impact | Data Destruction | T1485 |

---

## 11. Key Investigation Questions

1. What data was accessed (system, dataset, table, folder path)?
2. Who accessed it (user/service account), and was access authorized?
3. When did access begin and end (time window)?
4. What is the data classification (public/internal/confidential/regulatory)?
5. Was data copied, exported, archived, or staged?
6. Was data exfiltrated (where, how, how much)?
7. What is the external destination (domain/IP/service/provider)?
8. Was encryption used (TLS, archives with password, tunneling)?
9. Was the identity compromised (phishing, token theft, MFA bypass)?
10. Are there indicators of persistence (new rules, tokens, scheduled tasks)?
11. Are backups or logs affected or tampered with?
12. Does this trigger client contractual notification or regulator reporting?
13. What immediate containment action is required and who approves it?

---

## 12. Critical Do's and Do Not's

### Do

- Preserve logs and evidence before making destructive changes
- Engage GRC/Compliance and Legal early for likely breach cases
- Identify data owners and validate data classification quickly
- Block known exfil destinations and revoke sessions promptly when confirmed
- Maintain a clear timeline and documented decision trail
- Use chain-of-custody for evidence that may be required legally

### Do Not

- Delay containment if active exfiltration is confirmed
- Modify cloud permissions without capturing pre-change evidence
- Assume "no exfil" without checking proxy/firewall/cloud logs
- Close the incident without documenting scope, data type, and exposure status
- Share breach details broadly without need-to-know controls

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify breach indicators, create ticket, preserve initial evidence |
| L2 Investigation | Confirm access/exfil indicators, scope affected assets and identities |
| SOC Lead | Approve severity, coordinate communications and containment approvals |
| L3 / IR Team | Lead deeper forensics, attack chain reconstruction, evidence integrity |
| Data Owner | Confirm data type, sensitivity, and business impact |
| GRC / Compliance | Assess reporting requirements and notification timelines |
| Legal | Guide notification language, preservation, and law enforcement considerations |
| Management / CISO | Approve major actions, external communications, and disclosure strategy |
| MSSP SDM / Client Owner | Coordinate client notifications and contractual deliverables |

---

## 14. Regulatory and Client Reporting Considerations

This category frequently triggers reporting requirements. Perform a structured assessment:

| Consideration | Action |
|--------------|--------|
| Regulated sector impact (e.g., BFSI) | Follow RBI reporting guidance and timelines |
| Customer data exposure | Determine notification requirements and client obligations |
| Contractual breach clauses | Notify client per SLA and MSA/SOW terms |
| CERT-In applicability | Confirm whether incident type is reportable and within what timeline |
| Cross-border data | Consider jurisdictional requirements if applicable |
| Evidence preservation | Maintain defensible evidence for audits, claims, or legal action |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Proxy / SWG logs | Critical | Upload destinations, POST activity, file transfers |
| Firewall / NetFlow | Critical | Data volumes, destination IPs/ASNs, ports |
| Cloud audit logs | Critical | Downloads, sharing changes, token creation |
| Database audit logs | Critical | Exports, large queries, privileged actions |
| DLP alerts (if available) | High | Sensitive data movement confirmation |
| File server audit logs | High | Mass access, file paths, access volumes |
| Email and mailbox audit logs | High | Forwarding rules, mailbox exports, external sharing |
| EDR telemetry | High | Archive tools, staging directories, process execution |
| Screenshots / exports of relevant portals | Medium | Preserve state and results |
| Chain-of-custody forms | Critical | Required when evidence may be used legally |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Data Breach Master Playbook | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification Guidance | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Chain-of-Custody Forms | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**