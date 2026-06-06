# Tabletop Exercise (TTX) Guide

---

# 1. Document Control

| Field          | Value                                     |
| -------------- | ----------------------------------------- |
| Document Name  | Tabletop Exercise (TTX) Guide             |
| Document ID    | MSSP-TRN-005                              |
| Version        | 1.0                                       |
| Effective Date | 30-May-2026                               |
| Owner          | MSSP IR Team Lead / SOC Manager           |
| Approved By    | MSSP CISO                                 |
| Classification | Confidential – MSSP Internal              |
| Review Cycle   | Annually (or upon TTX methodology change) |

---

# 2. Purpose

This document defines the standardized **Tabletop Exercise (TTX) Guide** governing how the MSSP plans, executes, evaluates, and improves discussion-based incident response simulations across SOC tiers, IR Team, executives, and client engagements — providing structured methodology for low-cost, high-value preparedness validation.

A formal tabletop exercise guide is critical because:

- tabletop exercises are the most cost-effective method to validate IR readiness without operational disruption
- regulatory frameworks (RBI, NIST, ISO 27001 A.5.24) mandate periodic IR testing
- clients increasingly require evidence of MSSP IR exercise participation
- IR Team and SOC analyst skills atrophy without regular practice
- new playbooks, procedures, and personnel must be validated before live incidents
- gaps in coordination, decision-making, communication, and authority emerge only under simulation
- multi-tenant scenarios require practice to enforce segregation discipline under pressure
- cross-client coordination (CCIC) requires rehearsal before real incidents
- regulatory engagement, legal coordination, and executive communication require practiced execution
- post-incident lessons learned require structured TTX-driven gap identification
- TTXs build muscle memory for crisis decision-making and bridge call leadership
- TTXs validate playbook completeness, accuracy, and usability
- TTXs surface tool gaps, integration issues, and detection blind spots
- TTXs reveal training gaps and informing onboarding/refresher needs
- TTXs build cross-functional trust between SOC, IR, Legal, Compliance, Executive teams
- TTXs satisfy ISO 27001 internal audit and NIST CSF maturity assessment evidence
- without a structured guide, TTXs become inconsistent, ineffective, and unauditable
- this guide is the foundation for the MSSP exercise program

This guide ensures:

