# Tabletop Exercise – Insider Threat Scenario

---

# 1. Document Control

| Field                | Value                                                    |
| -------------------- | -------------------------------------------------------- |
| Document Name        | TTX – Insider Threat Scenario                            |
| Document ID          | MSSP-TRN-TTX-004                                         |
| Version              | 1.0                                                      |
| Effective Date       | 30-May-2026                                              |
| Owner                | MSSP IR Team Lead / HR Lead                              |
| Approved By          | MSSP CISO                                                |
| Classification       | Confidential – MSSP Internal                             |
| Review Cycle         | Annually (or upon insider threat program update)         |
| Scenario Difficulty  | High                                                     |
| Recommended Audience | L2 + L3 + IR Team + HR + Legal + Compliance + CISO + SDM |

---

# 2. Purpose

This document defines a standardized **Insider Threat Tabletop Exercise Scenario** designed to test the MSSP's ability to detect, investigate, contain, and respond to a malicious insider conducting unauthorized data access and exfiltration — validating L2/L3 behavioral analysis, IR Team incident command, HR coordination, legal coordination, evidence handling for employment/criminal action, executive communication, privacy considerations, and post-incident program improvement.

A formal Insider Threat TTX is critical because:

- insider threats are among the most damaging incidents (trusted access, knowledge of controls)
- insider threat investigations have unique legal, HR, privacy, and ethical considerations
- coordination between MSSP, client, HR, Legal, and Compliance is rarely practiced live
- evidence handling for employment termination, civil action, or criminal prosecution requires specialized care
- privacy considerations (employee monitoring, DPDP, GDPR) must be respected
- premature insider confrontation can destroy evidence and tip off the actor
- multi-tenant MSSPs face insider threats both internally (MSSP employee) and externally (at clients)
- behavioral analysis under uncertainty requires structured methodology
- chain of custody for insider evidence has legal admissibility implications
- IR Team must coordinate with client HR/Legal — not direct the action
- privileged user insider threats (admins, executives) require elevated discretion
- regulatory considerations (RBI insider threat reporting, sector-specific) require awareness
- ISO 27001 A.5.27, NIST CSF DE.CM, A.6.4 disciplinary processes require validated readiness
- without structured TTX, insider response gaps lead to evidence loss and legal exposure
- this scenario is the foundation for annual mandatory insider threat exercise

This scenario ensures:

- structured insider threat simulation across detection, investigation, containment
- HR-Legal-IR-MSSP coordination practice
- privacy-respecting investigation methodology
- evidence handling for employment/criminal proceedings
- discrete containment without tipping off the actor
- per-client HR/Legal authority respected
- multi-tenant discipline during insider investigation
- privileged user insider threat handling
- post-incident program improvement
- audit-ready exercise documentation

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md`
- `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

# 3. Scenario Overview

| Field                             | Value                                                                                  |
| --------------------------------- | -------------------------------------------------------------------------------------- |
| **Scenario Name**                 | "Operation Quiet Departure"                                                            |
| **Scenario Type**                 | Discussion-Based Tabletop Exercise                                                     |
| **Difficulty**                    | High                                                                                   |
| **Estimated Duration**            | 4-6 hours (full day with breaks recommended)                                           |
| **Threat Category**               | Insider Threat (Malicious Insider)                                                     |
| **Insider Profile (fictional)**   | Senior database administrator, 7 years tenure, recent performance issues               |
| **Affected Client (in scenario)** | "MediCorp" — fictional healthcare technology company                                   |
| **Insider Access Level**          | Privileged DBA access to customer health records (PHI)                                 |
| **Data at Risk**                  | 1.2M patient health records (PHI) + R&D intellectual property                          |
| **Detection Method**              | UEBA anomaly detection + DLP triggers                                                  |
| **Suspected Motivation**          | Resignation imminent; suspected to be joining competitor                               |
| **Primary Objective**             | Test insider detection, HR/Legal coordination, discrete containment, evidence handling |

