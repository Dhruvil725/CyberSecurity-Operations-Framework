# P3 – Medium Severity Incident Definition

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | P3 Medium Severity Definition |
| Document ID | IR-CLS-004 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the criteria, triggers, examples,
response requirements, and escalation obligations for a
**P3 – Medium** severity incident.

P3 represents suspicious or confirmed low-impact security
activity that requires investigation within the current
shift but does not demand immediate crisis-level response.

---

## 3. Definition

A **P3 – Medium** incident is defined as any security event that:

- Represents **suspicious or confirmed malicious activity**
  with limited or contained scope
- Requires **L2 investigation** within the shift
- Has **no immediate business service impact**
- Does **not** involve confirmed sensitive data compromise
- May **escalate to P2 or P1** if investigation reveals
  wider scope

---

## 4. P3 Classification Criteria

ONE OR MORE of the following conditions apply:

| Dimension | P3 Criteria |
|-----------|-------------|
| Business Impact | No immediate operational impact; isolated activity |
| Scope | Single endpoint or single user account affected |
| Data | No sensitive data confirmed at risk |
| Threat Activity | Suspicious process; anomalous behavior; policy violation |
| Availability | No service disruption |
| Regulatory | No regulatory notification required |

---

## 5. P3 Trigger Scenarios

### 5.1 Suspicious Process Execution
- Unusual PowerShell/cmd.exe spawned by Office application
- LOLBin (Living Off the Land Binary) executed without clear reason
- Script execution from temp/appdata directory
- Suspicious parent-child process relationship
- Encoded command line execution

### 5.2 Anomalous Login Activity
- Multiple failed logins followed by success (single account)
- Login from unusual geolocation (travel confirmed)
- Login at unusual hours (single user, no data access)
- Unusual login to VPN with valid credentials (unconfirmed threat)

### 5.3 Network Anomalies (Low Confidence)
- Outbound connection to suspicious domain (not confirmed C2)
- DNS query to newly registered domain from endpoint
- Unusual protocol on internal network segment
- Low-volume port scan from internal host

### 5.4 Policy Violations
- Unauthorized software installation detected
- USB device usage detected
- Shadow IT application usage (cloud storage, etc.)
- Non-compliant device accessing corporate resources

### 5.5 Phishing – No User Interaction Confirmed
- Phishing email delivered but no click/open confirmed
- Suspicious email with malicious link reported by user
- Business Email Compromise (BEC) attempt identified

### 5.6 Endpoint Alerts – Low Confidence
- AV/EDR alert on potentially unwanted application (PUA)
- EDR behavioral alert with low confidence score
- AMSI detection without execution confirmation
- Single host anomalous memory activity

### 5.7 Web Application – Reconnaissance
- Directory traversal attempts (no success)
- SQL injection probing (no data access confirmed)
- Web scanner signatures detected against public site
- Admin panel brute force (no success)

### 5.8 Account Activity – Suspicious
- Service account used at unusual hours
- Disabled account attempted login
- Dormant account suddenly active (no HR change)
- Account accessing shares outside normal pattern

### 5.9 Cloud – Low Risk Anomaly
- Unusual cloud login location (MFA passed, no suspicious activity)
- Non-critical resource permission change
- New IAM user created by admin (verify authorization)
- Cloud billing spike (potential crypto-mining investigation)

---

## 6. P3 SLA Requirements

| SLA Metric | Target |
|------------|--------|
| L1 Triage | ≤ 15 minutes |
| L2 Escalation (if needed) | ≤ 30 minutes |
| L2 Acknowledgement | ≤ 15 minutes |
| Initial Investigation Start | ≤ 4 hours |
| Status Update Cadence | Every 4 hours |
| Resolution Target | ≤ 24 hours |
| Ticket Closure | ≤ 3 business days post resolution |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7. Response Actions (P3)

### Initial (0–30 minutes)
- [ ] L1 validates alert and creates P3 ticket
- [ ] L1 documents:
  - Alert source
  - Affected asset/user
  - Timestamp
  - Initial context
- [ ] L1 determines if escalation to L2 is required
- [ ] SOC Lead informed via ticket update

### Investigation (within shift)
- [ ] L2 (or L1 if within capability) investigates:
  - Process/command line review
  - Network connection analysis
  - Authentication log review
  - File system activity
  - TI enrichment of IoCs
