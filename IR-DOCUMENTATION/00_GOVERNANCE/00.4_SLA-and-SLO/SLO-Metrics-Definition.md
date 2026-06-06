# SLO Metrics Definition – Incident Response & SOC Operations

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | SLO Metrics Definition – IR & SOC |
| Document ID | IR-SLO-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the Service Level Objectives (SLOs) for the
SOC and Incident Response program.

SLOs differ from SLAs in that:

| Term | Definition |
|------|------------|
| SLA | Contractual commitment (external/internal) |
| SLO | Internal performance target (operational goal) |
| SLI | Service Level Indicator (the actual measured metric) |

SLOs are used to:
- Measure SOC operational effectiveness
- Identify trends and degradation early
- Drive continuous improvement
- Support management reporting
- Provide input to SLA compliance tracking

---

## 3. Scope

Applies to:
- All SOC tiers (L1/L2/L3)
- SOC Lead operations
- IR Team performance
- MSSP client delivery performance
- Tool and platform performance (SIEM/EDR/Ticketing)

---

## 4. SLO Categories

SLOs are organized into the following categories:

1. Detection & Triage
2. Investigation & Analysis
3. Escalation & Communication
4. Containment & Response
5. Recovery & Closure
6. Reporting & Documentation
7. Tool & Platform Availability
8. Team Performance


---

## 5. SLO Definitions (Detailed)

---

### Category 1 – Detection & Triage

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-001 | Mean Time to Detect (MTTD) | Average time from event occurrence to alert generation in SIEM/EDR | ≤ 5 minutes | Per alert timestamp |
| SLO-002 | Mean Time to Triage (MTTT) | Average time from alert receipt to L1 classification | ≤ 10 minutes (P1/P2) | Ticket timestamps |
| SLO-003 | False Positive Rate | % of alerts closed as false positive vs total alerts | ≤ 30% | Monthly count |
| SLO-004 | Alert Queue Clearance Rate | % of alerts triaged within SLA window per shift | ≥ 95% | Daily report |
| SLO-005 | Missed Alert Rate | % of alerts not actioned within SLA window | ≤ 1% | Daily monitoring |

---

### Category 2 – Investigation & Analysis

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-006 | Mean Time to Investigate (MTTI) | Average time from escalation receipt to L2 investigation start | ≤ 15 minutes (P1/P2) | Ticket timestamps |
| SLO-007 | Investigation Accuracy Rate | % of incidents correctly classified and scoped by L2 | ≥ 95% | QA review |
| SLO-008 | MITRE ATT&CK Mapping Rate | % of confirmed incidents with documented MITRE mapping | ≥ 90% | Ticket audit |
| SLO-009 | Threat Intel Enrichment Rate | % of P1/P2 incidents enriched with TI within 30 minutes | ≥ 95% | Ticket timestamps |
| SLO-010 | Escalation Accuracy Rate | % of L1→L2 escalations that were valid (not noise) | ≥ 85% | L2 feedback loop |

---

### Category 3 – Escalation & Communication

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-011 | Mean Time to Escalate (MTTE) | Average time from triage completion to escalation to next tier | ≤ 10 minutes (P1) | Ticket timestamps |
| SLO-012 | Management Notification Time | Time from P1 declaration to management notification | ≤ 15 minutes | Ticket / email timestamps |
| SLO-013 | Client Notification Time (MSSP) | Time from P1/P2 declaration to client notification | ≤ 15 minutes (P1) ≤ 30 minutes (P2) | Ticket / email timestamps |
| SLO-014 | Bridge Call Activation Time | Time from P1 declaration to bridge call join | ≤ 20 minutes | Bridge call log |
| SLO-015 | Status Update Adherence | % of P1/P2 incidents with status updates within defined cadence | ≥ 95% | Ticket audit |

---

### Category 4 – Containment & Response

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-016 | Mean Time to Contain (MTTC) | Average time from incident declaration to containment action completion | ≤ 1 hour (P1) ≤ 2 hours (P2) | Ticket timestamps |
| SLO-017 | Containment Success Rate | % of containment actions that successfully stopped threat progression | ≥ 95% | Post-incident review |
| SLO-018 | IR Team Activation Time | Time from P1 trigger to IR Team active engagement | ≤ 30 minutes | Ticket / bridge log |
| SLO-019 | Unauthorized Lateral Movement Rate | % of confirmed incidents where lateral movement was not detected before containment | ≤ 5% | PIR review |
| SLO-020 | Reinfection Rate | % of eradicated incidents that reoccurred within 30 days | ≤ 2% | Incident register |

---

