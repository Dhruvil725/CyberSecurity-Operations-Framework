# Master Triage Decision Tree (SOC Alert Handling)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Master Triage Decision Tree |
| Document ID | IR-TRIAGE-001 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document provides the authoritative triage decision process used by SOC Analysts (L1/L2/L3) and SOC Leads to:

- qualify alerts as incidents (or non-incidents)
- assign priority and severity (P1–P4)
- determine escalation requirements
- standardize ticket documentation and evidence capture
- minimize false positives while preventing delayed escalation

---

## 3. Scope

Applies to:
- SIEM alerts
- EDR alerts
- Firewall/IDS/WAF alerts
- Cloud/SaaS security alerts
- User-reported security events
- Threat intelligence-driven indicators (IOC matches)

This process is used for:
- Enterprise internal SOC operations
- MSSP client operations (with additional multi-client requirements)

---

## 4. Roles and Responsibilities (Triage Context)

| Role | Primary Responsibilities During Triage |
|------|----------------------------------------|
| L1 SOC Analyst | Validate alert, gather initial context, create ticket, apply initial classification and severity recommendation |
| L2 SOC Analyst | Deep investigation, confirm incident, scope impact, recommend containment and escalation |
| L3 SOC Analyst | Advanced analysis, forensics guidance, threat hunting, TTP/MITRE mapping support |
| SOC Lead | Owns triage quality, approves major reclassification, coordinates response, triggers bridge calls and management notifications |
| IR Team | Engaged for P1/P2 major incidents and coordinated containment/eradication/recovery |
| IT / Network / IAM | Executes technical changes (account disables, firewall blocks, isolation) per authority matrix and change control |

Reference: `00_GOVERNANCE/00.3_Roles-and-Responsibilities/`

---

## 5. Triage Inputs (Minimum Data Required)

Before making a disposition decision, capture the following minimum data in the ticket:

### 5.1 Alert Metadata (Mandatory)
- Alert source (SIEM / EDR / WAF / firewall / cloud)
- Rule name / detection name
- Time detected (UTC) and time observed
- Affected asset(s): hostname, IP, user
- Detection evidence: log snippets, EDR telemetry summary, WAF request sample
- Initial severity recommendation (P1–P4) and justification
- Related incidents or alert clusters (if any)

### 5.2 Environment Context (As Available)
- Asset criticality (business critical vs standard)
- Asset owner / business unit
- Exposure (internet-facing / internal / restricted)
- Known maintenance/change windows (if applicable)

---

## 6. Triage Disposition Outcomes (Standard)

Every alert must end in one of these outcomes:

| Disposition | Description | Ticket Status |
|------------|-------------|--------------|
| Confirmed Incident | Malicious activity confirmed and requires IR handling | Incident Open |
| Suspected Incident | Strong indicators; requires deeper investigation | Incident Open |
| Benign True Positive | Alert is valid but activity is legitimate/authorized | Closed |
| False Positive | Detection fired incorrectly or due to misconfiguration | Closed |
| Informational | Not actionable; record for trend metrics | Closed |
| Duplicate | Already tracked under an existing ticket/incident | Closed (linked) |

---

## 7. Master Triage Decision Process (Step-by-Step)

### Step 1: Validate Alert Integrity
Decision questions:
1. Is the alert complete (has asset, user, timestamp, evidence)?
2. Is the log source healthy (no ingestion gaps, no parsing errors)?
3. Is this alert part of an outage/noise event (tool malfunction, SIEM backlog, known issue)?

Actions:
- If tool issue suspected, create a tooling ticket and annotate security ticket accordingly.
- If alert is incomplete, enrich using available telemetry (EDR, CMDB, DNS/proxy, identity logs).

Output:
- Alert is either valid for triage or flagged as tooling/data issue.

---

### Step 2: Determine Authorization / Expected Activity
Decision questions:
1. Is the activity part of an approved change, pentest, vulnerability scan, or administrative task?
2. Does the user/host normally perform this activity?
3. Is there an approved ticket/change record that matches the activity?

Actions:
- If authorized and fully explained, disposition as Benign True Positive and close.
- If partially explained or uncertain, proceed to Step 3.

Output:
- Authorized vs unauthorized status (preliminary).

---

### Step 3: Determine Likelihood of Malicious Activity
Evaluate indicators across four areas:

#### 3.1 Identity Indicators
- unusual login location or device
- impossible travel or concurrent sessions
- abnormal MFA prompts or MFA method changes
- new privileged assignments or group membership changes

