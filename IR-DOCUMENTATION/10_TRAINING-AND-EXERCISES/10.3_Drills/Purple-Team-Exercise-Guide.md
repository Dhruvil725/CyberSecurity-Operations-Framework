# Purple Team Exercise Guide

---

# 1. Document Control

| Field          | Value                                             |
| -------------- | ------------------------------------------------- |
| Document Name  | Purple Team Exercise Guide                        |
| Document ID    | MSSP-TRN-DRL-002                                  |
| Version        | 1.0                                               |
| Effective Date | 30-May-2026                                       |
| Owner          | MSSP Detection Engineering Lead / IR Team Lead    |
| Approved By    | MSSP CISO                                         |
| Classification | Confidential – MSSP Internal                      |
| Review Cycle   | Annually (or upon purple team methodology change) |

---

# 2. Purpose

This document defines the standardized **Purple Team Exercise Guide** governing how the MSSP plans, executes, evaluates, and improves collaborative red-and-blue exercises designed to systematically improve detection coverage, response capability, and analyst skills across multi-tenant environments — providing structured methodology for high-value, controlled adversary emulation where red and blue teams work together openly.

A formal Purple Team Exercise Guide is critical because:

- purple team exercises produce the highest detection-improvement value per exercise hour
- unlike red team (adversarial), purple team is collaborative and openly transparent
- purple team exercises systematically validate detection coverage against MITRE ATT&CK
- detection engineering depends on structured purple team feedback loops
- new playbooks and detection rules require validation before live deployment
- new SOC analysts benefit from observing live attack execution and detection
- multi-tenant MSSPs must validate detection consistency across tenants
- ISO 27001 A.5.7 (testing) and NIST CSF DE.DP (detection process testing) require structured testing
- RBI Cyber Security Framework and BFSI clients expect demonstrable detection validation
- without structured guide, purple team becomes inconsistent ad-hoc exercises with weak improvement output
- without methodology, purple team findings are not systematically tracked to closure
- this guide is the operational backbone for the MSSP purple team program
- purple team is essential bridge between red team (adversarial) and tabletop (discussion)
- regulatory audits increasingly expect purple team evidence

This guide ensures:

- consistent purple team methodology across all exercises
- structured scenario design based on MITRE ATT&CK
- collaborative execution with red and blue teams in same room (physical or virtual)
- detection coverage matrix tracking
- real-time iterative tuning during exercise
- multi-tenant safety controls
- post-exercise detection engineering improvement
- analyst skill development through observation
- audit-ready records linking purple team to detection maturity
- linkage to red team SOP, drill program, and detection improvement tracking

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 3. Scope

This guide applies to all MSSP purple team exercises:

| Scope Element                                       | Coverage                 |
| --------------------------------------------------- | ------------------------ |
| MSSP-internal purple team exercises                 | Full scope               |
| Third-party red team + MSSP blue team collaboration | Per engagement           |
| Client-authorized purple team in client environment | With client coordination |
| MITRE ATT&CK technique validation exercises         | Standard                 |
| New detection rule validation                       | Standard                 |
| New playbook validation                             | Standard                 |
| New analyst training exercises                      | Standard                 |
| Continuous purple team (CPT)                        | Quarterly+               |
| Compliance-driven purple team                       | RBI/ISO/NIST evidence    |

Out of scope:

- Discussion-based tabletop exercises (covered by `10.2_Tabletop-Exercises/`)
- Adversarial red team exercises (covered by `Red-Team-IR-Integration-SOP.md`)
- Vulnerability scanning (covered by Vuln Mgmt program)
- Routine pen-testing (covered by Pen-Test SOP)
- Bug bounty (covered by separate program)

---

# 4. Definitions

| Term                  | Definition                                                      |
| --------------------- | --------------------------------------------------------------- |
| Purple Team           | Collaborative exercise between red (offense) and blue (defense) |
| Red Team              | Offensive team executing TTPs                                   |
| Blue Team             | Defensive team (SOC + IR Team)                                  |
| White Team            | Exercise control / facilitators                                 |
| Detection Coverage    | % of TTPs detected by current rules                             |
| Detection Engineering | Discipline of creating/tuning detection rules                   |
| MITRE ATT&CK          | Framework of adversary tactics, techniques, procedures          |
| TTP                   | Tactic, Technique, Procedure                                    |
| Atomic Test           | Single TTP execution (e.g., Atomic Red Team)                    |
| Iterative Tuning      | Real-time detection rule adjustment during exercise             |
| Detection Gap         | TTP not detected by current rules                               |
| Coverage Matrix       | Tracking detection vs MITRE ATT&CK techniques                   |
| Coverage Heatmap      | Visual representation of coverage matrix                        |
| BAS                   | Breach and Attack Simulation (automated purple team)            |
| CPT                   | Continuous Purple Team                                          |
| Round Trip Time       | Detect → Triage → Investigate → Contain duration                |

