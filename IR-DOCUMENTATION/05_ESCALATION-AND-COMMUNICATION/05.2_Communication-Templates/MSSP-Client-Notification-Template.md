# MSSP Client Notification Template

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – MSSP Client Notification |
| Document ID | COM-TPL-005 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | MSSP Service Delivery Manager (SDM) / SOC Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes **client-facing notifications** for incidents handled under MSSP operations.

Client notification is critical because:

- Notification timelines are contractually bound (SLA/SLO)
- Client approvals may be required before containment actions (isolation, firewall blocks)
- Client communications must be accurate, actionable, and tenant-safe
- Incomplete messages delay client response and increase incident impact
- Audit readiness requires traceable records of what was communicated and when
- Multi-tenant MSSP operations require strict segregation to prevent cross-client disclosure

This template ensures:

- Consistent, professional, and actionable client updates
- Clear separation of confirmed facts vs suspected items
- Documented required client actions and timeframes
- Safe communication controls and evidence referencing
- SLA-aligned cadence and escalation path for no-response situations

---

# 3. Scope

Use this template for client notifications related to:

| Category | Examples |
|---|---|
| P1 incidents | Ransomware, confirmed breach, domain compromise, major outage |
| P2 incidents | Confirmed malware, privileged account risk, likely intrusion |
| Action required events | Password reset, host isolation approval, patching, log requests |
| Client advisory | High-confidence TI affecting client environment (when action required) |
| Closure notifications | Incident resolved and closed (or moved to PIR phase) |

Out of scope:

- Monthly reporting summaries (separate reporting docs)
- Client onboarding/offboarding communications

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 4. Instructions (Mandatory)

- Verify tenant/client ID before sending.
- Use UTC timestamps.
- Do not include sensitive data (credentials/PII/raw logs/PCAP) in email body.
- Provide secure links/references for evidence (client-segregated).
- Clearly state whether actions require client approval.
- Record notification in ticket (time, recipient, method, summary).

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Mandatory)

**`[Severity] – Security Incident Notification – [Client Name] – [Incident Category] – [UTC Time]`**

Examples:
- `P1 – Security Incident Notification – ClientABC – Ransomware – 2026-05-25 04:25 UTC`
- `P2 – Security Incident Notification – ClientXYZ – Malware – 2026-05-25 09:15 UTC`

---

## Message Body (Mandatory)

**Client:** `Client Name (Client ID)`  
**Severity:** `P1 / P2 / P3 / P4`  
**Incident Ticket ID (MSSP):** `MSSP-INC-YYYY-####` (or `INC-YYYY-####`)  
**Incident Category:** `Ransomware / Malware / Phishing / Intrusion / Credential Attack / Cloud / DDoS / Other`  
**Detected At (UTC):** `YYYY-MM-DD HH:MM`  
**Notification Time (UTC):** `YYYY-MM-DD HH:MM`  
**MSSP Contact:** `Name/Role + phone/email`  

---

### 1) Summary (Client-Friendly, 2–4 lines)
- `Short summary of what was detected and why it matters`

---

### 2) What We Know (Confirmed)
- `Fact 1…`
- `Fact 2…`
- `Fact 3…`

---

### 3) What We Are Investigating (Unconfirmed)
- `Item 1…`
- `Item 2…`

---

### 4) Scope (Best Known at This Time)
- **Affected systems/hosts:** `...`
- **Affected users/accounts:** `...`
- **Environment:** `Prod/Dev/Cloud/Other`
- **Spread indicators:** `Yes/No/Unknown`
- **Service impact:** `None/Limited/Unknown` + details

---

### 5) Evidence Summary (High-Level)
> Do not include raw sensitive artifacts. Provide safe references.

- **Indicators observed:** `IPs/domains/URLs/hashes (as appropriate)`
- **Telemetry sources:** `EDR/SIEM/Firewall/Cloud audit`
- **Client-safe evidence references:** `Evidence IDs/paths/links`

---

### 6) Actions Taken by MSSP (So Far)
> Include time (UTC) and outcomes.

- `Action – Time (UTC) – Outcome`
- `Action – Time (UTC) – Outcome`

---

### 7) Actions Required from Client (Mandatory If Any)

> If the client must act, make it explicit and time-bound.

| Client Action Required | Reason | Required By (UTC) | Owner (Client) | Status/Notes |
|---|---|---:|---|---|
|  |  |  |  |  |
|  |  |  |  |  |

Examples:
- Reset password for `userX` and confirm MFA status
- Validate whether host `SRV-APP-01` is business critical and can be isolated
- Provide confirmation of recent approved change activity
- Provide relevant logs not available to MSSP

---

### 8) Approvals Requested from Client (Mandatory If Any)

> Required when MSSP needs authorization to perform impactful containment.

| Approval Needed | Proposed Action | Impact | Needed By (UTC) | Approver (Client) | Approved? |
|---|---|---|---:|---|---|
|  |  |  |  |  |  |

Examples:
- Approve EDR isolation of host(s)
- Approve disabling privileged account
- Approve firewall block that may affect vendor connectivity
- Approve forensic collection (disk/memory/log exports)

---

### 9) Current Risk Assessment
- **Data exposure risk:** `High/Medium/Low/Unknown` + rationale
- **Privilege risk:** `High/Medium/Low/Unknown` + rationale
- **Business disruption risk:** `High/Medium/Low/Unknown` + rationale

---

### 10) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM`
- **Update cadence:**  
  - P1: every 30 minutes minimum  
  - P2: every 60 minutes minimum  
  - P3/P4: milestone updates  

---

### 11) Escalation Path (If Client Cannot Reach MSSP Contact)
- Primary: `Name/Role – phone/email`
- Backup: `Name/Role – phone/email`
- 24x7 hotline (if applicable): `...`

---

# 6. Mandatory Ticket Entry (After Sending)

Update the incident ticket with:

- Client ID and name
- Notified contact (name/role)
- Method (phone/email)
- Notification time (UTC)
- Summary sent
- Client response/approvals/instructions
- Next update commitment
- SLA compliance status (met/not met + reason)

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| P1 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md` |
| P2 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P2-Initial-Alert-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |
| Client IR Contacts | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| Evidence Handling (Client) | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/MSSP-Client-Evidence-Handling.md` |

---

# 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | MSSP SDM / SOC Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**