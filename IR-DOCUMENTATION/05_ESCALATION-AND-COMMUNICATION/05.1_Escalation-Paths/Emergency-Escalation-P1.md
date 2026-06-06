# Emergency Escalation – P1 (Critical Incident)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Emergency Escalation (P1) |
| Document ID | ESC-PATH-001 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | SOC Manager / SOC Operations Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the **mandatory emergency escalation process** for **P1 (Critical)** incidents to ensure:

- Immediate activation of incident response leadership and key stakeholders
- SLA-compliant response and continuous status updates
- Clear decision-making authority for containment actions
- Audit-ready documentation of escalation actions, approvals, and timelines
- MSSP client escalation compliance (where applicable)
- Regulatory notification readiness (RBI/CERT-In or other regulators as applicable)

This SOP is designed for scenarios where **minutes matter** and rapid coordination is required to limit business impact.

---

# 3. Scope

This SOP applies to all **P1 incidents**, including (not limited to):

| P1 Scenario | Examples |
|---|---|
| Ransomware | Encryption in progress, ransom note on production systems |
| Data breach/exfiltration | Confirmed sensitive data transfer to unknown destination |
| Privileged compromise | Domain admin takeover, DC compromise, DCSync |
| Major service outage | DDoS causing unavailability of critical services |
| Active C2 at scale | Multiple hosts beaconing to known malicious infrastructure |
| Supply chain compromise | Trusted software update delivering malicious code |
| Cloud compromise | Root/API key compromise, mass resource modification |

This SOP covers escalation across:

- L1/L2/L3 SOC tiers
- SOC Lead and IR Team activation
- Management and executive notification
- MSSP client notification
- Compliance/Legal and regulatory readiness

---

# 4. Definitions

| Term | Definition |
|---|---|
| P1 | Critical incident with active compromise or severe business impact |
| Bridge call | Dedicated incident coordination call for P1/P2 incidents |
| War room | Collaboration channel (chat + call + ticket) for incident coordination |
| Containment authority | Approved roles who can isolate systems, disable accounts, block traffic |
| MTTA | Mean Time to Acknowledge |
| MTTR | Mean Time to Respond/Resolve (as defined in SLO metrics) |

References:  
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md`  
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 5. Roles and Responsibilities (P1)

| Role | Responsibilities |
|---|---|
| L1 Analyst | Immediate ticket creation, triage, declare suspected P1, notify SOC Lead |
| SOC Lead | Confirms P1, initiates bridge call, coordinates tiers, manages SLA + comms cadence |
| L2 Analyst | Deep investigation, scope expansion, IOC identification, evidence preservation |
| L3 Analyst | Advanced forensics/malware analysis, root cause confirmation, attacker TTP validation |
| IR Team Lead | Owns containment decisions and incident command; directs eradication/recovery |
| SOC Manager | Executive coordination; approvals for high-impact actions; ensures documentation quality |
| CISO | Executive decision-making; regulatory readiness; external coordination as needed |
| IT Ops / Cloud Ops | Executes remediation, restores services, supports isolation and patching |
| Compliance / Legal | Regulatory assessment, notifications, legal hold guidance, law enforcement engagement |
| MSSP Service Delivery | Client coordination, client comms, SLA compliance for client notifications |

Reference:  
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 6. P1 Declaration Triggers (Mandatory)

A ticket must be treated as **suspected P1** and escalated immediately if any are true:

| Trigger | Examples |
|---|---|
| Active encryption/disruption | Ransomware encryption observed |
| Confirmed data exfil | Large transfer to unknown external destination |
| Domain compromise indicators | LSASS dump + DA login anomalies; DCSync |
| Multiple systems impacted | Rapid spread to multiple hosts/subnets |
| Critical system impacted | Payment, identity, core banking, production ERP |
| Confirmed external attacker control | Interactive sessions, C2 confirmed |
| Material outage | Service down impacting customers/operations |
| Confirmed zero-day exploitation | Active exploitation in environment |

If unsure, **escalate as P1** and downgrade later with SOC Lead approval.

---

# 7. SLA Targets (P1 Emergency)

| Activity | Target Time |
|---|---:|
| Ticket creation | Immediate |
| SOC Lead notified | ≤ 15 minutes |
| P1 confirmation decision | ≤ 15 minutes from suspicion |
| IR Team activation | ≤ 30 minutes |
| Bridge call started | ≤ 30 minutes |
| First management notification | ≤ 30 minutes |
| Status updates (minimum) | Every 30 minutes |
| Containment decision | As soon as evidence supports action (documented) |

Reference:  
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 8. Emergency Escalation Workflow (P1)

## 8.1 Step 1 — Immediate Actions (L1 / First Responder)

1. **Create or update incident ticket** (mandatory)
2. Assign **P1 (Critical)** priority (suspected P1 acceptable)
3. Capture minimum details:
   - detection source (SIEM/EDR/user/client)
   - affected hosts/users
   - detection time (UTC)
   - initial evidence references (alert IDs, screenshots, queries)
4. Notify SOC Lead immediately (phone + chat + ticket mention)
5. If automation exists (SOAR), ensure incident bridge workflow is triggered

Mandatory ticket fields reference:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

## 8.2 Step 2 — SOC Lead P1 Validation and Command Setup

SOC Lead must:

1. Confirm P1 status against P1 definition
2. Initiate **bridge call** and create **war room channel**
3. Assign incident roles:
   - Incident Commander (IR Team Lead or SOC Lead until IR arrives)
   - Communications Lead (SOC Lead / MSSP SDM as applicable)
   - Technical Lead (L2/L3)
4. Confirm escalation to IR Team Lead + SOC Manager
5. Establish status update cadence (every 30 minutes minimum)

Reference:  
`03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md`

---

## 8.3 Step 3 — IR Team Activation (Mandatory)

IR Team Lead must be activated and must:

- Confirm containment authority plan
- Decide initial containment strategy (host isolation, account disablement, firewall blocks)
- Confirm evidence preservation requirements (memory/disk/logs)
- Coordinate with IT Ops for execution and rollback

Reference:  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 8.4 Step 4 — Management and Executive Escalation (Mandatory)

Within **30 minutes** of P1 confirmation, notify:

- SOC Manager
- CISO
- Relevant IT leadership (IT Ops/Cloud Ops lead)
- Compliance/Legal (if breach or regulatory triggers likely)

Minimum message must include:

- Incident summary (what/where/when)
- Current impact and risk
- Actions taken and planned next actions
- Next update time

Reference:  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`