- [ ] Determine if activity is:
  - Confirmed malicious → Upgrade to P2
  - Suspicious but contained → Maintain P3
  - False positive → Downgrade to P4 and close

### Containment (if required)
- [ ] Isolate endpoint only if threat confirmed
- [ ] Block IoC (domain/IP/hash) if confident
- [ ] Disable account only if compromise confirmed
- [ ] All containment requires SOC Lead approval for P3

### Documentation
- [ ] Full investigation notes in ticket
- [ ] Evidence attached (screenshots/log exports)
- [ ] Resolution notes and actions taken
- [ ] Ticket closed with proper disposition

---

## 8. Escalation Path (P3)
L1 Analyst

↓ (if L2 investigation needed)

L2 Analyst

↓ (if P2/P1 criteria met)

SOC Lead → P2 or P1 declared


Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md`

---

## 9. Upgrade to P2 / P1 Criteria

Immediately upgrade P3 when ANY of the following occur:

| Condition | Upgrade To |
|-----------|-----------|
| Malware execution confirmed | P2 |
| Credential compromise confirmed | P2 |
| Lateral movement detected | P2 |
| Sensitive data accessed | P2 |
| Multiple hosts affected | P2 |
| Domain Controller involved | P1 |
| Ransomware activity detected | P1 |
| Data exfiltration confirmed | P1 |

All upgrades require SOC Lead approval and ticket note with
timestamp and justification.

---

## 10. Communication Requirements (P3)

| Stakeholder | Method | Timeline |
|-------------|--------|----------|
| SOC Lead | Ticket update | Within triage window |
| L2 Analyst | Ticket escalation | If investigation needed |
| Management | Not required unless escalated | - |
| MSSP Client | Ticket/Portal update | Per contract (usually P2+) |

---

## 11. Evidence Requirements (P3)

Minimum evidence to collect:

- [ ] SIEM alert details and raw log
- [ ] EDR alert details and process tree
- [ ] Relevant authentication logs
- [ ] Network connection logs
- [ ] Screenshots of alert console
- [ ] TI enrichment results
- [ ] Notes on investigation steps taken

---

## 12. MITRE ATT&CK Common Techniques (P3 Context)

| Tactic | Common Techniques |
|--------|------------------|
| Reconnaissance | T1595 (Active Scanning), T1598 (Phishing for Info) |
| Initial Access | T1566.001 (Spearphishing Attachment) |
| Execution | T1059.001 (PowerShell), T1059.003 (Windows CMD) |
| Persistence | T1547.001 (Registry Run Keys) |
| Defense Evasion | T1027 (Obfuscated Files), T1036 (Masquerading) |
| Discovery | T1087 (Account Discovery), T1083 (File Discovery) |
| Collection | T1025 (Data from Removable Media) |

---

## 13. Downgrade to P4 Criteria

P3 may be downgraded when:

| Condition | Action |
|-----------|--------|
| Activity confirmed authorized | Close as P4 |
| Confirmed false positive | Close as P4 |
| No malicious indicators found | Close as P4 |
| Known vulnerability scanner or pentest | Close as P4 with note |

All downgrades require SOC Lead review for P3 closures.

---

## 14. Batch Handling (P3)

For recurring P3 alerts of the same type within a shift:

- Group into single ticket with reference alerts noted
- Investigate root cause once (if pattern exists)
- Document in shift handover
- If pattern repeats across days → review detection tuning
- If pattern indicates campaign → upgrade to P2

---

## 15. Post Incident (P3)

- [ ] Ticket closed with full disposition
- [ ] Included in weekly incident summary
- [ ] Recurring P3 patterns flagged for tuning review
- [ ] No PIR required unless escalated to P2+

Reference:
`07_REPORTING/07.2_Operational-Reports/Weekly-Incident-Summary.md`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Severity Classification Guide | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md |
| P2 High Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md |
| P4 Low Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P4-Low-Definition.md |
| L1 Alert Handling SOP | 03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md |
| False Positive Handling | 01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md |
| Internal SLA Definitions | 00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md |

---

## 17. Review & Update

This document shall be reviewed:
- Quarterly
- After significant pattern of P3→P2 escalations
- Upon changes to detection use cases
- Upon SOC tooling changes

---

## 18. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**