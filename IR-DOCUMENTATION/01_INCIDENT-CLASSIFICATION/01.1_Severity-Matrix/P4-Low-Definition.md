# P4 – Low Severity Incident Definition

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | P4 Low Severity Definition |
| Document ID | IR-CLS-005 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the criteria, triggers, examples,
response requirements, and handling procedures for a
**P4 – Low** severity incident.

P4 represents the lowest severity level in the IR
classification framework. It covers informational,
low-risk, and policy-level alerts that require
documentation and basic triage but do not require
urgent investigation or escalation.

---

## 3. Definition

A **P4 – Low** incident is defined as any security event that:

- Has **no confirmed malicious activity** or confirmed
  operational impact
- Is **informational** or represents a **minor policy
  violation**
- Requires **basic triage and documentation** only
- Has **no data, service, or regulatory risk**
- May be **batched and handled** during low-activity
  periods

---

## 4. P4 Classification Criteria

ALL of the following conditions apply:

| Dimension | P4 Criteria |
|-----------|-------------|
| Business Impact | No operational impact |
| Scope | Single alert, single asset, single user |
| Data | No sensitive data involved or at risk |
| Threat Activity | Blocked/prevented; no confirmed execution |
| Availability | No service disruption |
| Regulatory | No regulatory notification required |

---

## 5. P4 Trigger Scenarios

### 5.1 Blocked Security Events
- Phishing email blocked by email security gateway
  (no user interaction)
- Malicious URL blocked by web proxy
- Malicious file blocked by EDR/AV before execution
- Firewall blocked outbound connection to known bad IP
- IDS/IPS blocked known attack signature (no success)

### 5.2 Informational Alerts
- Threat intelligence match on historical/passive IoC
- SIEM informational rule triggered (no action needed)
- EDR low-confidence behavioral alert (PUA/Adware)
- Cloud audit log informational entry
- Certificate expiry warning (non-critical)

### 5.3 Minor Policy Violations
- Unauthorized software detected (low risk/non-malicious)
- USB device plugged in (monitoring only policy)
- Employee accessing social media (policy block logged)
- Non-corporate device attempted network connection
- Personal email client configured on corporate device

### 5.4 Reconnaissance / Probing (No Success)
- External port scan (no successful connection)
- Web crawler/bot accessing public-facing website
- Login page brute force (all attempts blocked)
- Directory traversal attempt (no success, WAF blocked)
- Vulnerability scanner signature on perimeter (no success)

### 5.5 Routine / Known Activity
- Authorized penetration test generating alerts
  (documented and approved)
- Known vulnerability scanner running scheduled scan
- IT admin performing authorized privileged actions
  (alert generated due to detection rule)
- Scheduled script running with expected behavior
- Known false positive pattern pending tuning

### 5.6 User-Reported Low Risk Events
- User reports suspicious email (already blocked)
- User reports unusual pop-up (cleared by restart)
- User reports slow device (no malware indicator found)
- User reports unfamiliar login prompt (confirmed system update)

### 5.7 Cloud – Informational
- Routine cloud API call logged as alert
- Non-critical IAM permission change by authorized admin
- Cloud security posture management (CSPM) low-severity finding
- Non-sensitive S3/Blob storage access log alert

---

## 6. P4 SLA Requirements

| SLA Metric | Target |
|------------|--------|
| L1 Triage | ≤ 30 minutes |
| Initial Review | Within current shift |
| Escalation (if needed) | ≤ 1 hour |
| Resolution Target | ≤ 72 hours |
| Ticket Closure | ≤ 5 business days |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 7. Response Actions (P4)

### Triage (L1)
- [ ] Review alert in SIEM/EDR/Ticketing
- [ ] Validate alert context:
  - Is the activity confirmed blocked/prevented?
  - Is there any execution or access confirmed?
  - Is there any lateral movement indication?
  - Is any sensitive data involved?
- [ ] If all answers are NO → classify as P4
- [ ] Create ticket or tag existing alert as P4
- [ ] Document:
  - Alert source
  - Alert type
  - Asset/user involved
  - Disposition (false positive / blocked / informational)
  - Action taken (none required / tuning request)

### Handling Options
Based on triage findings choose one:

| Disposition | Action |
|-------------|--------|
| Confirmed False Positive | Close ticket; raise tuning request |
| Confirmed Blocked/Prevented | Close ticket; note in daily report |
| Informational (no action) | Close ticket; note in trend tracker |
| Policy violation | Close ticket; notify HR/manager if repeat |
| Pending tuning | Log in detection tuning backlog |
| Authorized activity | Close ticket; whitelist if appropriate |

