# Role Definition – L1 SOC Analyst

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Role | L1 SOC Analyst |
| Document ID | IR-ROLE-001 |
| Version | 1.0 |
| Owner | SOC Manager |
| Review Cycle | Annual |
| Classification | Internal |

---

## 2. Role Purpose

The L1 SOC Analyst is responsible for:

- 24x7 monitoring of security alerts
- Initial triage and validation of alerts
- Ticket creation and documentation
- Escalation to L2 as required

L1 is the **first line of defense** within the Security Operations Center (SOC).

---

## 3. Reporting Structure

Reports To:
- SOC Lead / Shift Lead

Escalates To:
- L2 Analyst
- SOC Lead (for P1/P2 incidents)

---

## 4. Key Responsibilities

### 4.1 Monitoring
- Monitor SIEM dashboards
- Monitor EDR alerts
- Monitor Firewall / IDS alerts
- Monitor Threat Intelligence alerts

---

### 4.2 Alert Triage
- Validate alert legitimacy
- Identify false positives
- Classify severity (P1–P4)
- Enrich alerts with contextual data

---

### 4.3 Incident Ticketing
- Create ticket in ticketing system
- Document:
  - Time detected
  - Affected asset
  - Source IP/user
  - Alert description
  - Initial findings
- Attach logs/screenshots as evidence

---

### 4.4 Escalation
Escalate to L2 when:
- Suspicious activity confirmed
- Lateral movement suspected
- Malware execution detected
- Data exfiltration suspected
- Privileged account compromise suspected
- P1 or P2 severity identified

---

### 4.5 Communication
- Notify SOC Lead for critical incidents
- Update ticket notes regularly
- Participate in shift handover briefing

---

## 5. Decision Authority

L1 MAY:
- Close confirmed false positives
- Enrich alerts
- Perform basic containment (if predefined in SOP)

L1 MAY NOT:
- Isolate production servers without approval
- Notify clients directly (unless defined)
- Declare major incident independently

---

## 6. Required Skills

- Basic networking knowledge
- Log analysis fundamentals
- Understanding of common attack types
- SIEM query familiarity
- EDR interface usage
- Documentation skills

---

## 7. Performance KPIs

- Mean Time to Detect (MTTD)
- Alert Triage Time
- False Positive Accuracy
- Escalation Accuracy
- Documentation Quality

---

## 8. Tools Used

- SIEM Platform
- EDR Console
- Ticketing System
- Threat Intelligence Platform
- Email Security Gateway
- Firewall Monitoring Console

---

## 9. Compliance Responsibility

L1 must ensure:
- Accurate documentation for audit trails
- Evidence preservation
- SLA adherence
- Proper classification per Severity Matrix

---

## 10. Training Requirements

- SOC onboarding program
- Annual security awareness training
- Tool-specific training
- Playbook training
- Incident simulation participation

---

## 11. Review & Update

This role definition shall be reviewed:
- Annually
- Upon SOC structure change
- After major incident lessons learned

---

**End of Document**