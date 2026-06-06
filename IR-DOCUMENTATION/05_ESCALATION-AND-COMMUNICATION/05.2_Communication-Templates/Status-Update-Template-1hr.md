 # Status Update Template – 1 Hour (P2 / Extended Incidents)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Status Update (1 Hour) |
| Document ID | COM-TPL-007 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes the **hourly status update** cadence for:

- **P2 (High)** incidents (default cadence), and
- **P1 incidents** after stabilization when SOC Lead approves moving from 30-minute to hourly cadence.

A structured status update is critical because:

- It ensures predictable communication to stakeholders
- It supports SLA compliance and operational transparency
- It improves coordination across SOC, IR, IT Ops, and (if applicable) MSSP clients
- It provides an audit-ready timeline of incident actions, decisions, and outcomes
- It ensures scope and impact are continuously reassessed and documented

This template ensures:

- Consistent content across updates regardless of who authors the update
- Clear separation of confirmed facts vs assumptions
- Explicit identification of blockers, risks, and decisions required

---

# 3. Scope

Use this template for:

| Severity | When to Use |
|---|---|
| P2 | Mandatory (minimum every 60 minutes) |
| P1 | When SOC Lead approves hourly cadence after stabilization |
| P3 | Optional (if management/client requires hourly SITREP) |

Recipients may include:

- SOC/IR teams and IT operations
- Management/CISO (as required)
- Compliance/Legal (as applicable)
- MSSP client stakeholders (if applicable and contractually required)

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Start with “since last update”.
- Provide evidence references as IDs/links (do not paste raw sensitive logs).
- If scope/impact is unknown, state “unknown” and list what is being validated.
- Ensure the update is recorded in the ticket and/or linked bridge notes.

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Recommended)

**`Status Update – [Incident ID] – [Severity] – Update #[N] – [UTC Time]`**

Example:
`Status Update – INC-2026-0102 – P2 – Update #4 – 2026-05-25 12:00 UTC`

---

## Message Body (Mandatory)

**Incident Ticket ID:** `INC-YYYY-####`  
**Severity:** `P1 / P2 / P3`  
**Incident Category:** `...`  
**Client/Tenant (if applicable):** `Client ID/Name`  
**Update Number:** `#N`  
**Update Time (UTC):** `YYYY-MM-DD HH:MM`  
**Incident Commander / Owner:** `Name/Role`  
**Bridge Call:** `Active/Not Active`  

---

### 1) Since Last Update (What Changed)
- `Change 1…`
- `Change 2…`
- `Change 3…`

---

### 2) Current Status (Phase)
- `Triage / Investigation / Containment / Eradication / Recovery / Monitoring`

---

### 3) Scope (Best Known)
- **Affected Hosts:** `...`
- **Affected Users/Accounts:** `...`
- **Affected Services:** `...`
- **Spread Indicators:** `Yes/No/Unknown` + notes
- **Exfiltration Indicators:** `Yes/No/Unknown` + notes

---

### 4) Actions Completed (Last 60 Minutes)

| Action | Owner (Executor) | Authorized By | Time (UTC) | Outcome |
|---|---|---|---:|---|
|  |  |  |  |  |
|  |  |  |  |  |

---

### 5) Key Findings (Investigation)
- **Confirmed facts:**  
  - `...`
- **Suspected / under validation:**  
  - `...`

**Evidence references (safe links/IDs):**  
- SIEM: `...`  
- EDR: `...`  
- Network/Cloud: `...`  

---

### 6) Containment / Eradication / Recovery Progress
- **Containment status:** `Not started / In progress / Completed` + notes
- **Eradication status:** `Not started / In progress / Completed` + notes
- **Recovery status:** `Not started / In progress / Completed` + notes
- **Validation performed:** `...` (how we confirmed reduced/ended activity)

---

### 7) Current Risks and Blockers
- **Risks:** `...`
- **Blockers:** `approvals pending / access needed / logs missing / client response pending`

---

### 8) Decisions Required (If Any)

| Decision Needed | Why | Needed By (UTC) | Owner | Status |
|---|---|---:|---|---|
|  |  |  |  |  |

---

### 9) Communications / Notifications
- **Management notified:** `Yes/No` + time (UTC)
- **Compliance/Legal engaged:** `Yes/No` + time (UTC)
- **Client notified (MSSP):** `Yes/No` + time (UTC)
- **Regulatory readiness check:** `Required/Not required/Under assessment`

---

### 10) Next 60-Minute Plan (Next Actions)

| Next Action | Owner | Due (UTC) | Notes |
|---|---|---:|---|
|  |  |  |  |
|  |  |  |  |

---

### 11) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM` (hourly cadence)
- **Next checkpoint (bridge call if active):** `YYYY-MM-DD HH:MM`

---

# 6. Mandatory Ticket Entry (After Sending)

Update the incident ticket with:

- Update number and timestamp (UTC)
- Summary of changes since last update
- Actions completed and outcomes
- Evidence references added/updated
- Decisions required and approvals captured
- Blockers and risks
- Next update time commitment

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| P2 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P2-Initial-Alert-Template.md` |
| P1 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |

---

# 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Lead / SOC Operations Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
