# Red Team – IR Integration SOP

---

# 1. Document Control

| Field          | Value                                          |
| -------------- | ---------------------------------------------- |
| Document Name  | Red Team – IR Integration SOP                  |
| Document ID    | MSSP-TRN-DRL-001                               |
| Version        | 1.0                                            |
| Effective Date | 30-May-2026                                    |
| Owner          | MSSP IR Team Lead / Detection Engineering Lead |
| Approved By    | MSSP CISO                                      |
| Classification | Confidential – MSSP Internal                   |
| Review Cycle   | Annually (or upon red team program change)     |

---

# 2. Purpose

This document defines the standardized **Red Team – Incident Response (IR) Integration SOP** governing how red team operations are safely integrated with MSSP SOC and IR Team operations across multi-tenant environments — ensuring red team exercises produce meaningful detection improvement, IR validation, and SOC training value without operational disruption, evidence contamination, false-positive cascades, or tenant segregation breaches.

A formal Red Team – IR Integration SOP is critical because:

- red team exercises that surprise the SOC produce realistic detection metrics but risk operational chaos
- red team exercises that fully pre-brief the SOC produce sanitized detection metrics but reduce realism
- balanced "selective brief" approaches require structured protocols to be effective and safe
- without integration discipline, red team activity is misclassified as real incidents — wasting SOC effort
- red team activity in multi-tenant environments can affect other clients if scope leaks
- evidence contamination during red team operations can compromise real incident investigations running in parallel
- false-positive alert cascades from red team can mask real attacker activity
- per-client red team exercises require strict tenant segregation and authorization
- ISO 27001 A.5.7 (threat intelligence + testing), NIST CSF DE.DP (detection processes), RBI CSF require structured testing
- regulatory frameworks expect demonstrable detection capability validation
- SOC analyst training value depends on structured de-briefing and feedback loops
- detection engineering gains require structured red team finding capture
- without SOP, red team value is lost to inconsistent execution and weak post-exercise improvement
- this SOP is the foundation for the MSSP red team program

This SOP ensures:

- defined authorization and scoping for all red team activities
- structured "white card" protocols for incident declaration during exercises
- selective SOC briefing models (white box / grey box / black box)
- multi-tenant safety controls preventing scope leakage
- evidence integrity preservation
- false-positive cascade prevention
- structured detection engineering feedback from red team findings
- IR Team observation and learning from red team activities
- post-exercise lessons learned and detection improvement
- audit-ready records linking red team operations to detection maturity
- linkage to purple team exercises and drill program

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 3. Scope

This SOP applies to all red team activities involving MSSP SOC/IR Team operations:

| Scope Element                                | Coverage                |
| -------------------------------------------- | ----------------------- |
| MSSP internal red team (if applicable)       | Full scope              |
| Third-party red team engagements             | Per scope of engagement |
| Client-authorized red team against client    | With MSSP visibility    |
| Client-authorized red team against MSSP      | Per scope               |
| Penetration testing with active exploitation | Per scope               |
| Adversary emulation exercises                | Per scope               |
| Continuous automated red teaming (BAS/CART)  | Per scope               |
| Phishing simulations (active payloads)       | Per scope               |
| Physical red team (where applicable)         | Per scope               |
| Social engineering red team                  | Per scope               |

Out of scope:

- Discussion-based tabletop exercises (covered by `10.2_Tabletop-Exercises/`)
- Purple team exercises (covered by `Purple-Team-Exercise-Guide.md` — referenced here)
- Vulnerability scanning without exploitation (covered by Vuln Mgmt program)
- Bug bounty programs (covered by separate program)
- Compliance audits (covered by `09.4_MSSP-Compliance/`)
- Routine pen-tests without IR engagement (covered by Pen-Test SOP)

---

# 4. Definitions

| Term                      | Definition                                             |
| ------------------------- | ------------------------------------------------------ |
| Red Team                  | Authorized offensive testing simulating real adversary |
| Blue Team                 | Defensive team (SOC + IR Team)                         |
| Purple Team               | Collaborative red+blue exercise                        |
| White Cell / White Team   | Exercise control team (not playing)                    |
| White Card                | Out-of-band notification of red team activity          |
| Black Box                 | Blue team has NO prior knowledge                       |
| Grey Box                  | Blue team has partial knowledge                        |
| White Box                 | Blue team has full prior knowledge                     |
| Rules of Engagement (RoE) | Authorized scope, methods, timing                      |
| Trusted Agent             | Pre-briefed blue team member coordinating              |
| Get-Out-of-Jail Letter    | Authorization letter for red team                      |
| BAS                       | Breach and Attack Simulation (automated)               |
| CART                      | Continuous Automated Red Team                          |
| C2                        | Command and Control                                    |
| TTP                       | Tactics, Techniques, Procedures                        |
| Engagement Window         | Authorized time period for red team activity           |
| Hot Stop                  | Immediate cessation of red team activity               |
| Exercise Control          | White team authority to manage exercise                |

