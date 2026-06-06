# Tabletop Exercise (TTX) Evaluation Scorecard

---

# 1. Document Control

| Field          | Value                                                                    |
| -------------- | ------------------------------------------------------------------------ |
| Document Name  | TTX Evaluation Scorecard                                                 |
| Document ID    | MSSP-TRN-TTX-003                                                         |
| Version        | 1.0                                                                      |
| Effective Date | 30-May-2026                                                              |
| Owner          | MSSP IR Team Lead / Training Lead                                        |
| Approved By    | MSSP CISO                                                                |
| Classification | Confidential – MSSP Internal                                             |
| Review Cycle   | Annually (or upon TTX methodology change)                                |
| Applies To     | All TTX scenarios (Ransomware, APT, Insider Threat, Data Breach, custom) |

---

# 2. Purpose

This document defines the standardized **Tabletop Exercise (TTX) Evaluation Scorecard** used by MSSP evaluators to objectively assess participant performance across all TTX scenarios — ensuring consistent, audit-ready, comparable evaluation that drives meaningful improvement.

A formal TTX evaluation scorecard is critical because:

- subjective TTX feedback produces inconsistent improvement actions across exercises
- inconsistent evaluation undermines TTX value and credibility
- ISO 27001 A.5.24 and NIST CSF RS.MA require evidence of incident response testing
- regulatory audits (RBI, internal ISMS) require objective TTX evaluation records
- year-over-year comparison requires consistent scoring methodology
- per-role evaluation enables targeted training interventions
- per-objective evaluation enables targeted playbook/process improvements
- multi-tenant discipline must be evaluated explicitly under pressure
- legal/regulatory/communication competencies need structured assessment
- critical failure triggers must be unambiguously documented
- AAR (After-Action Report) quality depends on structured scoring inputs
- evaluators benefit from clear guidance to reduce evaluator variability
- post-TTX action items require evidence-based justification from scorecards
- new evaluators need clear scoring rubric to onboard quickly
- without consistent scorecards, TTX investment is wasted on inconsistent learning
- this scorecard is the operational backbone for the MSSP exercise evaluation program

This scorecard ensures:

- consistent 5-point scoring rubric across all TTX scenarios
- per-objective evaluation with measurable criteria
- per-role observation framework
- standardized critical failure documentation
- multi-tenant discipline evaluation built into every scorecard
- audit-ready scoring records
- comparable evaluation across exercises and over time
- structured input for AAR development
- evaluator training and calibration guidance
- linkage to lessons learned, playbook updates, and improvement tracking

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md`
- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`

---

# 3. Scope

This scorecard applies to all MSSP tabletop exercises:

| Scope Element             | Coverage                                                       |
| ------------------------- | -------------------------------------------------------------- |
| All TTX scenario types    | Ransomware, APT, Insider Threat, Data Breach, Phishing, custom |
| All audience levels       | L1, L2, L3, IR Team, SOC Lead, Cross-functional, Executive     |
| All TTX formats           | Discussion-based, workshop, functional, full-scale, mini       |
| Per-objective scoring     | All TTX objectives                                             |
| Per-role observation      | All participant roles                                          |
| Multi-tenant discipline   | Mandatory in all scorecards                                    |
| Critical failure triggers | Standardized across all TTXs                                   |
| Evaluator notes           | Free-form observations                                         |
| Quotes capture            | For AAR enrichment                                             |

Out of scope:

- Live drill / red team / purple team scoring (covered by `10.3_Drills/`)
- Live incident performance evaluation (covered by performance management)
- Client TTX scoring (uses tailored scorecard with client input)
- Individual disciplinary assessment (covered by HR processes)

---

# 4. Definitions