- consistent TTX methodology across all scenario types
- defined roles for facilitator, evaluators, participants, observers
- standardized planning, execution, and after-action processes
- multi-tenant TTX scenarios with proper segregation
- audit-ready documentation of all TTX activities
- structured evaluation against measurable objectives
- linkage to lessons learned, playbook updates, and improvement tracking
- per-scenario customization while maintaining consistent quality

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`

---

# 3. Scope

This guide applies to all MSSP tabletop exercises:

| Scope Element          | Coverage                                  |
| ---------------------- | ----------------------------------------- |
| MSSP-internal TTXs     | SOC + IR Team practice                    |
| Per-client TTXs        | With client participation                 |
| Cross-functional TTXs  | SOC + IR + Legal + Compliance + Executive |
| Multi-tenant TTXs      | Cross-client coordination practice        |
| Onboarding TTXs        | New analyst exercises                     |
| Annual mandatory TTXs  | Per playbook/scenario category            |
| Quarterly focused TTXs | Specific skill/scenario                   |
| Pre-deployment TTXs    | New playbook/tool validation              |
| Post-incident TTXs     | Lessons learned reinforcement             |
| Regulatory TTXs        | RBI/CERT-In/sector-specific               |
| Client-requested TTXs  | Per MSA / on-demand                       |

Out of scope:

- Technical drills with live tooling (covered by `10.3_Drills/`)
- Red team / purple team exercises (covered by `10.3_Drills/`)
- Live incident response (covered by `02_PLAYBOOKS/`)
- BCP/DR exercises (covered by separate BCP/DR program)

---

# 4. Definitions

| Term                               | Definition                                       |
| ---------------------------------- | ------------------------------------------------ |
| Tabletop Exercise (TTX)            | Discussion-based simulation of incident scenario |
| Facilitator                        | Person leading the TTX                           |
| Evaluator                          | Person assessing participant performance         |
| Observer                           | Non-participating attendee for learning          |
| Participant                        | Active role player in the TTX                    |
| Scenario                           | Documented incident situation to simulate        |
| Inject                             | Information added during TTX to advance scenario |
| Master Scenario Events List (MSEL) | Timeline of all injects and decision points      |
| White Team                         | Facilitators + evaluators (control team)         |
| Hot Wash                           | Immediate post-TTX debrief                       |
| After-Action Report (AAR)          | Formal TTX documentation and findings            |
| TTX Objectives                     | Measurable goals for the exercise                |
| Discussion-Based                   | No live system interaction                       |
| Operations-Based                   | Includes live system actions (= drill, not TTX)  |
| Exercise Cycle                     | Plan → Conduct → Evaluate → Improve              |

---

# 5. Roles and Responsibilities

| Role                                     | Responsibilities                                     |
| ---------------------------------------- | ---------------------------------------------------- |
| **MSSP IR Team Lead**                    | TTX program ownership; scenario approval; AAR review |
| **MSSP SOC Manager**                     | TTX participation; resource allocation; AAR review   |
| **MSSP Training Lead / Compliance Lead** | TTX scheduling; documentation; metrics               |
| **TTX Facilitator**                      | Lead the exercise; manage injects; control pace      |
| **TTX Evaluators**                       | Assess participants; complete scorecards             |
| **Scenario Designer**                    | Develop scenario + MSEL                              |
| **Participants**                         | Engage authentically as their role                   |
| **Observers**                            | Learn without participating                          |
| **MSSP Threat Intel Lead**               | Provide threat actor/TTP realism                     |
| **MSSP Compliance Lead**                 | Regulatory realism injects                           |
| **MSSP Legal Counsel**                   | Legal injects + evaluation                           |
| **MSSP CISO**                            | Executive participation in major TTXs                |
| **Per-Client SDM**                       | Client TTX coordination (if client-involving)        |

---

# 6. Tabletop Exercise Principles (Mandatory)

| Principle                 | Requirement                                               |
| ------------------------- | --------------------------------------------------------- |
| **Objective-Driven**      | Every TTX has measurable objectives                       |
| **Realistic Scenarios**   | Based on real threat intelligence and client environments |
| **Safe Environment**      | No-blame, learning-focused culture                        |
| **Discussion-Based**      | No live system interaction (would be drill, not TTX)      |
| **Time-Boxed**            | Defined start, end, and inject timing                     |
| **Multi-Tenant Aware**    | Tenant segregation respected even in simulation           |
| **Documented Throughout** | Decisions, gaps, observations captured live               |
| **Evaluated Objectively** | Scorecard-based assessment                                |
| **Improvement-Focused**   | AAR drives actionable improvements                        |
| **Audit-Ready**           | All records retained for compliance evidence              |
| **Inclusive**             | Cross-functional participation encouraged                 |
| **Periodic**              | Regular cadence (annual mandatory + quarterly focused)    |

---

# 7. Tabletop Exercise Types (Mandatory)

## 7.1 By Scope

| Type                     | Description                                | Typical Duration |
| ------------------------ | ------------------------------------------ | ---------------- |
| **Discussion-Based TTX** | Talk-through scenario with decisions       | 2-4 hours        |
| **Workshop TTX**         | Deep-dive working session                  | Half day         |
| **Functional TTX**       | Specific function focus (e.g., comms only) | 1-2 hours        |
| **Full-Scale TTX**       | Multi-team, multi-hour with breaks         | Full day         |
| **Mini TTX**             | Quick scenario for skill refresh           | 30-60 min        |

## 7.2 By Audience

| Type                     | Audience                              |
| ------------------------ | ------------------------------------- |
| **Tactical TTX**         | L1/L2/L3 analyst focus                |
| **Operational TTX**      | SOC Lead + IR Team focus              |
| **Strategic TTX**        | Executive + CISO focus                |
| **Cross-Functional TTX** | All tiers + Legal + Compliance + Exec |
| **Client TTX**           | MSSP + client team                    |
| **Regulatory TTX**       | Focus on regulatory engagement        |

## 7.3 By Frequency

| Type                      | Cadence                         |
| ------------------------- | ------------------------------- |
| **Annual Mandatory TTX**  | Each major playbook category    |
| **Quarterly Focused TTX** | Specific skill/scenario         |
| **Onboarding TTX**        | Per onboarding cohort           |
| **Post-Incident TTX**     | After major incident            |
| **Pre-Deployment TTX**    | Before new playbook/tool launch |
| **Ad-Hoc TTX**            | On-demand for emerging threats  |

---

# 8. TTX Lifecycle (Mandatory)

┌──────────────────────────────────────────────────────────┐
│ Phase 1: PLAN │
│ Define objectives, scenario, participants, logistics │
└──────────────────────────────────────────────────────────┘
                                                                             │
                                                                            ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 2: DESIGN │
│ Scenario document, MSEL, injects, evaluation criteria │
└──────────────────────────────────────────────────────────┘
                                                                             │
                                                                            ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 3: PREPARE │
│ Schedule, brief facilitators/evaluators, logistics │
└──────────────────────────────────────────────────────────┘
                                                                             │
                                                                            ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 4: CONDUCT │
│ Execute TTX with facilitator-led injects │
└──────────────────────────────────────────────────────────┘
                                                                            │
                                                                           ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 5: HOT WASH │
│ Immediate post-TTX debrief (30-60 min) │
└──────────────────────────────────────────────────────────┘
                                                                           │
                                                                          ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 6: EVALUATE │
│ Compile evaluator scorecards + observations │
└──────────────────────────────────────────────────────────┘
                                                                            │
                                                                           ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 7: AFTER-ACTION REPORT (AAR) │
│ Document findings, recommendations, action items │
└──────────────────────────────────────────────────────────┘
                                                                            │
                                                                           ▼
┌──────────────────────────────────────────────────────────┐
│ Phase 8: IMPROVE │
│ Track actions through closure; update playbooks/training│
└──────────────────────────────────────────────────────────┘

---

# 9. Phase 1: Plan (Mandatory)

## 9.1 Define Objectives

Every TTX must have 3-7 measurable objectives. Examples:

| Objective Category  | Example                                             |
| ------------------- | --------------------------------------------------- |
| **Process**         | Validate ransomware playbook execution end-to-end   |
| **Decision-Making** | Test containment authority decisions under pressure |
| **Communication**   | Validate executive notification within 30 min       |
| **Coordination**    | Test cross-team coordination (SOC + IR + Legal)     |
| **Regulatory**      | Validate RBI reporting workflow within 2 hours      |
| **Multi-Tenant**    | Test CCIC coordination for cross-client incident    |
| **Tool**            | Identify gaps in SIEM/SOAR integration              |
| **Skill**           | Validate L2 escalation criteria application         |

## 9.2 Select Scenario Type

| Selection Factor          | Considerations                               |
| ------------------------- | -------------------------------------------- |
| Current threat landscape  | What's actively targeting client industries  |
| Recent incident lessons   | What gaps emerged in real incidents          |
| Playbook validation needs | Which playbooks haven't been tested recently |
| New personnel             | New onboarding cohorts                       |
| Regulatory drivers        | RBI/CERT-In/sector-specific expectations     |
| Client requests           | Per MSA exercise obligations                 |

## 9.3 Define Participants

| Role Category     | Required for Most TTX       |
| ----------------- | --------------------------- |
| L1 Analyst        | Yes (operational TTXs)      |
| L2 Analyst        | Yes (operational TTXs)      |
| L3 Analyst        | Yes (most TTXs)             |
| SOC Lead          | Yes (most TTXs)             |
| IR Team Member    | Yes (most TTXs)             |
| IR Team Lead      | Yes (P1-equivalent TTXs)    |
| Threat Intel Lead | Recommended                 |
| Compliance Lead   | Yes (regulatory TTXs)       |
| Legal Counsel     | Yes (legal-involving TTXs)  |
| Per-Client SDM    | Yes (client-involving TTXs) |
| SOC Manager       | Recommended                 |
| CISO              | P1-equivalent TTXs          |
| Executive         | Strategic TTXs              |

## 9.4 Define Logistics

| Element   | Requirement                                         |
| --------- | --------------------------------------------------- |
| Duration  | Per TTX type (2-8 hours)                            |
| Location  | Physical, virtual, or hybrid                        |
| Materials | Scenario brief, MSEL (facilitator only), scorecards |
| Equipment | Whiteboards, conference systems, projection         |
| Catering  | For >4 hour exercises                               |
| Recording | Optional (with consent)                             |

---

# 10. Phase 2: Design (Mandatory)

## 10.1 Scenario Document Structure

Each scenario document must include:

| Section              | Content                                                 |
| -------------------- | ------------------------------------------------------- |
| Scenario name        | Descriptive title                                       |
| Scenario summary     | 1-paragraph overview                                    |
| Background           | Client/environment context (sanitized for multi-tenant) |
| Initial situation    | Starting conditions                                     |
| Timeline             | Approximate scenario span                               |
| Threat actor profile | Realistic actor based on TI                             |
| TTPs involved        | MITRE ATT&CK mapping                                    |
| Affected systems     | Realistic system landscape                              |
| Business impact      | Realistic impact narrative                              |
| Regulatory exposure  | Realistic regulatory considerations                     |

## 10.2 Master Scenario Events List (MSEL)

The MSEL is the facilitator's playbook containing all injects:

| Field               | Description                                        |
| ------------------- | -------------------------------------------------- |
| Inject #            | Sequential number                                  |
| Inject time (T+)    | Relative time from scenario start                  |
| Inject method       | Verbal, written, email, simulated alert            |
| Inject content      | What information is delivered                      |
| Source              | Who delivers (facilitator role)                    |
| Expected response   | What participants should do                        |
| Evaluation criteria | What evaluators assess                             |
| Branch logic        | If/then progression based on participant decisions |

**MSEL example (excerpt):**

| #   | T+     | Method  | Content                                                | Expected                                  | Criteria                |
| --- | ------ | ------- | ------------------------------------------------------ | ----------------------------------------- | ----------------------- |
| 1   | 0 min  | Verbal  | "SIEM alert: ransomware encryption activity on host X" | L1 acknowledges, triages, creates ticket  | TTA < 5 min             |
| 2   | 10 min | Written | "EDR shows 50+ hosts affected"                         | L1 escalates to L2; L2 escalates to L3+IR | Escalation < 15 min     |
| 3   | 30 min | Verbal  | "Client CISO calls demanding status"                   | IR Team activates client comms            | Client briefed < 30 min |

## 10.3 Inject Types

| Type                   | Use                                  |
| ---------------------- | ------------------------------------ |
| Information injects    | New facts revealed                   |
| Decision injects       | Force participants to decide         |
| Pressure injects       | Time pressure or stakeholder demands |
| Curveball injects      | Unexpected complications             |
| Cross-client injects   | Multi-tenant scenario expansion      |
| Regulatory injects     | Regulator demands during incident    |
| Media/external injects | Press inquiries, social media        |
| Vendor injects         | Vendor/3rd-party developments        |

## 10.4 Evaluation Criteria

For each objective, define:

| Element             | Description                          |
| ------------------- | ------------------------------------ |
| Objective ID        | Unique identifier                    |
| Success criteria    | Specific measurable outcome          |
| Evaluation method   | Observation, scorecard, decision log |
| Pass/fail threshold | Minimum acceptable performance       |
| Weight              | Importance for overall TTX scoring   |

## 10.5 Multi-Tenant Scenario Considerations

| Consideration                     | Requirement                                  |
| --------------------------------- | -------------------------------------------- |
| Use fictional client names        | Never real client names                      |
| Use sanitized client environments | Generic but realistic                        |
| Test tenant segregation           | Include cross-client temptation injects      |
| Test sanitization                 | Include cross-client intel sharing decisions |
| Test CCIC activation              | Include multi-tenant trigger injects         |

---

# 11. Phase 3: Prepare (Mandatory)

## 11.1 Scheduling

| Activity                        | Timeline  |
| ------------------------------- | --------- |
| TTX scheduled                   | T-30 days |
| Calendar invites sent           | T-30 days |
| Participant briefing (pre-read) | T-7 days  |
| Facilitator/evaluator briefing  | T-5 days  |
| Logistics confirmation          | T-3 days  |
| Pre-TTX reminder                | T-1 day   |

## 11.2 Pre-Read Materials for Participants

| Material                    | Required |
| --------------------------- | -------- |
| Scenario summary (not MSEL) | Yes      |
| Their role expectations     | Yes      |
| Relevant playbook reference | Yes      |
| Relevant SOP reference      | Yes      |
| Ground rules                | Yes      |
| TTX objectives (high-level) | Yes      |

## 11.3 Facilitator/Evaluator Briefing

| Item                   | Coverage |
| ---------------------- | -------- |
| Full scenario + MSEL   | Yes      |
| Inject delivery timing | Yes      |
| Branch logic           | Yes      |
| Evaluation criteria    | Yes      |
| Scorecard usage        | Yes      |
| Hot wash facilitation  | Yes      |
| AAR template           | Yes      |

## 11.4 Logistics Checklist

- [ ] Venue confirmed (physical/virtual)
- [ ] Equipment tested (projector, conferencing)
- [ ] Materials printed (scenario brief, scorecards)
- [ ] Facilitator/evaluator scripts ready
- [ ] Timekeeping mechanism ready
- [ ] Recording arrangement (if applicable)
- [ ] Catering arranged (if >4 hours)
- [ ] Backup facilitator identified

---

# 12. Phase 4: Conduct (Mandatory)

## 12.1 Standard TTX Agenda

| Time      | Activity                              |
| --------- | ------------------------------------- |
| 0:00-0:15 | Welcome, introductions, ground rules  |
| 0:15-0:30 | Scenario briefing (initial situation) |
| 0:30-0:45 | Objectives + evaluation overview      |
| 0:45-3:00 | Scenario execution with injects       |
| 3:00-3:15 | Break                                 |
| 3:15-3:45 | Scenario conclusion + final injects   |
| 3:45-4:30 | Hot wash debrief                      |
| 4:30      | Close + AAR timeline communicated     |

## 12.2 Ground Rules (Communicated at Start)

| Rule                        | Description                  |
| --------------------------- | ---------------------------- |
| **Safe space**              | No blame; learning-focused   |
| **Confidentiality**         | TTX content stays internal   |
| **Engage authentically**    | Play your role realistically |
| **Time-bound**              | Respect facilitator pacing   |
| **Decisions documented**    | All decisions logged         |
| **No tool interaction**     | Discussion only              |
| **Multi-tenant discipline** | Tenant segregation enforced  |
| **Questions welcomed**      | Ask facilitator when stuck   |

## 12.3 Facilitator Responsibilities During TTX

- Deliver injects on schedule (or per branch logic)
- Maintain pace (avoid getting stuck on tangents)
- Prompt under-participating roles
- De-escalate over-arguing
- Capture decisions and gaps
- Manage breaks
- Steer hot wash discussion

## 12.4 Evaluator Responsibilities During TTX

- Observe assigned participant(s)
- Complete scorecard in real-time
- Document specific observations (quotes, decisions)
- Note gaps and strengths
- Avoid intervening in scenario

## 12.5 Participant Expected Behavior

- Engage as their actual role
- Make decisions using actual playbooks/SOPs
- Communicate as they would in real incident
- Respect facilitator pacing
- Document their decisions
- Maintain multi-tenant discipline

---

# 13. Phase 5: Hot Wash (Mandatory)

## 13.1 Hot Wash Purpose

Immediate post-TTX debrief to capture top-of-mind observations:

| Element                        | Duration |
| ------------------------------ | -------- |
| What went well                 | 10 min   |
| What did not go well           | 10 min   |
| Immediate gaps identified      | 10 min   |
| Quick wins (low-hanging fruit) | 10 min   |
| Next steps + AAR timeline      | 5 min    |

## 13.2 Hot Wash Facilitation

| Technique                         | Use                              |
| --------------------------------- | -------------------------------- |
| Round-robin sharing               | Ensure every participant speaks  |
| Plus/Delta analysis               | What worked / what to change     |
| Categorize feedback               | Process, people, tools, training |
| Capture verbatim quotes           | Preserve participant voice       |
| Avoid solutioning during hot wash | Defer to AAR                     |

---

# 14. Phase 6: Evaluate (Mandatory)

## 14.1 Scorecard Compilation

| Activity                         | Owner         |
| -------------------------------- | ------------- |
| Collect all evaluator scorecards | Training Lead |
| Compile against objectives       | Training Lead |
| Calculate per-objective scores   | Training Lead |
| Calculate overall TTX score      | Training Lead |
| Identify recurring observations  | Training Lead |

## 14.2 Scoring Framework

Per `TTX-Evaluation-Scorecard.md`:

| Score | Description                        |
| ----- | ---------------------------------- |
| 5     | Exceeds expectations               |
| 4     | Meets expectations fully           |
| 3     | Meets expectations with minor gaps |
| 2     | Partial — major gaps               |
| 1     | Did not meet expectations          |
| N/A   | Not applicable / not observed      |

## 14.3 Objective-Level Pass/Fail

| Overall Score | Objective Status                  |
| ------------- | --------------------------------- |
| ≥4.0          | Pass with excellence              |
| ≥3.0          | Pass                              |
| 2.0-2.9       | Marginal — improvement needed     |
| <2.0          | Fail — corrective action required |

---

# 15. Phase 7: After-Action Report (AAR) (Mandatory)

## 15.1 AAR Standard Structure

| Section                | Content                          |
| ---------------------- | -------------------------------- |
| 1\. Executive Summary  | TTX overview + key findings      |
| 2\. TTX Objectives     | List with achievement status     |
| 3\. Participants       | List by role                     |
| 4\. Scenario Summary   | What was simulated               |
| 5\. Timeline of Events | Major scenario milestones        |
| 6\. Strengths Observed | What went well                   |
| 7\. Gaps Identified    | What did not go well             |
| 8\. Recommendations    | Specific actionable improvements |
| 9\. Action Items       | Owner + due date + tracking      |
| 10\. Lessons Learned   | Generalized takeaways            |
| 11\. Appendix          | Scorecards, decisions, quotes    |

## 15.2 AAR Timeline

| Activity                            | Timeline          |
| ----------------------------------- | ----------------- |
| Draft AAR                           | T+7 days post-TTX |
| Review with facilitators/evaluators | T+10 days         |
| Distribute to participants          | T+14 days         |
| Action items entered in tracker     | T+14 days         |
| AAR sign-off by IR Team Lead        | T+21 days         |
| Formal closure                      | T+30 days         |

## 15.3 AAR Distribution

| Audience                       | Distribution                          |
| ------------------------------ | ------------------------------------- |
| Participants                   | Full AAR                              |
| SOC Manager                    | Full AAR                              |
| IR Team Lead                   | Full AAR                              |
| CISO                           | Executive summary + selected sections |
| Action item owners             | Action item extracts                  |
| Training Lead                  | Full AAR for trend analysis           |
| Compliance Lead                | Full AAR for audit evidence           |
| Per-client SDM (if client TTX) | Sanitized AAR                         |

---

# 16. Phase 8: Improve (Mandatory)

## 16.1 Action Item Tracking

All AAR action items tracked in `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`:

| Field            | Required                      |
| ---------------- | ----------------------------- |
| Action ID        | Yes                           |
| Source TTX       | Yes                           |
| Description      | Yes                           |
| Owner            | Yes                           |
| Due date         | Yes                           |
| Priority         | Yes                           |
| Status           | Yes (Open/In Progress/Closed) |
| Closure evidence | Yes                           |
| Verification     | Yes                           |

## 16.2 Improvement Categories

| Category              | Examples                                |
| --------------------- | --------------------------------------- |
| Playbook updates      | Add missing steps; clarify ambiguity    |
| SOP updates           | Refine procedures                       |
| Tool improvements     | Configure missing detections; tune SOAR |
| Training updates      | Add to onboarding; refresher needed     |
| Communication updates | Refine templates; clarify escalation    |
| Process updates       | Streamline workflows                    |
| Authority updates     | Refine containment authority matrix     |
| Documentation updates | Improve runbooks                        |

## 16.3 Playbook & Detection Improvement Linkage

| Improvement Type       | Tracked In                                                                      |
| ---------------------- | ------------------------------------------------------------------------------- |
| Playbook updates       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| Detection improvements | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Control gaps           | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`           |
| General improvements   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |

---

# 17. Annual TTX Program (Mandatory)

## 17.1 Mandatory Annual TTX Calendar

| Quarter | TTX Scenarios                        |
| ------- | ------------------------------------ |
| Q1      | Ransomware + Phishing/BEC            |
| Q2      | APT/Targeted Attack + Insider Threat |
| Q3      | Data Breach + Cloud Incident         |
| Q4      | Supply Chain + Multi-Tenant CCIC     |

## 17.2 Minimum Annual TTX Requirements

| Requirement           | Quantity  |
| --------------------- | --------- |
| Total TTXs per year   | Minimum 8 |
| L1/L2 tactical TTXs   | 4         |
| L3/IR Team TTXs       | 4         |
| Cross-functional TTXs | 2         |
| Executive TTXs        | 1         |
| Multi-tenant TTXs     | 2         |
| Regulatory TTXs       | 1         |
| Client-involving TTXs | Per MSA   |

---

# 18. Multi-Tenant TTX Considerations (Mandatory)

| Aspect                                | Requirement                     |
| ------------------------------------- | ------------------------------- |
| Fictional client names                | Mandatory in scenarios          |
| Sanitized client environments         | Mandatory                       |
| Cross-tenant temptation injects       | Recommended (test discipline)   |
| CCIC activation scenarios             | Required annually               |
| Cross-tenant sanitization decisions   | Test annually                   |
| Per-client TTX (with client)          | Tenant-scoped only              |
| Sanitized aggregated TTX learnings    | For cross-portfolio improvement |
| No cross-client data in TTX materials | Strict prohibition              |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 19. Quality Checklist (Per TTX)