---

# 4. TTX Objectives (Mandatory)

| ID         | Objective                                                 | Success Criteria                                            |
| ---------- | --------------------------------------------------------- | ----------------------------------------------------------- |
| **OBJ-1**  | Validate insider threat detection via UEBA + DLP          | L2 correlates anomalies + DLP triggers within 60 min        |
| **OBJ-2**  | Test L3 behavioral analysis methodology                   | L3 produces behavioral timeline within 120 min              |
| **OBJ-3**  | Validate IR Team activation for insider P1/P2             | IR Team Lead assumes IC within 45 min                       |
| **OBJ-4**  | Test HR engagement timing and protocol                    | HR engaged BEFORE any insider-facing action                 |
| **OBJ-5**  | Test Legal engagement timing                              | Legal engaged in parallel with HR; legal hold issued        |
| **OBJ-6**  | Validate discrete monitoring (no tip-off)                 | No actions that alert the insider during evidence gathering |
| **OBJ-7**  | Test client HR/Legal authority respect                    | MSSP advises; client HR/Legal decide                        |
| **OBJ-8**  | Validate evidence handling for employment/criminal action | Forensic-grade CoC; legal-admissible evidence               |
| **OBJ-9**  | Test privacy-respecting investigation                     | DPDP/employee privacy considerations applied                |
| **OBJ-10** | Test executive communication                              | CISO + Client CISO briefed appropriately                    |
| **OBJ-11** | Validate multi-tenant discipline during insider scenario  | No cross-client info leakage                                |
| **OBJ-12** | Test discreet containment timing                          | Containment action timed with HR/Legal coordination         |

---

# 5. Participants and Roles (Mandatory)

## 5.1 Required Participants

| Role                      | Played By             | Active in Scenario       |
| ------------------------- | --------------------- | ------------------------ |
| IR Team Lead              | Senior IR Team member | Yes (Incident Commander) |
| L3 Forensics Lead         | Senior L3             | Yes                      |
| L2 Lead Analyst           | Senior L2             | Yes                      |
| Threat Intel Lead         | Threat Intel Lead     | Yes                      |
| SOC Lead                  | SOC Lead              | Yes                      |
| Per-Client SDM (MediCorp) | SDM                   | Yes                      |
| Compliance Lead           | Compliance Lead       | Yes                      |
| Legal Counsel             | Legal Counsel         | Yes (critical role)      |
| HR Lead (MSSP or Client)  | HR                    | Yes (critical role)      |
| MSSP CISO                 | CISO                  | Yes (executive role)     |
| Detection Engineer        | Detection Eng         | Yes                      |

## 5.2 Optional / Observer Participants

| Role                              | Played By                |
| --------------------------------- | ------------------------ |
| Junior L3 (learning)              | Observer                 |
| New IR Team member (learning)     | Observer                 |
| Internal Auditor                  | Observer                 |
| DPO                               | Observer (privacy angle) |
| Physical Security (if applicable) | Observer                 |

## 5.3 White Team (Facilitators + Evaluators)

| Role                                | Person                              |
| ----------------------------------- | ----------------------------------- |
| Lead Facilitator                    | IR Team Lead (or designated senior) |
| Co-Facilitator                      | HR Lead                             |
| Evaluator – IR Command              | SOC Manager                         |
| Evaluator – L3 Behavioral Analysis  | Senior L3                           |
| Evaluator – HR Coordination         | HR Lead                             |
| Evaluator – Legal Coordination      | Legal Counsel                       |
| Evaluator – Discrete Operations     | IR Team Lead                        |
| Evaluator – Privacy                 | Compliance Lead / DPO               |
| Evaluator – Multi-Tenant Discipline | Compliance Lead                     |
| Evaluator – Communication           | CISO or designate                   |
| Timekeeper                          | Training Lead                       |
| Scribe / Note-Taker                 | Training Lead                       |

---

# 6. Insider Profile (Fictional – for Realism)

