# P1 – Critical Severity Incident Definition

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | P1 Critical Severity Definition |
| Document ID | IR-CLS-002 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the criteria, triggers, examples, response
requirements, and escalation obligations for a **P1 – Critical**
severity incident.

P1 is the highest severity level in the IR classification framework.
It requires immediate activation of all response resources and
mandatory executive notification.

---

## 3. Definition

A **P1 – Critical** incident is defined as any security event that:

- Has caused or is actively causing **severe harm** to business
  operations, data confidentiality, or service availability
- Requires **immediate coordinated response** from SOC, IR Team,
  and Management
- Cannot be contained by routine SOC operations alone
- Has **regulatory reporting implications** (RBI/CERT-In)

---

## 4. P1 Classification Criteria

ALL or MULTIPLE of the following conditions apply:

| Dimension | P1 Criteria |
|-----------|-------------|
| Business Impact | Critical business service disrupted or at risk of imminent disruption |
| Scope | Multiple systems, servers, or users affected; lateral movement detected |
| Data | Customer PII / financial data / credentials / IP confirmed compromised or at high risk |
| Threat Activity | Active malware, ransomware, active C2, confirmed exploitation in progress |
| Regulatory | Regulatory notification is likely required |
| Availability | Major service outage caused by security event |

---

## 5. P1 Trigger Scenarios

The following scenarios automatically trigger P1 classification:

### 5.1 Ransomware
- Active encryption of files detected on endpoints/servers
- Ransom note dropped in file systems
- Ransomware operator persistence detected
- Wiper malware detected and executing

### 5.2 Data Exfiltration / Breach
- Confirmed exfiltration of sensitive customer or financial data
- Large-scale data transfers to external/unknown destinations
- Database dump activity detected with external transfer
- Cloud storage bucket exposure with sensitive data confirmed

### 5.3 Active Compromise of Critical Infrastructure
- Domain Controller (DC) or Active Directory compromise
- Enterprise admin account compromise
- SIEM, EDR, or security tool compromise
- Critical production server rootkit detected

### 5.4 Advanced Persistent Threat (APT)
- Confirmed APT actor TTPs detected
- Long-term persistent backdoor discovered
- Repeated reinfection after eradication
- Supply chain compromise affecting production

### 5.5 Critical Service Disruption
- Security-caused outage of business-critical applications
- Core banking, payment gateway, or customer portal offline
- Security-caused network outage affecting enterprise-wide operations

### 5.6 Mass Credential Compromise
- Enterprise-wide credential dump discovered
- Mass password spray success across multiple privileged accounts
- SSO/MFA provider compromise confirmed

### 5.7 Cloud Critical Incidents
- Cloud environment admin account takeover
- Mass deletion or encryption of cloud resources
- Publicly exposed cloud storage with confirmed sensitive data

---

## 6. P1 SLA Requirements

| SLA Metric | Target |
|------------|--------|
| L1 Triage | ≤ 5 minutes |
| L2 Escalation | ≤ 10 minutes |
| L2 Acknowledgement | ≤ 5 minutes |
| L3 / IR Team Escalation | ≤ 15 minutes |
| IR Team Activation | ≤ 30 minutes |
| Management Notification | ≤ 15 minutes from declaration |
| Client Notification (MSSP) | ≤ 15 minutes from declaration |
| Bridge Call Activation | ≤ 20 minutes |
| Initial Containment Action | ≤ 1 hour |
| Status Update Cadence | Every 30 minutes |
| Resolution Target | ≤ 4 hours (containment) |
| Final Incident Report | ≤ 24 hours post closure |
| Post Incident Review | ≤ 5 business days |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7. Mandatory Response Actions (P1)

### Immediate (0–15 minutes)
- [ ] L1 creates P1 ticket immediately
- [ ] L1 notifies SOC Lead directly (phone/Teams/radio)
- [ ] SOC Lead declares P1 incident
- [ ] SOC Lead activates bridge call
- [ ] SOC Lead notifies Management/CISO
- [ ] SOC Lead notifies MSSP client (if applicable)
- [ ] L2 begins deep investigation immediately
- [ ] L3 engaged for technical analysis

### Short Term (15–60 minutes)
- [ ] IR Team activated and briefed
- [ ] Incident Commander (IC) assigned
- [ ] Containment strategy defined and approved
- [ ] Containment actions executed with approvals
- [ ] Evidence collection initiated (logs/memory/disk)
- [ ] Status updates sent every 30 minutes

### Medium Term (1–4 hours)
- [ ] Containment confirmed
- [ ] Eradication planning begins
- [ ] Regulatory reporting assessed (RBI/CERT-In)
- [ ] Root cause investigation underway
- [ ] Business impact assessment completed
- [ ] External vendors/retainers engaged if required

