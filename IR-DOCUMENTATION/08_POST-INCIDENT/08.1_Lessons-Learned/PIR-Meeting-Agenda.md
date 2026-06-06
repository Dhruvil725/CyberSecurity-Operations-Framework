# Post-Incident Review (PIR) Meeting Agenda

---

# 1. Document Control

| Field          | Value                         |
| -------------- | ----------------------------- |
| Document Name  | Template – PIR Meeting Agenda |
| Document ID    | PIR-AGN-001                   |
| Version        | 1.0                           |
| Effective Date | 30-May-2026                   |
| Owner          | IR Team Lead / SOC Manager    |
| Approved By    | CISO                          |
| Classification | Internal – Confidential       |
| Review Cycle   | Annually                      |

---

# 2. Purpose

This document provides the standardized **Post-Incident Review (PIR) Meeting Agenda** template used to conduct structured, time-boxed, and outcome-driven PIR sessions following incident closure.

A standardized PIR agenda is critical because:

- unstructured PIRs lead to incomplete lessons learned and missed improvement opportunities
- time-boxing ensures efficient use of stakeholders' time
- consistent structure enables comparison across incidents and trend analysis
- NIST SP 800-61 mandates structured post-incident activity
- ISO 27001 Annex A.5.27 requires learning from incidents
- RBI Cyber Security Framework expects documented review processes
- MSSP operations require repeatable, client-presentable PIR processes
- audit evidence requires meeting records with clear agenda and outcomes

This agenda template ensures:

- consistent meeting structure across all PIR sessions
- defined time allocation per agenda item
- clear pre-meeting preparation requirements
- defined attendee roles and expectations
- structured capture of decisions and action items
- linkage to Lessons Learned documentation

Reference alignment:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

# 3. Scope

This agenda template is used for:

| Scenario                       | PIR Required?   | Timeline Post-Closure                            |
| ------------------------------ | --------------- | ------------------------------------------------ |
| P1 incidents                   | **Mandatory**   | Within 5 working days                            |
| P2 incidents                   | **Mandatory**   | Within 10 working days                           |
| P3 incidents (TP, significant) | **Recommended** | Within 15 working days                           |
| P4 incidents                   | Optional        | As needed                                        |
| Near-miss events               | **Recommended** | Within 10 working days                           |
| Tabletop / Drill exercises     | **Mandatory**   | Within 5 working days                            |
| Recurring incident pattern     | **Mandatory**   | Within 10 working days of pattern identification |
| MSSP client incidents          | Per client SLA  | Per SLA                                          |

Out of scope:

- routine BAU operational reviews
- false positive closures without learning value

---

# 4. Definitions

| Term             | Definition                                                                      |
| ---------------- | ------------------------------------------------------------------------------- |
| PIR              | Post-Incident Review – structured retrospective meeting after incident closure  |
| Facilitator      | Person leading the PIR session, ensuring agenda adherence and blameless culture |
| Scribe           | Person responsible for capturing notes, decisions, and action items             |
| Action Item      | Specific task assigned with owner and due date                                  |
| Blameless Review | Discussion focused on systems/processes, not individual blame                   |
| Time-box         | Allocated time slot for each agenda item                                        |
| Pre-read         | Materials shared with attendees before the meeting                              |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                             |
| ------------------------ | ---------------------------------------------------------------------------- |
| PIR Facilitator          | Leads session; enforces time-box; ensures blameless culture; drives outcomes |
| Scribe                   | Captures notes, decisions, action items; finalizes meeting minutes           |
| IR Team Lead             | Presents incident timeline, scope, and technical analysis                    |
| SOC Lead                 | Provides SOC operational perspective and tooling insights                    |
| L1/L2/L3 Analysts        | Share frontline observations and challenges faced                            |
| SOC Manager              | Approves outcomes; ensures action items are tracked                          |
| CISO (P1 only)           | Provides strategic direction and approves major actions                      |
| Compliance Lead          | Validates regulatory/audit considerations                                    |
| IT Operations Rep        | Shares infrastructure/operational context                                    |
| Business Stakeholder     | Provides business impact perspective                                         |
| MSSP SDM (if applicable) | Coordinates client-facing follow-up                                          |
| Action Owners            | Commit to assigned actions with realistic timelines                          |

---

# 6. PIR Meeting Principles (Mandatory)