| Attribute                       | Detail                                                               |
| ------------------------------- | -------------------------------------------------------------------- |
| **Insider Name (fictional)**    | "Raj Kumar" (use generic name)                                       |
| **Role**                        | Senior Database Administrator                                        |
| **Tenure**                      | 7 years at MediCorp                                                  |
| **Access Level**                | Privileged DBA — full access to patient DB + R&D systems             |
| **Performance Status**          | Performance issues last 6 months; PIP (Performance Improvement Plan) |
| **Recent Behavior**             | Increased after-hours access; declining engagement                   |
| **Suspected Motivation**        | Joining competitor; financial pressure (separation rumors)           |
| **Technical Sophistication**    | High (knows monitoring controls)                                     |
| **Risk Indicators (HRI)**       | Resignation rumors, performance issues, financial stress             |
| **Privileged Actions Observed** | Bulk database queries; USB device usage; cloud storage uploads       |

**Reference:** This is a fictional composite — no resemblance to real persons intended.

---

# 7. Scenario Background

## 7.1 MSSP Context

The MSSP provides 24x7 MDR + insider threat monitoring services to MediCorp:

- **MediCorp** – Healthcare technology company; ~3,500 employees; handles PHI for 1.2M patients
- Subject to DPDP Act, HIPAA-aligned controls (if US clients), healthcare regulator requirements
- Insider threat program in place with UEBA + DLP + Privileged Access Monitoring (PAM)
- DBA team: 8 members; "Raj Kumar" is one of three senior DBAs

## 7.2 Initial Situation (Day 0 — Detection Day)

The MSSP UEBA system generates anomaly alerts:

| Time     | Event                                                                               | Source |
| -------- | ----------------------------------------------------------------------------------- | ------ |
| T+0      | UEBA: Raj Kumar shows 350% increase in database query volume over 30 days           | UEBA   |
| T+30 min | DLP: Multiple file transfers to personal cloud storage (Dropbox) in last 7 days     | DLP    |
| T+60 min | PAM: After-hours access spike — last 14 days, weekends + late nights                | PAM    |
| T+90 min | EDR: USB storage device detected on Raj's workstation (last 5 days, multiple times) | EDR    |

**Hidden background (revealed via injects):**

- Raj has been planning resignation for 3 months
- Recruited by direct competitor — joining in 4 weeks
- Has been systematically downloading patient records + R&D documents
- Has uploaded ~800 MB to personal Dropbox over 30 days
- Has copied ~2.3 GB to personal USB
- Performance issues created cover for "extra hours"
- Plans to deliver client list + R&D to new employer
- MediCorp HR not yet informed of suspected resignation

---

# 8. Master Scenario Events List (MSEL) — FACILITATOR ONLY

⚠️ **CONFIDENTIAL — DO NOT SHARE WITH PARTICIPANTS BEFORE EXERCISE**

## 8.1 Phase 1: Detection & Initial Validation (T+0 to T+60 min)

| #   | T+     | Method  | Content                                                                          | Expected Response                                      | Evaluator Notes   |
| --- | ------ | ------- | -------------------------------------------------------------------------------- | ------------------------------------------------------ | ----------------- |
| 1   | 0 min  | Verbal  | "UEBA alert: Raj Kumar (DBA) — 350% query volume increase over baseline"         | L2 acknowledges; begins behavioral correlation         | TTA < 15 min      |
| 2   | 15 min | Written | "DLP alert: multiple file uploads to personal Dropbox by same user, last 7 days" | L2 correlates UEBA + DLP                               | Correlation done  |
| 3   | 30 min | Verbal  | "PAM alert: after-hours access spike, weekends + late nights"                    | L2 escalates to L3 — suspected insider                 | Escalation timing |
| 4   | 45 min | Verbal  | "EDR alert: USB storage on Raj's workstation, 5 times last week"                 | L3 begins comprehensive behavioral analysis            | L3 engagement     |
| 5   | 55 min | Verbal  | "L3 produces preliminary risk assessment: HIGH risk insider"                     | Severity P1/P2 declared; IR Team activation considered | Severity correct  |