| Term                    | Definition                                    |
| ----------------------- | --------------------------------------------- |
| Scorecard               | This evaluation document                      |
| Evaluator               | Person performing TTX assessment              |
| Objective               | TTX measurable goal being evaluated           |
| Criterion               | Specific element evaluated under an objective |
| Score                   | Numerical rating (1-5)                        |
| Weight                  | Importance multiplier for an objective        |
| Pass Threshold          | Minimum score for objective success           |
| Critical Failure        | Severe issue triggering TTX failure           |
| Calibration             | Evaluator consistency alignment               |
| Inter-Rater Reliability | Consistency between evaluators                |
| AAR                     | After-Action Report (post-TTX)                |
| Observation             | Specific behavior noted by evaluator          |
| Quote                   | Verbatim participant statement captured       |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                              |
| ------------------------ | ------------------------------------------------------------- |
| **MSSP IR Team Lead**    | Scorecard owner; methodology approval                         |
| **MSSP Training Lead**   | Scorecard distribution; compilation; AAR input                |
| **MSSP SOC Manager**     | Evaluator assignment; calibration                             |
| **Lead Evaluator**       | Coordinates per-TTX evaluation                                |
| **Domain Evaluators**    | Per-objective scoring (e.g., legal, multi-tenant, IR command) |
| **Evaluators (general)** | Score against assigned objectives; document observations      |
| **MSSP Compliance Lead** | Audit-ready records; evidence retention                       |
| **Scribe / Note-Taker**  | Verbatim quote capture for AAR                                |

---

# 6. Scoring Rubric (Mandatory)

## 6.1 5-Point Scoring Scale

| Score   | Label                              | Description                                                                                   |
| ------- | ---------------------------------- | --------------------------------------------------------------------------------------------- |
| **5**   | Exceeds Expectations               | Performed beyond defined success criteria; demonstrates excellence, initiative, or innovation |
| **4**   | Meets Expectations Fully           | Performed all defined success criteria correctly and timely                                   |
| **3**   | Meets Expectations with Minor Gaps | Performed core criteria; minor gaps that do not affect outcome                                |
| **2**   | Partial — Major Gaps               | Performed some criteria; significant gaps requiring corrective action                         |
| **1**   | Did Not Meet Expectations          | Failed to perform required criteria; significant remediation needed                           |
| **N/A** | Not Applicable / Not Observed      | Criterion not applicable to scenario or not observed by evaluator                             |

## 6.2 Scoring Guidance for Evaluators

| Score | When to Use                                                                                                             |
| ----- | ----------------------------------------------------------------------------------------------------------------------- |
| 5     | Reserved for genuinely exceptional performance — innovative approach, helping others, exceeding timelines significantly |
| 4     | Default for solid expected performance — most performers should fall here                                               |
| 3     | When core objective achieved but minor improvements noted                                                               |
| 2     | When objective only partially achieved — requires action item                                                           |
| 1     | When objective failed — requires immediate corrective action                                                            |
| N/A   | When criterion not assessable in this scenario — DO NOT score 1 if N/A                                                  |

## 6.3 Anti-Bias Guidelines

| Bias                                       | Mitigation                             |
| ------------------------------------------ | -------------------------------------- |
| Halo effect (one positive carries all)     | Score each criterion independently     |
| Recency bias (last action remembered most) | Take notes throughout, not only at end |
| Personality bias                           | Score behavior, not person             |
| Severity bias (overly harsh or lenient)    | Calibrate against rubric examples      |
| Central tendency (always score 3)          | Use full scale when warranted          |
| Confirmation bias                          | Document evidence supporting score     |

---

# 7. Per-Objective Scoring Framework (Mandatory)

## 7.1 Standard Objective Scorecard Template

| Objective ID          |                                      |
| --------------------- | ------------------------------------ |
| Objective description |                                      |
| Success criteria      | (Listed from scenario)               |
| Evaluator             |                                      |
| Weight                | 1-3 (1=standard, 2=high, 3=critical) |
| Score                 | 1-5 or N/A                           |
| Score justification   | (Evidence-based explanation)         |
| Specific observations | (What was observed)                  |
| Quotes captured       | (Verbatim if relevant)               |
| Recommendation        | (Improvement suggestion)             |
| Pass/Fail             | (Per pass threshold)                 |

## 7.2 Standard Pass Thresholds

| Objective Type                                       | Default Threshold |
| ---------------------------------------------------- | ----------------- |
| Standard objective                                   | Score ≥3          |
| High-importance objective                            | Score ≥3.5        |
| Critical objective (e.g., multi-tenant, legal-first) | Score ≥4          |

## 7.3 Weighted Scoring Calculation

Weighted Objective Score = Score × Weight

Overall TTX Score = Σ(Weighted Objective Scores) / Σ(Weights)

---

# 8. Per-Role Observation Framework (Mandatory)

## 8.1 L1 Analyst Observation