---

## 8.5 Step 5 — Client Escalation (MSSP) (If Applicable)

For MSSP-managed incidents:

- Notify client within contractual SLA (P1: immediate/within 30 minutes typical)
- Use approved client communication template
- Document client approvals/instructions in ticket
- Ensure tenant segregation and evidence handling requirements

Reference:  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

## 8.6 Step 6 — Regulatory Readiness Check (If Applicable)

Compliance/Legal + CISO must assess reportability:

- RBI incident reporting requirements (BFSI)
- CERT-In reporting guidelines (as applicable)
- Contractual notification obligations

Document in ticket:

- Whether regulatory reporting is required (Yes/No)
- Decision owner and time (UTC)
- If yes, report workflow initiated and reference ID(s)

Reference:  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

---

# 9. P1 Bridge Call Operating Rules (Mandatory)

## 9.1 Attendance (Minimum)

- SOC Lead (chair)
- L2/L3 technical leads
- IR Team Lead (incident commander once active)
- IT Ops lead (and cloud/network leads as needed)
- SOC Manager / CISO (as needed)
- MSSP client representative (if MSSP and contract allows)

## 9.2 Cadence

- Status update every **30 minutes** minimum
- Immediate updates for major events:
  - confirmed exfiltration
  - containment executed
  - ransomware spread
  - critical service outage/restoration
  - regulator/client notification sent

## 9.3 Documentation

SOC Lead must ensure:

- Bridge call notes are recorded in ticket or linked doc
- All decisions have owner + timestamp (UTC)
- All containment actions include authorization and executor

Reference:  
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md`

---

# 10. P1 Escalation Documentation Checklist (Mandatory)

Every P1 escalation must include in the ticket:

| Item | Requirement |
|---|---|
| P1 declaration time (UTC) | Mandatory |
| Declared by | Mandatory |
| SOC Lead notified time (UTC) | Mandatory |
| IR Team activation time (UTC) | Mandatory |
| Bridge call start time (UTC) | Mandatory |
| Stakeholders notified (names/times) | Mandatory |
| Containment decisions (authorized by, executed by, time) | Mandatory |
| Evidence preserved references | Mandatory |
| Client notification details (MSSP) | Mandatory if applicable |
| Regulatory assessment decision | Mandatory |

Reference:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 11. Escalation Failure Handling (If SLA at Risk)

If any P1 SLA target is at risk:

1. SOC Lead escalates to SOC Manager immediately
2. SOC Manager escalates to CISO if resources/authority needed
3. Document:
   - reason for delay
   - mitigation steps
   - revised timeline
4. If MSSP, notify client proactively when delay may impact SLA

Reference:  
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP P1 events:

- Confirm incident is scoped to correct tenant/client
- Ensure evidence and comms are tenant segregated
- Ensure no cross-client indicators or data are disclosed
- Use client-specific escalation matrix and contacts

Reference:  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Related Documents

| Document | Path |
|---|---|
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| L1 to L2 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md` |
| L2 to L3 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |
| L3 to IR Team Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md` |
| IR Team to Management Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/IR-Team-to-Management-Escalation.md` |
| SOCLead P1/P2 Bridge Call SOP | `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| RBI Incident Reporting SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |

---

# 14. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | SOC Manager / SOC Operations Lead | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**