## 8.2 Phase 2: IR Team Activation + HR/Legal Engagement (T+60 to T+120 min)

| #   | T+      | Method | Content                                                         | Expected Response                                     | Evaluator Notes           |
| --- | ------- | ------ | --------------------------------------------------------------- | ----------------------------------------------------- | ------------------------- |
| 6   | 60 min  | Verbal | "Question: who do you engage FIRST — Client SDM, HR, or Legal?" | HR + Legal engaged BEFORE insider-facing actions      | HR-Legal-first sequencing |
| 7   | 70 min  | Verbal | "IR Team Lead activates — assumes IC"                           | IR Team Lead assumes command                          | IC assumption clear       |
| 8   | 80 min  | Verbal | "MSSP SDM notifies MediCorp CISO confidentially"                | Discrete client notification                          | Discretion maintained     |
| 9   | 90 min  | Verbal | "MediCorp HR engaged — needs to provide employment context"     | HR engaged; HR provides Raj's PIP/performance context | HR engagement             |
| 10  | 100 min | Verbal | "MediCorp Legal engaged — needs to provide legal guidance"      | Legal engaged; legal hold issued                      | Legal hold issued         |
| 11  | 110 min | Verbal | "MSSP CISO joins — strategic oversight"                         | CISO briefed; strategic decisions discussed           | Exec engagement           |

## 8.3 Phase 3: Discrete Investigation (T+120 to T+180 min)

| #   | T+      | Method  | Content                                                                               | Expected Response                                           | Evaluator Notes        |
| --- | ------- | ------- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------- | ---------------------- |
| 12  | 125 min | Verbal  | "L3 conducts deep forensic analysis — discreetly (no insider tip-off)"                | Discrete investigation; no actions visible to insider       | Discretion paramount   |
| 13  | 135 min | Written | "Forensic timeline: 30-day exfiltration; ~800 MB to Dropbox; ~2.3 GB to USB"          | Comprehensive scope quantified                              | Quantification rigor   |
| 14  | 145 min | Verbal  | "Question: is monitoring of Raj's communications/email allowed?"                      | Legal advises per employment contract + DPDP + jurisdiction | Privacy considerations |
| 15  | 155 min | Verbal  | "Privacy concern: Raj has not been informed of monitoring"                            | DPDP/employee privacy boundaries discussed                  | Privacy boundary       |
| 16  | 165 min | Verbal  | "L3 confirms: Raj searched for 'how to extract Oracle data to CSV' (browser history)" | Intent indicators documented                                | Intent vs. capability  |
| 17  | 175 min | Verbal  | "Question: confront Raj now or continue monitoring for evidence?"                     | HR + Legal + Client CISO decision; not MSSP unilateral      | Decision authority     |

## 8.4 Phase 4: Discreet Containment Planning (T+180 to T+240 min)

| #   | T+      | Method  | Content                                                                             | Expected Response                                  | Evaluator Notes        |
| --- | ------- | ------- | ----------------------------------------------------------------------------------- | -------------------------------------------------- | ---------------------- |
| 18  | 185 min | Verbal  | "Containment planning: how to revoke access without tip-off?"                       | Coordinated timing with HR/Legal                   | Coordination           |
| 19  | 195 min | Written | "MediCorp HR plans confrontation meeting — Wednesday 10am"                          | Containment timed with meeting                     | Timing coordination    |
| 20  | 205 min | Verbal  | "MediCorp Legal prepares employment termination paperwork + civil action documents" | Legal action coordination noted                    | Legal action awareness |
| 21  | 215 min | Verbal  | "Question: revoke privileged access before or during HR meeting?"                   | DURING — to prevent tip-off; per-client decision   | Timing rationale       |
| 22  | 225 min | Verbal  | "MediCorp CISO asks: 'Can we image his workstation before the meeting?'"            | Yes, if can be done covertly (after-hours, remote) | Evidence preservation  |
| 23  | 235 min | Verbal  | "Question: should USB devices be located?"                                          | Physical recovery via HR/Legal (not MSSP)          | Authority boundary     |

