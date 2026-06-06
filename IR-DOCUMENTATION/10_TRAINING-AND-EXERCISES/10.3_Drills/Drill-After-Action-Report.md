# Drill / Exercise After-Action Report (AAR) Template

---

# 1. Document Control

| Field          | Value                                               |
| -------------- | --------------------------------------------------- |
| Document Name  | Drill / Exercise After-Action Report (AAR) Template |
| Document ID    | MSSP-TRN-DRL-004                                    |
| Version        | 1.0                                                 |
| Effective Date | 30-May-2026                                         |
| Owner          | MSSP IR Team Lead / Training Lead                   |
| Approved By    | MSSP CISO                                           |
| Classification | Confidential – MSSP Internal                        |
| Review Cycle   | Annually (or upon AAR methodology change)           |
| Applies To     | All TTXs, red team, purple team, operational drills |

---

# 2. Purpose

This document defines the standardized **After-Action Report (AAR) Template** used to document findings, recommendations, and action items from all MSSP drills, tabletop exercises, red team engagements, purple team exercises, and operational drills — ensuring consistent, audit-ready, improvement-driving post-exercise documentation that closes the exercise-to-improvement loop.

A formal AAR template is critical because:

- without structured post-exercise documentation, exercise value is lost
- inconsistent AARs produce fragmented and non-comparable improvement tracking
- ISO 27001 A.5.24 and NIST CSF RS.IM require evidence of exercise-driven improvement
- regulatory audits require AAR records as evidence of testing program
- action items without tracked closure produce no actual improvement
- year-over-year comparison requires consistent AAR structure
- detection engineering improvements require traceable AAR-to-rule linkage
- playbook updates require traceable AAR-to-playbook linkage
- client AARs (per MSA) require sanitized, professional format
- audit evidence depends on signed, dated, attributable AARs
- this template is the standard output for all MSSP exercises

This template ensures:

- consistent AAR structure across all exercise types
- all required sections present for audit compliance
- action items standardized with owner, due date, tracking
- linkage to improvement registers and detection logs
- sanitization guidance for client-facing AARs
- multi-tenant discipline maintained in AAR content
- approval chain defined
- records retention aligned to policy

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`
- `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

# 3. Scope

This template applies to AARs from:

| Exercise Type            | Uses This Template      |
| ------------------------ | ----------------------- |
| Tabletop exercises (TTX) | Yes                     |
| Red team engagements     | Yes                     |
| Purple team exercises    | Yes                     |
| Operational drills       | Yes                     |
| Client exercises         | Yes (sanitized version) |
| BAS/CART reviews         | Adapted version         |
| Onboarding exercises     | Simplified version      |
| Post-incident exercises  | Yes                     |
| Regulatory drills        | Yes                     |

---

# 4. AAR Timeline (Mandatory)

| Activity                                 | Timeline                              |
| ---------------------------------------- | ------------------------------------- |
| Hot wash conducted                       | Same day (immediately after exercise) |
| AAR draft completed                      | T+7 days                              |
| AAR reviewed (facilitators + evaluators) | T+10 days                             |
| AAR distributed to participants          | T+14 days                             |
| Action items entered in tracker          | T+14 days                             |
| AAR signed by IR Team Lead               | T+21 days                             |
| AAR archived                             | T+30 days                             |

---

# 5. AAR Standard Structure (Mandatory)

## Section 1: Cover Page

──────────────────────────────────────────────────
AFTER-ACTION REPORT (AAR)

Exercise Name: ________________________________
Exercise Type: [ ] TTX [ ] Red Team [ ] Purple Team [ ] Drill [ ] Other
Exercise Date: ________________________________
Exercise Duration: ________________________________
AAR Author: ________________________________
AAR Date: ________________________________
Classification: Confidential – MSSP Internal
──────────────────────────────────────────────────

---

## Section 2: Executive Summary

| Element                          | Content                          |
| -------------------------------- | -------------------------------- |
| Exercise name                    |                                  |
| Exercise type                    |                                  |
| Date and duration                |                                  |
| Scenario summary (1-2 sentences) |                                  |
| Key objectives                   |                                  |
| Overall outcome                  | Pass / Fail / Pass with Concerns |
| Critical findings (top 3)        |                                  |
| Overall multi-tenant discipline  | Pass / Fail                      |
| Total action items generated     |                                  |
| Next exercise planned            |                                  |

---

## Section 3: Exercise Objectives and Status

| Objective ID | Description | Weight | Score (1-5) | Pass/Fail | Notes |
| ------------ | ----------- | ------ | ----------- | --------- | ----- |
| OBJ-1        |             |        |             |           |       |
| OBJ-2        |             |        |             |           |       |
| OBJ-3        |             |        |             |           |       |
| OBJ-4        |             |        |             |           |       |
| ...          |             |        |             |           |       |

