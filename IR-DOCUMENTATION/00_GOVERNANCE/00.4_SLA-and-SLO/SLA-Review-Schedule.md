# SLA Review Schedule – Incident Response & SOC Operations

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | SLA Review Schedule – IR & SOC |
| Document ID | IR-SLA-004 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager / Service Delivery Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Annual |

---

## 2. Purpose

This document defines the schedule, process, participants,
and outputs for regular SLA and SLO review activities across:

- Internal SOC SLA performance
- MSSP client SLA compliance
- SLO metric trending and improvement

Regular reviews ensure:
- SLAs remain relevant and achievable
- Breaches are identified and corrected early
- Clients are kept informed of service performance
- Continuous improvement is structured and tracked
- Compliance with ISO 27001 / NIST / RBI expectations

---

## 3. Scope

Applies to:
- All SOC tiers (L1/L2/L3)
- SOC Lead / Shift Lead
- IR Team
- MSSP Service Delivery Manager (SDM)
- SOC Manager / Head of SOC
- MSSP Clients (for client-facing reviews)
- GRC / Compliance (for regulatory review alignment)

---

## 4. Review Types & Schedule Overview

| Review Type | Frequency | Primary Audience | Owner |
|------------|-----------|-----------------|-------|
| Daily SLA Monitoring Check | Daily | SOC Lead | SOC Lead |
| Weekly SLA Performance Review | Weekly | SOC Manager | SOC Manager |
| Monthly SLA Compliance Review | Monthly | Management / Client | SOC Manager / SDM |
| Quarterly SLA & SLO Formal Review | Quarterly | CISO / Client | SOC Manager / SDM |
| Annual SLA Document Review | Annual | CISO / Management | SOC Manager / SDM |
| Ad-hoc Review (post breach/incident) | As needed | SOC Manager / CISO | SOC Manager |

---

## 5. Daily SLA Monitoring Check

### Purpose
Ensure real-time SLA adherence during each shift.

### Frequency
Every shift (minimum once per 24 hours)

### Owner
SOC Lead / Shift Lead

### Activities
- [ ] Review open incident tickets for SLA timer status
- [ ] Identify any at-risk (≥75% of SLA time consumed) tickets
- [ ] Verify alert queue clearance rate
- [ ] Check shift handover notes for SLA issues
- [ ] Escalate any at-risk or breached SLAs immediately

### Output
- Shift SLA status noted in shift handover document
- Breach notification (if applicable)