| Criterion                    | Evaluation Focus                 |
| ---------------------------- | -------------------------------- |
| Alert acknowledgement timing | Within SLA                       |
| Triage accuracy              | Correct TP/FP/escalate decisions |
| Tenant context awareness     | Verified before action           |
| Escalation timing            | Per escalation criteria          |
| Documentation quality        | Per ticket standards             |
| Tool proficiency             | Correct tool usage               |
| Communication clarity        | Clear updates to L2/SOC Lead     |

## 8.2 L2 Analyst Observation

| Criterion                      | Evaluation Focus                 |
| ------------------------------ | -------------------------------- |
| Investigation methodology      | Structured per L2 SOP            |
| Hypothesis quality             | Reasonable, evidence-based       |
| Multi-source pivoting          | Effective use of SIEM/EDR/NDR/TI |
| Tenant context discipline      | No cross-tenant contamination    |
| Escalation timing to L3        | Per escalation criteria          |
| Investigation documentation    | Per L2 standards                 |
| Containment recommendations    | Per playbook + authority matrix  |
| Threat hunting (if applicable) | Hypothesis-driven                |

## 8.3 L3 Analyst Observation

| Criterion                        | Evaluation Focus                |
| -------------------------------- | ------------------------------- |
| Forensic methodology             | Per L3 SOPs                     |
| Evidence preservation            | Chain of custody applied        |
| Memory/disk/network analysis     | Appropriate technique selection |
| Malware analysis (if applicable) | Safe lab procedures             |
| Timeline construction            | Accurate, evidence-based        |
| TTP mapping                      | MITRE ATT&CK accurate           |
| Tenant context discipline        | No cross-tenant contamination   |
| Technical report quality         | Per L3 reporting standards      |
| Coordination with IR Team        | Smooth escalation               |

## 8.4 IR Team Member Observation

| Criterion                           | Evaluation Focus           |
| ----------------------------------- | -------------------------- |
| Incident Command assumption         | Clear, timely              |
| Bridge call leadership              | Effective facilitation     |
| War room operations                 | Functional setup           |
| Decision-making under pressure      | Framework-based            |
| Containment authority application   | Per authority matrix       |
| Multi-tenant CCIC coordination      | Per CCIC procedure         |
| Executive communication             | Clear, business-translated |
| Client communication                | Per-client, sanitized      |
| Regulatory engagement               | Timeline-aware             |
| Legal coordination                  | Legal-first sequencing     |
| Vendor coordination (if applicable) | Per protocols              |

## 8.5 SOC Lead Observation

| Criterion                      | Evaluation Focus            |
| ------------------------------ | --------------------------- |
| Queue oversight                | Active monitoring           |
| Escalation management          | Timely, accurate            |
| Resource allocation            | Per workload                |
| Per-client SLA tracking        | Active awareness            |
| Coordination across tiers      | Smooth handoffs             |
| IR Team escalation trigger     | Per IRT activation criteria |
| Shift handover (if applicable) | Per template                |

## 8.6 Threat Intel Lead Observation

| Criterion                     | Evaluation Focus            |
| ----------------------------- | --------------------------- |
| TI enrichment timing          | Within scenario timeline    |
| External TI integration       | Effective use of advisories |
| TTP mapping                   | MITRE ATT&CK accurate       |
| Attribution methodology       | Diamond Model usage         |
| Attribution confidence levels | Appropriate qualification   |
| Cross-client correlation      | Sanitized portfolio brief   |
| Sanitization process          | No client identification    |

## 8.7 Compliance Lead Observation

| Criterion                          | Evaluation Focus                    |
| ---------------------------------- | ----------------------------------- |
| Regulatory timeline awareness      | DPDP, RBI, CERT-In, sector          |
| Per-client regulatory boundary     | No joint filings unless coordinated |
| Audit-ready documentation          | Per evidence standards              |
| Multi-tenant compliance discipline | No cross-client disclosure          |
| Coordination with Legal            | Per Legal Counsel SOP               |

## 8.8 Legal Counsel Observation

| Criterion                           | Evaluation Focus                |
| ----------------------------------- | ------------------------------- |
| Legal-first sequencing              | Engaged before external comms   |
| Legal hold issuance                 | Timely, scope-correct           |
| Privilege protection                | Attorney-client maintained      |
| Law enforcement engagement decision | Per protocols                   |
| External communication review       | Approved before issuance        |
| Litigation readiness                | Evidence preservation supported |