**Overall Weighted Score:** _____ / 5.0

---

## Section 4: Participants

| Role | Name | Attendance       |
| ---- | ---- | ---------------- |
|      |      | Present / Absent |
|      |      |                  |
|      |      |                  |

**Total Participants:** _____
**Attendance Rate:** _____%

---

## Section 5: Scenario Summary

| Element                        | Details |
| ------------------------------ | ------- |
| Scenario name                  |         |
| Threat actor (fictional)       |         |
| Threat category                |         |
| Client/environment (fictional) |         |
| Initial vector                 |         |
| Key progression                |         |
| Resolution (as simulated)      |         |

---

## Section 6: Exercise Timeline

| Time | Event / Inject | Expected Response | Actual Response | Assessment             |
| ---- | -------------- | ----------------- | --------------- | ---------------------- |
| T+0  |                |                   |                 | Met / Partial / Missed |
| T+X  |                |                   |                 |                        |
| T+X  |                |                   |                 |                        |
| ...  |                |                   |                 |                        |

---

## Section 7: Strengths Observed

(List 5-10 specific strengths with evidence)

| #   | Strength | Evidence |
| --- | -------- | -------- |
| 1   |          |          |
| 2   |          |          |
| 3   |          |          |
| 4   |          |          |
| 5   |          |          |

---

## Section 8: Gaps Identified

(List 5-10 specific gaps with evidence and impact)

| #   | Gap | Evidence | Impact | Priority |
| --- | --- | -------- | ------ | -------- |
| 1   |     |          |        | P1/P2/P3 |
| 2   |     |          |        |          |
| 3   |     |          |        |          |
| 4   |     |          |        |          |
| 5   |     |          |        |          |

---

## Section 9: Multi-Tenant Discipline Assessment

| Criterion                               | Score (1-5) | Observations |
| --------------------------------------- | ----------- | ------------ |
| No cross-client information leakage     |             |              |
| Tenant context verified before actions  |             |              |
| Per-client communications separated     |             |              |
| CCIC properly activated (if applicable) |             |              |
| Sanitization applied correctly          |             |              |
| Per-client regulatory filings respected |             |              |

**Overall Multi-Tenant Score:** _____ / 5.0

**Critical Multi-Tenant Failures:** Yes / No (if yes, detail below)

---

## Section 10: Critical Failure Triggers

| Critical Failure              | Observed? (Y/N) | Evidence | Action Required |
| ----------------------------- | --------------- | -------- | --------------- |
| Cross-client info leakage     |                 |          |                 |
| Joint bridge call             |                 |          |                 |
| External comm without legal   |                 |          |                 |
| Legal hold missed             |                 |          |                 |
| CCIC not appointed            |                 |          |                 |
| Containment without authority |                 |          |                 |
| Regulatory timeline missed    |                 |          |                 |
| Scenario-specific failures    |                 |          |                 |

---

## Section 11: Detection Coverage (Purple Team / Red Team Only)

| Technique ID | Technique Name | Detected? | Detection Time | FP Rate | Gap Type |
| ------------ | -------------- | --------- | -------------- | ------- | -------- |
|              |                | Y/N       |                |         |          |
|              |                |           |                |         |          |

**Baseline Coverage:** _____% 
**Post-Iteration Coverage:** _____% 
**Detection Improvement:** _____% 

---

## Section 12: Recommendations

(List 5-10 specific, actionable recommendations)

| #   | Recommendation | Category                                      | Priority | Estimated Effort |
| --- | -------------- | --------------------------------------------- | -------- | ---------------- |
| 1   |                | Detection / Process / Training / Tool / Comms |          |                  |
| 2   |                |                                               |          |                  |
| 3   |                |                                               |          |                  |
| 4   |                |                                               |          |                  |
| 5   |                |                                               |          |                  |

---

## Section 13: Action Items

| Action ID        | Description | Category | Owner | Due Date | Priority | Status |
| ---------------- | ----------- | -------- | ----- | -------- | -------- | ------ |
| AAR-YYYY-####-01 |             |          |       |          |          | Open   |
| AAR-YYYY-####-02 |             |          |       |          |          | Open   |
| AAR-YYYY-####-03 |             |          |       |          |          | Open   |
| ...              |             |          |       |          |          |        |

**Action items tracked in:**

- `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`

**Detection-specific items tracked in:**

- `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

**Playbook-specific items tracked in:**

- `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

## Section 14: Lessons Learned

(Generalized takeaways applicable beyond this specific exercise)

| #   | Lesson | Applicability                    |
| --- | ------ | -------------------------------- |
| 1   |        | All SOC / Per client / MSSP-wide |
| 2   |        |                                  |
| 3   |        |                                  |

**Lessons learned fed to:**

- `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`

---

