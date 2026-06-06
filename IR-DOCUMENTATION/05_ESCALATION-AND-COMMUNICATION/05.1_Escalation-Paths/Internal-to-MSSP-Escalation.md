# Internal-to-MSSP Escalation

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Internal-to-MSSP Escalation |
| Document ID | ESC-PATH-003 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | MSSP Service Delivery Manager (SDM) / SOC Operations Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how the internal SOC escalates security alerts/incidents to **MSSP client stakeholders** in a controlled, SLA-aligned, and audit-ready manner.

Internal-to-MSSP escalation is critical because:

- Client notification obligations are contractually bound (SLA/SLO)
- Incorrect tenant identification can cause **cross-client data exposure**
- Poorly structured communication delays containment and increases business impact
- Audit and compliance require clear records of **what was communicated, when, and to whom**
- Certain incidents require **regulatory readiness** (RBI/CERT-In) and client coordination
- Client-specific approvals may be required before containment actions (e.g., isolation, blocking)

This SOP ensures:

- Correct tenant/client verification before communication
- Standard notification triggers and timelines by severity
- Secure communication and data minimization
- Documentation standards in the ticketing system
- Proper handoff to IR Team and client incident managers (where applicable)
- Consistent escalation for multi-tenant MSSP operations

---

# 3. Scope

This SOP applies to all escalations from internal SOC operations to MSSP clients for:

| Incident/Alert Type | Examples |
|---|---|
| Security alerts requiring client action | Compromised user, endpoint malware, suspicious admin access |
| Confirmed incidents | Ransomware, data breach, insider threat, supply chain |
| Client-impacting outages | DDoS, service disruption due to attack |
| Containment approvals | EDR isolate, firewall block, account disablement |
| Evidence requests | Log exports, host images, user interviews |
| Regulatory-driven events | RBI/CERT-In reportable incidents (as applicable) |

Out of scope:

- Client onboarding/offboarding procedures
- Client internal escalation matrix (stored in client folder)
- General monthly reporting (covered by MSSP reporting templates)

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`  
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Client/tenant | A distinct MSSP customer environment with segregated data and controls |
| Client notification | Communication to client stakeholders about an alert/incident and required actions |
| Client approval | Client authorization required before executing containment actions (contract-dependent) |
| TLP | Traffic Light Protocol classification for sharing intelligence/information |
| SLA | Contractual service response/notification commitments |
| War room | Dedicated collaboration space for incident coordination |
| Bridge call | Real-time incident coordination call (P1 mandatory) |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Initial ticket creation; identify client tag; notify SOC Lead |
| L2 Analyst | Validate incident details; prepare technical summary and evidence references |
| SOC Lead | Confirms severity; triggers client escalation; ensures SLA compliance and update cadence |
| MSSP SDM | Owns client communications process; validates client contacts; coordinates approvals |
| IR Team Lead | Directs containment and forensic actions; ensures client approval when required |
| SOC Manager | Oversight; escalates communication failures; ensures audit quality |
| Client Primary Contact (CISO/IT Lead) | Receives notifications; provides approvals and client-side actions |
| Compliance/Legal (as needed) | Advises on breach communications, regulatory timelines, and wording |

References:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`

---

# 6. Mandatory Principles for Client Escalation

| Principle | Requirement |
|---|---|
| Tenant verification first | Confirm correct client/tenant before sending any details |
| Minimum necessary disclosure | Share only what the client needs to act; avoid sensitive internal info |
| Secure channels only | No client incident details over non-approved channels |
| SLA-driven | Notification timelines follow client SLA (and default internal SLA if not specified) |
| Clear ask | Every notification must state required client actions and response time |
| Document everything | All communications must be summarized in the incident ticket with timestamps (UTC) |
| No cross-client indicators | Never include other client names, indicators, or evidence references |

---

# 7. Client Escalation Triggers (When to Notify Client)

Client notification is required when any applies:

## 7.1 Mandatory Client Notification Triggers

| Trigger | Examples |
|---|---|
| P1 incident declared | Ransomware, confirmed breach, domain compromise |
| P2 confirmed security incident | Confirmed malware, privileged account risk, lateral movement indicators |
| Client action required | Password reset, disable user, patch, isolate host, collect logs |
| Client environment materially impacted | Service disruption, critical system compromise |
| Client data potentially affected | Possible exfiltration, data access anomaly |
| Regulatory reporting likely | RBI/CERT-In thresholds potentially met |
| SLA breach risk | Delay expected; proactive transparency required |

## 7.2 Conditional Triggers (Based on Contract/Client Profile)

| Trigger | Notes |
|---|---|
| P3 suspicious activity | Notify if client requires all P3 notifications |
| TI advisory affecting client | Notify if high relevance and action required |
| Repeated low severity activity | Notify as trend advisory / hardening recommendation |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`

---

# 8. Client Escalation Timelines (Minimum Standard)

> If client contract defines stricter timelines, contract overrides.

| Severity | First Client Notification Target | Update Frequency | Method (Minimum) |
|---|---:|---|---|
| P1 | ≤ 30 minutes (or immediate) | Every 30 minutes | Phone + email + ticket record |
| P2 | ≤ 60 minutes | Every 60 minutes | Email + phone if required |
| P3 | ≤ 4 hours | Milestones | Email |
| P4 | ≤ 24–72 hours | At completion | Email (optional) |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

# 9. Tenant Verification Procedure (Mandatory Before Notification)

Before contacting a client, the SOC Lead or MSSP SDM must confirm:

## 9.1 Verification Checklist

| Verification Step | Requirement |
|---|---|
| Ticket has correct Client ID/Client Name | Mandatory |
| Affected asset belongs to client tenant | Mandatory |
| Evidence links stored in client-segregated location | Mandatory |
| SIEM/EDR tenant context confirmed | Mandatory |
| No cross-tenant indicators in notes/screenshots | Mandatory |
| Correct client contact list referenced | Mandatory |
| TLP/sharing restrictions considered | Mandatory |

If tenant cannot be verified, **do not notify client** until verified—escalate to SOC Manager immediately.

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`