## 8.5 Phase 5: Containment Execution + Evidence Handling (T+240 to T+300 min)

| #   | T+      | Method  | Content                                                                | Expected Response                               | Evaluator Notes     |
| --- | ------- | ------- | ---------------------------------------------------------------------- | ----------------------------------------------- | ------------------- |
| 24  | 245 min | Verbal  | "Wednesday 10am: HR meeting begins; SIMULTANEOUS access revocation"    | Coordinated execution                           | Coordination tested |
| 25  | 255 min | Written | "Workstation imaged covertly Tuesday night — forensic image preserved" | CoC documented; forensic-grade                  | CoC quality         |
| 26  | 265 min | Verbal  | "All privileged access revoked at 10:00 AM exactly"                    | Containment effective                           | Containment timing  |
| 27  | 275 min | Verbal  | "Raj confronted with evidence; denies wrongdoing"                      | HR/Legal handle confrontation; MSSP not in room | Authority respected |
| 28  | 285 min | Verbal  | "Raj surrenders USB devices voluntarily (2 devices, ~2.3 GB matched)"  | Evidence chain preserved                        | Evidence handling   |
| 29  | 295 min | Verbal  | "MediCorp HR places Raj on administrative leave pending investigation" | Status documented; access remains revoked       | Status clarity      |

## 8.6 Phase 6: Post-Incident + Regulatory + Recovery (T+300 to T+360 min)

| #   | T+      | Method  | Content                                                                                   | Expected Response                                     | Evaluator Notes      |
| --- | ------- | ------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------- | -------------------- |
| 30  | 305 min | Verbal  | "Question: is this a reportable data breach under DPDP?"                                  | Compliance + Legal assess; likely YES given PHI scope | Regulatory analysis  |
| 31  | 315 min | Verbal  | "Dropbox content retrieval — civil legal action initiated by MediCorp"                    | MediCorp Legal coordinates with Dropbox subpoena      | Legal action         |
| 32  | 325 min | Verbal  | "Question: criminal referral to law enforcement?"                                         | MediCorp Legal decision; MSSP supports with evidence  | Decision authority   |
| 33  | 335 min | Written | "Other DBAs reviewed: no similar patterns"                                                | Broader insider review confirmed                      | Broader review       |
| 34  | 345 min | Verbal  | "Question: lessons for insider threat program — applicable to other clients (sanitized)?" | Sanitized cross-portfolio brief planned               | Sanitization process |
| 35  | 355 min | Verbal  | "Long-term: Raj's competitor onboarding monitored for 90 days"                            | Long-term monitoring discussed                        | Long-term plan       |
| 36  | 360 min | Verbal  | "Scenario freeze — move to hot wash"                                                      | Hot wash begins                                       | —                    |

---

# 9. Pre-Read for Participants (NON-CONFIDENTIAL)

## 9.1 Scenario Brief (Share with Participants Pre-TTX)

### Background

You will participate in a 4-6 hour tabletop exercise simulating a malicious insider threat at an MSSP client — a senior database administrator with privileged access exfiltrating patient health records to a personal Dropbox account and USB devices. The scenario involves insider detection, IR Team incident command, HR-Legal-first coordination, discrete monitoring, evidence preservation for employment and potential criminal action, privacy considerations, and post-incident program improvement.

### Your Preparation

Before the TTX, please:

1. Review your role-specific playbooks (Insider Threat Master, HR-Legal Coordination)
2. Review your role-specific SOPs
3. Review the Client Data Segregation Policy
4. Review employee privacy considerations (DPDP)
5. Be ready to engage as your actual role under realistic pressure

### What You Will NOT Have

- The Master Scenario Events List (MSEL) — facilitator only
- Specific inject timing
- Resolution path — to be determined by your decisions

