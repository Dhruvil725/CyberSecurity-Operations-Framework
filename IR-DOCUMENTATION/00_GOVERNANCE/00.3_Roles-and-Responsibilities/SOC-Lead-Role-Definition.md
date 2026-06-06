# Role Definition – SOC Lead (Shift Lead / Incident Coordinator)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Role | SOC Lead |
| Document ID | IR-ROLE-004 |
| Version | 1.0 |
| Owner | Head of SOC / SOC Manager |
| Review Cycle | Annual |
| Classification | Confidential |

---

## 2. Role Purpose

The SOC Lead is responsible for operational leadership of the SOC during a shift and acts as the primary incident coordinator for P1/P2 incidents. The SOC Lead ensures:

- Consistent triage quality and SLA adherence
- Effective escalation and cross-team coordination
- Accurate and timely communication (internal + MSSP client)
- Proper incident documentation and closure standards

---

## 3. Reporting Structure

Reports To:
- SOC Manager / Head of SOC

Leads:
- L1 Analysts (shift)
- L2 Analysts (shift, as applicable)

Coordinates With:
- L3 Analysts
- Incident Response Team (IRT)
- IT / Network / Cloud Operations
- GRC / Compliance / Legal (as needed)
- MSSP Client contacts (per contract)

---

## 4. Key Responsibilities

### 4.1 Shift Operations Management
- Assign alert queues and priorities to analysts
- Ensure continuous monitoring coverage
- Conduct shift handover and briefing
- Validate quality of ticket notes and artifacts

### 4.2 Incident Coordination (P1/P2)
- Act as Incident Coordinator until IRT assumes command (if applicable)
- Initiate bridge call / war room for major incidents
- Ensure tasks are assigned, tracked, and updated
- Maintain incident timeline and status updates cadence

### 4.3 Escalation & Decision Governance
- Enforce escalation criteria L1→L2→L3→IRT
- Approve/deny high-impact containment actions as per authority matrix
- Ensure executive notification triggers are met
- Ensure client notification follows SLA and communication templates

### 4.4 Stakeholder Communication
- Provide regular updates to management for P1/P2
- Coordinate technical updates with L2/L3 and IR Team
- Ensure client communications are accurate, timely, and approved
- Ensure regulatory communication is initiated through Compliance/CISO where required

### 4.5 SLA / SLO Management
- Track SLA timers for triage, response, and escalation
- Record SLA breaches and trigger breach procedure
- Ensure correct severity classification and prioritization
- Identify operational bottlenecks and propose improvements

### 4.6 Quality Assurance (QA)
- Review incident tickets before closure for completeness:
  - evidence attached
  - clear narrative
  - timeline
  - actions taken
  - next steps / recommendations
- Monitor false-positive trends and initiate tuning requests
- Ensure playbooks/SOPs are followed or deviations documented

---

## 5. Decision Authority

SOC Lead MAY:
- Reclassify severity (P1–P4) with justification
- Initiate incident bridge call for P1/P2
- Approve defined containment actions (as per Containment Authority Matrix)
- Direct analyst workload and investigation approach
- Escalate to IRT and management based on triggers

SOC Lead MAY NOT (without required approvals):
- Authorize regulatory submissions (Compliance/CISO)
- Approve business-impacting actions outside authority (e.g., shutting down critical services)
- Provide legal statements or public communication

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 6. Required Skills

- Strong incident coordination and prioritization
- Advanced understanding of SOC operations and workflows
- SIEM/EDR operational expertise (not necessarily deep forensics)
- Communication and stakeholder management
- Knowledge of incident severity models and SLAs
- Ability to drive decisions under time pressure

---

## 7. Performance KPIs

- SLA compliance rate (triage/escalation/response)
- Mean time to engage stakeholders (P1/P2)
- Ticket quality score / audit readiness
- Escalation accuracy (right tier, right time)
- Reduction in repeat incidents through improvement actions
- Shift handover quality and operational continuity

---

## 8. Tools Used

- SIEM console and dashboards
- EDR console (containment status/visibility)
- Ticketing platform (workflow + approvals)
- Communication channels (bridge calls, email, chat ops)
- Threat intelligence portal (context enrichment)

---

## 9. Compliance Responsibility

The SOC Lead ensures:
- Incidents are properly categorized and recorded for audit trails
- Evidence handling procedures are initiated and followed
- Required notifications are triggered on time (internal/client/regulatory via appropriate owners)
- Documentation supports ISO 27001 / NIST / RBI expectations

---

## 10. Review & Update

This role definition shall be reviewed:
- Annually
- After major incidents (PIR outcomes)
- Upon SOC operating model or tooling changes

---

**End of Document**