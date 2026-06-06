# Ticket Escalation Workflow

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Ticket Escalation Workflow |
| Document ID | TOOL-TKT-003 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the escalation workflow for security tickets within the SOC ticketing system.

Proper escalation is critical because:

- Delayed escalation directly increases attacker dwell time
- Incorrect escalation wastes resources and delays response
- Missing escalation documentation creates audit gaps
- SLA breaches occur when escalation timelines are not followed
- MSSP client contracts define escalation obligations
- Regulatory requirements mandate documented escalation chains

This document ensures:

- Clear escalation triggers at every tier
- Defined escalation paths from L1 through IR Team
- Documented ownership transfer at each escalation point
- SLA-compliant escalation timelines
- Audit-ready escalation records in every ticket
- MSSP client escalation compliance

---

# 3. Scope

This workflow applies to all escalation activities across:

| Scope Area | Examples |
|---|---|
| Tier escalations | L1 to L2, L2 to L3, L3 to IR Team |
| Management escalations | IR Team to SOC Manager to CISO |
| Client escalations | MSSP client notification escalations |
| Tool-based escalations | SIEM/EDR auto-escalation triggers |
| Regulatory escalations | RBI, CERT-In notification triggers |
| Cross-team escalations | Legal, HR, Compliance involvement |

---

# 4. Escalation Principles

| Principle | Requirement |
|---|---|
| Escalate early | When in doubt escalate up |
| Document every escalation | In ticket before escalating |
| Named ownership transfer | Receiving analyst must be named |
| No silent escalation | Verbal + ticket update mandatory |
| SLA clock continues | Escalation does not reset SLA |
| Receiving party must acknowledge | Acknowledgment documented in ticket |

---

# 5. Roles and Escalation Authority

| Role | Escalation Authority |
|---|---|
| L1 Analyst | Escalate to L2 or SOC Lead |
| L2 Analyst | Escalate to L3 or SOC Lead |
| L3 Analyst | Escalate to IR Team or SOC Lead |
| SOC Lead | Escalate to IR Team or Management |
| IR Team Lead | Escalate to SOC Manager / CISO |
| SOC Manager | Escalate to CISO / Legal / Regulatory |

---

# 6. Escalation Tier Overview

| Escalation Level | From | To | Trigger |
|---|---|---|---|
| Tier 1 Escalation | L1 Analyst | L2 Analyst | Confirmed or suspected TP requiring deep investigation |
| Tier 2 Escalation | L2 Analyst | L3 Analyst | Advanced forensics or malware analysis required |
| Tier 3 Escalation | L3 Analyst | IR Team | Active compromise confirmed |
| Management Escalation | IR Team | SOC Manager / CISO | P1 incident or regulatory trigger |
| Regulatory Escalation | SOC Manager | RBI / CERT-In | Reportable incident threshold met |
| Client Escalation | SOC Lead | MSSP Client | Client notification threshold met |

---

# 7. Tier 1 Escalation — L1 to L2

---

## 7.1 Escalation Triggers

L1 must escalate to L2 when any of the following are observed:

| Trigger | Reason |
|---|---|
| Alert confirmed as True Positive | Requires deeper investigation |
| Malware or ransomware indicators found | L2 investigation required |
| Privileged account suspicious activity | High risk requires L2 |
| Multiple hosts showing same alert pattern | Potential campaign |
| Lateral movement indicators | L2 network investigation required |
| Phishing with confirmed credential harvest | BEC or account takeover risk |
| IOC match with high-confidence threat intel | Threat actor activity possible |
| L1 investigation exceeds 30 minutes without resolution | Escalate for efficiency |
| P1 or P2 severity assigned | Mandatory L2 involvement |
| Uncertainty on FP/TP decision | Escalate rather than close incorrectly |

---

## 7.2 L1 Pre-Escalation Checklist

Before escalating L1 must complete:

| Task | Requirement |
|---|---|
| Alert reviewed in SIEM/EDR | Mandatory |
| Host and user context checked | Mandatory |
| Related alerts searched | Mandatory |
| Initial findings documented in ticket | Mandatory |
| Severity assigned | Mandatory |
| Escalation reason written in ticket | Mandatory |