### Ground Rules

- This is a safe, no-blame learning environment
- Engage authentically as your role
- Make decisions using actual playbooks and SOPs
- Maintain multi-tenant discipline
- HR-Legal-first sequencing is being tested — do not act on insider before HR/Legal engagement
- Discrete operations are critical — no actions that would tip off the insider during evidence gathering
- All decisions will be documented and discussed in hot wash
- Hot wash will follow immediately; AAR within 14 days

---

# 10. Evaluation Framework (Mandatory)

## 10.1 Per-Objective Scoring

Use `TTX-Evaluation-Scorecard.md` for detailed scoring. Summary:

| Objective                                | Evaluator               | Pass Threshold      |
| ---------------------------------------- | ----------------------- | ------------------- |
| OBJ-1: Insider Detection via UEBA+DLP    | L2 Evaluator            | Score ≥3            |
| OBJ-2: L3 Behavioral Analysis            | L3 Evaluator            | Score ≥3            |
| OBJ-3: IR Team Activation                | IR Command Evaluator    | Score ≥3            |
| OBJ-4: HR Engagement Timing              | HR Evaluator            | Score ≥4 (critical) |
| OBJ-5: Legal Engagement Timing           | Legal Evaluator         | Score ≥4 (critical) |
| OBJ-6: Discrete Monitoring (no tip-off)  | Discrete Ops Evaluator  | Score ≥4 (critical) |
| OBJ-7: Client HR/Legal Authority Respect | Multi-Tenant Evaluator  | Score ≥4 (critical) |
| OBJ-8: Evidence Handling for Action      | L3/Legal Evaluator      | Score ≥3            |
| OBJ-9: Privacy-Respecting Investigation  | Privacy Evaluator       | Score ≥3            |
| OBJ-10: Executive Communication          | Communication Evaluator | Score ≥3            |
| OBJ-11: Multi-Tenant Discipline          | Multi-Tenant Evaluator  | Score ≥4 (critical) |
| OBJ-12: Discrete Containment Timing      | Discrete Ops Evaluator  | Score ≥3            |

## 10.2 Critical Failure Triggers

The TTX is marked **FAIL** if any of:

- Insider-facing action taken before HR + Legal engagement
- Insider tipped off during evidence gathering phase
- MSSP unilaterally confronted insider (instead of client HR/Legal)
- MSSP unilaterally terminated employment (instead of client HR/Legal)
- MSSP unilaterally engaged law enforcement (instead of client Legal decision)
- Privacy considerations ignored (e.g., reading personal communications without authorization)
- Cross-client information leakage
- Evidence collected without proper authorization or CoC
- Legal hold not issued before forensic activities

---

# 11. Hot Wash Agenda (Mandatory)

| Time      | Activity                            |
| --------- | ----------------------------------- |
| 0-10 min  | What went well — round robin        |
| 10-25 min | What did not go well — round robin  |
| 25-40 min | Specific gaps identified            |
| 40-50 min | Quick wins (immediate improvements) |
| 50-60 min | Next steps + AAR timeline           |

---

# 12. Expected Findings Areas (For Facilitator Preparation)

Based on prior Insider Threat TTX patterns, expect findings in:

| Area                             | Common Gaps                                      |
| -------------------------------- | ------------------------------------------------ |
| HR-Legal-first sequencing        | Pressure to act technically before HR/Legal      |
| Discrete operations              | Actions visible to insider during evidence phase |
| Client authority respect         | MSSP overstepping into HR/Legal decisions        |
| Privacy considerations           | DPDP/employee privacy unclear                    |
| Evidence handling for employment | CoC weak for legal action                        |
| Containment timing               | Premature containment tips off insider           |
| Confrontation boundary           | MSSP attempting to confront vs supporting        |
| Law enforcement decisions        | MSSP unilateral vs client-led                    |
| Broader insider review           | Only focusing on identified insider              |
| Long-term monitoring             | Not planning for residual risk                   |

