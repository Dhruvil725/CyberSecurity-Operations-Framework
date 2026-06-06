# P2 – High Severity Incident Definition

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | P2 High Severity Definition |
| Document ID | IR-CLS-003 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the criteria, triggers, examples, response
requirements, and escalation obligations for a **P2 – High**
severity incident.

P2 is the second highest severity level. It represents a
significant security threat that requires urgent investigation
and coordinated response but has not yet reached the
enterprise-wide impact level of a P1.

---

## 3. Definition

A **P2 – High** incident is defined as any security event that:

- Represents a **significant and confirmed** threat to
  organizational or client systems, data, or operations
- Requires **urgent L2 investigation** and likely containment
- May **escalate to P1** if scope expands
- Needs **management notification** within 30 minutes
- May have **regulatory implications** if not contained

---

## 4. P2 Classification Criteria

ONE OR MORE of the following conditions apply:

| Dimension | P2 Criteria |
|-----------|-------------|
| Business Impact | Non-critical service degraded; partial operational disruption |
| Scope | Single server or limited user set confirmed compromised |
| Data | Internal confidential data at risk; potential but unconfirmed exfiltration |
| Threat Activity | Malware execution; privilege escalation; successful credential compromise |
| Availability | Non-critical service disruption due to security event |
| Regulatory | Regulatory implication possible but not yet confirmed |

---

## 5. P2 Trigger Scenarios

The following scenarios trigger P2 classification:

### 5.1 Malware Execution
- Confirmed malware execution on endpoint(s)
- Trojan/RAT detected and active on host
- Crypto-miner deployed on server(s)
- Worm-like propagation suspected but not confirmed
- Macro-based malware executed via phishing email

### 5.2 Privilege Escalation
- Standard user escalated to local admin without authorization
- Non-admin account accessing admin shares
- Suspicious use of PsExec/WMI/PowerShell by non-admin
- Service account used interactively

### 5.3 Credential Compromise
- Single privileged account credential confirmed compromised
- Successful brute force on admin account
- Password spray success on multiple standard accounts
- Credential reuse attack succeeding on internal systems
- MFA bypass attempt confirmed successful

### 5.4 Phishing – User Interaction Confirmed
- User clicked phishing link and entered credentials
- Phishing email with malicious attachment opened
- OAuth consent granted to malicious application
- Callback to phishing infrastructure confirmed

### 5.5 Web Application Attack – Partial Success
- SQL injection attempt with partial data access confirmed
- Authentication bypass on web application
- File upload vulnerability exploited
- Admin panel accessed without authorization

### 5.6 Suspicious Lateral Movement (Early Stage)
- Suspicious RDP/SMB connections between internal hosts
- Pass-the-hash or Pass-the-ticket suspected
- Unusual service account lateral movement
- Reconnaissance tools (BloodHound/ADRecon) detected

### 5.7 Data at Risk (Unconfirmed Exfiltration)
- Large internal file transfers to unusual locations
- Cloud sync tool uploading large volumes externally
- Anomalous database query volumes
- Sensitive data accessed by unauthorized user

### 5.8 Cloud – High Impact (Non-Critical)
- Non-admin cloud account compromise
- Unusual API calls to cloud management plane
- Cloud resource modification by unauthorized identity
- Security group changes exposing non-critical assets

### 5.9 Insider Activity – Suspected
- Authorized user accessing data outside normal patterns
- Mass download of files by single user
- After-hours access to sensitive systems by employee

---

## 6. P2 SLA Requirements

| SLA Metric | Target |
|------------|--------|
| L1 Triage | ≤ 10 minutes |
| L2 Escalation | ≤ 15 minutes |
| L2 Acknowledgement | ≤ 10 minutes |
| L3 Escalation (if needed) | ≤ 30 minutes |
| Management Notification | ≤ 30 minutes from declaration |
| Client Notification (MSSP) | ≤ 30 minutes from declaration |
| Initial Containment Action | ≤ 2 hours |
| Status Update Cadence | Every 1 hour |
| Resolution Target | ≤ 8 hours (containment) |
| Final Incident Report | ≤ 48 hours post closure |
| Post Incident Review | ≤ 5 business days |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7. Mandatory Response Actions (P2)

### Immediate (0–15 minutes)
- [ ] L1 creates P2 ticket with full details
- [ ] L1 notifies SOC Lead via ticket + direct message
- [ ] SOC Lead acknowledges and assigns L2
- [ ] L2 begins investigation immediately
- [ ] SOC Lead notifies Management (within 30 mins)
- [ ] SOC Lead notifies MSSP client (if applicable)

### Short Term (15 minutes – 2 hours)
- [ ] L2 confirms scope and affected assets
- [ ] L2 enriches with TI and MITRE mapping
- [ ] Containment strategy recommended
- [ ] Containment approved and executed
- [ ] Evidence collection initiated
- [ ] Status update sent every 1 hour