---

# 5. Roles and Responsibilities

| Role                                | Responsibilities                                           |
| ----------------------------------- | ---------------------------------------------------------- |
| **MSSP CISO**                       | Approve purple team scope; review outcomes                 |
| **MSSP Detection Engineering Lead** | Program ownership; detection gap closure; iterative tuning |
| **MSSP IR Team Lead**               | Blue team coordination; playbook validation                |
| **MSSP SOC Manager**                | Blue team participation; analyst training value            |
| **MSSP Threat Intel Lead**          | TTP selection per threat landscape                         |
| **MSSP Compliance Lead**            | Audit evidence; multi-tenant safety                        |
| **Red Team Lead**                   | TTP execution; scenario realism                            |
| **Red Team Operators**              | Execute TTPs per plan                                      |
| **Blue Team (L1/L2/L3/IR)**         | Detect, triage, investigate, respond                       |
| **White Team / Facilitator**        | Manage exercise pace; document                             |
| **Per-Client SDM**                  | Client coordination (client environment)                   |
| **Detection Engineers**             | Tune rules in real-time; track gaps                        |
| **Scribe**                          | Capture coverage matrix + timeline                         |

---

# 6. Purple Team Principles (Mandatory)

| Principle                          | Requirement                                    |
| ---------------------------------- | ---------------------------------------------- |
| **Collaborative, Not Adversarial** | Red and blue teams work together openly        |
| **Detection-First Focus**          | Primary goal is detection improvement          |
| **MITRE ATT&CK Aligned**           | All TTPs mapped to ATT&CK                      |
| **Iterative Tuning**               | Real-time rule adjustment when TTP missed      |
| **Coverage Matrix Tracking**       | Every TTP scored: detected/missed/late         |
| **Transparency**                   | Red shows TTPs; blue shows alerts in real-time |
| **Multi-Tenant Safety**            | Strict tenant scope enforcement                |
| **Audit-Ready Records**            | All TTPs, detections, tunings logged           |
| **No Surprise**                    | All participants know exercise is occurring    |
| **Knowledge Transfer**             | Junior analysts observe + learn                |
| **Improvement-Driven**             | Every gap → tracked improvement action         |
| **Continuous Cycle**               | Quarterly+ frequency                           |

---

# 7. Purple Team Exercise Types (Mandatory)

## 7.1 By Scope

| Type                            | Description                                                    | Duration        |
| ------------------------------- | -------------------------------------------------------------- | --------------- |
| **Single-Technique Validation** | Validate detection for 1 TTP                                   | 1-2 hours       |
| **Multi-Technique Chain**       | Validate full attack chain (e.g., initial access → C2 → recon) | Half day        |
| **Adversary Emulation**         | Emulate specific actor (e.g., APT29) end-to-end                | Full day        |
| **Continuous Purple (CPT)**     | Ongoing scheduled exercises                                    | Continuous      |
| **Compliance Purple**           | Coverage validation for audit                                  | Per audit cycle |

## 7.2 By Audience

| Type                        | Audience                                 |
| --------------------------- | ---------------------------------------- |
| **Tactical Purple**         | L1/L2 with detection eng                 |
| **Operational Purple**      | L2/L3 + IR Team                          |
| **Strategic Purple**        | Executive briefing on coverage state     |
| **Cross-Functional Purple** | All tiers + threat intel + detection eng |

## 7.3 By Frequency

| Type                | Cadence                           |
| ------------------- | --------------------------------- |
| Quarterly mandatory | Each major TTP category           |
| Monthly focused     | Specific technique cluster        |
| Continuous (BAS)    | Daily/weekly automated            |
| Pre-deployment      | Before new playbook/tool launch   |
| Post-incident       | Validate fixes from real incident |

---

# 8. Purple Team Lifecycle (Mandatory)