---

# 13. Improvement Areas to Probe (Facilitator Prompts)

If participants miss these, prompt with:

| Prompt                                                        | Tests                     |
| ------------------------------------------------------------- | ------------------------- |
| "Have you engaged HR and Legal before acting on the insider?" | HR-Legal-first sequencing |
| "Will this action tip off the insider?"                       | Discrete operations       |
| "Who confronts the insider — MSSP or client HR?"              | Authority boundary        |
| "Can we monitor his personal email?"                          | Privacy boundaries        |
| "Has the legal hold been issued?"                             | Evidence preservation     |
| "Are other DBAs showing similar patterns?"                    | Broader insider review    |
| "Is this a reportable breach under DPDP?"                     | Regulatory analysis       |
| "Who decides on law enforcement referral?"                    | Decision authority        |
| "How is evidence preserved for employment action?"            | Evidence handling         |
| "How will we monitor competitor onboarding?"                  | Long-term monitoring      |

---

# 14. Multi-Tenant Considerations (Mandatory)

Although this is a single-client scenario, multi-tenant discipline is tested:

| Test                               | Inject                                            |
| ---------------------------------- | ------------------------------------------------- |
| Cross-client mention temptation    | Throughout — no other client should be referenced |
| Sanitized portfolio insider review | Inject 34                                         |
| Per-client HR/Legal authority      | Inject 17, 27, 32                                 |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 15. Logistics Checklist (Mandatory)

## 15.1 T-30 Days

- [ ] TTX scheduled
- [ ] Calendar invites sent
- [ ] Venue confirmed (in-person/virtual/hybrid)
- [ ] Scenario reviewed and approved by IR Team Lead + HR + Legal

## 15.2 T-7 Days

- [ ] Pre-read distributed to participants
- [ ] Role assignments confirmed
- [ ] Facilitator MSEL final
- [ ] Evaluator scorecards prepared
- [ ] HR + Legal availability confirmed (critical roles)
- [ ] Equipment tested

## 15.3 T-1 Day

- [ ] Reminder sent
- [ ] Materials printed
- [ ] Backup facilitator confirmed
- [ ] Catering arranged

## 15.4 Day of TTX

- [ ] Sign-in sheet
- [ ] Ground rules briefing
- [ ] HR-Legal-first sequencing emphasized
- [ ] Discrete operations emphasized
- [ ] Timekeeping started
- [ ] Recording (if applicable, with consent)
- [ ] Hot wash facilitation
- [ ] AAR timeline communicated

---

# 16. Required Materials (Mandatory)