---

## 7.3 Escalation Documentation Standard (Ticket Update)

L1 must add the following to the ticket before escalating:

| Field | Requirement |
|---|---|
| Escalation timestamp (UTC) | Mandatory |
| Escalated to | Named L2 analyst |
| Escalation reason | Technical justification |
| Actions taken so far | Summary of L1 work |
| Key findings | What was observed |
| Evidence references | Alert IDs, screenshots, queries |
| Recommended next steps | L1 recommendation |

---

## 7.4 L2 Acknowledgment Requirement

| Requirement | Standard |
|---|---|
| L2 must acknowledge in ticket | Within SLA timeline |
| L2 must confirm receipt verbally | Mandatory for P1/P2 |
| L2 must update ticket as new owner | Mandatory |

---

## 7.5 SLA for Tier 1 Escalation

| Priority | L1 Escalation Decision | L2 Acknowledgment |
|---|---|---|
| P1 | Immediate | Within 15 minutes |
| P2 | Within 30 minutes | Within 30 minutes |
| P3 | Within 2 hours | Within 2 hours |
| P4 | As needed | Within 4 hours |

---

# 8. Tier 2 Escalation — L2 to L3

---

## 8.1 Escalation Triggers

L2 must escalate to L3 when:

| Trigger | Reason |
|---|---|
| Malware sample requires reverse engineering | L3 malware analysis capability |
| Memory forensics required | L3 forensics capability |
| Disk forensics required | L3 forensics capability |
| Advanced persistent threat indicators | L3 attribution and analysis |
| Rootkit or bootkit suspected | L3 advanced analysis |
| Novel or unknown attack technique | L3 research capability |
| Zero-day exploitation suspected | L3 + vendor coordination |
| Supply chain compromise suspected | L3 investigation scope |
| APT campaign indicators | L3 threat intel integration |
| Incident scope beyond L2 capability | Mandatory escalation |

---

## 8.2 L2 Pre-Escalation Checklist

Before escalating L2 must complete:

| Task | Requirement |
|---|---|
| Full investigation scope documented | Mandatory |
| Evidence collected and preserved | Mandatory |
| Timeline of events built | Mandatory |
| IOCs identified and documented | Mandatory |
| Affected systems inventoried | Mandatory |
| Escalation package prepared | Mandatory |
| Ticket fully updated | Mandatory |

---

## 8.3 Escalation Package Contents

L2 must prepare an escalation package containing:

| Item | Requirement |
|---|---|
| Incident summary | Current understanding of incident |
| Timeline | Events in chronological order |
| Affected assets | All hosts and accounts identified |
| IOC list | All indicators collected |
| Evidence references | All evidence locations |
| MITRE ATT&CK mapping | Techniques identified |
| L2 hypothesis | Current assessment |
| Requested L3 actions | What L3 needs to do |

---

## 8.4 SLA for Tier 2 Escalation

| Priority | L2 Escalation Decision | L3 Acknowledgment |
|---|---|---|
| P1 | Immediate | Within 15 minutes |
| P2 | Within 1 hour | Within 30 minutes |
| P3 | Within 4 hours | Within 2 hours |

---

# 9. Tier 3 Escalation — L3 to IR Team

---

## 9.1 Escalation Triggers

L3 must escalate to IR Team when:

| Trigger | Reason |
|---|---|
| Active compromise confirmed | IR Team activation required |
| Ransomware confirmed active | IR Team containment authority |
| Data exfiltration confirmed | IR Team and legal notification |
| Domain-wide compromise | IR Team scope management |
| Critical system compromised | IR Team decision authority |
| Business continuity impact | IR Team crisis coordination |
| Regulatory notification required | IR Team + compliance |
| Onsite forensic response needed | IR Team deployment |
| Multi-client MSSP impact | IR Team multi-tenant coordination |

---

## 9.2 IR Team Activation Documentation

L3 must document in ticket:

