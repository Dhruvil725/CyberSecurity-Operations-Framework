# Ticket Fields Standards

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Ticket Fields Standards |
| Document ID | TOOL-TKT-004 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the mandatory and optional fields for all security tickets created within the SOC ticketing system.

Standardized ticket fields are critical because:

- Inconsistent fields create investigation gaps
- Missing fields cause SLA tracking failures
- Audit evidence depends on complete ticket records
- MSSP client reporting relies on accurate field data
- Escalation decisions depend on proper field population
- Metrics and KPI reporting is driven by ticket field data
- Regulatory compliance requires documented incident records

This document ensures:

- Uniform ticket structure across all analysts
- Complete and accurate incident documentation
- Audit-ready ticket records at all times
- Consistent data for reporting and metrics
- SLA tracking accuracy
- MSSP multi-tenant data integrity

---

# 3. Scope

This standard applies to all ticket types:

| Ticket Type | Examples |
|---|---|
| Security alert tickets | SIEM/EDR triggered events |
| Confirmed incident tickets | Active malware, breach, ransomware |
| Change request tickets | Firewall blocks, isolation requests |
| Service request tickets | Evidence handling, client notifications |
| Operational task tickets | Health checks, coverage reviews |
| MSSP client incident tickets | Client-specific security events |
| Post-incident action tickets | RCA, lessons learned, improvements |

---

# 4. Field Classification

All ticket fields are classified as:

| Classification | Meaning |
|---|---|
| MANDATORY | Must be completed at ticket creation |
| MANDATORY-CONDITIONAL | Required when specific conditions are met |
| RECOMMENDED | Should be completed where information is available |
| OPTIONAL | Completed at analyst discretion |

---

# 5. Core Ticket Fields — All Ticket Types

---

## 5.1 Identification Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Ticket ID | MANDATORY | Auto-generated unique identifier | INC-2026-0001 |
| Ticket Title | MANDATORY | Descriptive summary of the event | P2 – Encoded PowerShell – FIN-WS-12 |
| Ticket Type | MANDATORY | Alert / Incident / Change / Task | Incident |
| Incident Category | MANDATORY | Malware / Phishing / Ransomware etc | Malware-Trojan |
| Detection Source | MANDATORY | Where alert originated | SIEM / EDR / Manual / Client |
| Parent Ticket | OPTIONAL | If child of a major incident | INC-2026-0001 |
| Duplicate Of | MANDATORY-CONDITIONAL | If duplicate identified | INC-2026-0001 |

---

## 5.2 Timing Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Detection Time (UTC) | MANDATORY | When alert was generated | 2026-05-25T03:14:00Z |
| Ticket Creation Time (UTC) | MANDATORY | When ticket was created | 2026-05-25T03:16:00Z |
| First Acknowledged Time (UTC) | MANDATORY | When analyst acknowledged | 2026-05-25T03:18:00Z |
| Escalation Time (UTC) | MANDATORY-CONDITIONAL | When escalated | 2026-05-25T03:30:00Z |
| Containment Start Time (UTC) | MANDATORY-CONDITIONAL | When containment began | 2026-05-25T04:00:00Z |
| Containment Completion Time (UTC) | MANDATORY-CONDITIONAL | When containment completed | 2026-05-25T04:30:00Z |
| Resolution Time (UTC) | MANDATORY | When incident resolved | 2026-05-25T06:00:00Z |
| Closure Time (UTC) | MANDATORY | When ticket formally closed | 2026-05-25T07:00:00Z |

---