## Section 15: Verbatim Quotes (Appendix)

| Speaker (role) | Quote | Context |
| -------------- | ----- | ------- |
|                |       |         |
|                |       |         |

---

## Section 16: Evaluator Scorecards (Appendix)

(Attach all completed evaluator scorecards per `TTX-Evaluation-Scorecard.md`)

---

## Section 17: AAR Distribution

| Audience                    | Distribution                     | Version                   |
| --------------------------- | -------------------------------- | ------------------------- |
| Participants                | Full AAR                         | Internal                  |
| SOC Manager                 | Full AAR                         | Internal                  |
| IR Team Lead                | Full AAR                         | Internal                  |
| CISO                        | Executive summary + key sections | Internal                  |
| Compliance Lead             | Full AAR                         | Internal (audit evidence) |
| Action item owners          | Relevant extracts                | Internal                  |
| Client (if client exercise) | Sanitized AAR                    | Per client                |
| Audit records               | Full AAR                         | Archive                   |

---

## Section 18: Sanitization for Client AAR (If Applicable)

When distributing AAR to clients:

| Element                       | Sanitization            |
| ----------------------------- | ----------------------- |
| Other client names            | Removed                 |
| MSSP internal process details | Generalized             |
| Evaluator names               | Optional (per policy)   |
| Verbatim quotes               | Removed or generalized  |
| Detection coverage specifics  | Per client's scope only |
| Multi-tenant observations     | Removed                 |

---

## Section 19: AAR Approval

| Role                          | Name | Signature | Date |
| ----------------------------- | ---- | --------- | ---- |
| AAR Author                    |      |           |      |
| Lead Facilitator              |      |           |      |
| IR Team Lead                  |      |           |      |
| SOC Manager                   |      |           |      |
| MSSP CISO (P1-equivalent TTX) |      |           |      |

---

# 6. AAR Quality Checklist (Mandatory)

Before finalizing AAR:

- [ ] Cover page complete
- [ ] Executive summary complete
- [ ] All objectives scored
- [ ] Participant list complete with attendance
- [ ] Scenario summary accurate
- [ ] Timeline complete
- [ ] Strengths documented (≥5)
- [ ] Gaps documented (≥5)
- [ ] Multi-tenant assessment completed
- [ ] Critical failure triggers reviewed
- [ ] Detection coverage included (if applicable)
- [ ] Recommendations documented (≥5)
- [ ] Action items with owners and due dates
- [ ] Lessons learned documented
- [ ] Scorecards attached
- [ ] AAR reviewed by facilitators
- [ ] AAR approved and signed
- [ ] AAR distributed per distribution list
- [ ] Action items entered in tracker
- [ ] AAR archived per retention policy

---

# 7. Records Retention

| Record                      | Retention               |
| --------------------------- | ----------------------- |
| AAR (signed)                | 7 years                 |
| Evaluator scorecards        | 3 years                 |
| Participant sign-in         | 3 years                 |
| Hot wash notes              | 3 years                 |
| Action item records         | Until closure + 3 years |
| Detection coverage matrices | 7 years                 |

---

# 8. Integration with Other Processes

| Process                               | Integration                |
| ------------------------------------- | -------------------------- |
| All exercise types                    | AAR is standard output     |
| Lessons Learned Register              | AAR feeds register         |
| Action Items Tracker                  | AAR items tracked          |
| Detection Improvement Log             | Detection gaps tracked     |
| Playbook Update Log                   | Playbook gaps tracked      |
| Control Gap Tracker                   | Control gaps tracked       |
| Security Improvement Register         | Improvements tracked       |
| ISO 27001 / NIST CSF Audits           | AAR as compliance evidence |
| Annual Exercise Review                | AARs reviewed for trends   |
| Client reporting (if client exercise) | Sanitized AAR delivered    |

---

# 9. Related Documents

| Document                       | Path                                                                              |
| ------------------------------ | --------------------------------------------------------------------------------- |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`    |
| TTX Evaluation Scorecard       | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`   |
| Red Team IR Integration SOP    | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`            |
| Purple Team Exercise Guide     | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`             |
| Drill Schedule Annual          | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`                  |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`               |
| Lessons Learned Register       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`             |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                 |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`         |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`               |
| Control Gap Tracker            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`             |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`   |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| MSSP Audit Readiness Checklist | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`         |

---

# 10. Revision History

| Version | Date        | Author                            | Changes         |
| ------- | ----------- | --------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / Training Lead | Initial version |

---

# 11. Approval

Approved by:

| Role               | Name | Signature | Date |
| ------------------ | ---- | --------- | ---- |
| MSSP IR Team Lead  |      |           |      |
| MSSP Training Lead |      |           |      |
| MSSP SOC Manager   |      |           |      |
| MSSP CISO          |      |           |      |

---

**End of Document**