#### 3.2 Endpoint Indicators
- suspicious parent-child process chain
- LOLBin abuse (PowerShell, mshta, rundll32, regsvr32) in abnormal context
- persistence artifacts (tasks, services, run keys)
- security tool tampering indicators

#### 3.3 Network Indicators
- C2-like beaconing pattern
- unusual outbound ports/destinations
- internal east-west scanning or SMB/RDP spread
- exfiltration-like traffic patterns

#### 3.4 Data Indicators
- mass access to sensitive repositories
- creation of large archives prior to transfer
- external sharing/forwarding rules
- DLP triggers (if available)

Actions:
- If multiple strong indicators exist, escalate severity recommendation and proceed to Step 4.
- If weak indicators only, proceed to Step 4 but likely P3/P4.

Output:
- Malicious likelihood rating (Low / Medium / High).

---

### Step 4: Determine Impact and Scope
Decision questions:
1. Is a business-critical system affected?
2. How many assets/users are affected (single vs multiple)?
3. Is there evidence of lateral movement?
4. Is sensitive/regulatory data involved or at risk?
5. Is the activity ongoing (active threat) or historical?

Actions:
- Scope initial affected assets (minimum) using:
  - EDR search
  - SIEM correlation
  - identity log correlation
  - proxy/firewall correlation

Output:
- Impact rating (Low / Medium / High / Critical)
- Scope rating (Single / Limited / Broad)

---

### Step 5: Assign Severity (P1–P4)
Severity must be assigned using the Severity Matrix.

Reference:
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md`

Required ticket fields:
- Selected severity
- Reasoning (impact + scope + data + threat activity)
- Any escalation trigger met (yes/no)

---

### Step 6: Decide Escalation Path
Use this escalation logic:

| Condition | Escalate To | Time Requirement |
|----------|-------------|------------------|
| P1 declared or likely | SOC Lead + IR Team | Immediately |
| P2 declared | SOC Lead + L2 | Immediately |
| P3 suspicious and needs deeper validation | L2 | Within SLA window |
| Privileged account suspected | SOC Lead + L2/L3 | Immediately |
| Data exfiltration suspected | SOC Lead + IR Team (if P1/P2) | Immediately |
| Malware execution suspected | L2 (and L3 if required) | Immediately |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

### Step 7: Evidence Preservation (Triage-Level)
Minimum evidence to attach in ticket before closure or escalation:

- SIEM raw logs (export or screenshot + query used)
- EDR alert details (process tree, hash, network connections)
- Identity evidence (sign-in logs, failed/success patterns)
- Network evidence (proxy/firewall logs, DNS logs)
- User report evidence (email headers, screenshots) if applicable

For P1/P2 incidents:
- initiate chain-of-custody where required

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

### Step 8: Final Triage Decision
Choose one of the dispositions (Section 6) and document:

- What happened (summary)
- What was affected (assets, accounts)
- What evidence supports decision
- What actions were taken (block, isolate, reset)
- Next steps (escalation, monitoring, tuning)

---

## 8. Triage Quality Checklist (Mandatory)

Before closing or escalating, verify:

- Ticket has all required fields populated
- Severity is justified with evidence
- Any escalation trigger is acknowledged
- Related alerts are linked (duplicates/campaigns)
- Evidence attachments are included
- Communication requirements are met (P1/P2)

---

## 9. Triage “Stop and Escalate Immediately” Triggers

Escalate immediately to SOC Lead (and IR Team as required) if any are true:

- ransomware behavior or encryption indicators
- confirmed C2 beaconing from server or privileged host
- domain controller or identity system involved
- confirmed data exfiltration indicators
- privileged account compromise suspected/confirmed
- security tool tampering confirmed (EDR disabled, logs cleared)
- multiple hosts affected in short time window
- any situation likely to become P1 within the next hour

---

## 10. Metrics Captured from Triage

Record these for SLA/SLO reporting:

- time received
- time triage started
- time triage completed
- time escalated (if escalated)
- severity assigned and any reclassification
- disposition type (FP/BTP/Incident/etc.)

Reference:
- `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`
- `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 11. Related Documents

| Document | Path |
|---------|------|
| Alert-to-Incident Qualification | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Alert-to-Incident-Qualification.md` |
| False Positive Handling | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md` |
| Multi-Client Triage (MSSP) | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Escalation Paths | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |
| Ticketing Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**