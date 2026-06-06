# Management Notification Template

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Management Notification |
| Document ID | COM-TPL-004 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / SOC Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This template standardizes notifications to **management and executive stakeholders** during security incidents.

Management notifications are critical because:

- Executives own business risk and must make timely decisions (containment approvals, downtime, vendor engagement)
- Management requires clear impact summaries, not raw technical logs
- Regulatory and legal obligations often require early awareness and documented decisions
- Inconsistent messaging causes confusion, reputational risk, and audit gaps
- MSSP incidents may require parallel client executive coordination

This template ensures:

- Consistent content structure and clarity for non-technical audiences
- Separation of confirmed facts vs assumptions
- Clear decision requests and time sensitivity
- Predictable update cadence and accountability
- Audit-ready documentation with UTC timestamps and ticket references

---

# 3. Scope

Use this template for:

| Scenario | Examples |
|---|---|
| P1 incidents | Ransomware, confirmed breach, domain compromise, major outage |
| P2 incidents with material risk | Privileged account takeover, suspected exfiltration |
| Significant trends | Repeated attacks indicating systemic risk (as required) |
| Regulatory readiness | RBI/CERT-In assessment triggers (as applicable) |

Recipients may include:

- SOC Manager / CISO
- CIO/CTO/COO/CEO (as defined)
- Business unit heads
- Compliance / Legal / Privacy (as applicable)

---

# 4. Instructions (Mandatory)

- Use UTC timestamps.
- Do not include sensitive evidence (credentials/PII/raw logs/PCAP) in the email body.
- If information is uncertain, label it as “suspected” or “under investigation.”
- Include **decisions required** with deadlines.
- Record the notification in the incident ticket (who/when/how/summary).

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 5. Template (Copy/Paste)

## Subject Line (Mandatory)

**`[P1/P2] – Management Notification – [Incident Category] – [Business Unit/Client] – [UTC Time]`**

Examples:
- `P1 – Management Notification – Ransomware – Internal – 2026-05-25 04:20 UTC`
- `P2 – Management Notification – Privileged Compromise – ClientABC – 2026-05-25 09:10 UTC`

---

## Message Body (Mandatory)

**Incident Ticket ID:** `INC-YYYY-####`  
**Severity:** `P1 / P2 / P3 (management notification only when required)`  
**Incident Category:** `Ransomware / Data Breach / Intrusion / Cloud / Credential Attack / DDoS / Other`  
**Detected At (UTC):** `YYYY-MM-DD HH:MM`  
**Current Time (UTC):** `YYYY-MM-DD HH:MM`  
**Incident Commander:** `Name/Role`  
**Bridge Call:** `Active/Not Active` + `Link (if active)`  

---

### 1) Executive Summary (Non-Technical, 3–6 lines)
- `What happened`
- `Where/which business services impacted`
- `Current status (containment/investigation/recovery)`
- `Primary risk (data exposure/outage/fraud)`
- `What is being done right now`

---

### 2) Confirmed Facts (What We Know)
- `Fact 1 (with time UTC)`
- `Fact 2`
- `Fact 3`

---

### 3) Suspected / Under Investigation
- `Hypothesis 1`
- `Hypothesis 2`
- `Unknowns and what we are doing to confirm them`

---

### 4) Business Impact (Current)
- **Service Availability:** `Normal / Degraded / Down / Unknown`
- **Affected Business Units:** `...`
- **Customer Impact:** `Yes/No/Unknown` + details
- **Operational Impact:** `...`
- **Financial Impact:** `Unknown / Estimated` (if available)

---

### 5) Data Risk (If Applicable)
- **Data exposure suspected/confirmed:** `Suspected / Confirmed / No evidence / Unknown`
- **Data types potentially affected:** `PII / financial / credentials / IP / other`
- **Exfiltration evidence:** `Yes/No/Unknown` + brief rationale

---

### 6) Actions Taken (So Far)
> Include time (UTC) and owners.

- `Action – Owner – Time (UTC) – Outcome`
- `Action – Owner – Time (UTC) – Outcome`

---

### 7) Current Containment / Recovery Plan (Next 1–4 Hours)
- `Containment step(s)`
- `Recovery step(s)`
- `Monitoring plan`

**Estimated time to containment:** `...`  
**Estimated time to service restoration (if impacted):** `...`

---

### 8) Decisions Required from Management (If Any)
> Be explicit and time-bound.

| Decision Needed | Why | Options | Recommended Option | Needed By (UTC) | Owner |
|---|---|---|---|---:|---|
|  |  |  |  |  |  |

Examples:
- Approve isolation of a critical subnet
- Approve temporary shutdown of a service
- Approve external IR retainer engagement
- Approve customer/client communications

---

### 9) Notifications and Compliance (If Applicable)
- **Compliance/Legal engaged:** `Yes/No` + time (UTC)
- **Regulatory assessment:** `Required/Not required/Under assessment`
- **RBI/CERT-In readiness:** `Yes/No/Under assessment`
- **Client notification (MSSP):** `Yes/No` + time (UTC)

---

### 10) Next Update Commitment
- **Next update by (UTC):** `YYYY-MM-DD HH:MM`
- **Update cadence:** `Every 30 min (P1) / Every 60 min (P2) / Milestones`

---

# 6. Mandatory Ticket Entry (After Sending)

Update incident ticket with:

- Recipients and roles notified
- Channel used (phone/email/bridge)
- Timestamp (UTC)
- Summary of message
- Decisions requested and outcomes (approved/denied)
- Next update commitment

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 7. Related Documents

| Document | Path |
|---|---|
| P1 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md` |
| P2 Initial Alert Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P2-Initial-Alert-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |
| Bridge Call Agenda Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md` |
| IR Team to Management Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/IR-Team-to-Management-Escalation.md` |
| Regulatory Communication SOPs | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |

---

# 8. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / SOC Lead | Initial version |

---

# 9. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**