### Medium Term (2–8 hours)
- [ ] Containment confirmed
- [ ] Eradication steps defined
- [ ] Recovery planning initiated
- [ ] Assess upgrade to P1 if scope expands
- [ ] Regulatory impact assessed

---

## 8. Escalation Path (P2)
L1 Analyst

↓ (≤ 15 mins)

L2 Analyst

↓ (if needed ≤ 30 mins)

L3 Analyst

↓ (if P1 triggers met)

IR Team + SOC Lead
↓

Management / CISO (≤ 30 mins from declaration)


Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md`

---

## 9. Upgrade to P1 Criteria

Immediately upgrade P2 to P1 if ANY of the following occur:

| Condition | Action |
|-----------|--------|
| Lateral movement confirmed beyond initial host | Upgrade to P1 |
| Domain Controller or AD compromise detected | Upgrade to P1 |
| Ransomware encryption begins | Upgrade to P1 |
| Confirmed sensitive data exfiltration | Upgrade to P1 |
| Multiple privileged accounts compromised | Upgrade to P1 |
| Business-critical service goes offline | Upgrade to P1 |
| Regulatory notification confirmed required | Upgrade to P1 |

All upgrades require SOC Lead approval and ticket note with
timestamp and justification.

---

## 10. Communication Requirements (P2)

| Stakeholder | Method | Timeline | Template |
|-------------|--------|----------|---------|
| SOC Lead | Direct message/Teams | Immediately | Verbal |
| Management/CISO | Email + call | ≤ 30 minutes | Management-Notification-Template.md |
| MSSP Client | Email + Portal | ≤ 30 minutes | MSSP-Client-Notification-Template.md |
| Ongoing Status Updates | Email + Ticket | Every 1 hour | Status-Update-Template-1hr.md |

---

## 11. Evidence Requirements (P2)

Minimum evidence to be collected for all P2 incidents:

- [ ] SIEM log export (relevant timeframe)
- [ ] EDR telemetry for affected hosts
- [ ] Authentication/AD logs
- [ ] Network connection logs
- [ ] Email logs (if phishing involved)
- [ ] Process execution logs
- [ ] Relevant file hashes and artifacts
- [ ] Chain-of-custody initiated (if forensic collection needed)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 12. Regulatory Assessment (P2)

Assess during every P2:

| Question | Yes/No | Action |
|----------|--------|--------|
| Could this involve customer data? | | Notify GRC proactively |
| Is scope expanding rapidly? | | Prepare for upgrade to P1 |
| Is a regulated client affected (MSSP)? | | Assess client SLA notification |
| Is financial system impacted? | | Notify GRC/Legal |

---

## 13. MITRE ATT&CK Common Techniques (P2 Context)

| Tactic | Common Techniques |
|--------|------------------|
| Initial Access | T1566 (Phishing), T1078 (Valid Accounts), T1190 (Exploit Public App) |
| Execution | T1059 (Scripting Interpreter), T1204 (User Execution) |
| Persistence | T1053 (Scheduled Task), T1547 (Registry Autostart) |
| Privilege Escalation | T1068 (Exploitation), T1078.003 (Local Account) |
| Defense Evasion | T1055 (Process Injection), T1112 (Registry Modification) |
| Credential Access | T1110 (Brute Force), T1555 (Credentials from Password Stores) |
| Discovery | T1018 (Remote System Discovery), T1087 (Account Discovery) |
| Lateral Movement | T1021 (Remote Services), T1550 (Use Alt Auth Material) |
| Collection | T1114 (Email Collection), T1560 (Archive Collected Data) |

---

## 14. Downgrade Criteria

P2 may be downgraded when:

| Condition | Downgrade To |
|-----------|-------------|
| Confirmed false positive | P4 (close) |
| Scope confirmed single endpoint, no data risk | P3 |
| Activity confirmed authorized after investigation | P4 (close) |
| Threat fully contained, no persistence evidence | P3 |

All downgrades require SOC Lead approval and ticket note.

---

## 15. Post-Incident Requirements (P2)

- [ ] Post Incident Review (PIR) within 5 business days
- [ ] Root Cause Analysis (RCA) documented
- [ ] Lessons Learned registered
- [ ] Corrective actions assigned with owners/dates
- [ ] Incident report delivered within 48 hours post closure
- [ ] Detection improvements reviewed
- [ ] Playbook reviewed for gaps

Reference:
`08_POST-INCIDENT/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Severity Classification Guide | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md |
| P1 Critical Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md |
| P3 Medium Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P3-Medium-Definition.md |
| Severity Escalation Criteria | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md |
| L2 to L3 Escalation | 05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md |
| Internal SLA Definitions | 00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md |
| Evidence Collection SOP | 06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md |

---

## 17. Review & Update

This document shall be reviewed:
- Quarterly
- After every P2 incident that escalated to P1
- Upon changes to regulatory requirements
- Upon SOC tooling or process changes

---

## 18. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document** 