---

# 5. Roles and Responsibilities

| Role                                | Responsibilities                                              |
| ----------------------------------- | ------------------------------------------------------------- |
| **MSSP CISO**                       | Approve red team engagements; final authority on scope/timing |
| **MSSP IR Team Lead**               | Trusted agent for SOC; coordinate exercise control            |
| **MSSP SOC Manager**                | SOC operational continuity during exercise                    |
| **MSSP Detection Engineering Lead** | Detection feedback ownership; rule tuning post-exercise       |
| **MSSP Threat Intel Lead**          | TTP context; attribution realism                              |
| **MSSP Compliance Lead**            | Authorization documentation; audit-readiness                  |
| **MSSP Legal Counsel**              | RoE legal review; client agreement validation                 |
| **Red Team Lead**                   | Conduct red team operations per RoE; report findings          |
| **Red Team Operators**              | Execute red team actions; document evidence                   |
| **White Team / Exercise Control**   | Manage exercise; issue white cards; hot stop authority        |
| **Trusted Agents (in SOC)**         | Selectively know about exercise; do not influence blue team   |
| **SOC Analysts (Blue Team)**        | Respond to alerts authentically (per knowledge level)         |
| **Per-Client SDM**                  | Client coordination if client environment involved            |
| **Client CISO**                     | Authorize red team against client (when applicable)           |

---

# 6. Red Team Integration Principles (Mandatory)

| Principle                          | Requirement                                                             |
| ---------------------------------- | ----------------------------------------------------------------------- |
| **Authorization First**            | No red team activity without written CISO + scope approval              |
| **Scope Discipline**               | Strict adherence to RoE; out-of-scope = hot stop                        |
| **Multi-Tenant Safety**            | Red team scope cannot affect other clients                              |
| **Trusted Agent Protocol**         | Selective pre-briefing; trusted agents never influence blue team        |
| **White Card Discipline**          | Real incidents during exercise distinguished from red team activity     |
| **Evidence Integrity**             | Red team artifacts clearly distinguishable from real attacker artifacts |
| **No Real Damage**                 | No destructive actions; data exfiltration simulated only                |
| **Engagement Window**              | Activity only within authorized time window                             |
| **Hot Stop Authority**             | White team can stop exercise at any time                                |
| **Post-Exercise Disclosure**       | Full disclosure to blue team after exercise                             |
| **Detection Engineering Feedback** | Every red team TTP feeds detection improvement                          |
| **Audit-Ready Records**            | All actions logged, timestamped, attributable                           |

---

# 7. Red Team Exercise Models (Mandatory)

## 7.1 Black Box

| Attribute           | Detail                            |
| ------------------- | --------------------------------- |
| Blue team knowledge | None                              |
| Detection realism   | Maximum                           |
| Operational risk    | High (false-positive cascade)     |
| White cards needed  | Critical (real incident handling) |
| Trusted agents      | Minimum (IR Team Lead + CISO)     |
| Best for            | Mature SOC; quarterly maximum     |

## 7.2 Grey Box

| Attribute           | Detail                                             |
| ------------------- | -------------------------------------------------- |
| Blue team knowledge | Aware exercise will occur in window; not specifics |
| Detection realism   | High                                               |
| Operational risk    | Medium                                             |
| White cards needed  | High                                               |
| Trusted agents      | IR Team Lead + SOC Manager + CISO                  |
| Best for            | Standard model; monthly to quarterly               |

## 7.3 White Box

| Attribute           | Detail                             |
| ------------------- | ---------------------------------- |
| Blue team knowledge | Full (essentially purple team)     |
| Detection realism   | Lower                              |
| Operational risk    | Low                                |
| White cards needed  | Low                                |
| Trusted agents      | All SOC management                 |
| Best for            | New detection validation; training |

## 7.4 Selection Matrix