| Principle       | Description                                             |
| --------------- | ------------------------------------------------------- |
| Blameless       | No individual blame; focus on systems and processes     |
| Time-boxed      | Strict adherence to time allocations                    |
| Evidence-based  | Reference tickets, timestamps, and evidence             |
| Inclusive       | All response stakeholders invited                       |
| Action-oriented | Every gap must result in action or documented rationale |
| Confidential    | Discussion is internal; sanitized share-out only        |
| Honest          | Candid discussion of what didn't work                   |
| Outcome-driven  | Meeting must produce documented LL and action items     |

---

# 7. Pre-Meeting Preparation (Mandatory)

## 7.1 Facilitator Responsibilities (T-3 Days)

- [ ] Schedule PIR within timeline (P1: 5 days, P2: 10 days)
- [ ] Identify and invite required attendees
- [ ] Book meeting room / virtual session
- [ ] Assign scribe
- [ ] Share pre-read materials (T-2 days minimum)
- [ ] Prepare incident timeline summary
- [ ] Coordinate with RCA owner for RCA status
- [ ] Confirm attendee availability

## 7.2 Attendee Responsibilities (T-1 Day)

- [ ] Review pre-read materials
- [ ] Review incident ticket and timeline
- [ ] Review own actions during incident
- [ ] Prepare observations (what went well / didn't go well)
- [ ] Prepare improvement suggestions
- [ ] Confirm attendance

## 7.3 Pre-Read Package (Mandatory)

The following must be shared with attendees before the meeting:

| Document                            | Source                                       | Mandatory?  |
| ----------------------------------- | -------------------------------------------- | ----------- |
| Final Incident Report               | `07_REPORTING/07.1_Incident-Reports/`        | Yes         |
| Incident Timeline                   | Ticketing system / Timeline Builder          | Yes         |
| RCA Document (Draft)                | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/` | Yes (P1/P2) |
| Key Metrics Summary                 | SOC dashboard                                | Yes         |
| Communications Log                  | Incident ticket                              | Yes         |
| Evidence Inventory                  | Evidence vault                               | Yes         |
| Previous Related LL (if applicable) | LL Register                                  | Recommended |

---

# 8. Standard PIR Meeting Agenda (Copy/Paste)

## 8.1 Meeting Metadata (Mandatory)

| Field                     | Value                        |
| ------------------------- | ---------------------------- |
| PIR ID                    | `PIR-YYYY-####`              |
| Incident ID / Ticket ID   | `INC-YYYY-####`              |
| Incident Category         | `...`                        |
| Incident Severity (Final) | P1 / P2 / P3 / P4            |
| Meeting Date (UTC)        | `YYYY-MM-DD`                 |
| Meeting Time (UTC)        | `HH:MM – HH:MM`              |
| Duration                  | `60 / 90 / 120 minutes`      |
| Mode                      | In-Person / Virtual / Hybrid |
| Location / Link           | `...`                        |
| Facilitator               | `Name / Role`                |
| Scribe                    | `Name / Role`                |
| Client/Tenant (MSSP only) | `Client ID / Name`           |

---

## 8.2 Standard Agenda – P1/P2 Incidents (90–120 minutes)

| #         | Agenda Item                              | Owner                 | Duration    | Outcome Expected                 |
| --------- | ---------------------------------------- | --------------------- | ----------- | -------------------------------- |
| 1         | Welcome & Ground Rules (Blameless)       | Facilitator           | 5 min       | Aligned expectations             |
| 2         | Attendance & Introductions               | Facilitator           | 5 min       | All present confirmed            |
| 3         | Incident Overview & Timeline Walkthrough | IR Team Lead          | 15 min      | Shared understanding of events   |
| 4         | Detection & Triage Review                | SOC Lead              | 10 min      | Detection effectiveness assessed |
| 5         | Containment & Eradication Review         | IR Team Lead          | 10 min      | Response effectiveness assessed  |
| 6         | Recovery & Validation Review             | IR Team Lead / IT Ops | 10 min      | Recovery effectiveness assessed  |
| 7         | Communications Review                    | SOC Manager           | 5 min       | Stakeholder comms effectiveness  |
| 8         | Root Cause Discussion                    | RCA Owner             | 10 min      | RCA validated                    |
| 9         | What Went Well (Round-robin)             | Facilitator           | 10 min      | Strengths documented             |
| 10        | What Didn't Go Well (Round-robin)        | Facilitator           | 15 min      | Gaps identified                  |
| 11        | Gaps & Improvement Discussion            | All                   | 15 min      | Improvement areas prioritized    |
| 12        | Action Items & Owner Assignment          | Facilitator           | 10 min      | Actions assigned with dates      |
| 13        | Metrics Review                           | SOC Manager           | 5 min       | SLA performance assessed         |
| 14        | Closing & Next Steps                     | Facilitator           | 5 min       | LL finalization plan             |
| **Total** |                                          |                       | **120 min** |                                  |

---

## 8.3 Standard Agenda – P3 Incidents (60 minutes)

| #         | Agenda Item                   | Owner                     | Duration   | Outcome Expected     |
| --------- | ----------------------------- | ------------------------- | ---------- | -------------------- |
| 1         | Welcome & Ground Rules        | Facilitator               | 3 min      | Aligned expectations |
| 2         | Incident Overview & Timeline  | IR Team Lead / L2         | 10 min     | Shared understanding |
| 3         | Response Effectiveness Review | SOC Lead                  | 10 min     | Response assessed    |
| 4         | Root Cause Summary            | RCA Owner                 | 5 min      | RCA shared           |
| 5         | What Went Well                | Facilitator               | 5 min      | Strengths documented |
| 6         | What Didn't Go Well           | Facilitator               | 10 min     | Gaps identified      |
| 7         | Action Items & Assignment     | Facilitator               | 10 min     | Actions assigned     |
| 8         | Metrics & Closing             | SOC Manager / Facilitator | 7 min      | Next steps confirmed |
| **Total** |                               |                           | **60 min** |                      |

---

## 8.4 Standard Agenda – Tabletop / Drill Exercises (90 minutes)

| #         | Agenda Item                 | Owner         | Duration   | Outcome Expected     |
| --------- | --------------------------- | ------------- | ---------- | -------------------- |
| 1         | Welcome & Ground Rules      | Facilitator   | 5 min      | Aligned expectations |
| 2         | Exercise Scenario Recap     | Exercise Lead | 10 min     | Scenario understood  |
| 3         | Response Walkthrough        | Participants  | 20 min     | Response assessed    |
| 4         | Decision Points Review      | Facilitator   | 15 min     | Decisions analyzed   |
| 5         | Communication Effectiveness | Facilitator   | 10 min     | Comms assessed       |
| 6         | What Went Well              | Facilitator   | 10 min     | Strengths documented |
| 7         | What Didn't Go Well         | Facilitator   | 10 min     | Gaps identified      |
| 8         | Action Items & Closing      | Facilitator   | 10 min     | Actions assigned     |
| **Total** |                             |               | **90 min** |                      |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
`10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`

---

# 9. Facilitation Guidelines (Mandatory)

## 9.1 Opening the Meeting

The facilitator must open with:

> *"This is a blameless review. Our goal is to learn and improve, not to assign blame. We will discuss what happened, what went well, what didn't, and what we will do differently. Every voice matters. Let's focus on systems, processes, and tools — not individuals."*

## 9.2 During the Meeting

- Enforce time-box strictly
- Ensure every attendee speaks (round-robin for key sections)
- Redirect blame-focused discussions to system/process focus
- Capture every action item with owner and due date
- Ask "why" five times to reach root cause
- Park off-topic discussions for follow-up
- Avoid jumping to solutions before understanding gaps

## 9.3 Common Pitfalls to Avoid

| Pitfall                | Mitigation                                                                  |
| ---------------------- | --------------------------------------------------------------------------- |
| Blame culture          | Reframe to system/process focus                                             |
| Dominant voices        | Round-robin to ensure all heard                                             |
| Solution-jumping       | Complete gap analysis first                                                 |
| Vague action items     | Use SMART criteria (Specific, Measurable, Achievable, Relevant, Time-bound) |
| No owners assigned     | Every action must have single accountable owner                             |
| Skipping documentation | Scribe must capture in real-time                                            |
| Time overrun           | Strict time-box enforcement                                                 |
| Missing stakeholders   | Verify attendance pre-meeting                                               |

---

# 10. Action Item Capture Template (Mandatory)

During the meeting, scribe must capture:

| Action ID | Action Description | Category                                         | Type    | Owner | Due Date (UTC) | Priority         | Tracking Ref |
| --------- | ------------------ | ------------------------------------------------ | ------- | ----- | -------------- | ---------------- | ------------ |
| AI-001    |                    | Playbook / Detection / Tool / Training / Process | CA / PA |       |                | High / Med / Low |              |
| AI-002    |                    |                                                  |         |       |                |                  |              |
| AI-003    |                    |                                                  |         |       |                |                  |              |

**Action Item SMART Criteria:**

- **S**pecific – Clear and unambiguous
- **M**easurable – Completion criteria defined
- **A**chievable – Realistic within owner's capability
- **R**elevant – Addresses identified gap
- **T**ime-bound – Has clear due date

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`

---

# 11. Decisions Log Template (Mandatory)

| Decision # | Decision | Made By | Rationale | Impact |
| ---------- | -------- | ------- | --------- | ------ |
| D-001      |          |         |           |        |
| D-002      |          |         |           |        |

---

# 12. Post-Meeting Activities (Mandatory)

## 12.1 Scribe Responsibilities (Within 24 Hours)

- [ ] Finalize meeting minutes
- [ ] Circulate draft minutes to facilitator for review
- [ ] Share final minutes with all attendees
- [ ] Update Lessons Learned document
- [ ] Log action items in tracker
- [ ] File minutes in incident archive

## 12.2 Facilitator Responsibilities (Within 48 Hours)

- [ ] Review and approve minutes
- [ ] Validate action items have owners and due dates
- [ ] Update Lessons Learned Register
- [ ] Escalate any unresolved disputes
- [ ] Brief SOC Manager / CISO on outcomes (P1/P2)

## 12.3 Action Owner Responsibilities (Within 1 Week)

- [ ] Acknowledge assigned action
- [ ] Confirm or negotiate due date
- [ ] Begin execution
- [ ] Provide bi-weekly status updates

---

# 13. Meeting Minutes Template (Copy/Paste)

**PIR Meeting Minutes**

**PIR ID:** PIR-YYYY-####
**Incident ID:** INC-YYYY-####
**Date / Time (UTC):** YYYY-MM-DD HH:MM
**Duration:** XX minutes
**Facilitator:** Name
**Scribe:** Name

### Attendees

- Name, Role
- Name, Role

### Absent (with reason)

- Name, Role – reason

### Key Discussion Points

1. ...
2. ...
3. ...

### What Went Well

1. ...
2. ...

### What Didn't Go Well

1. ...
2. ...

### Decisions Made

| #   | Decision | Made By |
| --- | -------- | ------- |
| 1   | ...      | ...     |

### Action Items

| ID     | Action | Owner | Due Date | Priority |
| ------ | ------ | ----- | -------- | -------- |
| AI-001 | ...    | ...   | ...      | ...      |

### Next Steps

- LL document finalization by: [date]
- Action tracker update: completed
- Next review checkpoint: [date]

### Distribution

- All attendees
- SOC Manager
- CISO (P1/P2 only)
- Filed in: [archive path]

* * *

14. MSSP Considerations (If Applicable)
    =======================================

For MSSP-managed clients:

* PIR may be conducted **internally first**, then **client-facing** follow-up
* Client may request **joint PIR** per SLA
* Agenda must be **tenant-scoped**; no cross-client references
* Client-facing minutes must be **sanitized**
* Client-specific action items tracked in **client folder**
* MSSP-internal learnings filed separately for service improvement
* Cross-client trends discussed only in **anonymized aggregate form** internally

References:  
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

* * *

15. Quality Checklist (Post-PIR)
    ================================

Before considering PIR complete:

* [ ]  All agenda items covered within time-box
* [ ]  All required attendees present (or absence documented)
* [ ]  Blameless culture maintained throughout
* [ ]  Incident timeline reviewed
* [ ]  What went well captured (minimum 3 items)
* [ ]  What didn't go well captured (minimum 3 items)
* [ ]  All gaps have corresponding actions or rationale
* [ ]  All action items are SMART
* [ ]  All action items have single owner and due date
* [ ]  Decisions logged with rationale
* [ ]  Meeting minutes finalized within 24 hours
* [ ]  Action items logged in tracker
* [ ]  LL document updated
* [ ]  Minutes filed in incident archive
* [ ]  MSSP: tenant scoping verified

* * *

16. Related Documents
    =====================

| Document                       | Path                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------- |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`             |
| Lessons Learned Register       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`           |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`               |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                     |
| RCA 5-Why Template             | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-5-Why-Template.md`               |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`          |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`  |
| Drill After Action Report      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`            |

* * *

17. Revision History
    ====================

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

* * *

18. Approval
    ============

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

* * *

**End of Document**
