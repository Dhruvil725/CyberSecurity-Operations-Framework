# IR Team to Management Escalation

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – IR Team to Management Escalation |
| Document ID | ESC-PATH-004 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how the Incident Response (IR) Team escalates incidents, decisions, and risk updates to **management and executive stakeholders** in a consistent, time-bound, and audit-ready manner.

Management escalation is critical because:

- Executives own business risk and must authorize high-impact decisions (containment actions, downtime, vendor engagement)
- Poor escalation leads to delayed approvals, extended attacker dwell time, and increased business impact
- Regulatory and legal obligations require documented decision trails and timelines
- Messaging must be accurate, consistent, and aligned to approved communication standards
- MSSP incidents may require client executive coordination and contractual commitments
- Incident status must be communicated using a predictable cadence to support crisis governance

This SOP ensures:

- Clear triggers for escalation to management
- Defined notification timelines and channels by severity
- Standard content requirements (what must be included in updates)
- Decision logging and approval documentation (who approved what, when, and why)
- Alignment with P1 bridge call process and regulatory readiness workflows
- Consistent handoff from technical response to executive decision-making

---

# 3. Scope

This SOP applies to escalation from IR Team to:

| Stakeholder Group | Examples |
|---|---|
| Security leadership | SOC Manager, CISO |
| Executive management | CIO/CTO, COO, CEO (as defined), Business Unit Heads |
| Risk functions | Compliance, Legal Counsel, Privacy/DPO (if applicable) |
| Operational leadership | IT Ops lead, Cloud Ops lead, Network lead |
| Communications function | PR/Corporate Communications (if reputational risk exists) |
| MSSP client management (if MSSP) | Client CISO/CIO/IT Head (per contract and escalation matrix) |

In scope incidents:

- P1 (mandatory)
- P2 with business impact or breach risk (often mandatory)
- P3/P4 when trends indicate systemic risk or repeated failures (as needed)

Out of scope:

- Routine operational reporting (daily/weekly SOC reports) unless incident-driven
- Client-only escalation paths (covered in Internal-to-MSSP escalation SOP)

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Management escalation | Formal notification to management for awareness, decisions, approvals, or crisis coordination |
| Decision authority | The role authorized to approve containment actions and business-impacting steps |
| Material impact | Significant disruption to critical services, financial impact, reputational impact, or regulatory impact |
| P1 / P2 | Severity classifications per SOC severity matrix |
| SITREP | Situation report – structured incident update to stakeholders |
| Legal hold | Instruction to preserve data/evidence for potential legal actions |

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| IR Team Lead (Incident Commander) | Owns management escalation content, cadence, and decision requests |
| SOC Lead | Supports status updates cadence; ensures operational timelines and ticket updates |
| SOC Manager | Ensures leadership alignment; escalates to CISO/executive team; oversees SLA and quality |
| CISO | Executive sponsor; authorizes external engagement; regulatory posture decisions |
| Compliance Lead | Regulatory assessment, reporting obligations, regulator communications support |
| Legal Counsel | Legal advice, law enforcement engagement, breach wording, legal hold |
| IT Ops / Cloud Ops Lead | Executes remediation and recovery; provides business/service impact inputs |
| MSSP SDM (if applicable) | Coordinates client leadership communication and contractual obligations |

---

# 6. Management Escalation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Accuracy over speed, but timely | Share verified facts; label assumptions clearly; escalate quickly for P1 |
| Single message owner | IR Team Lead controls official incident narrative and SITREP |
| Use approved templates | Prevent inconsistent wording and audit gaps |
| Decision-focused escalation | Management updates must include decisions needed and impact of delay |
| Time-bound commitments | Provide next update time and stick to cadence |
| Document all decisions | Every approval/denial must be recorded in ticket with UTC timestamps |
| Need-to-know | Limit distribution to necessary stakeholders; avoid oversharing sensitive evidence |
| MSSP segregation | Never mix client details; follow client-specific escalation paths |

---

# 7. Escalation Triggers (When IR Must Escalate to Management)

## 7.1 Mandatory Triggers

IR Team Lead must escalate to SOC Manager + CISO immediately when:

| Trigger | Examples |
|---|---|
| P1 incident declared/confirmed | Ransomware, confirmed data breach, DC compromise |
| Confirmed data exfiltration or breach indicators | DLP confirmation, cloud bulk downloads, outbound staging evidence |
| Privileged identity compromise | Domain admin or cloud root compromise |
| Critical service outage due to cyber incident | Payment systems down, customer portal unavailable |
| Need for high-impact containment | Network segmentation lockdown, shutdown services, mass password resets |
| Potential regulatory reporting obligation | RBI/CERT-In triggers likely |
| Third-party/vendor involvement required | IR retainer, cloud provider support, forensic lab |
| Media/reputational risk identified | Public-facing breach rumors, social media claims |

## 7.2 Conditional Triggers

Escalate when:

- SLA breach risk for P1/P2 due to resource constraints
- Insider threat requiring HR/legal involvement
- Repeat incidents indicate systemic control failure (trend risk)
- Significant customer/business partner impact is expected

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

# 8. Escalation Timelines (Management Notification)

> These are minimum internal standards. Client contracts or regulations may require faster notification.

| Severity | Initial Management Notification | Update Cadence | Channel (Minimum) |
|---|---:|---|---|
| P1 | ≤ 30 minutes of confirmation | Every 30 minutes | Phone + bridge call + written SITREP |
| P2 (material risk) | ≤ 60 minutes | Every 60 minutes | Phone/email + written update |
| P3 (trend/systemic risk) | Same business day | Milestones | Email |
| P4 | As required | At completion | Email (optional) |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 9. Escalation Channels and Format