| Field | Requirement |
|---|---|
| IR Team activation timestamp (UTC) | Mandatory |
| Activation trigger | Specific reason |
| Current incident status | Full summary |
| Containment status | What has been done |
| Evidence status | What has been preserved |
| Business impact assessment | Current known impact |
| Recommended immediate actions | L3 recommendation |

---

## 9.3 SLA for Tier 3 Escalation

| Priority | IR Team Notification | IR Team Acknowledgment |
|---|---|---|
| P1 | Immediate | Within 15 minutes |
| P2 | Within 30 minutes | Within 30 minutes |

---

# 10. Management Escalation

---

## 10.1 Management Escalation Triggers

| Trigger | Notification Required |
|---|---|
| P1 incident declared | SOC Manager + CISO |
| Data breach confirmed | CISO + Legal Counsel |
| Regulatory notification required | CISO + Compliance |
| Major client impact (MSSP) | SOC Manager + Account Manager |
| Media or reputational risk | CISO + Communications |
| Law enforcement engagement required | CISO + Legal |
| SLA breach on P1/P2 | SOC Manager |

---

## 10.2 Management Notification Standards

| Field | Requirement |
|---|---|
| Notification method | Phone call + email |
| Notification time (UTC) | Documented in ticket |
| Notified person | Named in ticket |
| Summary provided | Incident status and impact |
| Next update time | Committed and documented |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`

---

# 11. Regulatory Escalation

---

## 11.1 Regulatory Escalation Triggers

| Trigger | Regulatory Body |
|---|---|
| Major cyber incident in BFSI | RBI |
| Data breach affecting customers | RBI + CERT-In |
| Critical infrastructure impact | CERT-In |
| Ransomware on production systems | CERT-In |
| Supply chain compromise | CERT-In |

---

## 11.2 Regulatory Notification Process

| Step | Action | Owner |
|---|---|---|
| Step 1 | Confirm regulatory threshold met | SOC Lead / IR Team |
| Step 2 | Notify CISO and Compliance | IR Team Lead |
| Step 3 | Prepare regulatory report | Compliance + IR Team |
| Step 4 | Submit within required timeline | Compliance team |
| Step 5 | Document submission in ticket | Mandatory |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 12. MSSP Client Escalation

---

## 12.1 Client Escalation Triggers

| Trigger | Action |
|---|---|
| P1 incident on client environment | Immediate client notification |
| P2 incident confirmed | Client notification within 1 hour |
| Data breach suspected | Immediate client notification |
| SLA breach risk | Proactive client notification |
| Regulatory reporting required | Client + compliance team |

---

## 12.2 Client Escalation Documentation

| Field | Requirement |
|---|---|
| Client notified (named contact) | Mandatory |
| Notification method | Phone + email |
| Notification timestamp (UTC) | Mandatory |
| Summary communicated | Documented in ticket |
| Client response/instruction | Documented in ticket |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 13. Escalation Failure Scenarios

| Failure | Risk | Prevention |
|---|---|---|
| L1 closes TP as FP without escalation | Threat persists undetected | Mandatory escalation criteria checklist |
| L2 delays escalation to L3 | Forensic evidence lost | Time-bound escalation SLA |
| IR Team not notified of P1 | Management unaware | Auto-escalation triggers |
| Regulatory notification missed | Regulatory penalty | Notification checklist in ticket |
| Client not notified | SLA breach | Client notification checklist |
| No acknowledgment documented | Audit gap | Mandatory acknowledgment in ticket |

---

# 14. Escalation Ticket Documentation Checklist

Every escalation must have the following in the ticket:

| Item | Requirement |
|---|---|
| Escalation timestamp (UTC) | Mandatory |
| Escalation trigger reason | Mandatory |
| Escalated to (named person) | Mandatory |
| Actions completed before escalation | Mandatory |
| Evidence references | Mandatory |
| Receiving analyst acknowledgment | Mandatory |
| Next update commitment | Mandatory |

---

# 15. Related Documents

| Document | Path |
|---|---|
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Priority Matrix | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Ticket Closure Criteria | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Closure-Criteria.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| L1 to L2 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md` |
| L2 to L3 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |

---

# 16. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**