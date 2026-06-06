# Bridge Call Agenda Template (P1/P2 Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Bridge Call Agenda (P1/P2) |
| Document ID | COM-TPL-001 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template provides a standardized **bridge call agenda** for coordinating P1/P2 security incidents.

A structured bridge call is critical because:

- It establishes incident command and decision authority early
- It reduces confusion and duplicated work during high-pressure events
- It ensures time-bound actions aligned to SLA/SLO targets
- It ensures consistent stakeholder communication and documentation
- It creates an audit-ready decision trail (who approved what, when, and why)
- It supports MSSP operations by ensuring client-safe, tenant-scoped communications

---

# 3. Scope

Use this template for:

| Severity | When to Use |
|---|---|
| P1 | Mandatory – bridge call must be initiated |
| P2 | Recommended – when containment coordination or multi-team involvement is required |

Applicable across:

- SOC (L1/L2/L3), IR Team, IT Ops/Network/Cloud
- Compliance/Legal involvement (as applicable)
- MSSP client stakeholders (where contract allows/requires)

---

# 4. Usage Instructions (Mandatory)

1. Start the bridge call and assign a **Bridge Chair** (typically SOC Lead).
2. Create/confirm the **incident ticket ID** and **war room channel**.
3. Use this agenda as the call structure and log decisions/actions in the ticket in real time.
4. Maintain cadence:
   - **P1:** updates every 30 minutes minimum
   - **P2:** updates every 60 minutes minimum (or as defined)

Documentation requirement:
- All decisions, approvals, and containment actions must be recorded in the incident ticket with UTC timestamps.

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 5. Bridge Call Details (Fill-In)

| Field | Value |
|---|---|
| Incident Ticket ID | `INC-YYYY-####` |
| Severity | `P1 / P2` |
| Incident Category | `Ransomware / Data Breach / Phishing / Malware / Intrusion / Cloud / Other` |
| Bridge Call Start Time (UTC) | `YYYY-MM-DD HH:MM` |
| Bridge Chair (Name/Role) | `...` |
| Incident Commander (Name/Role) | `...` |
| Communications Lead (Name/Role) | `...` |
| Technical Lead (Name/Role) | `...` |
| War Room Channel / Link | `...` |
| Meeting Link / Dial-in | `...` |
| Client/Tenant (MSSP) | `Client ID/Name (if applicable)` |
| Recording Enabled | `Yes/No (policy-dependent)` |
| Notes Taker | `Name/Role` |

---

# 6. Attendance (Roll Call)

> Record participants and their responsibilities.

| Name | Role/Team | Responsibility in Incident | Contact Method |
|---|---|---|---|
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

Minimum recommended participants (as applicable):

- SOC Lead (Bridge Chair)
- L2/L3 Technical Leads
- IR Team Lead (Incident Commander for P1)
- IT Ops lead / Cloud Ops lead / Network lead
- Compliance + Legal (if breach/regulatory triggers likely)
- MSSP SDM + Client incident contact (MSSP only, tenant-scoped)

---

# 7. Agenda (Standard)

## 7.1 Opening and Governance (5 minutes)

1. Confirm incident ticket ID and severity (P1/P2)
2. Confirm bridge chair and incident commander
3. Confirm note-taking and documentation method (ticket link)
4. Confirm communication cadence and next update time
5. Confirm any immediate safety/business constraints (e.g., “cannot isolate DC”, “core service must stay up”)

**Decisions / Notes (UTC):**  
- `...`

---

## 7.2 Incident Summary (5 minutes)

Provide a concise summary:

- **What happened (confirmed facts):** `...`
- **Where (systems/tenant):** `...`
- **When (UTC timeline):** `...`
- **Current impact:** `...`
- **Current status:** `Triage / Investigation / Containment / Recovery`

**Evidence references:**  
- SIEM: `...`  
- EDR: `...`  
- Network/Cloud: `...`