┌──────────────────────────────────────────────────────────┐
│ Phase 1: PLAN │
│ Objectives, TTP selection, scope │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 2: DESIGN │
│ Scenario, coverage matrix, tools │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 3: PREPARE │
│ Lab setup, participants, communication │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 4: EXECUTE │
│ Run TTPs; capture detections; iterate │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 5: ITERATE │
│ Real-time rule tuning; re-test │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 6: EVALUATE │
│ Final coverage matrix; gaps identified │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 7: AFTER-ACTION │
│ AAR; detection improvements; playbook updates │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 8: TRACK │
│ Action items closure; next exercise scheduled │
└──────────────────────────────────────────────────────────┘

---

# 9. Phase 1: Plan (Mandatory)

## 9.1 Define Objectives

Each purple team exercise must have 3-5 measurable objectives:

| Objective Category | Example                                           |
| ------------------ | ------------------------------------------------- |
| **Coverage**       | Validate detection for 15 MITRE ATT&CK techniques |
| **Tuning**         | Reduce FP rate for 5 noisy rules                  |
| **New Detection**  | Validate new detection rules pre-production       |
| **Playbook**       | Validate new playbook end-to-end                  |
| **Training**       | Onboard 3 new L2 analysts to TTP recognition      |
| **Multi-Tenant**   | Validate detection consistency across tenants     |

## 9.2 TTP Selection Sources

| Source                             | Use Case                      |
| ---------------------------------- | ----------------------------- |
| MITRE ATT&CK current coverage gaps | Close known blind spots       |
| Recent threat intelligence         | Test against current actors   |
| Industry-specific TTPs             | Tailored per client portfolio |
| Atomic Red Team library            | Standard reusable TTPs        |
| Prior red team findings            | Validate fixes                |
| Client environment-specific TTPs   | Per assigned tenant           |

## 9.3 Define Participants

| Role                       | Required         |
| -------------------------- | ---------------- |
| Red Team operator(s)       | Yes              |
| Detection Engineering Lead | Yes              |
| Detection Engineers        | Yes (for tuning) |
| L1 Analyst                 | Yes (learning)   |
| L2 Analyst                 | Yes (active)     |
| L3 Analyst                 | Yes (active)     |
| IR Team member             | Recommended      |
| SOC Lead                   | Yes              |
| Threat Intel Lead          | Recommended      |
| Scribe / Facilitator       | Yes              |

---

# 10. Phase 2: Design (Mandatory)

## 10.1 Scenario Document

| Element                    | Content                                    |
| -------------------------- | ------------------------------------------ |
| Scenario name              | Descriptive title                          |
| MITRE ATT&CK techniques    | List with sub-techniques                   |
| Attack chain sequence      | Initial → C2 → Recon → Lateral → Objective |
| Tools/payloads             | Specific tools to be used                  |
| Expected detection sources | SIEM, EDR, NDR, etc.                       |
| Expected blue team actions | Per playbook                               |
| Iteration plan             | Order of TTPs                              |

## 10.2 Coverage Matrix Template

| Technique ID | Technique Name            | Tactic         | Tool          | Expected Source | Detected? | Detection Time | FP Rate | Notes |
| ------------ | ------------------------- | -------------- | ------------- | --------------- | --------- | -------------- | ------- | ----- |
| T1059.001    | PowerShell                | Execution      | Cobalt Strike | EDR             | TBD       | TBD            | TBD     |       |
| T1078        | Valid Accounts            | Initial Access | Manual        | SIEM IdP        | TBD       | TBD            | TBD     |       |
| T1486        | Data Encrypted for Impact | Impact         | Custom        | EDR + DLP       | TBD       | TBD            | TBD     |       |

## 10.3 Iteration Strategy

| Approach                   | Use                             |
| -------------------------- | ------------------------------- |
| Sequential by attack chain | Most common                     |
| Sequential by tactic       | Test full tactic coverage       |
| Random                     | Test detection unpredictability |
| Stratified                 | Mix of known + new TTPs         |

---

# 11. Phase 3: Prepare (Mandatory)

## 11.1 Lab Setup

| Element                            | Requirement                     |
| ---------------------------------- | ------------------------------- |
| Isolated tenant or lab environment | Mandatory for production safety |
| Tools deployed                     | Red team toolchain ready        |
| Detection rules in baseline state  | Documented                      |
| Communication channel              | Shared room / virtual war room  |
| Display screens                    | Real-time SIEM + EDR views      |
| Coverage matrix display            | Live updated                    |

## 11.2 Multi-Tenant Safety Controls