| Use Case                   | Recommended Model                |
| -------------------------- | -------------------------------- |
| Annual maturity assessment | Black Box (with safety controls) |
| New playbook validation    | Grey Box                         |
| Detection rule tuning      | White Box                        |
| New analyst training       | White Box                        |
| Compliance evidence        | Grey Box                         |
| Continuous automated (BAS) | Grey Box                         |

---

# 8. Red Team Lifecycle (Mandatory)

┌──────────────────────────────────────────────────────────┐
│ Phase 1: PROPOSAL & AUTHORIZATION │
│ Scope, RoE, approvals │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 2: PLANNING & SCENARIO DEVELOPMENT │
│ TTPs, timeline, success criteria │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 3: PRE-EXERCISE PREPARATION │
│ Trusted agent briefings, white cards, evidence tagging │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 4: EXECUTION │
│ Red team activity per RoE; white team monitors │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 5: REAL INCIDENT HANDLING (PARALLEL) │
│ White cards differentiate real vs exercise │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 6: EXERCISE CONCLUSION │
│ Hot stop or natural conclusion │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 7: HOT WASH & DISCLOSURE │
│ Reveal exercise to blue team; immediate debrief │
└──────────────────────────────────────────────────────────┘
│
▼
┌──────────────────────────────────────────────────────────┐
│ Phase 8: AFTER-ACTION & IMPROVEMENT │
│ Detection feedback; playbook updates; AAR │
└──────────────────────────────────────────────────────────┘

---

# 9. Phase 1: Proposal & Authorization (Mandatory)

## 9.1 Proposal Document

Every red team engagement requires written proposal containing:

| Element                                  | Required              |
| ---------------------------------------- | --------------------- |
| Engagement objectives                    | Yes                   |
| Target environment                       | Yes (specific tenant) |
| Out-of-scope systems                     | Yes                   |
| Authorized TTPs                          | Yes                   |
| Prohibited TTPs (e.g., DoS, destruction) | Yes                   |
| Engagement window (dates/times)          | Yes                   |
| White team composition                   | Yes                   |
| Trusted agent list                       | Yes                   |
| Communication protocols                  | Yes                   |
| Hot stop conditions                      | Yes                   |
| Evidence handling                        | Yes                   |
| Reporting timeline                       | Yes                   |
| Get-out-of-jail letter                   | Yes                   |

## 9.2 Authorization Chain

| Approval                       | Required For                |
| ------------------------------ | --------------------------- |
| MSSP CISO                      | All red team engagements    |
| MSSP Legal Counsel             | RoE legal review            |
| MSSP Compliance Lead           | Authorization documentation |
| Client CISO (in writing)       | Client environment red team |
| Client Legal (in writing)      | Client environment red team |
| Per-Client SDM acknowledgement | Client environment red team |

## 9.3 Get-Out-of-Jail Letter

| Element                                         | Required                  |
| ----------------------------------------------- | ------------------------- |
| Authorized red team personnel names             | Yes                       |
| Engagement window                               | Yes                       |
| Authorized actions                              | Yes                       |
| Authorized targets                              | Yes                       |
| Authorized contact for verification             | Yes (CISO + IR Team Lead) |
| Signed by CISO + (if client) Client CISO        | Yes                       |
| Carried by red team operators during engagement | Yes                       |

---

# 10. Phase 2: Planning & Scenario Development (Mandatory)

## 10.1 TTP Selection

| Source                           | Use                       |
| -------------------------------- | ------------------------- |
| MITRE ATT&CK framework           | Primary TTP source        |
| Recent threat intelligence       | Realistic actor emulation |
| Known client environment threats | Targeted relevance        |
| Detection gap hypothesis         | Test specific blind spots |
| Prior red team findings          | Validate fixes            |

## 10.2 Scenario Document

| Element                   | Content                                           |
| ------------------------- | ------------------------------------------------- |
| Adversary persona         | Realistic actor profile                           |
| Attack chain              | Initial access → C2 → recon → lateral → objective |
| Success criteria          | What "win" looks like for red team                |
| Detection opportunities   | Expected blue team alerts                         |
| Containment opportunities | Expected blue team responses                      |
| Pivot points              | Where scenario can branch                         |

## 10.3 Communication Plan

| Channel                                            | Use             |
| -------------------------------------------------- | --------------- |
| Out-of-band channel (e.g., dedicated Signal group) | White team only |
| White card delivery method                         | Pre-defined     |
| Hot stop signal                                    | Pre-defined     |
| Post-exercise disclosure channel                   | Pre-defined     |