| Material                                          | Source                                                                                          |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Scenario brief (pre-read)                         | Section 9 of this document                                                                      |
| MSEL (facilitator only)                           | Section 8 of this document                                                                      |
| Evaluation scorecards                             | `TTX-Evaluation-Scorecard.md`                                                                   |
| Reference: Insider Threat Master Playbook         | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md`                                  |
| Reference: Insider HR-Legal Coordination Playbook | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`                   |
| Reference: Insider Containment Playbook           | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md`                             |
| Reference: Insider L3 Forensics Playbook          | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md`                            |
| Reference: Legal Counsel Engagement SOP           | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Reference: Evidence Collection SOP                | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`          |
| Sign-in sheet                                     | Template                                                                                        |
| Timekeeping (visible clock)                       | Mandatory                                                                                       |
| Whiteboard / virtual whiteboard                   | Mandatory                                                                                       |

---

# 17. AAR Template (Post-TTX)

After-action report will document per `Tabletop-Exercise-Guide.md` Section 15:

| Section           | Content                          |
| ----------------- | -------------------------------- |
| Executive summary | TTX overview + headline findings |
| Objectives status | Pass/fail per objective          |
| Participant list  | By role                          |
| Scenario summary  | What was simulated               |
| Timeline          | Major scenario milestones        |
| Strengths         | What went well                   |
| Gaps              | What did not go well             |
| Recommendations   | Specific actionable improvements |
| Action items      | Owner + due date                 |
| Lessons learned   | Generalized takeaways            |
| Appendix          | Scorecards + decisions + quotes  |

---

# 18. Quality Checklist (Per Insider Threat TTX Execution)

Before declaring this TTX complete:

- [ ] All 12 objectives evaluated
- [ ] Scorecards collected from all evaluators
- [ ] Hot wash conducted immediately post-TTX
- [ ] Critical failure triggers reviewed (especially HR-Legal-first + discreteness)
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Action items entered in tracker
- [ ] HR coordination observations documented
- [ ] Legal coordination observations documented
- [ ] Discrete operations effectiveness assessed
- [ ] Authority boundary observations documented
- [ ] Privacy observations documented
- [ ] Multi-tenant discipline observations documented
- [ ] Records archived per retention policy

---

# 19. Records Retention

| Record                       | Retention               |
| ---------------------------- | ----------------------- |
| TTX scenario (this document) | 7 years                 |
| MSEL (facilitator copy)      | 3 years                 |
| Sign-in sheet                | 3 years                 |
| Evaluator scorecards         | 3 years                 |
| Hot wash notes               | 3 years                 |
| AAR                          | 7 years                 |
| Action items records         | Until closure + 3 years |

---

# 20. Integration with Other Processes

| Process                                | Integration                   |
| -------------------------------------- | ----------------------------- |
| Tabletop Exercise Guide                | Master methodology            |
| Insider Threat Master Playbook         | Validated by this TTX         |
| Insider HR-Legal Coordination Playbook | Validated by this TTX         |
| Insider Containment Playbook           | Validated by this TTX         |
| Legal Counsel Engagement SOP           | Tested by this TTX            |
| Evidence Collection SOP                | Tested by this TTX            |
| CoC procedures                         | Tested by this TTX            |
| Client Data Segregation Policy         | Tested by this TTX            |
| IR Team Onboarding                     | TTX participation requirement |
| L3 Onboarding                          | TTX participation requirement |
| Lessons Learned Register               | AAR feeds register            |
| Playbook Update Log                    | Playbook gaps tracked         |
| Control Gap Tracker                    | Control gaps tracked          |
| Insider Threat Program                 | Refined post-TTX              |

---

# 21. Related Documents

| Document                             | Path                                                                                            |
| ------------------------------------ | ----------------------------------------------------------------------------------------------- |
| Tabletop Exercise Guide              | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`                  |
| TTX Evaluation Scorecard             | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`                 |
| TTX Ransomware Scenario              | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`                  |
| TTX APT Scenario                     | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`                         |
| TTX Data Breach Scenario             | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`                  |
| Insider Threat Master Playbook       | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md`                                  |
| Insider Threat L1 Triage             | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md`                               |
| Insider Threat L2 Investigation      | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md`                        |
| Insider Threat L3 Forensics          | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md`                            |
| Insider Threat HR-Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`                   |
| Insider Threat Containment           | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md`                             |
| Insider Threat MITRE Mapping         | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md`                           |
| Legal Counsel Engagement SOP         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Evidence Collection SOP              | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`          |
| Digital Evidence Handling            | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md`        |
| CoC Master Form                      | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`                     |
| IRT Containment Authority Matrix     | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`            |
| Client Data Segregation Policy       | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Lessons Learned Template             | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                             |
| Playbook Update Log                  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                             |
| Control Gap Tracker                  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`                           |

---

# 22. Revision History

| Version | Date        | Author                      | Changes         |
| ------- | ----------- | --------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / HR Lead | Initial version |

---

# 23. Approval

Approved by:

| Role               | Name | Signature | Date |
| ------------------ | ---- | --------- | ---- |
| MSSP IR Team Lead  |      |           |      |
| MSSP HR Lead       |      |           |      |
| MSSP Legal Counsel |      |           |      |
| MSSP CISO          |      |           |      |

---

**End of Document**
