# Escalation Matrix – Master

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Escalation Matrix – Master |
| Document ID | ESC-PATH-002 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the **master escalation matrix** for security alerts and incidents handled by the SOC and IR function.

A master escalation matrix is critical because:

- It ensures **time-bound escalation** aligned to SLA/SLO requirements
- It ensures **clear accountability** (who must be notified, when, and how)
- It prevents delayed response during **P1/P2 critical events**
- It provides **audit-ready evidence** of incident governance and decision paths
- It supports MSSP operations with defined client escalation and segregation rules
- It enables consistent communications across SOC tiers, IR team, management, and compliance/legal

This matrix ensures:

- Standard escalation triggers for each tier (L1/L2/L3/IR)
- Defined notification timelines (acknowledgment + response)
- Defined escalation fallback/backup contacts for no-response scenarios
- Defined authority and decision rights for containment actions
- Standard documentation requirements in tickets

---

# 3. Scope

This escalation matrix applies to:

| Area | Included |
|---|---|
| SOC tiers | L1, L2, L3 |
| Leadership | SOC Lead, SOC Manager |
| IR team | IR Team Lead and responders |
| Business stakeholders | IT Ops, App Owners, Business Owners |
| Risk functions | Compliance, Legal, Privacy/DPO (if applicable) |
| MSSP | Client notifications, tenant-specific escalations |
| Regulatory readiness | RBI/CERT-In assessment and routing (where applicable) |

Out of scope:

- Incident category-specific deep technical steps (covered in playbooks)
- Contact details (maintained in contact directory)

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Escalation | Formal transfer of ownership, attention, or authority to a higher tier or stakeholder |
| Acknowledgment | Confirmation by receiving party that escalation is received and accepted |
| P1 | Critical incident requiring emergency response and often bridge call |
| P2 | High priority incident requiring urgent response and frequent updates |
| Bridge Call | Live coordination call initiated for P1 and (as needed) P2 |
| War Room | Dedicated chat/channel + ticket + bridge call artifacts for coordination |
| SLA | Service Level Agreement (response/triage/updates) |
| SLO | Service Level Objective (targets for performance metrics) |

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`  
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 5. Escalation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Escalate early | If uncertain whether impact is high, escalate to SOC Lead immediately |
| No silent escalations | Escalation requires ticket update + direct notification for P1/P2 |
| Ownership is explicit | Ticket must show current owner and next responsible party |
| SLA clock does not reset | Escalation does not pause or reset SLA timelines |
| Document decisions | Any severity change, containment decision, or downgrade must be justified |
| Use backups | If no acknowledgment, follow fallback path and document attempts |
| MSSP segregation | Never share one client details with another; ensure tenant accuracy before notifying |

---

# 6. Communication Channels and Order of Use

## 6.1 Approved Channels (Standard)

| Channel | Allowed Use | Notes |
|---|---|---|
| Ticketing system | Mandatory record | Source of truth for audit |
| Phone/On-call | P1/P2 mandatory | Use for immediate acknowledgment |
| Secure chat (war room) | P1/P2 mandatory | Used for coordination and updates |
| Email | Notifications and summaries | Not sufficient alone for P1 |
| Bridge call | P1 mandatory | P2 as required by SOC Lead |

## 6.2 Order of Contact (P1/P2)

For P1/P2 escalations, use **in this order**:

1. Phone / on-call page
2. Secure chat mention (war room channel)
3. Ticket assignment + escalation note
4. Email summary (optional, but recommended for management/compliance)

---

# 7. Escalation Timelines (Master)

These are escalation acknowledgment targets (minimum). Client SLAs may override for MSSP.

| Priority | Escalation Triggered By | Acknowledgment Target | Update Frequency Target |
|---|---|---:|---|
| P1 | L1/SOC Lead | ≤ 15 minutes | Every 30 minutes |
| P2 | L1/L2/SOC Lead | ≤ 30 minutes | Every 60 minutes |
| P3 | L1/L2 | ≤ 2 hours | Milestones |
| P4 | L1 | ≤ 4 hours | At completion |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 8. Escalation Levels (Tier Escalation)

## 8.1 SOC Tier Escalation Path

| From | To | Typical Trigger |
|---|---|---|
| L1 | L2 | TP suspected/confirmed; needs deep investigation |
| L2 | L3 | Forensics/malware analysis required; advanced scope |
| L3 | IR Team | Active compromise confirmed; containment required |
| Any tier | SOC Lead | P1/P2 or SLA risk or uncertainty |
| SOC Lead | SOC Manager | P1 confirmed, major business impact, SLA breach risk |
| SOC Manager | CISO | P1, regulatory impact, reputational risk |

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md`