---

# 11. Phase 3: Pre-Exercise Preparation (Mandatory)

## 11.1 Trusted Agent Briefings

| Agent                                 | Briefing Content                         |
| ------------------------------------- | ---------------------------------------- |
| MSSP CISO                             | Full scenario + RoE                      |
| MSSP IR Team Lead                     | Full scenario + RoE + hot stop authority |
| MSSP SOC Manager                      | Engagement window + escalation handling  |
| MSSP Compliance Lead                  | Authorization + audit recording          |
| Detection Eng Lead (selective)        | Post-exercise feedback role              |
| Per-Client SDM (if client engagement) | Client coordination                      |

## 11.2 White Card Preparation

White cards are pre-prepared notifications used during exercise to:

| Use Case                                   | White Card Content                                       |
| ------------------------------------------ | -------------------------------------------------------- |
| Real P1 incident during exercise           | "REAL INCIDENT — stand down red team activity at X"      |
| Blue team about to take destructive action | "EXERCISE — do not isolate host X"                       |
| Out-of-scope escalation                    | "EXERCISE — disregard alert from system Y"               |
| Hot stop                                   | "EXERCISE TERMINATED — all red team activity ceases NOW" |

## 11.3 Evidence Tagging Protocol

| Element                                      | Requirement                      |
| -------------------------------------------- | -------------------------------- |
| Red team artifacts include unique identifier | E.g., "RT-EXERCISE-2026-Q2"      |
| Red team C2 infrastructure documented        | IP/domain list to white team     |
| Red team tooling signed/tagged               | Where possible                   |
| Time-bounded artifacts                       | Visible within engagement window |

---

# 12. Phase 4: Execution (Mandatory)

## 12.1 Red Team Operational Rules

| Rule                                                       | Detail                                     |
| ---------------------------------------------------------- | ------------------------------------------ |
| Stay within RoE                                            | Strict                                     |
| Document every action                                      | Timestamped log                            |
| No real data exfiltration                                  | Simulate only                              |
| No destruction                                             | No data deletion, encryption, modification |
| No DoS unless explicitly authorized                        | Strict                                     |
| No social engineering of named individuals without consent | Strict                                     |
| Respect engagement window                                  | Activity only in window                    |
| Hot stop response                                          | Immediate cessation when called            |

## 12.2 White Team Monitoring

| Activity                           | Owner                     |
| ---------------------------------- | ------------------------- |
| Real-time observation of red team  | White team                |
| Real-time observation of blue team | White team                |
| Real incident triage capability    | IR Team Lead              |
| White card issuance                | White team / IR Team Lead |
| Hot stop authority                 | IR Team Lead + CISO       |

## 12.3 Multi-Tenant Safety Controls (Mandatory)

| Control                                          | Requirement           |
| ------------------------------------------------ | --------------------- |
| Tenant scope verification before each action     | Red team checks scope |
| Network controls preventing tenant spillover     | Pre-validated         |
| Detection rule scope verification                | Pre-validated         |
| Containment authority limited to exercise tenant | Pre-validated         |
| Any spillover = immediate hot stop               | Strict                |

---

# 13. Phase 5: Real Incident Handling During Exercise (Mandatory)

## 13.1 Real Incident Detection Protocol

When a real (non-exercise) incident is suspected during an active red team engagement:

| Step | Action                                                   | Owner        | Timeline            |
| ---- | -------------------------------------------------------- | ------------ | ------------------- |
| 1    | SOC analyst observes anomaly                             | L1/L2        | Standard triage     |
| 2    | Suspected indicators of real activity (not matching RoE) | L2/L3        | Standard escalation |
| 3    | Escalation to SOC Lead with "EXERCISE QUESTION" flag     | SOC Lead     | Within 15 min       |
| 4    | SOC Lead pings white team via out-of-band channel        | SOC Lead     | Within 5 min        |
| 5    | White team verifies against red team activity log        | White team   | Within 5 min        |
| 6    | White card issued: "REAL" or "EXERCISE"                  | White team   | Within 5 min        |
| 7    | If REAL → exercise paused; full IR activation            | IR Team Lead | Per standard IR     |
| 8    | If EXERCISE → analyst informed (after exercise)          | White team   | Post-exercise       |

## 13.2 Hot Stop Triggers

The exercise is immediately stopped if:

- Real incident detected
- Out-of-scope activity
- Multi-tenant spillover
- Operational risk identified
- Legal/regulatory concern raised
- Client request (if client engagement)
- CISO/IR Team Lead decision

---

# 14. Phase 6: Exercise Conclusion (Mandatory)

## 14.1 Natural Conclusion

| Action                               | Owner         |
| ------------------------------------ | ------------- |
| Red team completes scenario          | Red Team Lead |
| All artifacts inventoried            | Red Team      |
| All C2 infrastructure decommissioned | Red Team      |
| All test accounts/payloads removed   | Red Team      |
| Closure confirmation to white team   | Red Team Lead |

## 14.2 Hot Stop Conclusion

| Action                                   | Owner                  |
| ---------------------------------------- | ---------------------- |
| Immediate cessation of red team activity | All red team operators |
| Hot stop reason documented               | White team             |
| Artifacts inventoried                    | Red Team               |
| Decision on continuation later           | CISO + IR Team Lead    |

---

# 15. Phase 7: Hot Wash & Disclosure (Mandatory)

## 15.1 Immediate Post-Exercise Disclosure

| Step | Action                                | Owner         | Timeline       |
| ---- | ------------------------------------- | ------------- | -------------- |
| 1    | Red team completion confirmed         | Red Team Lead | Immediately    |
| 2    | Blue team notified: exercise complete | IR Team Lead  | Within 1 hour  |
| 3    | Blue team gathered for disclosure     | IR Team Lead  | Within 4 hours |
| 4    | Red team presents activity timeline   | Red Team Lead | At disclosure  |
| 5    | Blue team presents response timeline  | SOC Lead      | At disclosure  |
| 6    | Hot wash discussion                   | All           | At disclosure  |
| 7    | Detected vs missed TTPs identified    | Detection Eng | At disclosure  |

## 15.2 Hot Wash Agenda (60-90 min)

| Time      | Activity                       |
| --------- | ------------------------------ |
| 0-15 min  | Red team activity walkthrough  |
| 15-30 min | Blue team response walkthrough |
| 30-45 min | Detected vs missed analysis    |
| 45-60 min | Strengths + gaps discussion    |
| 60-75 min | Quick-win improvements         |
| 75-90 min | Next steps + AAR timeline      |

---

# 16. Phase 8: After-Action & Improvement (Mandatory)

## 16.1 After-Action Report (AAR)

Per `Drill-After-Action-Report.md`:

| Section               | Content                              |
| --------------------- | ------------------------------------ |
| Executive summary     | Engagement overview                  |
| Objectives + outcomes | What was tested + result             |
| Red team timeline     | Detailed TTP execution               |
| Blue team timeline    | Detection + response                 |
| Detection gaps        | TTPs not detected                    |
| Response gaps         | Detection without effective response |
| Strengths             | What worked well                     |
| Recommendations       | Detection eng + playbook + training  |
| Action items          | Owner + due date                     |

## 16.2 Detection Engineering Feedback

| Feedback Item                            | Logged In                      |
| ---------------------------------------- | ------------------------------ |
| Missed TTP → new detection rule          | `Detection-Improvement-Log.md` |
| Detected but late → tuning               | `Detection-Improvement-Log.md` |
| Detected but mis-classified → rule logic | `Detection-Improvement-Log.md` |
| Playbook gap → playbook update           | `Playbook-Update-Log.md`       |
| Control gap → control tracker            | `Control-Gap-Tracker.xlsx`     |

## 16.3 Detection Improvement Linkage

Each AAR action item that involves a detection improvement must:

- Reference specific MITRE ATT&CK technique
- Reference specific tool/data source needed
- Be tracked in `Detection-Improvement-Log.md` per Section 16.2
- Be re-tested in next red team or purple team exercise

---

# 17. Multi-Tenant Considerations (Mandatory)

| Aspect                                                 | Requirement                    |
| ------------------------------------------------------ | ------------------------------ |
| Red team scope strictly to single tenant               | Mandatory                      |
| Tenant spillover prevention controls verified          | Pre-exercise                   |
| Multi-tenant tools (SIEM/EDR/SOAR) scope verification  | Pre-exercise                   |
| Other clients' detection rules unaffected              | Verified                       |
| Findings cross-applicable to other clients (sanitized) | Per portfolio defense          |
| No cross-tenant data exposure during exercise          | Strict                         |
| Per-client authorization for red team engagement       | Mandatory (client environment) |
| Hot stop if any tenant spillover detected              | Mandatory                      |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 18. Continuous / Automated Red Team (BAS/CART) (Mandatory)