---

## 7.3 Threat Assessment (10 minutes)

Discuss and document:

- Suspected attack vector: `...`
- Known IOCs/TTPs: `...`
- Scope (current): `hosts/users/services`
- Scope (unknowns/questions): `...`
- Risk assessment:
  - Exfiltration risk: `Low/Med/High/Unknown`
  - Lateral movement risk: `Low/Med/High/Unknown`
  - Business continuity risk: `Low/Med/High/Unknown`

**Decisions / Notes (UTC):**  
- `...`

---

## 7.4 Containment Plan and Approvals (10–15 minutes)

> Capture decisions and approval authority clearly.

### Proposed containment actions
| Action | Scope/Target | Owner (Executor) | Approval Required From | Approved? (Y/N) | Time (UTC) |
|---|---|---|---|---|---:|
|  |  |  |  |  |  |
|  |  |  |  |  |  |

Examples:
- EDR isolate host(s)
- Disable/reset accounts
- Firewall block IP/domain
- Network segmentation/quarantine VLAN
- Suspend cloud keys/sessions

**Rollback plan summary:**  
- `...`

Reference:  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 7.5 Evidence Preservation and Forensics (10 minutes)

Confirm:

- Evidence required (logs/memory/disk/PCAP): `...`
- Who will collect: `...`
- Where evidence will be stored (path): `...`
- CoC required? `Yes/No` + rationale
- Any legal hold considerations: `...`

| Evidence Item | Source | Owner | Target Time (UTC) | Status | Reference/Path |
|---|---|---|---:|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

## 7.6 Investigation Workstreams (10 minutes)

Define parallel workstreams and owners.

| Workstream | Owner | Objective | Next Deliverable | Due (UTC) |
|---|---|---|---|---:|
| Endpoint / EDR |  |  |  |  |
| SIEM / Log correlation |  |  |  |  |
| Identity / IAM |  |  |  |  |
| Network |  |  |  |  |
| Cloud |  |  |  |  |
| Threat Intel |  |  |  |  |

---

## 7.7 Recovery Planning (5–10 minutes)

Discuss:

- Systems to restore: `...`
- Dependencies and sequencing: `...`
- Backup/restore validation: `...`
- Monitoring plan post-recovery: `...`
- Risk of reinfection: `...`

**Recovery owner:** `...`  
**ETA:** `...`

References:  
`02_PLAYBOOKS/` (recovery steps by incident type)

---

## 7.8 Communications and Notifications (5 minutes)

Confirm required notifications:

| Notification Target | Required? (Y/N) | Owner | Method | Time Target (UTC) | Status |
|---|---|---|---|---:|---|
| Management / CISO |  |  |  |  |  |
| Compliance / Legal |  |  |  |  |  |
| MSSP Client (if applicable) |  |  |  |  |  |
| Regulatory readiness check |  |  |  |  |  |
| External vendor/IR retainer |  |  |  |  |  |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 7.9 Action Items and Next Checkpoint (5 minutes)

### Action Items Tracker (Live)
| # | Action Item | Owner | Due (UTC) | Status | Notes |
|---:|---|---|---:|---|---|
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |

### Next Update Checkpoint
- **Next bridge update time (UTC):** `YYYY-MM-DD HH:MM`
- **Next written status update time (UTC):** `YYYY-MM-DD HH:MM`

---

# 8. Closure of Bridge Call (When Applicable)

Bridge call may be ended only when:

- Threat activity is contained and validated
- Recovery is stable and monitoring is in place
- Stakeholders agree on transition to standard ticket updates
- A final SITREP is sent for P1/P2 (as required)

Record:
- **Bridge end time (UTC):** `...`
- **Reason:** `...`
- **Next comms plan:** `...`

---

# 9. Related Documents

| Document | Path |
|---|---|
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |

---

# 10. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Lead / SOC Operations Lead | Initial version |

---

# 11. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**