---

# 9. Master Escalation Matrix (By Priority)

> Use this as the authoritative “who must be notified and when” table.

## 9.1 P1 – Critical Incident Escalation

| Notify / Escalate To | Trigger | Method | Time Target | Mandatory? |
|---|---|---|---:|---|
| SOC Lead | Suspected/confirmed P1 | Phone + chat + ticket | ≤ 15 min | Yes |
| L2 + L3 | P1 declared | Ticket assignment + chat | Immediate | Yes |
| IR Team Lead | P1 declared | Phone + ticket + chat | ≤ 30 min | Yes |
| SOC Manager | P1 declared | Phone + email + ticket | ≤ 30 min | Yes |
| CISO | P1 confirmed | Phone + email | ≤ 30 min | Yes |
| IT Ops / Cloud Ops Lead | Containment/recovery required | Phone + war room | ≤ 30 min | Yes |
| Compliance + Legal | Data breach/regulatory triggers possible | Phone + email | ≤ 60 min | Yes (if applicable) |
| MSSP Client (if MSSP) | Client environment impacted | Phone + email + ticket note | Per contract (typically ≤ 30 min) | Yes (if applicable) |

Bridge call: **Mandatory** for P1  
Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

## 9.2 P2 – High Incident Escalation

| Notify / Escalate To | Trigger | Method | Time Target | Mandatory? |
|---|---|---|---:|---|
| SOC Lead | P2 declared or privileged asset/user involved | Chat + ticket; phone if needed | ≤ 30 min | Yes |
| L2 | P2 declared | Ticket assignment | ≤ 30 min | Yes |
| L3 | Forensics needed / suspected advanced threat | Ticket + chat | ≤ 60 min | Conditional |
| IR Team Lead | Containment required | Phone + ticket | ≤ 60 min | Conditional |
| SOC Manager | Business impact / SLA risk | Email + ticket | ≤ 2 hours | Conditional |
| Compliance + Legal | Potential breach | Email + ticket | ≤ 4 hours | Conditional |
| MSSP Client | Client impacted | Per contract | Per SLA | Conditional |

Bridge call: **As required** by SOC Lead.

---

## 9.3 P3 – Medium Escalation

| Notify / Escalate To | Trigger | Method | Time Target | Mandatory? |
|---|---|---|---:|---|
| L2 | Complex investigation / repeated suspicious activity | Ticket assignment | ≤ 2 hours | Conditional |
| SOC Lead | Pattern indicates escalation to P2 | Ticket + chat | ≤ 2 hours | Conditional |
| IR Team | Evidence of compromise emerges | Ticket + phone | Immediate after confirmation | Conditional |

---

## 9.4 P4 – Low / Informational Escalation

| Notify / Escalate To | Trigger | Method | Time Target | Mandatory? |
|---|---|---|---:|---|
| L2 / SOC Lead | Trend/noise indicates tuning need | Ticket comment | ≤ 72 hours | Conditional |
| Detection Engineering | Rule tuning required | Ticket | ≤ 72 hours | Conditional |

---

# 10. Escalation Matrix (By Incident Category) – Guidance Addendum

Some categories require earlier escalation even if initial severity is unclear.

| Category | Early Escalation Trigger | Escalate To |
|---|---|---|
| Ransomware | Any encryption indicators | SOC Lead + IR Team immediately |
| Data breach/exfiltration | Large outbound transfer, DLP triggers, unusual cloud downloads | SOC Lead + IR Team + Compliance |
| Insider threat | HR/legal sensitivity | IR Team Lead + Legal/HR coordination SOP |
| Supply chain | Vendor compromise suspected | IR Team + Management + Vendor management |
| Cloud compromise | Root/API keys, IAM privilege escalation | IR Team + Cloud Ops |
| Privileged compromise | DA/GA accounts | SOC Lead + IR Team immediately |

References:
`01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/`  
`02_PLAYBOOKS/`

---

# 11. Acknowledgment and Fallback Escalation Rules (Mandatory)

## 11.1 Acknowledgment Requirements

The receiving party must acknowledge:

- In ticket (comment + timestamp UTC)
- In chat/phone for P1/P2

## 11.2 Fallback Rules (No Response)

If no acknowledgment within target time:

| Priority | First Fallback | Second Fallback | Documentation |
|---|---|---|---|
| P1 | Call backup on-call (same role) | Escalate to SOC Manager | Record attempt times in ticket |
| P2 | Ping backup + SOC Lead | Escalate to SOC Manager if risk | Record attempt times in ticket |
| P3/P4 | Reassign to alternate analyst | Notify SOC Lead during shift brief | Record reassignment |

All contact attempts must be recorded with timestamps (UTC).

---

# 12. Containment Decision Authority (Escalation for Action)

Escalation is not only about awareness—it is required to obtain authority for containment.

Minimum standards:

| Containment Action | Examples | Minimum Authority |
|---|---|---|
| Endpoint isolation | EDR isolate host | SOC Lead (P2/P3) / IR Team Lead (P1) |
| Account disable/reset | Disable compromised user/admin | SOC Lead + IT/IAM Owner; IR Team for P1 |
| Firewall block | Block C2 IP/Domain | Network Security Lead + IR Team Lead for P1 |
| Segmentation isolation | Quarantine VLAN / zone deny | IR Team Lead + SOC Manager |
| Service shutdown | Stop critical service | SOC Manager + Business Owner (best effort in P1) |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 13. Management, Legal, Compliance Escalation (Decision Points)

Escalate to management/compliance/legal when any applies:

| Decision Point | Escalate To | Reason |
|---|---|---|
| Customer data possibly exposed | Compliance + Legal + CISO | Notification obligations |
| Material outage | SOC Manager + CISO | Business continuity impact |
| Media/reputation risk | CISO | Communications governance |
| Law enforcement involvement likely | Legal | Evidence and legal hold |
| Regulatory reporting may be required | Compliance | RBI/CERT-In readiness |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`  
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

# 14. MSSP Escalation Controls (Mandatory)

For MSSP operations, escalation must be **tenant-scoped**.

## 14.1 Tenant Verification (Mandatory Step Before Client Notification)

Before notifying a client:

- Confirm correct client/tenant ID in ticket
- Confirm impacted asset belongs to that tenant
- Confirm evidence links are tenant segregated
- Confirm the client contact list is current

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

## 14.2 Client Escalation Minimum Requirements

| Requirement | Standard |
|---|---|
| Client notified person (name + role) | Mandatory |
| Notification method | Mandatory |
| Notification time (UTC) | Mandatory |
| Summary communicated | Mandatory |
| Client instructions/approval | Mandatory if containment impacts client operations |
| SLA adherence documented | Mandatory |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`

---

# 15. Documentation Requirements (Ticket-Level) (Mandatory)

Every escalation must be documented in the ticket with:

| Required Field | Notes |
|---|---|
| Escalation timestamp (UTC) | Mandatory |
| Escalated from/to | Named person/team |
| Reason for escalation | Technical justification |
| Evidence references | Alert IDs, SIEM queries, EDR links, PCAP references |
| Ownership change | Assigned-to updated |
| Acknowledgment record | Who acknowledged + time |
| Next update commitment | Especially for P1/P2 |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 16. Escalation Matrix Template (Operational Copy)

> Use this section if you want to maintain an internal table with real names/phones in a restricted version of this document.  
> If contact data is stored separately, keep this as “role-based only”.

## 16.1 Role-Based Escalation Table (Fill-In)

| Role | Primary Contact | Backup Contact | On-Call Method | Hours |
|---|---|---|---|---|
| SOC Lead | `[Name]` | `[Name]` | Phone/On-call | 24x7 |
| IR Team Lead | `[Name]` | `[Name]` | Phone/On-call | 24x7 |
| Network Security Lead | `[Name]` | `[Name]` | Phone/On-call | 24x7/Business |
| SIEM Engineer | `[Name]` | `[Name]` | Chat + phone | Business/On-call |
| EDR Admin | `[Name]` | `[Name]` | Chat + phone | Business/On-call |
| SOC Manager | `[Name]` | `[Name]` | Phone | Business/On-call |
| CISO | `[Name]` | `[Name]` | Phone | On-call |
| Compliance Lead | `[Name]` | `[Name]` | Phone + email | On-call |
| Legal Counsel | `[Name]` | `[Name]` | Phone + email | On-call |
| MSSP SDM | `[Name]` | `[Name]` | Phone + email | Business/On-call |

> Contact details should be stored in:
`05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/`

---

# 17. Related Documents

| Document | Path |
|---|---|
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| L1 to L2 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md` |
| L2 to L3 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |
| L3 to IR Team Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md` |
| IR Team to Management Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/IR-Team-to-Management-Escalation.md` |
| Internal to MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |
| Bridge Call SOP | `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**