| Control                                   | Requirement        |
| ----------------------------------------- | ------------------ |
| Exercise tenant scope verified            | Mandatory          |
| Tenant spillover prevention               | Pre-validated      |
| Other tenants' detection rules unaffected | Verified           |
| Red team payloads tagged                  | Unique exercise ID |

## 11.3 Participant Pre-Briefing

| Topic                  | Coverage               |
| ---------------------- | ---------------------- |
| Exercise objectives    | All participants       |
| Scenario overview      | All participants       |
| Roles and expectations | Per role               |
| Communication channels | Out-of-band for issues |
| Hot stop protocol      | All participants       |

---

# 12. Phase 4: Execute (Mandatory)

## 12.1 Standard Execution Agenda

| Time      | Activity                                     |
| --------- | -------------------------------------------- |
| 0:00-0:15 | Welcome, objectives recap, ground rules      |
| 0:15-0:30 | Baseline coverage matrix review              |
| 0:30-3:00 | Iterative TTP execution + detection tracking |
| 3:00-3:15 | Break                                        |
| 3:15-4:00 | Continued execution                          |
| 4:00-4:30 | Final coverage matrix review                 |
| 4:30-5:30 | Hot wash + immediate findings                |

## 12.2 Per-TTP Execution Pattern

For each TTP:

Red team announces: "About to execute T1059.001 (PowerShell encoded command)"
Red team executes TTP
Blue team observes detection (or absence)
Detection time recorded
Detection accuracy assessed (true positive / false positive)
Coverage matrix updated
If detected → review detection quality
If missed → flag for detection engineering
Move to next TTP

---

## 12.3 Real-Time Documentation

| Capture                       | Owner         |
| ----------------------------- | ------------- |
| TTP execution timeline        | Red team      |
| Detection event timeline      | Blue team     |
| Coverage matrix entries       | Scribe        |
| Tuning suggestions            | Detection eng |
| Playbook gaps observed        | IR Team       |
| Quotes / notable observations | Scribe        |

---

# 13. Phase 5: Iterate (Mandatory)

## 13.1 Real-Time Detection Tuning

When a TTP is missed:

| Step | Action                                 | Owner         |
| ---- | -------------------------------------- | ------------- |
| 1    | TTP missed flagged                     | Blue team     |
| 2    | Root cause discussion                  | Detection eng |
| 3    | Quick rule fix attempted (if feasible) | Detection eng |
| 4    | Rule deployed in test mode             | Detection eng |
| 5    | TTP re-executed                        | Red team      |
| 6    | Detection validated                    | Blue team     |
| 7    | Coverage matrix updated                | Scribe        |
| 8    | Rule queued for production deployment  | Detection eng |

## 13.2 When NOT to Tune in Real-Time

| Situation                              | Action                              |
| -------------------------------------- | ----------------------------------- |
| Complex rule requiring days to develop | Log as action item; don't tune live |
| Rule affects multiple tenants          | Defer to controlled deployment      |
| FP risk requires testing               | Defer to test environment           |
| Rule requires new data source          | Log requirement; don't tune live    |

## 13.3 Iteration Discipline

| Discipline                      | Detail                |
| ------------------------------- | --------------------- |
| Maximum 3 iterations per TTP    | Avoid scope creep     |
| Time-box iterations             | 15-30 min max each    |
| Document all iteration attempts | For learning          |
| Failed iterations also valuable | Track as action items |

---

# 14. Phase 6: Evaluate (Mandatory)

## 14.1 Final Coverage Matrix

After exercise, compile:

| Metric                                 | Value |
| -------------------------------------- | ----- |
| Total TTPs executed                    |       |
| TTPs detected at baseline              |       |
| TTPs missed at baseline                |       |
| TTPs detected after iteration          |       |
| Detection coverage % (baseline)        |       |
| Detection coverage % (after iteration) |       |
| Average detection time                 |       |
| Average FP rate                        |       |

## 14.2 Coverage Heatmap

Visual representation per MITRE ATT&CK tactic:

| Tactic               | Coverage % | Color            |
| -------------------- | ---------- | ---------------- |
| Initial Access       | _____      | Green/Yellow/Red |
| Execution            | _____      | Green/Yellow/Red |
| Persistence          | _____      | Green/Yellow/Red |
| Privilege Escalation | _____      | Green/Yellow/Red |
| Defense Evasion      | _____      | Green/Yellow/Red |
| Credential Access    | _____      | Green/Yellow/Red |
| Discovery            | _____      | Green/Yellow/Red |
| Lateral Movement     | _____      | Green/Yellow/Red |
| Collection           | _____      | Green/Yellow/Red |
| Command and Control  | _____      | Green/Yellow/Red |
| Exfiltration         | _____      | Green/Yellow/Red |
| Impact               | _____      | Green/Yellow/Red |

