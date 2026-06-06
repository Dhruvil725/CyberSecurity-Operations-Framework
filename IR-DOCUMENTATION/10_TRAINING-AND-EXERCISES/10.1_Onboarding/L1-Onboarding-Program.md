# L1 SOC Analyst Onboarding Program

---

# 1. Document Control

| Field          | Value                                         |
| -------------- | --------------------------------------------- |
| Document Name  | L1 SOC Analyst Onboarding Program             |
| Document ID    | MSSP-TRN-001                                  |
| Version        | 1.0                                           |
| Effective Date | 30-May-2026                                   |
| Owner          | MSSP SOC Manager / HR Lead                    |
| Approved By    | MSSP CISO                                     |
| Classification | Confidential – MSSP Internal                  |
| Review Cycle   | Annually (or upon SOC operating model change) |

---

# 2. Purpose

This document defines the standardized **L1 SOC Analyst Onboarding Program** governing the structured induction, training, certification, and operational readiness of new Level 1 (L1) SOC analysts joining the MSSP — ensuring consistent quality, multi-tenant readiness, and SLA-compliant operational performance from Day 1 of independent shift work.

A formal L1 onboarding program is critical because:

- L1 analysts are the front-line of MSSP SOC operations handling the largest alert volumes
- inconsistent L1 onboarding directly causes SLA breaches and missed detections
- multi-tenant environments require strict tenant context discipline from new analysts
- L1 analysts handle alerts from multiple clients with different severity matrices and playbooks
- alert fatigue, FP handling, and escalation decisions require formal training
- ISO 27001 A.6.3 and NIST CSF PR.AT require structured awareness and training
- RBI Cyber Security Framework requires competency for personnel handling regulated data
- MSSP SLA compliance depends on L1 analyst speed and accuracy
- new analyst errors in tenant segregation create breach risk
- SOAR, SIEM, EDR tools require structured tool training
- per-client playbooks must be learned before independent client coverage
- shift handover discipline must be embedded early
- escalation criteria must be clearly understood to prevent under/over-escalation
- false positive feedback drives detection improvement loop
- audit and compliance reviews require evidence of structured onboarding
- this program is the foundation for L1 analyst lifecycle quality

This program ensures:

- consistent 6-week structured onboarding for all new L1 analysts
- defined competency milestones with measurable assessments
- multi-tenant policy training mandatory before client assignment
- tool proficiency certification before independent shifts
- playbook familiarity per assigned client tier
- mentorship pairing for first 30 days
- formal certification before solo shift coverage
- audit-ready evidence of training completion
- linkage to L1 role definition, SOC procedures, and multi-tenant policies

**Reference alignment:**

- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L1-Analyst-Role-Definition.md`
- `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/`
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
- `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/`

---

# 3. Scope

This program applies to all new L1 SOC analysts joining the MSSP:

| Scope Element                    | Coverage                         |
| -------------------------------- | -------------------------------- |
| New L1 hires (external)          | Full 6-week program              |
| L1 transfers (internal)          | Tailored 3-week program          |
| L1 returning (>6 months absence) | Refresher 2-week program         |
| L1 role changes from L0/intern   | Full 6-week program              |
| Per-client assignment training   | Per assigned client              |
| Tool training                    | SIEM, EDR, SOAR, TI, ticketing   |
| Policy training                  | All MSSP policies + multi-tenant |
| Procedure training               | All L1 SOPs                      |
| Playbook training                | Per assigned client tier         |
| Mentorship                       | Mandatory for first 30 days      |
| Certification                    | Mandatory before solo shifts     |

Out of scope:

- L2/L3/IR Team onboarding (separate programs)
- Management/leadership onboarding (covered by HR)
- General employee orientation (covered by HR)
- Advanced specialization training (covered by post-certification programs)

---

# 4. Definitions

| Term                  | Definition                                    |
| --------------------- | --------------------------------------------- |
| L1 Analyst            | Level 1 SOC analyst (front-line alert triage) |
| Onboarding            | Structured induction of new personnel         |
| Mentor                | Senior analyst paired with new hire           |
| Buddy                 | Peer analyst for daily support                |
| Shadowing             | Observing experienced analyst at work         |
| Reverse Shadowing     | Performing work observed by mentor            |
| Certification         | Formal validation of competency               |
| Tier Assignment       | Assignment to specific client tier            |
| Solo Shift            | First independent shift coverage              |
| Probation             | Initial employment evaluation period          |
| Competency Milestone  | Defined skill checkpoint                      |
| Multi-Tenant Briefing | Mandatory pre-assignment client overview      |

---

# 5. Roles and Responsibilities

| Role                        | Responsibilities                                                     |
| --------------------------- | -------------------------------------------------------------------- |
| **MSSP HR Lead**            | Recruitment; onboarding logistics; benefits; documentation           |
| **MSSP SOC Manager**        | Program ownership; mentor assignment; certification approval         |
| **MSSP SOC Lead**           | Operational onboarding; shift integration; daily mentoring oversight |
| **MSSP L3 / Senior L2**     | Mentor role for new L1                                               |
| **MSSP Compliance Lead**    | Multi-tenant policy training; compliance briefings                   |
| **MSSP Detection Engineer** | Tool training; rule context                                          |
| **MSSP Threat Intel Lead**  | TI platform training; IoC handling                                   |
| **MSSP IT Lead**            | System access provisioning                                           |
| **MSSP Legal Counsel**      | NDA execution; legal briefings                                       |
| **New L1 Analyst**          | Active participation; assessment completion; feedback                |
| **Buddy Analyst**           | Daily peer support during first 30 days                              |

---

# 6. Onboarding Program Principles (Mandatory)

| Principle                        | Requirement                                                    |
| -------------------------------- | -------------------------------------------------------------- |
| **Structured Progression**       | Defined weekly milestones; no skipping                         |
| **Multi-Tenant Awareness First** | Tenant segregation training mandatory before any client access |
| **Tool Proficiency Required**    | Certification before independent tool use                      |
| **Mentorship Mandatory**         | First 30 days paired with mentor                               |
| **Shadowing Before Solo**        | Minimum 40 hours shadowing before solo shift                   |
| **Assessment-Based Progression** | Pass/fail assessments at each milestone                        |
| **Per-Client Tier Training**     | Specific to assigned client portfolio                          |
| **Audit-Ready Documentation**    | All completion evidence captured                               |
| **Continuous Feedback**          | Weekly check-ins; bidirectional feedback                       |
| **Safety Net**                   | Mentor escalation always available                             |

---

# 7. L1 Onboarding Program Overview (6 Weeks)

Week 1: FOUNDATION & ORIENTATION
├── HR onboarding + admin setup
├── Security policies + NDAs
├── Multi-tenant policy training
├── MSSP organization overview
└── Initial tool exposure (read-only)

Week 2: TECHNICAL FOUNDATIONS
├── SIEM training (per-tenant context)
├── EDR training
├── Ticketing training
├── SOAR training
└── Knowledge base orientation

Week 3: SOC PROCEDURES
├── L1 SOPs deep dive
├── Alert handling workflow
├── False positive handling
├── Escalation criteria
└── Shift handover process

Week 4: PLAYBOOKS & SCENARIOS
├── Per-client playbook training
├── Per-incident type playbooks
├── Tabletop scenario participation
├── Mentor shadowing (passive)
└── First triage exercises

Week 5: SUPERVISED OPERATIONS
├── Mentor shadowing (active)
├── Reverse shadowing
├── Supervised alert handling
├── Per-client assignment briefing
└── Pre-certification assessment

Week 6: CERTIFICATION & SOLO READINESS
├── Final certification assessment
├── Tenant assignment confirmation
├── First supervised solo shift
├── 30-day mentor pairing continues
└── Probationary period begins

---

# 8. Week 1: Foundation & Orientation (Mandatory)

## 8.1 Day 1 – Admin & Welcome

| Activity                             | Duration | Owner       |
| ------------------------------------ | -------- | ----------- |
| HR orientation (benefits, policies)  | 2 hours  | HR          |
| Equipment + workspace setup          | 1 hour   | IT          |
| Email + Slack/Teams + calendar setup | 1 hour   | IT          |
| MSSP organization overview           | 1 hour   | SOC Manager |
| SOC tour + introductions             | 1 hour   | SOC Lead    |
| NDA + employment agreement signing   | 1 hour   | Legal/HR    |
| Day 1 wrap-up + Day 2 brief          | 30 min   | Mentor      |

## 8.2 Day 2 – Security Policies & Compliance

| Activity                                  | Duration | Owner           |
| ----------------------------------------- | -------- | --------------- |
| Information Security Policy training      | 2 hours  | Compliance Lead |
| Acceptable Use Policy                     | 1 hour   | HR + IT         |
| Data Classification training              | 1 hour   | Compliance Lead |
| Incident reporting (internal)             | 1 hour   | Compliance Lead |
| BYOD / Remote work policy (if applicable) | 1 hour   | IT              |
| Day 2 quiz                                | 30 min   | Compliance Lead |

## 8.3 Day 3 – Multi-Tenant Policy Training (Critical)

| Activity                                      | Duration | Owner             |
| --------------------------------------------- | -------- | ----------------- |
| **Client Data Segregation Policy training**   | 2 hours  | Compliance Lead   |
| **Cross-tenant prohibitions**                 | 1 hour   | Compliance Lead   |
| **Tenant context awareness**                  | 1 hour   | SOC Manager       |
| **Sanitization principles**                   | 1 hour   | Threat Intel Lead |
| **Real-world segregation case studies**       | 1 hour   | SOC Manager       |
| **Multi-tenant policy quiz (must pass 100%)** | 30 min   | Compliance Lead   |

**⚠️ Critical Gate:** New L1 cannot proceed without passing multi-tenant policy quiz.

## 8.4 Day 4 – MSSP Operational Overview

| Activity                               | Duration | Owner           |
| -------------------------------------- | -------- | --------------- |
| MSSP service tier overview             | 1 hour   | SOC Manager     |
| Client portfolio overview (anonymized) | 1 hour   | SOC Manager     |
| SOC tier model (L1/L2/L3/IR)           | 1 hour   | SOC Manager     |
| SLA framework introduction             | 1 hour   | Compliance Lead |
| 24x7 shift model                       | 1 hour   | SOC Lead        |
| Communication channels                 | 1 hour   | SOC Lead        |

## 8.5 Day 5 – Initial Tool Exposure

| Activity                        | Duration | Owner              |
| ------------------------------- | -------- | ------------------ |
| SIEM read-only walkthrough      | 2 hours  | Detection Engineer |
| EDR read-only walkthrough       | 1 hour   | Detection Engineer |
| Ticketing read-only walkthrough | 1 hour   | SOC Lead           |
| SOAR read-only walkthrough      | 1 hour   | Detection Engineer |
| Week 1 retrospective            | 1 hour   | Mentor + SOC Lead  |

### Week 1 Completion Criteria

- [ ] All admin setup completed
- [ ] All NDAs signed
- [ ] Multi-tenant policy quiz passed (100%)
- [ ] Security policies acknowledged
- [ ] Tool read-only access verified
- [ ] Mentor introduced

---

# 9. Week 2: Technical Foundations (Mandatory)

## 9.1 SIEM Training

| Topic                                                | Duration | Owner              |
| ---------------------------------------------------- | -------- | ------------------ |
| SIEM architecture overview                           | 2 hours  | Detection Engineer |
| Per-tenant index/namespace concept                   | 1 hour   | Detection Engineer |
| Search/query basics (KQL/SPL/etc.)                   | 4 hours  | Detection Engineer |
| Dashboard navigation                                 | 1 hour   | Detection Engineer |
| Alert interface                                      | 2 hours  | Detection Engineer |
| **Hands-on lab: 10 sample alerts (training tenant)** | 4 hours  | Detection Engineer |

## 9.2 EDR Training

| Topic                                      | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| EDR architecture                           | 1 hour   | Detection Engineer |
| Per-tenant console navigation              | 1 hour   | Detection Engineer |
| Endpoint investigation queries             | 2 hours  | Detection Engineer |
| Containment commands (read-only initially) | 1 hour   | Detection Engineer |
| Process tree analysis                      | 2 hours  | Detection Engineer |
| **Hands-on lab: 5 sample investigations**  | 3 hours  | Detection Engineer |

## 9.3 Ticketing Training

| Topic                               | Duration | Owner    |
| ----------------------------------- | -------- | -------- |
| Ticket lifecycle                    | 1 hour   | SOC Lead |
| Per-tenant ticket structure         | 1 hour   | SOC Lead |
| Standard fields                     | 1 hour   | SOC Lead |
| Status transitions                  | 1 hour   | SOC Lead |
| Ticket closure standards            | 1 hour   | SOC Lead |
| **Hands-on lab: 10 sample tickets** | 2 hours  | SOC Lead |

## 9.4 SOAR Training

| Topic                              | Duration | Owner              |
| ---------------------------------- | -------- | ------------------ |
| SOAR concepts                      | 1 hour   | Detection Engineer |
| Playbook execution view            | 1 hour   | Detection Engineer |
| Manual action triggering           | 1 hour   | Detection Engineer |
| Auto-response vs manual            | 1 hour   | Detection Engineer |
| **Hands-on lab: SOAR walkthrough** | 2 hours  | Detection Engineer |

## 9.5 Knowledge Base Orientation

| Topic                    | Duration | Owner             |
| ------------------------ | -------- | ----------------- |
| Knowledge base structure | 1 hour   | SOC Lead          |
| Search techniques        | 1 hour   | SOC Lead          |
| MITRE ATT&CK reference   | 2 hours  | Threat Intel Lead |
| Tool command reference   | 1 hour   | SOC Lead          |
| Common IoC reference     | 1 hour   | Threat Intel Lead |

### Week 2 Completion Criteria

- [ ] SIEM hands-on lab completed
- [ ] EDR hands-on lab completed
- [ ] Ticketing lab completed
- [ ] SOAR walkthrough completed
- [ ] Knowledge base navigation demonstrated
- [ ] Tool quiz passed (≥80%)

---

# 10. Week 3: SOC Procedures (Mandatory)

## 10.1 L1 SOP Training

| SOP                        | Duration | Owner              |
| -------------------------- | -------- | ------------------ |
| L1 Daily Shift Checklist   | 1 hour   | SOC Lead           |
| L1 Alert Handling SOP      | 3 hours  | SOC Lead           |
| L1 Escalation Criteria     | 2 hours  | SOC Lead           |
| L1 False Positive Handling | 2 hours  | Detection Engineer |
| L1 Ticket Creation SOP     | 1 hour   | SOC Lead           |
| L1 SIEM Alert Response     | 2 hours  | Detection Engineer |
| L1 EDR Alert Response      | 2 hours  | Detection Engineer |
| L1 Shift Handover Template | 1 hour   | SOC Lead           |

## 10.2 Multi-Client Alert Handling Procedure

| Topic                               | Duration | Owner           |
| ----------------------------------- | -------- | --------------- |
| Multi-Client Alert Handling SOP     | 2 hours  | SOC Manager     |
| Tenant routing and assignment       | 1 hour   | SOC Lead        |
| Per-client SLA awareness            | 2 hours  | Compliance Lead |
| Tenant context switching safeguards | 1 hour   | Compliance Lead |
| Alert storm response basics         | 1 hour   | SOC Lead        |

## 10.3 Triage Decision Trees

| Topic                             | Duration | Owner              |
| --------------------------------- | -------- | ------------------ |
| Master Triage Decision Tree       | 2 hours  | SOC Lead           |
| Alert-to-Incident Qualification   | 2 hours  | SOC Lead           |
| False Positive Handling deep dive | 2 hours  | Detection Engineer |
| Multi-Client Triage MSSP          | 2 hours  | SOC Manager        |

### Week 3 Completion Criteria

- [ ] All L1 SOPs reviewed and acknowledged
- [ ] Multi-client alert handling demonstrated in lab
- [ ] Triage decision tree quiz passed (≥80%)
- [ ] FP classification exercise completed

---

# 11. Week 4: Playbooks & Scenarios (Mandatory)

## 11.1 Per-Incident Type Playbook Training (L1 Focus)

| Playbook                         | Duration | Owner        |
| -------------------------------- | -------- | ------------ |
| Ransomware L1 Triage             | 2 hours  | IR Team Lead |
| Phishing L1 Triage               | 2 hours  | IR Team Lead |
| Malware L1 Triage                | 2 hours  | IR Team Lead |
| DDoS L1 Triage                   | 1 hour   | IR Team Lead |
| Credential Attack L1 Triage      | 2 hours  | IR Team Lead |
| Web Application Attack L1 Triage | 1 hour   | IR Team Lead |
| Cloud Incident L1 Triage         | 2 hours  | IR Team Lead |
| Network Intrusion L1 Triage      | 2 hours  | IR Team Lead |

## 11.2 Per-Client Playbook Familiarization

| Topic                                           | Duration | Owner           |
| ----------------------------------------------- | -------- | --------------- |
| Per-client environment profiles (assigned tier) | 2 hours  | SOC Manager     |
| Per-client IR policies (assigned tier)          | 2 hours  | Compliance Lead |
| Per-client escalation matrices (assigned tier)  | 1 hour   | SOC Lead        |
| Per-client custom playbooks (assigned tier)     | 3 hours  | IR Team Lead    |

## 11.3 Tabletop Scenario Participation

| Exercise                          | Duration | Owner        |
| --------------------------------- | -------- | ------------ |
| Phishing tabletop (observer)      | 2 hours  | IR Team Lead |
| Ransomware tabletop (observer)    | 2 hours  | IR Team Lead |
| Malware tabletop (active L1 role) | 2 hours  | IR Team Lead |

## 11.4 First Triage Exercises (Supervised)

| Exercise                                         | Duration | Owner  |
| ------------------------------------------------ | -------- | ------ |
| 10 supervised triage exercises (training tenant) | 6 hours  | Mentor |
| Triage classification feedback                   | 2 hours  | Mentor |

### Week 4 Completion Criteria

- [ ] All L1-tier playbooks reviewed
- [ ] Per-client playbooks (assigned tier) reviewed
- [ ] Tabletop participation completed
- [ ] 10 supervised triage exercises completed
- [ ] Playbook quiz passed (≥80%)

---

# 12. Week 5: Supervised Operations (Mandatory)

## 12.1 Active Shadowing (Mentor)

| Activity                                     | Duration   | Owner  |
| -------------------------------------------- | ---------- | ------ |
| Active shadowing of mentor during live shift | 20 hours   | Mentor |
| Real-time alert handling observation         | Continuous | Mentor |
| Per-tenant context switching observation     | Continuous | Mentor |
| Escalation observation                       | Continuous | Mentor |

## 12.2 Reverse Shadowing

| Activity                                       | Duration     | Owner  |
| ---------------------------------------------- | ------------ | ------ |
| New L1 handles alerts under mentor observation | 16 hours     | Mentor |
| Real-time mentor feedback                      | Continuous   | Mentor |
| End-of-shift debrief                           | 1 hour daily | Mentor |

## 12.3 Supervised Alert Handling

| Activity                                      | Duration  | Owner             |
| --------------------------------------------- | --------- | ----------------- |
| Supervised live alert triage (low complexity) | 8 hours   | Mentor + SOC Lead |
| Tenant verification every alert               | Mandatory | New L1            |
| Documentation of every action                 | Mandatory | New L1            |

## 12.4 Per-Client Assignment Briefing

| Activity                          | Duration | Owner          |
| --------------------------------- | -------- | -------------- |
| Specific client tier briefing     | 2 hours  | Per-client SDM |
| Per-client tools and dashboards   | 1 hour   | Per-client SDM |
| Per-client communication channels | 1 hour   | Per-client SDM |
| Per-client maintenance windows    | 1 hour   | Per-client SDM |

## 12.5 Pre-Certification Assessment

| Assessment                                 | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| Written assessment (policies + procedures) | 1 hour   | SOC Manager        |
| Tool proficiency assessment                | 1 hour   | Detection Engineer |
| Tabletop scenario (proctored)              | 2 hours  | IR Team Lead       |
| Triage assessment (10 alerts)              | 2 hours  | SOC Lead           |
| Multi-tenant scenario assessment           | 1 hour   | Compliance Lead    |

### Week 5 Completion Criteria

- [ ] Minimum 40 hours shadowing completed
- [ ] Minimum 16 hours reverse shadowing completed
- [ ] Minimum 8 hours supervised live triage
- [ ] All assigned client briefings completed
- [ ] Pre-certification assessment passed (≥80% overall)

---

# 13. Week 6: Certification & Solo Readiness (Mandatory)

## 13.1 Final Certification Assessment

| Component                                | Pass Threshold   |
| ---------------------------------------- | ---------------- |
| Written exam (all policies + procedures) | 85%              |
| Multi-tenant scenario exam               | 100% (must pass) |
| Tool proficiency practical               | 85%              |
| Tabletop scenario (proctored)            | Pass/Fail        |
| Live triage assessment (10 alerts)       | 85% accuracy     |
| Per-client SOP knowledge                 | 85%              |

## 13.2 Tenant Assignment Confirmation

| Activity                           | Owner           |
| ---------------------------------- | --------------- |
| Assigned client tier finalized     | SOC Manager     |
| RBAC/ABAC verified per assignment  | IT Lead         |
| Access tested per assigned tenants | New L1 + Mentor |
| Per-client SLA review              | SOC Lead        |

## 13.3 First Supervised Solo Shift

| Activity                          | Duration                   | Owner             |
| --------------------------------- | -------------------------- | ----------------- |
| First solo shift (mentor on-call) | Full shift                 | New L1            |
| Mentor 30-min check-ins           | Every 30 min first 2 hours | Mentor            |
| Shift debrief                     | 1 hour                     | Mentor + SOC Lead |

## 13.4 30-Day Continued Mentorship

| Activity                     | Cadence           | Owner            |
| ---------------------------- | ----------------- | ---------------- |
| Daily mentor check-in        | Daily for 30 days | Mentor           |
| Weekly SOC Lead review       | Weekly            | SOC Lead         |
| Bi-weekly SOC Manager review | Bi-weekly         | SOC Manager      |
| 30-day formal review         | Day 30            | SOC Manager + HR |

### Week 6 Completion Criteria

- [ ] Final certification assessment passed
- [ ] Multi-tenant exam passed at 100%
- [ ] Tenant assignment confirmed
- [ ] First solo shift completed successfully
- [ ] 30-day mentorship plan documented

---

# 14. Mentor Program (Mandatory)

## 14.1 Mentor Selection Criteria

| Criterion               | Requirement                                   |
| ----------------------- | --------------------------------------------- |
| Tenure                  | Minimum 2 years L2+ at MSSP                   |
| Performance             | Top quartile performer                        |
| Multi-tenant experience | Multiple client tier experience               |
| Communication skills    | Demonstrated training capability              |
| Availability            | Capacity to mentor without operational impact |

## 14.2 Mentor Responsibilities

- Daily check-ins during first 30 days
- Real-time shadowing during weeks 5-6
- Reverse shadowing supervision
- Per-tenant context coaching
- Escalation decision coaching
- Feedback to SOC Manager weekly
- Safety net for new L1 questions

## 14.3 Mentor Compensation/Recognition

- Mentorship counted in performance evaluation
- Mentor allowance (per company policy)
- Recognition in quarterly awards

---

# 15. Assessment Framework (Mandatory)

## 15.1 Weekly Assessments

| Week   | Assessment                   | Pass Threshold          |
| ------ | ---------------------------- | ----------------------- |
| Week 1 | Multi-tenant policy quiz     | 100%                    |
| Week 1 | Security policy quiz         | 80%                     |
| Week 2 | Tool proficiency quiz        | 80%                     |
| Week 3 | SOP knowledge quiz           | 80%                     |
| Week 3 | Triage decision tree quiz    | 80%                     |
| Week 4 | Playbook quiz                | 80%                     |
| Week 5 | Pre-certification assessment | 80% overall             |
| Week 6 | Final certification          | 85% (100% multi-tenant) |

## 15.2 Reassessment Policy

- 1 reassessment allowed per failed assessment
- Reassessment within 1 week
- 2nd failure → extended onboarding (additional 2 weeks)
- 3rd failure → role suitability review by SOC Manager + HR

---

# 16. Per-Client Tier Assignment Strategy (Mandatory)

## 16.1 Initial Assignment

| Client Tier                     | New L1 Eligibility                            |
| ------------------------------- | --------------------------------------------- |
| **Tier 1 (Critical/Regulated)** | Only after 90 days + Tier 2 success           |
| **Tier 2 (Standard)**           | After certification                           |
| **Tier 3 (Monitoring-only)**    | After certification (preferred starting tier) |

## 16.2 Tier Progression

| Milestone                    | Eligibility for Next Tier |
| ---------------------------- | ------------------------- |
| 90 days successful Tier 3    | Eligible for Tier 2       |
| 180 days successful Tier 2   | Eligible for Tier 1       |
| Quarterly performance review | Tier assignment review    |

---

# 17. Documentation & Records (Mandatory)

## 17.1 Onboarding Records Maintained

- [ ] Onboarding checklist (signed)
- [ ] NDA + employment agreement
- [ ] Multi-tenant policy quiz result
- [ ] All weekly assessment results
- [ ] Final certification result
- [ ] Shadowing hours log
- [ ] Mentor feedback reports
- [ ] 30-day review report
- [ ] Tenant assignment record
- [ ] RBAC/ABAC provisioning record

## 17.2 Records Retention

| Record                        | Retention                        |
| ----------------------------- | -------------------------------- |
| Onboarding completion records | Duration of employment + 7 years |
| Assessment results            | Duration of employment + 7 years |
| Mentor feedback               | Duration of employment + 3 years |
| NDA records                   | Per legal retention              |

---

# 18. Quality Checklist (Per New L1 Onboarding)

Before declaring L1 onboarding complete:

- [ ] All 6 weeks of structured program completed
- [ ] All weekly assessments passed
- [ ] Multi-tenant policy quiz passed at 100%
- [ ] Final certification passed at ≥85%
- [ ] Minimum 40 hours shadowing completed
- [ ] Minimum 16 hours reverse shadowing completed
- [ ] First solo shift completed successfully
- [ ] 30-day mentorship plan active
- [ ] Tenant assignment confirmed
- [ ] RBAC/ABAC verified
- [ ] All documentation captured
- [ ] HR record updated
- [ ] SOC Manager sign-off obtained

---

# 19. Continuous Post-Onboarding Development

| Activity                             | Frequency     |
| ------------------------------------ | ------------- |
| Daily SOC Lead check-in              | First 30 days |
| Weekly performance review            | First 90 days |
| Monthly skills refresher             | Ongoing       |
| Quarterly tabletop participation     | Ongoing       |
| Annual recertification               | Ongoing       |
| Annual multi-tenant policy refresher | Ongoing       |
| Career progression review            | Bi-annually   |

---

# 20. Integration with Other Processes

| Process                      | Integration            |
| ---------------------------- | ---------------------- |
| HR Onboarding                | Admin + benefits       |
| Multi-Tenant Policy Training | Mandatory week 1       |
| Tool Training                | Weeks 2 + ongoing      |
| L1 SOPs                      | Week 3 deep dive       |
| Per-Client Playbooks         | Week 4                 |
| Tabletop Exercises           | Week 4 participation   |
| Mentorship Program           | 6 weeks + 30 days      |
| Certification                | Week 6                 |
| Performance Management       | Probation period start |
| Career Progression           | Post-90 days           |

---

# 21. Related Documents

| Document                        | Path                                                                                       |
| ------------------------------- | ------------------------------------------------------------------------------------------ |
| L1 Analyst Role Definition      | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L1-Analyst-Role-Definition.md`              |
| L1 Daily Shift Checklist        | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Daily-Shift-Checklist.md`                    |
| L1 Alert Handling SOP           | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`                       |
| L1 Escalation Criteria          | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Escalation-Criteria.md`                      |
| L1 False Positive Handling      | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-False-Positive-Handling.md`                  |
| L1 Ticket Creation SOP          | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Ticket-Creation-SOP.md`                      |
| L1 SIEM Alert Response          | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-SIEM-Alert-Response.md`                      |
| L1 EDR Alert Response           | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-EDR-Alert-Response.md`                       |
| L1 Shift Handover Template      | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`                  |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`          |
| Multi-Client Alert Handling     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`             |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`         |
| Master Triage Decision Tree     | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md`     |
| Alert-to-Incident Qualification | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Alert-to-Incident-Qualification.md` |
| Severity Classification Guide   | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`         |
| Tabletop Exercise Guide         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`             |
| Attack Technique Reference      | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`              |
| MITRE ATT&CK Quick Reference    | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`            |
| Tool Command Reference          | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`                  |
| Common IoC Reference            | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`                    |
| L2 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`                       |

---

# 22. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SOC Manager / HR Lead | Initial version |

---

# 23. Approval

Approved by:

| Role             | Name | Signature | Date |
| ---------------- | ---- | --------- | ---- |
| MSSP SOC Lead    |      |           |      |
| MSSP SOC Manager |      |           |      |
| MSSP HR Lead     |      |           |      |
| MSSP CISO        |      |           |      |

---

**End of Document**