### Category 5 – Recovery & Closure

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-021 | Mean Time to Recover (MTTR) | Average time from containment to full service restoration | ≤ 4 hours (P1) ≤ 8 hours (P2) | Ticket timestamps |
| SLO-022 | Incident Closure Rate | % of incidents formally closed within defined SLA window | ≥ 98% | Ticket audit |
| SLO-023 | Post-Incident Review Completion | % of P1/P2 incidents with PIR completed within 5 business days | ≥ 95% | PIR register |
| SLO-024 | RCA Completion Rate | % of P1/P2 incidents with documented RCA | ≥ 95% | RCA register |
| SLO-025 | Corrective Action Closure Rate | % of PIR action items closed within agreed deadlines | ≥ 90% | Action tracker |

---

### Category 6 – Reporting & Documentation

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-026 | Daily SOC Report Delivery | % of daily reports delivered on time | ≥ 98% | Report log |
| SLO-027 | Incident Report Delivery (P1/P2) | % of final incident reports delivered within SLA | ≥ 95% | Report log |
| SLO-028 | Ticket Documentation Quality | % of tickets meeting documentation quality standards on QA review | ≥ 90% | QA audit |
| SLO-029 | Monthly Client Report Delivery | % of MSSP monthly reports delivered on time | ≥ 98% | Report log |
| SLO-030 | Evidence Completeness Rate | % of P1/P2 incidents with complete evidence log and CoC records | ≥ 98% | Evidence audit |

---

### Category 7 – Tool & Platform Availability

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-031 | SIEM Availability | % uptime of SIEM platform | ≥ 99.5% | Platform monitoring |
| SLO-032 | EDR Console Availability | % uptime of EDR console | ≥ 99.5% | Platform monitoring |
| SLO-033 | Ticketing System Availability | % uptime of ticketing system | ≥ 99.5% | Platform monitoring |
| SLO-034 | SIEM Ingestion Lag | % of time SIEM log ingestion lag exceeds 5 minutes | ≤ 1% | SIEM health check |
| SLO-035 | EDR Agent Coverage | % of endpoints with active and healthy EDR agent | ≥ 98% | EDR coverage report |

---

### Category 8 – Team Performance

| SLO ID | Metric | Definition | Target | Measurement |
|--------|--------|------------|--------|-------------|
| SLO-036 | Analyst Shift Coverage | % of shifts with required analyst headcount | ≥ 98% | Shift roster |
| SLO-037 | Training Completion Rate | % of SOC staff with mandatory annual training complete | 100% | Training register |
| SLO-038 | Tabletop Exercise Completion | Annual tabletop exercises completed | ≥ 2 per year | Exercise register |
| SLO-039 | SLA Breach Rate | % of incidents where at least one SLA metric was breached | ≤ 2% | SLA breach register |
| SLO-040 | Client Satisfaction Score | Average client satisfaction rating (post-incident/QBR) | ≥ 4.0 / 5.0 | Survey results |

---

## 6. SLO Measurement Process

### 6.1 Data Sources
- Ticketing system timestamps
- SIEM alert logs
- EDR console logs
- Bridge call records
- Report delivery logs
- QA audit records
- Client survey results

### 6.2 Measurement Frequency

| SLO Category | Measurement Frequency |
|-------------|----------------------|
| Detection & Triage | Daily |
| Investigation & Analysis | Weekly |
| Escalation & Communication | Per incident + Weekly |
| Containment & Response | Per incident + Weekly |
| Recovery & Closure | Per incident + Monthly |
| Reporting & Documentation | Monthly |
| Tool & Platform | Daily |
| Team Performance | Monthly |

---

## 7. SLO Reporting

SLO metrics are reported in:

| Report | Audience | Frequency |
|--------|---------|-----------|
| Daily SOC Metrics Dashboard | SOC Lead / Manager | Daily |
| Weekly Incident Summary | Management | Weekly |
| Monthly Metrics Report | Management / Client | Monthly |
| Quarterly SLA/SLO Review | CISO / Client | Quarterly |
| Annual IR Review | CISO / Board | Annual |

Reference:
`07_REPORTING/07.2_Operational-Reports/`

---

## 8. SLO Threshold Breach Actions

| SLO Performance | Action |
|----------------|--------|
| Meeting target (≥ defined %) | No action – maintain |
| At risk (within 5% of target) | SOC Lead review within 1 week |
| Breaching target (below threshold) | SOC Manager investigation + corrective action |
| Repeated breach (2+ months) | Formal improvement plan + CISO briefing |

---

## 9. SLO Review & Adjustment

SLOs shall be reviewed:
- Quarterly (standard review)
- After major incidents
- Upon tooling changes
- Upon team structure changes
- Upon client contract changes (MSSP)

---

## 10. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**