Before declaring TTX complete:

- [ ] TTX objectives documented and shared
- [ ] Scenario document approved by IR Team Lead
- [ ] MSEL complete with all injects
- [ ] Facilitators briefed and ready
- [ ] Evaluators briefed and scorecards ready
- [ ] Participants briefed with pre-read
- [ ] Logistics confirmed
- [ ] TTX executed per agenda
- [ ] Hot wash conducted immediately post-TTX
- [ ] Scorecards collected
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Action items entered in tracker
- [ ] Multi-tenant discipline maintained
- [ ] Records archived

---

# 20. Records Management (Mandatory)

## 20.1 TTX Records Maintained

- [ ] Scenario document
- [ ] MSEL
- [ ] Participant list (signed attendance)
- [ ] Pre-read materials distributed
- [ ] Facilitator notes
- [ ] All evaluator scorecards
- [ ] Hot wash notes
- [ ] AAR (signed by IR Team Lead)
- [ ] Action items tracker entries
- [ ] Improvement closure evidence

## 20.2 Retention

| Record                 | Retention               |
| ---------------------- | ----------------------- |
| TTX scenario documents | 7 years                 |
| AARs                   | 7 years                 |
| Scorecards             | 3 years                 |
| Action items records   | Until closure + 3 years |

---

# 21. TTX Metrics (Mandatory)