---

## 8. Escalation Path (P1)
L1 Analyst

↓ (≤ 10 mins)

L2 Analyst

↓ (≤ 15 mins)

L3 Analyst + SOC Lead

↓ (≤ 30 mins)

IR Team (Incident Commander)

↓ (immediately)

CISO + Management

↓ (if regulatory trigger)

GRC/Compliance → RBI/CERT-In Reporting

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

## 9. Communication Requirements (P1)

| Stakeholder | Method | Timeline | Template |
|-------------|--------|----------|---------|
| SOC Lead | Direct call/Teams | Immediately | Verbal |
| Management/CISO | Call + Email | ≤ 15 minutes | Management-Notification-Template.md |
| MSSP Client | Call + Email + Portal | ≤ 15 minutes | MSSP-Client-Notification-Template.md |
| Bridge Call Participants | Calendar invite + Bridge link | ≤ 20 minutes | Bridge-Call-Agenda-Template.md |
| Ongoing Status Updates | Email + Ticket + Bridge | Every 30 minutes | Status-Update-Template-30min.md |
| Regulatory Bodies | Formal submission | Per RBI timeline | RBI-Report-Template.md |

---

## 10. Evidence Requirements (P1)

Minimum evidence to be collected for all P1 incidents:

- [ ] System memory dump (affected hosts if safe)
- [ ] Full disk image or triage image (affected hosts)
- [ ] SIEM log export (relevant timeframe + 24 hrs before)
- [ ] EDR telemetry export
- [ ] Network capture (if available)
- [ ] Authentication/AD/IAM logs
- [ ] Cloud audit logs (if applicable)
- [ ] Email logs (if phishing involved)
- [ ] Chain-of-custody form initiated

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 11. Regulatory Reporting (P1)

Assess the following during every P1 incident:

| Question | Yes/No | Action |
|----------|--------|--------|
| Is customer data compromised? | | Notify GRC/Legal immediately |
| Is financial data compromised? | | RBI reporting may be required |
| Is service availability affected? | | Assess material disruption |
| Is a regulated entity impacted? | | CERT-In notification may apply |
| Is client data exposed (MSSP)? | | Client + regulatory notification |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 12. MITRE ATT&CK Common Techniques (P1 Context)

| Tactic | Common Techniques |
|--------|------------------|
| Initial Access | T1566 (Phishing), T1190 (Exploit Public App), T1133 (External Remote Services) |
| Execution | T1059 (Command and Scripting), T1204 (User Execution) |
| Persistence | T1547 (Boot Autostart), T1053 (Scheduled Task) |
| Privilege Escalation | T1068 (Exploitation for Privilege), T1078 (Valid Accounts) |
| Defense Evasion | T1070 (Indicator Removal), T1036 (Masquerading) |
| Credential Access | T1003 (Credential Dumping), T1110 (Brute Force) |
| Lateral Movement | T1021 (Remote Services), T1570 (Lateral Tool Transfer) |
| Exfiltration | T1041 (Exfil Over C2), T1048 (Exfil Over Alt Protocol) |
| Impact | T1486 (Data Encrypted for Impact), T1489 (Service Stop) |

---

## 13. Reclassification Criteria

P1 may be **downgraded** when:

| Condition | Downgrade To |
|-----------|-------------|
| Scope confirmed limited to single endpoint | P2 |
| No sensitive data confirmed at risk | P2 |
| Threat fully contained and no persistence | P2 |
| Confirmed false positive after investigation | P4 (close) |

All reclassifications require SOC Lead approval and ticket note.

---

## 14. Post-Incident Requirements (P1)

- [ ] Post Incident Review (PIR) within 5 business days
- [ ] Root Cause Analysis (RCA) completed
- [ ] Lessons Learned registered
- [ ] Corrective actions assigned with owners/dates
- [ ] Executive summary delivered
- [ ] Final incident report delivered
- [ ] Regulatory report filed (if required)
- [ ] Detection improvements identified
- [ ] Playbook updated (if gaps found)

Reference:
`08_POST-INCIDENT/`

---

## 15. Related Documents

| Document | Path |
|---------|------|
| Severity Classification Guide | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md |
| P2 High Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md |
| Severity Escalation Criteria | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md |
| Emergency Escalation P1 SOP | 05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md |
| Internal SLA Definitions | 00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md |
| IRT Activation Criteria | 03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md |
| Evidence Collection SOP | 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md |
| RBI Reporting SOP | 05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md |

---

## 16. Review & Update

This document shall be reviewed:
- Quarterly
- After every P1 incident
- Upon changes to regulatory requirements
- Upon SOC tooling or process changes

---

## 17. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**