## 8.9 DPO Observation (Data Breach scenarios)

| Criterion                          | Evaluation Focus                    |
| ---------------------------------- | ----------------------------------- |
| DPO engagement timing              | Within 1 hour of breach declaration |
| DPDP notification timeline         | Awareness and compliance            |
| Notification content review        | DPDP-compliant                      |
| Data subject notification strategy | Multi-channel, compliant            |
| Cross-border considerations        | Per applicable regimes              |

## 8.10 Per-Client SDM Observation

| Criterion                          | Evaluation Focus               |
| ---------------------------------- | ------------------------------ |
| Tenant boundary discipline         | Single-client focus            |
| Client communication quality       | Per-client templates           |
| Per-client escalation matrix usage | Correct contacts/timing        |
| Client decision authority respect  | Client owns client decisions   |
| Sanitized portfolio context        | No cross-client info to client |

## 8.11 MSSP CISO Observation

| Criterion                        | Evaluation Focus                  |
| -------------------------------- | --------------------------------- |
| Strategic decision-making        | Risk-based                        |
| Executive engagement             | Timely, clear                     |
| Cross-functional coordination    | All teams aligned                 |
| External stakeholder management  | Regulator, law enforcement, press |
| Final approval discipline        | Per authority matrix              |
| Cross-client portfolio awareness | Strategic-level only              |

---

# 9. Multi-Tenant Discipline Scorecard (Mandatory)

## 9.1 Multi-Tenant Critical Evaluation

This section is **mandatory for every TTX**, regardless of scenario:

| Criterion                                                   | Score (1-5) | Observations |
| ----------------------------------------------------------- | ----------- | ------------ |
| No cross-client information mentioned in shared discussions |             |              |
| Tenant context verified before every action                 |             |              |
| Per-client communications kept separate                     |             |              |
| No joint bridge calls across clients                        |             |              |
| Cross-client correlation done via sanitized aggregated view |             |              |
| CCIC properly activated (if multi-client scenario)          |             |              |
| Per-client regulatory filings respected                     |             |              |
| Sanitization applied to cross-portfolio briefs              |             |              |
| No cross-client disclosure to a client                      |             |              |
| Tenant segregation maintained under pressure                |             |              |

**Overall Multi-Tenant Discipline Score:** (average of above)

**Multi-Tenant Pass Threshold:** ≥4.0

---

# 10. Critical Failure Triggers (Mandatory)

## 10.1 Universal Critical Failures (Apply to Every TTX)

The TTX is marked **CRITICAL FAILURE** if any of:

| Critical Failure                                | Description                                                                           |
| ----------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Cross-client information leakage**            | Information from one client mentioned in another client's context                     |
| **Joint bridge call across clients**            | Multiple clients placed on same bridge                                                |
| **Cross-client disclosure to a client**         | Telling Client A about Client B's situation                                           |
| **Joint regulatory submission**                 | Filing single regulatory report covering multiple clients without proper coordination |
| **External communication without legal review** | Press/regulator/customer comms before legal approval (where required)                 |
| **Legal hold not issued**                       | Forensic activities before legal hold (where litigation likely)                       |
| **CCIC not appointed**                          | Multi-client scenario without CCIC within 30 min of correlation                       |
| **Containment without authority**               | Bypass of containment authority matrix                                                |
| **Regulatory timeline missed**                  | Mandatory regulatory reporting timeline ignored                                       |

## 10.2 Scenario-Specific Critical Failures

Refer to specific TTX scenario document for additional critical failures per scenario.

## 10.3 Critical Failure Handling

| Action                                  | Owner            |
| --------------------------------------- | ---------------- |
| Document specific failure with evidence | Evaluator        |
| Immediate flag to Lead Facilitator      | Evaluator        |
| Discuss in hot wash explicitly          | Lead Facilitator |
| Mandatory action item in AAR            | IR Team Lead     |
| Targeted re-training                    | Training Lead    |
| Re-test in next quarterly TTX           | SOC Manager      |

---

# 11. Standard TTX Scorecard Template (Mandatory)

## 11.1 Scorecard Header

| Field                                    | Value |
| ---------------------------------------- | ----- |
| TTX Scenario Name                        |       |
| TTX Date                                 |       |
| TTX Duration (actual)                    |       |
| Evaluator Name                           |       |
| Evaluator Role                           |       |
| Evaluator Assignment (objective or role) |       |
| Lead Facilitator                         |       |