---

# 10. Communication Content Standard (What Must Be Included)

All client escalations must include:

## 10.1 Minimum Required Content

| Item | Requirement |
|---|---|
| Incident summary | What happened in simple terms |
| Severity and status | P1/P2/P3/P4 + current phase (triage/investigation/containment) |
| Time (UTC) | Detection time and current time reference |
| Scope (best known) | Affected host(s), user(s), service(s) |
| Evidence highlights | Key indicators observed (no unrelated internal details) |
| Risk statement | Potential impact to client |
| Required client actions | Clear tasks + urgency |
| Next update time | Commitment for next update |
| MSSP contact point | Who client should respond to |

## 10.2 Do Not Include (Mandatory Restrictions)

- Other clients’ names, assets, or incidents
- Internal-only tooling details that expose security posture unnecessarily
- Raw sensitive data (PII, credentials, customer data)
- Full PCAPs or disk images via email (use secure transfer only)
- Unverified attribution statements

---

# 11. Escalation Workflow (Internal → Client)

## 11.1 Step 1 — Prepare Client Escalation Package

Owner: L2 Analyst + SOC Lead (MSSP SDM supports)

Package must include:

| Component | Requirement |
|---|---|
| Incident summary | Mandatory |
| Severity justification | Mandatory |
| Affected assets/users | Mandatory |
| Actions taken so far | Mandatory |
| Containment recommendation | Mandatory (if needed) |
| Evidence references | Mandatory (client-segregated paths/IDs) |
| Client actions required | Mandatory |
| Questions for client | Optional (e.g., “Is this host critical?”, “Any recent changes?”) |

## 11.2 Step 2 — Notify Client (Per SLA)

Owner: MSSP SDM (preferred) or SOC Lead (if SDM unavailable)

- Use approved templates
- Use secure communication channels
- For P1: **phone call + written follow-up**

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/P1-Initial-Alert-Template.md`

## 11.3 Step 3 — Capture Client Response and Approvals

Owner: MSSP SDM + SOC Lead

Document in the ticket:

- Who responded (name/role)
- Response time (UTC)
- Instructions/approvals granted
- Constraints (change windows, criticality, “do not isolate,” etc.)

## 11.4 Step 4 — Execute Client-Approved Actions

Owner: IR Team / SOC Lead / IT Ops (as applicable)

- Execute containment/remediation per authority matrix and client approvals
- Document executor, authorization, time (UTC), and outcome

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

## 11.5 Step 5 — Maintain Update Cadence Until Closure

Owner: SOC Lead + MSSP SDM

- P1: every 30 minutes minimum
- P2: every 60 minutes minimum
- P3/P4: milestone updates

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md`

---

# 12. Client Approval Matrix (Guidance)

> Actual approval requirements are contract/client-specific. Use this as baseline guidance.

| Action | Typical Client Approval Needed? | Notes |
|---|---|---|
| Isolate endpoint via EDR | Often Yes | Some clients allow MSSP to isolate without approval in P1 |
| Disable user account | Often Yes | If privileged account compromised, may execute immediately with post-notify |
| Reset passwords / force MFA | Yes | Client IAM/IT executes; MSSP requests |
| Firewall block external IP/domain | Sometimes | If impacts business connectivity, client approval required |
| Quarantine VLAN / segmentation changes | Yes | High business impact risk |
| Disk/memory acquisition | Yes | Evidence handling and privacy concerns |
| Regulatory notification submission | Yes | Usually handled by client; MSSP supports with evidence |

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

# 13. Documentation Requirements (Ticket-Level) (Mandatory)

For every internal-to-client escalation, the ticket must include:

| Required Field | Requirement |
|---|---|
| Client ID / Client Name | Mandatory |
| Client notification time (UTC) | Mandatory |
| Notified contact (name/role) | Mandatory |
| Notification method | Mandatory |
| Summary of message | Mandatory |
| Evidence references shared | Mandatory (safe references only) |
| Client response and instructions | Mandatory |
| Approvals granted/denied | Mandatory |
| Next update time promised | Mandatory |
| SLA met? | Mandatory (Yes/No; if No, reason) |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 14. Failure Handling (No Response / Escalation Blockers)

## 14.1 If Client Does Not Acknowledge Within SLA

Escalate in this order:

1. Client primary contact
2. Client backup contact
3. MSSP SDM escalates to client management escalation contact (if defined)
4. SOC Manager notified
5. Document all attempts (time, method, result)

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md`

## 14.2 If Client Denies Critical Containment Action

- Document denial and reasoning in ticket
- Escalate to SOC Manager + IR Team Lead immediately
- Provide risk statement and alternative containment options
- If regulatory risk exists, notify CISO/Compliance

---

# 15. MSSP Multi-Tenant Controls (Mandatory)

| Control | Requirement |
|---|---|
| Tenant tagging | All tickets and evidence must include correct client ID |
| Evidence segregation | Separate evidence paths per client; no shared folders |
| Communication segregation | Separate email threads/case numbers per client |
| Least disclosure | Only share details relevant to the client |
| Tool access segregation | Analysts access only assigned client tenants |
| Review before send | SOC Lead/SDM review for P1/P2 comms (recommended) |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Related Documents

| Document | Path |
|---|---|
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Status Update Template (30 min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| Status Update Template (1 hr) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-1hr.md` |
| Client IR Contacts | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |

---

# 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | MSSP SDM / SOC Operations Lead | Initial version |

---

# 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**