| Metric                             | Target                  |
| ---------------------------------- | ----------------------- |
| Annual TTX count                   | ≥8                      |
| Mandatory TTX coverage             | 100% scenarios annually |
| Participant attendance rate        | ≥90%                    |
| AAR completion within 14 days      | 100%                    |
| Action item closure rate (90 days) | ≥80%                    |
| Average TTX objective score        | ≥3.5                    |
| Repeat findings (recurring gaps)   | Decreasing trend        |

---

# 22. Integration with Other Processes

| Process                       | Integration                        |
| ----------------------------- | ---------------------------------- |
| IR Policy / Playbooks         | TTX validates playbooks            |
| L1/L2/L3/IR Team Onboarding   | TTX participation required         |
| Lessons Learned               | AAR feeds lessons learned register |
| Playbook Update Log           | Playbook gaps from TTX tracked     |
| Detection Improvement Log     | Detection gaps from TTX tracked    |
| Control Gap Tracker           | Control gaps from TTX tracked      |
| Security Improvement Register | TTX improvements logged            |
| ISO 27001 / NIST CSF Audits   | TTX evidence for compliance        |
| Drills Program                | TTXs complement live drills        |
| Client TTXs                   | Per MSA exercise requirements      |

---

# 23. Related Documents

| Document                        | Path                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| TTX Ransomware Scenario         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`     |
| TTX APT Scenario                | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`            |
| TTX Insider Threat Scenario     | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md` |
| TTX Data Breach Scenario        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`     |
| TTX Evaluation Scorecard        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`    |
| Drill Schedule Annual           | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`                   |
| Drill After-Action Report       | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`               |
| Red Team IR Integration SOP     | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`             |
| Purple Team Exercise Guide      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`              |
| IR Policy Master                | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                  |
| All Playbooks                   | `02_PLAYBOOKS/`                                                                    |
| L1 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`               |
| L2 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`               |
| L3 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`               |
| IR Team Onboarding Program      | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/IR-Team-Onboarding-Program.md`          |
| Lessons Learned Template        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                |
| Lessons Learned Register        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`              |
| Action Items Tracker            | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                  |
| Playbook Update Log             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| Control Gap Tracker             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`              |
| Security Improvement Register   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`    |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |

---

# 24. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / SOC Manager | Initial version |

---

# 25. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP IR Team Lead    |      |           |      |
| MSSP SOC Manager     |      |           |      |
| MSSP Compliance Lead |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