**Color coding:**

- Green: ≥80% coverage
- Yellow: 50-79% coverage
- Red: <50% coverage

## 14.3 Gap Categorization

| Gap Type                      | Examples                              |
| ----------------------------- | ------------------------------------- |
| **Detection rule missing**    | No rule exists for TTP                |
| **Detection rule too narrow** | Rule misses variations                |
| **Detection rule too noisy**  | Generates excessive FPs               |
| **Data source missing**       | No telemetry to detect                |
| **Tool integration gap**      | Tool data not in SIEM                 |
| **Tuning needed**             | Rule needs threshold/scope adjustment |
| **Response playbook gap**     | Detected but no clear response        |

---

# 15. Phase 7: After-Action (Mandatory)

## 15.1 AAR Components

Per `Drill-After-Action-Report.md`:

| Section                                   | Content                               |
| ----------------------------------------- | ------------------------------------- |
| Executive summary                         | Exercise overview + headline coverage |
| Objectives status                         | Met / partial / not met               |
| Coverage matrix (final)                   | All TTPs with detection state         |
| Coverage heatmap                          | Visual representation                 |
| Strengths                                 | What detection worked well            |
| Gaps                                      | TTPs not detected                     |
| Iterative tuning summary                  | Real-time fixes applied               |
| Detection improvements (production-ready) | Rules to deploy                       |
| Detection improvements (development)      | Rules requiring work                  |
| Playbook gaps                             | Response process improvements         |
| Training gaps                             | Skill development needs               |
| Action items                              | Owner + due date                      |
| Lessons learned                           | Generalized takeaways                 |

## 15.2 Detection Engineering Output

Every gap → tracked in `Detection-Improvement-Log.md`:

| Field                     | Required                    |
| ------------------------- | --------------------------- |
| MITRE ATT&CK technique ID | Yes                         |
| Gap description           | Yes                         |
| Tool/data source needed   | Yes                         |
| Recommended rule          | Yes (if known)              |
| Priority                  | Yes (P1/P2/P3)              |
| Owner                     | Yes (Detection Engineer)    |
| Due date                  | Yes                         |
| Status                    | Open / In Progress / Closed |

## 15.3 Playbook Update Output

Every playbook gap → tracked in `Playbook-Update-Log.md`:

| Field              | Required           |
| ------------------ | ------------------ |
| Playbook affected  | Yes                |
| Gap description    | Yes                |
| Recommended update | Yes                |
| Owner              | Yes (IR Team Lead) |
| Due date           | Yes                |

---

# 16. Phase 8: Track (Mandatory)

## 16.1 Action Item Tracking

All action items entered in:

- `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

## 16.2 Closure Verification

| Activity                                     | Owner                     |
| -------------------------------------------- | ------------------------- |
| Detection rule deployed to production        | Detection Engineer        |
| Detection rule validated in next purple team | Detection Eng + Blue team |
| Playbook update published                    | IR Team Lead              |
| Action item closure documented               | Compliance Lead           |

## 16.3 Next Exercise Planning

| Activity                      | Cadence           |
| ----------------------------- | ----------------- |
| Next purple team scheduled    | Quarterly minimum |
| Re-test of closed gaps        | Within 2 quarters |
| Coverage matrix trend tracked | Quarterly         |

---

# 17. Continuous Purple Team / BAS (Mandatory)

## 17.1 BAS Integration

| Element                  | Detail                  |
| ------------------------ | ----------------------- |
| BAS tool deployment      | Per tenant              |
| BAS schedule             | Daily / weekly          |
| BAS payload library      | Maintained              |
| BAS coverage matrix feed | Automatic               |
| BAS results review       | Weekly by Detection Eng |
| BAS escalation criteria  | New gap → action item   |

## 17.2 BAS vs Manual Purple

| Aspect               | BAS                  | Manual Purple        |
| -------------------- | -------------------- | -------------------- |
| Frequency            | Continuous           | Quarterly+           |
| TTP coverage         | Broad library        | Selected focus       |
| Iteration capability | Limited              | High                 |
| Training value       | Low                  | High                 |
| Setup cost           | High (initial)       | Per exercise         |
| Best for             | Coverage maintenance | Coverage improvement |

---

# 18. Multi-Tenant Considerations (Mandatory)

| Aspect                                        | Requirement           |
| --------------------------------------------- | --------------------- |
| Single-tenant exercise scope                  | Mandatory             |
| Exercise lab environment preferred            | Where possible        |
| Production tenant exercise: pre-validation    | Mandatory             |
| Tenant spillover prevention                   | Pre-validated         |
| Detection rules tested in isolation           | Where possible        |
| Sanitized findings shared across portfolio    | Per portfolio defense |
| No cross-tenant data exposure                 | Strict                |
| Per-client authorization (client environment) | Mandatory             |
| Multi-tenant coverage consistency tracked     | Quarterly             |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 19. Quality Checklist (Per Purple Team Exercise)

Before declaring exercise complete:

- [ ] Objectives defined and shared
- [ ] TTP list approved by Detection Eng Lead + IR Team Lead
- [ ] Multi-tenant safety controls verified
- [ ] Lab/exercise environment ready
- [ ] All participants briefed
- [ ] Coverage matrix prepared
- [ ] Execution per agenda
- [ ] Real-time documentation maintained
- [ ] Iterative tuning attempted where feasible
- [ ] Final coverage matrix complete
- [ ] Coverage heatmap generated
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Detection improvements logged
- [ ] Playbook updates logged
- [ ] Action items in tracker
- [ ] Records archived per retention policy

---

# 20. Records Retention

| Record                         | Retention               |
| ------------------------------ | ----------------------- |
| Scenario document              | 7 years                 |
| Coverage matrix (per exercise) | 7 years                 |
| Coverage heatmap               | 7 years                 |
| Iteration log                  | 5 years                 |
| AAR                            | 7 years                 |
| Detection feedback records     | Until closure + 3 years |
| Sign-in sheet                  | 3 years                 |

---

# 21. Annual Purple Team Calendar (Mandatory)

| Quarter | Purple Team Focus                                        |
| ------- | -------------------------------------------------------- |
| Q1      | Initial Access + Execution + Persistence tactics         |
| Q2      | Defense Evasion + Credential Access + Discovery          |
| Q3      | Lateral Movement + Collection + C2                       |
| Q4      | Exfiltration + Impact + Adversary emulation (full chain) |

| Continuous | BAS running daily/weekly |

---

# 22. Integration with Other Processes

| Process                        | Integration                           |
| ------------------------------ | ------------------------------------- |
| Red Team IR Integration SOP    | Complementary adversarial model       |
| Drill Schedule Annual          | Purple team in annual schedule        |
| Drill After-Action Report      | AAR template                          |
| Tabletop Exercise Guide        | Discussion-based complement           |
| Detection Improvement Log      | Purple team findings tracked          |
| Playbook Update Log            | Playbook gaps tracked                 |
| Control Gap Tracker            | Control gaps tracked                  |
| Security Improvement Register  | Improvements tracked                  |
| L1/L2/L3/IR Team Onboarding    | Purple team participation requirement |
| ISO 27001 / NIST CSF Audits    | Purple team evidence                  |
| MITRE ATT&CK Quick Reference   | TTP reference                         |
| Attack Technique Reference     | Technique deep-dives                  |
| Client Data Segregation Policy | Enforced throughout                   |

---

# 23. Related Documents

| Document                       | Path                                                                              |
| ------------------------------ | --------------------------------------------------------------------------------- |
| Red Team IR Integration SOP    | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`            |
| Drill Schedule Annual          | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`                  |
| Drill After-Action Report      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`              |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`    |
| TTX Evaluation Scorecard       | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`   |
| MITRE ATT&CK Quick Reference   | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`   |
| Attack Technique Reference     | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`     |
| Tool Command Reference         | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`         |
| Common IoC Reference           | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`           |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`         |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`               |
| Control Gap Tracker            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`             |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`   |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                 |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`               |
| SIEM Alert Tuning Guide        | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`                    |
| SIEM Use Cases Master          | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`                      |
| EDR Alert Handling Guide       | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md`                    |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| L1 Onboarding Program          | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`              |
| L2 Onboarding Program          | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`              |
| L3 Onboarding Program          | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`              |
| IR Team Onboarding Program     | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/IR-Team-Onboarding-Program.md`         |

---

# 24. Revision History

| Version | Date        | Author                                         | Changes         |
| ------- | ----------- | ---------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP Detection Engineering Lead / IR Team Lead | Initial version |

---

# 25. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP IR Team Lead               |      |           |      |
| MSSP SOC Manager                |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**