## 18.1 BAS Specific Controls

| Control                                 | Requirement                |
| --------------------------------------- | -------------------------- |
| BAS tool authorization                  | Per BAS engagement scope   |
| BAS schedule                            | Pre-published; out-of-band |
| BAS tenant scope                        | Per tenant                 |
| BAS payloads inventoried                | Maintained list            |
| BAS signature exclusions                | None — must be detected    |
| BAS results integrated to detection log | Mandatory                  |

## 18.2 CART Integration

Continuous Automated Red Team:

| Element                         | Detail                     |
| ------------------------------- | -------------------------- |
| Runs in known schedule windows  | Quarterly+                 |
| Trusted agents always informed  | SOC Manager + IR Team Lead |
| Findings fed to detection eng   | Weekly                     |
| Quarterly review of CART trends | SOC Manager                |

---

# 19. Quality Checklist (Per Red Team Engagement)

Before declaring engagement complete:

- [ ] Written authorization on file (CISO + Legal + Compliance)
- [ ] RoE signed by all parties
- [ ] Trusted agents briefed
- [ ] White cards prepared
- [ ] Multi-tenant safety controls verified
- [ ] Red team operational logs complete
- [ ] White team observation logs complete
- [ ] Hot wash conducted within 4 hours of completion
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Detection improvements logged
- [ ] Playbook updates logged
- [ ] Action items entered in tracker
- [ ] All red team artifacts decommissioned
- [ ] Records archived per retention policy

---

# 20. Records Retention

| Record                      | Retention               |
| --------------------------- | ----------------------- |
| Authorization documents     | 7 years                 |
| RoE                         | 7 years                 |
| Engagement proposal         | 7 years                 |
| Red team operational logs   | 5 years                 |
| White team observation logs | 5 years                 |
| Hot wash notes              | 3 years                 |
| AAR                         | 7 years                 |
| Detection feedback records  | Until closure + 3 years |
| Get-out-of-jail letter      | 7 years                 |

---

# 21. Annual Red Team Calendar (Mandatory)

| Quarter | Red Team Activity                               |
| ------- | ----------------------------------------------- |
| Q1      | Black Box internal SOC validation               |
| Q2      | Grey Box per-client engagement (Tier 1 client)  |
| Q3      | White Box for new playbook/detection validation |
| Q4      | Black Box maturity assessment                   |

| Continuous | BAS / CART running |

---

# 22. Integration with Other Processes

| Process                         | Integration                        |
| ------------------------------- | ---------------------------------- |
| Purple Team Exercise Guide      | Complementary collaborative model  |
| Drill Schedule Annual           | Red team in annual schedule        |
| Drill After-Action Report       | AAR template                       |
| Tabletop Exercise Guide         | Discussion-based complement        |
| Detection Improvement Log       | Red team findings tracked          |
| Playbook Update Log             | Playbook gaps tracked              |
| Control Gap Tracker             | Control gaps tracked               |
| L1/L2/L3/IR Team Onboarding     | Red team participation requirement |
| ISO 27001 / NIST CSF Audits     | Red team evidence                  |
| Client Data Segregation Policy  | Enforced throughout                |
| Cross-Client Incident Procedure | Adapted if multi-tenant scope      |

---

# 23. Related Documents

| Document                        | Path                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| Purple Team Exercise Guide      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`              |
| Drill Schedule Annual           | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-Schedule-Annual.md`                   |
| Drill After-Action Report       | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`               |
| Tabletop Exercise Guide         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`     |
| TTX Evaluation Scorecard        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`    |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| Playbook Update Log             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                |
| Control Gap Tracker             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`              |
| Security Improvement Register   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`    |
| Lessons Learned Template        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| IR Policy Master                | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                  |
| Policy Exception Register       | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`                         |
| Severity Classification Guide   | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| IRT Activation Criteria         | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`        |
| L1/L2/L3/IR Team Onboarding     | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/`                                       |
| MITRE ATT&CK Quick Reference    | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`    |
| Attack Technique Reference      | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`      |

---

# 24. Revision History

| Version | Date        | Author                                         | Changes         |
| ------- | ----------- | ---------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / Detection Engineering Lead | Initial version |

---

# 25. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP IR Team Lead               |      |           |      |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP Legal Counsel              |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**