## 11.2 Per-Objective Scoring Table

| Objective ID | Description | Weight | Score (1-5) | Pass/Fail | Justification |
| ------------ | ----------- | ------ | ----------- | --------- | ------------- |
| OBJ-1        |             | 1      |             |           |               |
| OBJ-2        |             | 1      |             |           |               |
| OBJ-3        |             | 2      |             |           |               |
| OBJ-4        |             | 3      |             |           |               |
| ...          |             |        |             |           |               |

**Overall Weighted Score:** _____ / 5.0

## 11.3 Per-Role Observation Summary

| Role                | Score (1-5) | Key Observations |
| ------------------- | ----------- | ---------------- |
| L1 Analyst          |             |                  |
| L2 Analyst          |             |                  |
| L3 Analyst          |             |                  |
| IR Team Member      |             |                  |
| SOC Lead            |             |                  |
| Threat Intel Lead   |             |                  |
| Compliance Lead     |             |                  |
| Legal Counsel       |             |                  |
| DPO (if applicable) |             |                  |
| Per-Client SDM      |             |                  |
| MSSP CISO           |             |                  |

## 11.4 Multi-Tenant Discipline Score

**Score:** _____ / 5.0
**Pass/Fail:** _____

## 11.5 Critical Failure Triggers Observed

| Critical Failure              | Observed? (Y/N) | Evidence |
| ----------------------------- | --------------- | -------- |
| Cross-client info leakage     |                 |          |
| Joint bridge call             |                 |          |
| Cross-client disclosure       |                 |          |
| Joint regulatory submission   |                 |          |
| External comm without legal   |                 |          |
| Legal hold missed             |                 |          |
| CCIC not appointed            |                 |          |
| Containment without authority |                 |          |
| Regulatory timeline missed    |                 |          |
| Scenario-specific failure     |                 |          |

**Overall Critical Failure:** Yes / No

## 11.6 Strengths Observed

(Free-form — list 3-5 specific strengths)

1. 
2. 
3. 
4. 
5. 

## 11.7 Gaps Identified

(Free-form — list 3-5 specific gaps)

1. 
2. 
3. 
4. 
5. 

## 11.8 Verbatim Quotes Captured

(For AAR enrichment)

| Speaker (role) | Quote | Context |
| -------------- | ----- | ------- |
|                |       |         |
|                |       |         |
|                |       |         |

## 11.9 Recommendations

(Free-form — list 3-5 specific actionable recommendations)

1. 
2. 
3. 
4. 
5. 

## 11.10 Evaluator Signature

| Field          | Value |
| -------------- | ----- |
| Evaluator Name |       |
| Signature      |       |
| Date           |       |

---

# 12. Compiled TTX Scorecard (Lead Facilitator Use)

## 12.1 Compilation Process

| Step | Action                           | Owner            |
| ---- | -------------------------------- | ---------------- |
| 1    | Collect all evaluator scorecards | Training Lead    |
| 2    | Validate completeness            | Training Lead    |
| 3    | Average per-objective scores     | Training Lead    |
| 4    | Calculate overall weighted score | Training Lead    |
| 5    | Identify recurring observations  | Training Lead    |
| 6    | Aggregate critical failures      | Training Lead    |
| 7    | Compile quotes for AAR           | Training Lead    |
| 8    | Generate compiled scorecard      | Training Lead    |
| 9    | Review with Lead Facilitator     | Lead Facilitator |
| 10   | Input to AAR                     | IR Team Lead     |

## 12.2 Compiled Scorecard Output

| Metric                        | Value                            |
| ----------------------------- | -------------------------------- |
| TTX overall weighted score    | _____ / 5.0                      |
| Objectives passed             | _____ / total                    |
| Objectives failed             | _____ / total                    |
| Multi-tenant discipline score | _____ / 5.0                      |
| Critical failures observed    | Y/N + details                    |
| Total recommendations         | _____                            |
| Total action items proposed   | _____                            |
| Overall TTX outcome           | Pass / Fail / Pass with Concerns |

---

# 13. Evaluator Calibration (Mandatory)

## 13.1 Annual Calibration Workshop

