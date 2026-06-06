# Incident Closure Notification

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Incident Closure Notification |
| Document ID | COM-TPL-008 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Lead / IR Team Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes the communication sent when an incident ticket is moved to **Closed** status.

Closure notification is critical because:

- Closure marks the incident record as finalized for audit and compliance
- Stakeholders must understand what happened, what was done, and what remains
- MSSP clients require closure summaries for service delivery and reporting
- Post-incident actions (RCA, lessons learned, improvements) must be tracked and assigned
- Incorrect closure communication can create confusion and unresolved risk

This template ensures:

- Consistent and complete closure summaries
- Clear statement of outcome (TP/FP/INFO/DUPLICATE)
- Confirmation of containment/eradication/recovery validation
- Clear documentation of follow-up actions and owners
- Audit-ready closure record linked to evidence and reports

---

# 3. Scope

Use this template for closure of:

| Ticket Type | Examples |
|---|---|
| Incident tickets | Ransomware, breach, intrusion, malware |
| High-impact alerts | P1/P2 events resolved without full incident conversion |
| MSSP client incidents | Client-specific ticket closures |
| Escalated incidents | Tickets closed due to transfer to IR case |

Not intended for:

- Routine informational tickets with no stakeholder distribution (unless required by client contract)

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Do not include sensitive evidence (raw logs/PCAP/credentials) in the message body.
- Include links/references to the final incident report if available.
- Clearly list follow-up actions and tracking references (RCA/PIR tickets).
- For MSSP, ensure content is tenant-scoped and does not reference other clients.

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Mandatory)

**`Incident Closed – [Incident ID] – [Severity] – [Category] – [Client/Business Unit]`**

Examples:
- `Incident Closed – INC-2026-0102 – P1 – Ransomware – Internal`
- `Incident Closed – INC-2026-0211 – P2 – Malware – ClientABC`

---

## Message Body (Mandatory)

**Incident Ticket ID:** `INC-YYYY-####`  
**Severity at Closure:** `P1 / P2 / P3 / P4`  
**Closure Reason Code:** `TP-CONTAINED / TP-ERADICATED / TP-RECOVERED / TP-ESCALATED / FP-IT / FP-TOOL / INFO / DUPLICATE`  
**Incident Category:** `...`  
**Client/Tenant (if applicable):** `Client ID/Name`  
**Detected At (UTC):** `YYYY-MM-DD HH:MM`  
**Contained At (UTC):** `YYYY-MM-DD HH:MM` (if applicable)  
**Resolved At (UTC):** `YYYY-MM-DD HH:MM`  
**Closed At (UTC):** `YYYY-MM-DD HH:MM`  
**Incident Owner / Commander:** `Name/Role`  

---

### 1) Executive Summary (Non-Technical)
- **What happened:** `...`
- **Impact:** `...`
- **Current risk status:** `Contained/Eradicated/Recovered/Monitoring`

---

### 2) Scope Summary (Final/Best Known)
- **Affected hosts/systems:** `...`
- **Affected users/accounts:** `...`
- **Affected services:** `...`
- **Data exposure:** `Confirmed / Suspected / No evidence / Unknown` + notes
- **Root cause (if identified):** `...` (or “under RCA”)

---

### 3) Key Actions Taken
> Include major actions only; keep it readable.

- `Containment action(s): ...`
- `Eradication action(s): ...`
- `Recovery action(s): ...`
- `Security control updates/tuning: ...`

---

### 4) Validation Performed (Why We Are Confident It Is Closed)
- `Validation method 1 (e.g., EDR clean scan + no IOC matches for 24 hours)`
- `Validation method 2 (e.g., SIEM queries showing no further suspicious auth)`
- `Validation method 3 (e.g., service monitoring stable)`

---

### 5) Evidence and Reporting References
- **Evidence package reference:** `Evidence path/ID` (tenant-scoped)
- **Final incident report:** `Link/ID` (if available)
- **Timeline reference:** `Link/ID` (if available)

> Do not attach raw evidence unless approved; reference secure storage.

---

### 6) Stakeholder Notifications Completed
- **Management notified:** `Yes/No` + time (UTC)
- **Compliance/Legal engaged:** `Yes/No` + time (UTC)
- **Client notified (MSSP):** `Yes/No` + time (UTC)
- **Regulatory reporting:** `Submitted / Not required / Under assessment` + reference (if submitted)

---

### 7) Follow-Up Actions (Post-Incident)
> These actions remain open after closure and must be tracked separately.

| Follow-Up Item | Owner | Due Date (UTC) | Tracking Reference |
|---|---|---:|---|
| RCA completion |  |  | `RCA-...` |
| Lessons Learned meeting |  |  | `PIR-...` |
| Detection improvement |  |  | `DET-IMP-...` |
| Control gap remediation |  |  | `CTRL-GAP-...` |
| Client remediation tasks |  |  | `TKT/CHG-...` |

---

### 8) Closure Statement
This incident is considered **closed** as of **[Closed At UTC]** based on the validation steps above.  
Any new related activity should reference **Incident Ticket ID: [INC-YYYY-####]**.

---

# 6. Mandatory Ticket Entry (Before Closure)

Ensure ticket includes:

- Closure reason code
- Closure summary narrative
- Evidence references
- Approvals as required by severity
- Post-incident tracking references (RCA/PIR)

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md` |
| Executive Summary Template | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| Lessons Learned Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Regulatory Communication SOPs | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Lead / IR Team Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**