Reference:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`

---

## 6. Weekly SLA Performance Review

### Purpose
Review SLA performance across the past 7 days and identify trends.

### Frequency
Every Monday (or first working day of the week)

### Owner
SOC Manager

### Participants
- SOC Lead(s)
- SOC Manager
- L2/L3 representatives (as needed)

### Agenda

| # | Agenda Item | Time |
|---|------------|------|
| 1 | Review of weekly incident count by severity | 10 mins |
| 2 | SLA compliance metrics review (per severity) | 10 mins |
| 3 | SLA breaches review (if any) | 10 mins |
| 4 | False positive rate and alert queue health | 5 mins |
| 5 | Tool and platform availability issues | 5 mins |
| 6 | Open action items from previous week | 5 mins |
| 7 | Actions and owners for this week | 5 mins |

### Output
- Weekly SLA summary notes
- Action items logged in tracker

Reference:
`07_REPORTING/07.2_Operational-Reports/Weekly-Incident-Summary.md`

---

## 7. Monthly SLA Compliance Review

### Purpose
Formal review of monthly SLA and SLO performance including
MSSP client reporting.

### Frequency
First week of each month (covering previous month)

### Owner
SOC Manager / MSSP SDM

### Participants

**Internal:**
- SOC Manager
- SOC Lead(s)
- IR Team Lead (if applicable)
- GRC / Compliance representative

**MSSP Client (separate call per client):**
- MSSP SDM
- Client Primary Security Contact
- Client IT/Operations representative (if needed)

### Agenda

| # | Agenda Item | Time |
|---|------------|------|
| 1 | Monthly incident summary (count/severity/type) | 10 mins |
| 2 | SLA compliance scorecard review | 10 mins |
| 3 | SLO metrics performance review | 10 mins |
| 4 | SLA breaches review and corrective actions | 10 mins |
| 5 | Tool availability and coverage review | 5 mins |
| 6 | Open improvement actions status | 10 mins |
| 7 | Client feedback (MSSP calls) | 10 mins |
| 8 | Next month focus areas | 5 mins |

### Output
- Monthly SLA Compliance Report
- Monthly Client Report (MSSP)
- Updated action tracker

Reference:
`07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Monthly-Client-Report.md`

---

## 8. Quarterly SLA & SLO Formal Review

### Purpose
Comprehensive review of SLA and SLO performance, trends,
and formal document review. This is the primary governance
review and feeds into board-level reporting.

### Frequency
Quarterly (January / April / July / October – first 2 weeks)

### Owner
SOC Manager / SDM / CISO

### Participants

**Internal:**
- CISO
- SOC Manager
- IR Team Lead
- SDM (MSSP)
- GRC / Compliance

**MSSP Client (Quarterly Business Review):**
- MSSP SDM + Account Manager
- Client CISO / Security Head
- Client Compliance (if applicable)

### Agenda

| # | Agenda Item | Time |
|---|------------|------|
| 1 | Quarter summary – incident landscape | 10 mins |
| 2 | SLA compliance quarterly scorecard | 15 mins |
| 3 | SLO trend analysis (3-month view) | 15 mins |
| 4 | SLA breach analysis and lessons learned | 10 mins |
| 5 | Tool performance and coverage trends | 10 mins |
| 6 | Threat landscape update | 10 mins |
| 7 | Service improvement actions review | 10 mins |
| 8 | SLA document amendments (if required) | 10 mins |
| 9 | Client priorities for next quarter | 10 mins |
| 10 | Sign-off on updated SLA documents (if amended) | 5 mins |

### Output
- Quarterly Trend Analysis Report
- Updated SLA document (if amended)
- QBR presentation/deck
- Signed amendment (if SLA changes agreed)
- Updated action tracker

Reference:
`07_REPORTING/07.2_Operational-Reports/Quarterly-Trend-Analysis.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`

---

## 9. Annual SLA Document Review

### Purpose
Full formal review and revalidation of all SLA and SLO
documents to ensure they remain current, relevant, and aligned
with operational realities and regulatory requirements.

### Frequency
Annual (aligned with ISMS annual review cycle)

### Owner
SOC Manager / CISO

### Participants
- CISO
- SOC Manager
- GRC / Compliance
- IR Team Lead
- SDM (MSSP)
- Legal (if contractual changes required)

### Review Checklist

| # | Review Item | Completed |
|---|------------|-----------|
| 1 | Review Internal-SLA-Definitions.md for relevance | |
| 2 | Review all MSSP Client SLA templates | |
| 3 | Review SLO metrics targets vs actual performance | |
| 4 | Review SLA Breach Escalation Procedure | |
| 5 | Review SLA Breach Register for patterns | |
| 6 | Assess tool/platform changes impacting SLAs | |
| 7 | Assess regulatory changes impacting SLAs (RBI/ISO/NIST) | |
| 8 | Assess team structure changes impacting SLAs | |
| 9 | Update documents with new version/date | |
| 10 | Obtain sign-off from CISO and relevant owners | |
| 11 | Communicate changes to all SOC staff | |
| 12 | Communicate changes to MSSP clients (if applicable) | |

### Output
- Updated SLA documents (all 4 files in this folder)
- Version history updated
- Distribution email to SOC team
- Client notifications (if SLA changes)
- ISMS audit evidence package updated

Reference:
`11_ARCHIVE/11.3_Audit-Records/`

---

## 10. Ad-Hoc Review (Post Breach / Post Major Incident)

### Trigger Conditions
An ad-hoc SLA review is initiated when:
- P1 SLA breach occurs
- Multiple P2 SLA breaches occur in same week
- Major incident reveals SLA gaps
- Client formally raises SLA concern
- Regulatory inspection identifies SLA deficiencies

### Owner
SOC Manager (internal) / SDM (client-facing)

### Timeframe
- Initiated: Within 24 hours of trigger
- Completed: Within 5 business days

### Activities
- [ ] Review specific breach or incident
- [ ] Identify SLA gap or unrealistic target
- [ ] Consult with SOC Lead and IR Team
- [ ] Propose SLA amendment or corrective action
- [ ] Brief CISO on findings
- [ ] Notify client if MSSP SLA impacted
- [ ] Update documents and version history

---

## 11. Annual SLA Review Calendar

| Month | Review Activity |
|-------|----------------|
| January | Q1 SLA & SLO Formal Review |
| January | Annual SLA Document Review |
| February | Monthly SLA Compliance Review |
| March | Monthly SLA Compliance Review |
| April | Q2 SLA & SLO Formal Review |
| May | Monthly SLA Compliance Review |
| June | Monthly SLA Compliance Review |
| July | Q3 SLA & SLO Formal Review |
| August | Monthly SLA Compliance Review |
| September | Monthly SLA Compliance Review |
| October | Q4 SLA & SLO Formal Review |
| November | Monthly SLA Compliance Review |
| December | Monthly SLA Compliance Review + Annual Prep |

Weekly reviews occur every week throughout the year.
Daily monitoring occurs every shift throughout the year.

---

## 12. SLA Review Action Tracker

All actions identified in reviews are tracked here until closed:

| Action ID | Review Type | Date Identified | Action Description | Owner | Due Date | Status | Closure Date |
|-----------|------------|----------------|-------------------|-------|---------|--------|-------------|
| SLA-ACT-001 | | | | | | | |

---

## 13. Document Distribution

Upon annual review and update, this document is distributed to:

- All SOC Leads
- SOC Manager
- IR Team Lead
- MSSP SDM
- GRC / Compliance
- MSSP Clients (relevant sections only)

---

## 14. Review & Update

This document shall be reviewed:
- Annually (mandatory)
- Upon major SLA breach
- Upon operational model change
- Upon regulatory requirement change

---

## 15. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**