| Element                              | Frequency |
| ------------------------------------ | --------- |
| All evaluators participate           | Annually  |
| Sample scenario scored independently | Yes       |
| Variance discussed                   | Yes       |
| Calibration on rubric application    | Yes       |
| Inter-rater reliability target       | ≥0.7      |
| Re-calibration if variance >1 point  | Yes       |

## 13.2 New Evaluator Onboarding

| Step | Action                                    |
| ---- | ----------------------------------------- |
| 1    | Review this scorecard document            |
| 2    | Review 3 prior AARs                       |
| 3    | Shadow 2 TTX evaluations                  |
| 4    | Co-evaluate 2 TTX evaluations with senior |
| 5    | Independent evaluation with senior review |
| 6    | Approved as evaluator                     |

---

# 14. Scenario-Specific Scorecard Customization

## 14.1 Per-Scenario Adjustments

Each TTX scenario document specifies:

- Specific objectives (with weights)
- Pass thresholds per objective
- Scenario-specific critical failures
- Recommended evaluator assignments

Refer to:

- `TTX-Ransomware-Scenario.md` Section 10
- `TTX-APT-Scenario.md` Section 10
- `TTX-Insider-Threat-Scenario.md` Section 10
- `TTX-DataBreach-Scenario.md` Section 10

## 14.2 Custom TTX Scorecards

For custom TTXs:

| Step | Action                                     |
| ---- | ------------------------------------------ |
| 1    | Use this scorecard as baseline             |
| 2    | Customize objectives per scenario          |
| 3    | Define scenario-specific critical failures |
| 4    | Approve scorecard with IR Team Lead        |
| 5    | Use during TTX                             |
| 6    | Archive with scenario documentation        |

---

# 15. Quality Checklist (Per Scorecard)

Before submitting a completed scorecard:

- [ ] All assigned objectives scored
- [ ] Scoring justifications provided
- [ ] Specific observations documented
- [ ] Verbatim quotes captured (where relevant)
- [ ] Multi-tenant discipline scored
- [ ] Critical failures explicitly checked
- [ ] Strengths identified
- [ ] Gaps identified
- [ ] Recommendations provided
- [ ] Evaluator signed and dated

---

# 16. Records Retention (Mandatory)

| Record                          | Retention |
| ------------------------------- | --------- |
| Individual evaluator scorecards | 3 years   |
| Compiled TTX scorecard          | 7 years   |
| Quotes archive                  | 3 years   |
| Calibration workshop records    | 5 years   |

---

# 17. Integration with Other Processes

| Process                     | Integration                               |
| --------------------------- | ----------------------------------------- |
| Tabletop Exercise Guide     | Master methodology                        |
| All TTX scenarios           | Use this scorecard                        |
| Drills                      | Adapted scorecard variant                 |
| Lessons Learned             | Scorecard feeds AAR                       |
| Playbook Update Log         | Scorecard gaps drive updates              |
| Detection Improvement Log   | Scorecard gaps drive detection updates    |
| Control Gap Tracker         | Scorecard gaps tracked                    |
| Onboarding Programs         | Scorecard used during onboarding TTXs     |
| Performance Management      | Scorecard observations inform performance |
| ISO 27001 / NIST CSF Audits | Scorecards as compliance evidence         |

---

# 18. Related Documents

| Document                        | Path                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| Tabletop Exercise Guide         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`     |
| TTX Ransomware Scenario         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`     |
| TTX APT Scenario                | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`            |
| TTX Insider Threat Scenario     | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md` |
| TTX Data Breach Scenario        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`     |
| Drill Schedule Annual           | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`                   |
| Drill After-Action Report       | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`               |
| Lessons Learned Template        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                |
| Lessons Learned Register        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`              |
| Action Items Tracker            | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                  |
| Playbook Update Log             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| Control Gap Tracker             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`              |
| Security Improvement Register   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`    |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| L1 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`               |
| L2 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`               |
| L3 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`               |
| IR Team Onboarding Program      | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/IR-Team-Onboarding-Program.md`          |

---

# 19. Revision History

| Version | Date        | Author                            | Changes         |
| ------- | ----------- | --------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / Training Lead | Initial version |

---

# 20. Approval

Approved by:

| Role               | Name | Signature | Date |
| ------------------ | ---- | --------- | ---- |
| MSSP IR Team Lead  |      |           |      |
| MSSP Training Lead |      |           |      |
| MSSP SOC Manager   |      |           |      |
| MSSP CISO          |      |           |      |

---

**End of Document**