### Escalation to P3 (if needed)
Escalate to P3 if during triage:
- Execution is confirmed (not just blocked)
- Multiple hosts showing same alert
- User interaction confirmed (phishing click etc.)
- Any anomalous post-alert activity detected

---

## 8. Escalation Path (P4)
L1 Analyst

↓ (only if P3/P2 criteria identified)

SOC Lead → Reclassify upward


P4 does NOT require SOC Lead approval for closure
UNLESS it is being upgraded.

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md`

---

## 9. Upgrade to P3 / P2 Criteria

Upgrade P4 immediately when ANY of the following occur:

| Condition | Upgrade To |
|-----------|-----------|
| Execution confirmed (not just blocked) | P3 |
| Multiple hosts affected | P3 |
| User credentials entered on phishing page | P2 |
| Successful brute force confirmed | P2 |
| Sensitive data accessed | P2 |
| Lateral movement indicators found | P2 |

---

## 10. Communication Requirements (P4)

| Stakeholder | Notification Required |
|-------------|----------------------|
| SOC Lead | Ticket update only (no direct notification) |
| L2 Analyst | Not required unless escalating |
| Management | Not required |
| MSSP Client | Not required (included in monthly summary) |

---

## 11. Evidence Requirements (P4)

Minimum documentation:

- [ ] Alert source and alert name
- [ ] Asset/user identified
- [ ] Timestamp of alert
- [ ] Disposition selected and reason
- [ ] Action taken (none/tuning request/whitelist)

> No forensic collection required for P4 unless
> upgrading to P3+

---

## 12. Batch Handling (P4)

P4 alerts that are repetitive may be batched:

- Group same-type alerts from same source into
  single ticket
- Document count and timeframe
- Note tuning request if needed
- Review in monthly alert tuning meeting

Example batch ticket note:
BATCH P4 – [Alert Name]
Count: 47 alerts
Period: 14-May-2026 00:00 to 23:59
Source: Email Gateway
Disposition: All blocked; no user interaction confirmed
Action: Tuning request raised – TUN-2026-044


---

## 13. False Positive Handling

P4 is the primary tier for false positive management.

| Step | Action |
|------|--------|
| Confirm FP | Validate through investigation context |
| Document | Note in ticket why it is an FP |
| Close ticket | Disposition = False Positive |
| Tuning request | Raise tuning ticket if recurring FP |
| Whitelist | Only with SOC Lead approval |
| Track | Log in monthly FP rate metric |

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md`

---

## 14. MITRE ATT&CK Common Techniques (P4 Context)

| Tactic | Common Techniques (Blocked/Prevented) |
|--------|--------------------------------------|
| Reconnaissance | T1595 (Active Scanning – external) |
| Initial Access | T1566 (Phishing – blocked before delivery) |
| Execution | T1204 (User Execution – prevented) |
| Defense Evasion | T1027 (Obfuscated Files – detected, not executed) |
| Discovery | T1046 (Network Service Scanning – blocked) |

---

## 15. Detection Tuning Integration

P4 alerts are the primary driver for detection tuning.

| Scenario | Action |
|----------|--------|
| Recurring P4 from same source/rule | Raise tuning request |
| Known authorized activity triggering P4 | Whitelist request (approved) |
| P4 rule with >50 alerts/day | Priority tuning review |
| P4 that consistently upgrades to P3 | Reclassify rule as P3 baseline |

Tuning requests tracked in:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

## 16. Reporting (P4)

P4 incidents are included in:

| Report | Frequency |
|--------|-----------|
| Daily SOC Report | Alert count by category |
| Weekly Incident Summary | P4 volume and FP rate |
| Monthly Metrics Report | FP rate trend; tuning actions |
| MSSP Client Monthly Report | Summary only (no detail) |

Reference:
`07_REPORTING/07.2_Operational-Reports/`

---

## 17. Related Documents

| Document | Path |
|---------|------|
| Severity Classification Guide | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md |
| P3 Medium Definition | 01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P3-Medium-Definition.md |
| False Positive Handling | 01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md |
| L1 Alert Handling SOP | 03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md |
| SIEM Alert Tuning Guide | 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md |
| Internal SLA Definitions | 00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md |

---

## 18. Review & Update

This document shall be reviewed:
- Quarterly
- When FP rate exceeds 30% threshold
- Upon new detection rule deployment
- Upon SOC tooling changes

---

## 19. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**