## 5.3 Priority and Severity Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Priority | MANDATORY | P1 / P2 / P3 / P4 | P2 |
| Severity | MANDATORY | Critical / High / Medium / Low | High |
| Priority Change Log | MANDATORY-CONDITIONAL | If priority changed during lifecycle | Changed P3 to P2 at 04:15 UTC – lateral movement observed |
| Priority Change Reason | MANDATORY-CONDITIONAL | Justification for change | Privileged account confirmed compromised |
| Priority Change Approved By | MANDATORY-CONDITIONAL | Who approved the change | SOC Lead – J.Smith |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md`
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 5.4 Ownership Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Assigned To | MANDATORY | Current ticket owner | L2 Analyst – A.Kumar |
| Created By | MANDATORY | Who created the ticket | L1 Analyst – R.Sharma |
| Team | MANDATORY | SOC / IR Team / MSSP | SOC L2 |
| Escalated To | MANDATORY-CONDITIONAL | Who ticket escalated to | L3 Analyst – P.Mehta |
| Escalation Acknowledged By | MANDATORY-CONDITIONAL | Who acknowledged escalation | P.Mehta at 03:45 UTC |
| Closed By | MANDATORY | Who closed the ticket | SOC Lead – J.Smith |
| Closure Approved By | MANDATORY | Who approved closure | IR Team Lead – D.Patel |

---

## 5.5 Affected Asset Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Affected Hostname(s) | MANDATORY | All impacted hosts | FIN-WS-12, FIN-WS-15 |
| Affected IP Address(es) | MANDATORY | IP of affected systems | 10.10.5.12, 10.10.5.15 |
| Affected User(s) | MANDATORY | All impacted user accounts | jsmith, akumar |
| User Privilege Level | MANDATORY | Standard / Privileged / Admin | Privileged |
| Affected Department | RECOMMENDED | Business unit impacted | Finance |
| Affected System Criticality | MANDATORY | Critical / High / Medium / Low | High |
| Asset Tag | RECOMMENDED | Asset register reference | ASSET-FIN-0042 |
| Operating System | RECOMMENDED | OS of affected host | Windows 11 Enterprise |
| Environment | MANDATORY | Production / Dev / Test / Cloud | Production |

---

## 5.6 Incident Description Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Initial Description | MANDATORY | What was detected and when | PowerShell encoded command observed on FIN-WS-12 at 03:14 UTC. Parent process WINWORD.EXE. |
| Alert ID / Rule Name | MANDATORY | SIEM or EDR alert reference | SIEM-RULE-PS-ENC-001 |
| Alert Details | MANDATORY | Raw alert or summary | Base64 encoded command: [value] |
| Related Alerts | RECOMMENDED | Linked alert IDs | SIEM-ALT-20260525-0042 |
| Attack Vector | RECOMMENDED | Initial access method | Email attachment |
| MITRE ATT&CK Technique | RECOMMENDED | Relevant technique | T1059.001 – PowerShell |
| Kill Chain Phase | RECOMMENDED | Current phase | Execution |

---

## 5.7 Investigation Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Investigation Notes | MANDATORY | Chronological analyst actions | [Timestamp UTC] – [Analyst] – [Action] – [Finding] |
| Tools Used | RECOMMENDED | Tools and queries used | SIEM KQL query, EDR process tree |
| Evidence References | MANDATORY | Links to evidence artifacts | /evidence/INC-2026-0001/memory-dump.raw |
| IOCs Identified | MANDATORY-CONDITIONAL | If IOCs found | IP: 185.220.x.x, Hash: [value] |
| Timeline of Events | MANDATORY-CONDITIONAL | For P1/P2 incidents | Chronological event log |
| Hypothesis | RECOMMENDED | Current analyst assessment | Possible BEC via phishing email |
| Confirmed TTP | RECOMMENDED | Confirmed techniques | T1078 – Valid Accounts |

---

## 5.8 Containment Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Containment Actions Taken | MANDATORY-CONDITIONAL | If containment performed | Host isolated via EDR at 04:00 UTC |
| Containment Executed By | MANDATORY-CONDITIONAL | Who performed containment | IR Team – D.Patel |
| Containment Authorized By | MANDATORY-CONDITIONAL | Who approved action | SOC Manager – K.Singh |
| Containment Timestamp (UTC) | MANDATORY-CONDITIONAL | When containment executed | 2026-05-25T04:00:00Z |
| Containment Outcome | MANDATORY-CONDITIONAL | Result of containment | Host successfully isolated |
| Systems Isolated | MANDATORY-CONDITIONAL | Isolated asset list | FIN-WS-12 |
| Accounts Disabled | MANDATORY-CONDITIONAL | Disabled account list | jsmith |
| Firewall Rules Applied | MANDATORY-CONDITIONAL | Block rules added | IP 185.220.x.x blocked |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 5.9 Resolution and Eradication Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Eradication Actions | MANDATORY-CONDITIONAL | Steps taken to remove threat | Malware removed, persistence cleared |
| Validation Performed | MANDATORY | How clean state confirmed | EDR clean scan, no IOC match |
| Root Cause | MANDATORY-CONDITIONAL | Identified root cause | Phishing email with macro-enabled attachment |
| Resolution Summary | MANDATORY | What was done to resolve | Full summary of actions |
| Outstanding Actions | RECOMMENDED | Remaining tasks | Patch KB5001234 pending |
| Post-Incident Ticket | MANDATORY-CONDITIONAL | RCA/PIR ticket reference | PIR-2026-0001 |

---

## 5.10 Closure Fields

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Closure Reason Code | MANDATORY | Standardized code | TP-CONTAINED |
| Closure Summary | MANDATORY | Full closure narrative | Threat confirmed and contained. Evidence preserved. No further activity. |
| False Positive Category | MANDATORY-CONDITIONAL | If FP – category | FP-IT / FP-TOOL |
| Lessons Learned Reference | RECOMMENDED | Link to lessons learned | LL-2026-0001 |
| Closed By | MANDATORY | Who closed the ticket | SOC Lead – J.Smith |
| Closure Approved By | MANDATORY | Who approved closure | IR Team Lead – D.Patel |
| Closure Time (UTC) | MANDATORY | Formal closure timestamp | 2026-05-25T07:00:00Z |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

# 6. MSSP-Specific Fields

For all MSSP-managed client tickets the following additional fields are mandatory:

| Field Name | Classification | Description | Format / Example |
|---|---|---|---|
| Client ID | MANDATORY | Unique client identifier | CLIENT-ABC-001 |
| Client Name | MANDATORY | Client organization name | ABC Bank Ltd |
| Client Environment | MANDATORY | Production / DR / Dev | Production |
| Client SLA Tier | MANDATORY | Gold / Silver / Bronze | Gold |
| Client Notification Time (UTC) | MANDATORY-CONDITIONAL | When client was notified | 2026-05-25T03:45:00Z |
| Client Notified Contact | MANDATORY-CONDITIONAL | Who was notified | John Doe – CISO ABC Bank |
| Client Notification Method | MANDATORY-CONDITIONAL | How notified | Phone + Email |
| Client Response Documented | MANDATORY-CONDITIONAL | Client instruction received | Client approved isolation |
| Regulatory Notification Required | MANDATORY | Yes / No | Yes |
| Regulatory Body | MANDATORY-CONDITIONAL | If yes – which body | RBI / CERT-In |
| Report Reference | MANDATORY-CONDITIONAL | Regulatory report ID | RBI-RPT-2026-001 |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 7. Investigation Notes Format Standard

All investigation notes must follow this format:
[YYYY-MM-DD HH:MM UTC] – [Analyst Name / Role] – [Action Taken] – [Finding / Result]


---

## 7.1 Good Investigation Note Examples
[2026-05-25 03:18 UTC] – R.Sharma / L1 – Reviewed SIEM alert SIEM-RULE-PS-ENC-001
on host FIN-WS-12. Parent process WINWORD.EXE. User jsmith (standard user).
Assessed as TP. Escalating to L2.

[2026-05-25 03:35 UTC] – A.Kumar / L2 – Reviewed EDR process tree on FIN-WS-12.
PowerShell spawned from WINWORD.EXE with base64 encoded command.
Decoded command: [value]. Contacted threat intel – IOC match confirmed.
Escalating to L3 for forensic analysis.


---

## 7.2 Poor Investigation Note Examples (Do Not Use)
Looks suspicious. Escalated.
Checked and closed.
No issues found.


---

# 8. Ticket Title Standards

| Format | Example |
|---|---|
| `[Priority] – [Alert Type] – [Host/User]` | `P2 – Encoded PowerShell – FIN-WS-12` |
| `[Priority] – [Incident Type] – [Client]` | `P1 – Ransomware – ClientABC` |
| `[Priority] – [Category] – [Asset]` | `P3 – Suspicious LOLBin – SRV-DC-01` |
| `[Priority] – [Threat] – [Environment]` | `P1 – Data Exfiltration – Production` |

---

# 9. Common Field Errors and Corrections

| Error | Risk | Correction |
|---|---|---|
| Generic title like "Alert #1234" | Investigation confusion | Use descriptive title standard |
| Missing detection time | SLA tracking failure | Always record from alert |
| No affected user documented | Investigation gap | Always include user context |
| Missing escalation timestamp | Audit gap | Record exact UTC time |
| Containment with no authorization | Compliance risk | Always document approver |
| Closure reason not coded | Metrics failure | Use standard closure codes |
| MSSP client ID missing | Data segregation risk | Mandatory for all client tickets |
| Investigation notes without timestamps | Audit failure | Use standard note format |

---

# 10. Field Completion by Ticket Stage

| Stage | Fields Required |
|---|---|
| Ticket Creation | ID, Title, Type, Category, Detection Source, Affected Assets, User, Priority, Detection Time, Creation Time, Assigned To, Initial Description |
| Triage | Investigation Notes, Related Alerts, FP/TP Decision, Escalation fields if applicable |
| Investigation | Investigation Notes, Tools Used, Evidence References, IOCs, Timeline (P1/P2) |
| Containment | Containment Actions, Executed By, Authorized By, Timestamp, Outcome |
| Resolution | Eradication Actions, Validation, Root Cause, Resolution Summary |
| Closure | Closure Reason Code, Closure Summary, Closed By, Approved By, Closure Time |

---

# 11. Related Documents

| Document | Path |
|---|---|
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Priority Matrix | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Client Environment Profile | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md` |

---

# 12. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**