## 9.1 Approved Channels (Standard)

| Channel | When Used | Notes |
|---|---|---|
| Bridge call | P1 mandatory; P2 optional | IR Team Lead or SOC Lead chairs |
| Phone/on-call | P1/P2 initial notification | Ensure acknowledgment |
| Email SITREP | All P1/P2 | Provides written audit trail |
| Secure chat (war room) | P1/P2 coordination | Do not use as sole record |
| Ticket updates | Always mandatory | Source of truth for actions/decisions |

References:
`03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 10. Required Content for Management Escalation (Mandatory)

Management updates must be structured and decision-oriented.

## 10.1 Initial Management Notification – Minimum Fields

| Field | Requirement |
|---|---|
| Incident ID + severity | Mandatory |
| Detection time + current time (UTC) | Mandatory |
| Summary (1–3 lines) | Mandatory |
| Current status | Triage / Investigation / Containment / Recovery |
| Impact assessment (known) | Mandatory (even if “unknown”) |
| Affected business services/systems | Mandatory (best known) |
| What is confirmed vs suspected | Mandatory |
| Immediate actions taken | Mandatory |
| Key risks | Mandatory |
| Decisions required from management | Mandatory (with deadlines) |
| Next update time | Mandatory |

Reference template:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`

---

## 10.2 Ongoing SITREP Update – Minimum Fields

| Field | Requirement |
|---|---|
| What changed since last update | Mandatory |
| Updated scope | Hosts/users/services |
| Containment progress | Actions executed + outcomes |
| Evidence status | What evidence preserved and where referenced |
| Recovery status | Service restoration steps + ETA |
| Risk outlook | What is likely next (with confidence statement) |
| External dependencies | Vendors, cloud provider, third parties |
| Customer/client impact | If applicable |
| Decisions required | Still pending items |
| Next update time | Mandatory |

---

# 11. Decision Requests (Management Approvals) – Required Details

When requesting management approval (shutdown/lockdown/broad containment), IR must provide:

## 11.1 Decision Request Checklist (Mandatory)

| Item | Requirement |
|---|---|
| Decision required | Explicit (“Approve isolation of subnet X”) |
| Reason | Security rationale and risk if delayed |
| Impact | Business impact and affected services/users |
| Alternatives | At least one alternative (if feasible) |
| Time sensitivity | “Needed within 15 min” |
| Rollback plan | How to restore if adverse impact |
| Owner | Who will execute |
| Evidence | Supporting findings references |

All approvals/denials must be documented in ticket with:

- Approver name/title
- Time (UTC)
- Decision and constraints (e.g., “approve isolation but keep access to app server”)

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 12. Regulatory and Legal Escalation Coordination (If Applicable)

Management escalation must include a regulatory readiness assessment for incidents where breach is possible.

## 12.1 Regulatory Decision Points

Escalate to Compliance + Legal + CISO when:

- Customer/regulated data exposure is suspected
- Payment systems or critical BFSI systems are impacted
- Ransomware impacts production systems
- Material outage occurs due to cyber incident

Document in ticket:

- Reportability assessment (Yes/No/Unknown)
- Decision owner and time (UTC)
- Next steps (drafting report, evidence package)

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 13. MSSP Client Management Escalation (If Applicable)

For MSSP incidents, management escalation must also consider:

- Contractual SLAs and client notification obligations
- Client approvals required for containment actions
- Client executive briefings for high impact incidents
- Segregation and confidentiality constraints

Minimum requirements:

| Item | Requirement |
|---|---|
| Client ID and scope confirmed | Mandatory |
| Client notification time recorded | Mandatory |
| Client approvals documented | Mandatory if containment affects client operations |
| Client executive summary prepared | Mandatory for P1 client incidents |
| No cross-tenant disclosure | Mandatory |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

# 14. Documentation Requirements (Ticket-Level) (Mandatory)

The incident ticket must record:

| Requirement | Standard |
|---|---|
| Management notification time (UTC) | Mandatory |
| Who was notified (names/roles) | Mandatory |
| Channel used | Mandatory |
| Summary communicated | Mandatory |
| Decisions requested | Mandatory |
| Decisions approved/denied | Mandatory |
| Approver identity + timestamp (UTC) | Mandatory |
| Follow-up actions assigned | Mandatory |
| Next update commitment | Mandatory for P1/P2 |

References:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 15. Escalation Failure Handling (Management Unavailable / Delays)

If management is unreachable within required timeline:

## 15.1 Fallback Contacts

Follow the escalation chain defined in:

- `Escalation-Matrix-Master.md`
- Contact directory on-call listings

## 15.2 Break-Glass Decision Authority

For P1 containment where delay increases harm:

- IR Team Lead may execute pre-approved containment actions under containment authority matrix
- SOC Manager and CISO must be notified as soon as feasible
- Document the break-glass rationale and timestamps in ticket

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 16. Quality Standards (Do/Do Not)

## 16.1 Do

- Use plain language for executives; include concise impact and decisions
- Clearly separate **confirmed facts** from **hypotheses**
- Include next update time and keep cadence
- Keep a running timeline in the ticket

## 16.2 Do Not

- Share unverified attribution (threat actor naming) as fact
- Include sensitive evidence dumps (PCAPs, full logs) in executive emails
- Overwhelm stakeholders with raw technical detail without summary
- Delay escalation while “investigating more” during suspected P1

---

# 17. Related Documents

| Document | Path |
|---|---|
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| L3 to IR Team Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| Bridge Call Agenda Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md` |
| Status Update Template (30min) | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| CERT-In Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**