# Tabletop Exercise – APT (Advanced Persistent Threat) Scenario

---

# 1. Document Control

| Field                | Value                                                   |
| -------------------- | ------------------------------------------------------- |
| Document Name        | TTX – APT Campaign Scenario                             |
| Document ID          | MSSP-TRN-TTX-001                                        |
| Version              | 1.0                         |
| Effective Date       | 30-May-2026                                             |
| Owner                | MSSP IR Team Lead / Threat Intel Lead                   |
| Approved By          | MSSP CISO                                               |
| Classification       | Confidential – MSSP Internal                            |
| Review Cycle         | Annually (or upon major APT campaign update)            |
| Scenario Difficulty  | High                                                    |
| Recommended Audience | L3 + IR Team + Threat Intel + Compliance + Legal + CISO |

---

# 2. Purpose

This document defines a standardized **Advanced Persistent Threat (APT) Tabletop Exercise Scenario** designed to test the MSSP's ability to detect, investigate, contain, eradicate, and recover from a sophisticated, long-dwell, multi-stage targeted intrusion across multi-tenant environments — validating IR Team incident command, L3 forensic depth, threat intelligence integration, attribution analysis, multi-tenant CCIC coordination, regulatory engagement, executive communication, and post-incident knowledge capture.

A formal APT TTX is critical because:

- APT campaigns represent the highest-impact, hardest-to-detect threat category for regulated clients
- APT actors operate with long dwell times (often 6-18 months) requiring deep historical analysis
- APT detection requires multi-source correlation across SIEM, EDR, NDR, identity, and threat intel
- APT response requires expert coordination across L3, IR Team, Threat Intel, Compliance, and Legal
- multi-tenant MSSPs often face APT actors targeting multiple clients across an industry
- CCIC coordination must be rehearsed before real cross-client APT campaigns
- regulatory engagement (RBI, CERT-In, sector-specific) is mandatory for major APT incidents
- attribution analysis under time pressure requires practiced methodology
- legal counsel coordination on attribution and law enforcement is rarely practiced live
- executive briefings during APT campaigns must translate sophisticated TTPs to business risk
- evidence preservation for potential legal action requires expert chain of custody
- supply chain and cloud-pivot APT scenarios are increasingly common
- NIST CSF RS.AN, RS.MI, RS.CO and ISO 27001 A.5.24/A.5.26 require validated APT readiness
- without structured TTX, APT response gaps remain hidden until real incidents
- this scenario is the foundation for annual mandatory APT exercise

This scenario ensures:

- structured APT campaign simulation across detection, investigation, containment, and recovery
- multi-stage progression testing dwell-time-aware analysis
- cross-functional coordination (L3, IR Team, TI, Compliance, Legal, Executive, Per-Client SDM)
- multi-tenant CCIC activation testing
- attribution analysis methodology practice
- regulatory engagement workflow validation
- legal coordination practice
- executive communication under pressure
- post-incident threat intelligence output (sanitized) for portfolio defense
- audit-ready exercise documentation

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`
- `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

---

# 3. Scenario Overview

| Field                                        | Value                                                                              |
| -------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Scenario Name**                            | "Operation Silent Cascade"                                                         |
| **Scenario Type**                            | Discussion-Based Tabletop Exercise                                                 |
| **Difficulty**                               | High                                                                               |
| **Estimated Duration**                       | 4-6 hours (full day with breaks recommended)                                       |
| **Threat Category**                          | APT / Targeted Intrusion                                                           |
| **Threat Actor (fictional)**                 | "APT-Phantom-7" (state-aligned, espionage-motivated)                               |
| **Targeted Industry (in scenario)**          | BFSI (banking) — multi-client portfolio impact                                     |
| **Number of Affected Clients (in scenario)** | 2 fictional clients ("BankAlpha", "BankBeta")                                      |
| **Dwell Time (in scenario)**                 | 9 months pre-detection                                                             |
| **Initial Access Vector**                    | Supply chain compromise of shared IT vendor                                        |
| **Primary Objective**                        | Test multi-tenant APT detection, IR command, CCIC, regulatory + legal coordination |

---

# 4. TTX Objectives (Mandatory)

| ID         | Objective                                               | Success Criteria                                                      |
| ---------- | ------------------------------------------------------- | --------------------------------------------------------------------- |
| **OBJ-1**  | Validate APT detection through multi-source correlation | L3 + TI demonstrate effective cross-source pivot within 90 min        |
| **OBJ-2**  | Test L3 deep forensic investigation methodology         | L3 produces accurate timeline + TTP mapping within 120 min            |
| **OBJ-3**  | Validate IR Team incident command for APT P1            | IR Team Lead assumes IC within 30 min; war room functional            |
| **OBJ-4**  | Test multi-tenant CCIC activation                       | CCIC appointed within 15 min of 2nd client correlation                |
| **OBJ-5**  | Validate attribution analysis methodology               | Attribution confidence levels applied with Diamond Model              |
| **OBJ-6**  | Test regulatory engagement (RBI + CERT-In)              | RBI report drafted within 2 hours; CERT-In within 6 hours             |
| **OBJ-7**  | Validate legal counsel coordination                     | Legal engaged before law enforcement contact; legal hold issued       |
| **OBJ-8**  | Test executive communication under pressure             | CISO + Client CISO briefed within 1 hour; updates every 60 min        |
| **OBJ-9**  | Validate evidence preservation for legal proceedings    | Chain of custody documented; forensic-grade preservation              |
| **OBJ-10** | Test sanitized cross-client intelligence sharing        | Sanitized TI output for portfolio defense within 24 hours (simulated) |

---

# 5. Participants and Roles (Mandatory)

## 5.1 Required Participants

| Role                       | Played By             | Active in Scenario       |
| -------------------------- | --------------------- | ------------------------ |
| IR Team Lead (CCIC)        | Senior IR Team member | Yes (Incident Commander) |
| L3 Forensics Lead          | Senior L3             | Yes                      |
| Threat Intel Lead          | Threat Intel Lead     | Yes                      |
| L2 Lead Analyst            | Senior L2             | Yes                      |
| SOC Lead                   | SOC Lead              | Yes                      |
| Per-Client SDM (BankAlpha) | SDM                   | Yes                      |
| Per-Client SDM (BankBeta)  | SDM                   | Yes                      |
| Compliance Lead            | Compliance Lead       | Yes                      |
| Legal Counsel              | Legal Counsel         | Yes                      |
| MSSP CISO                  | CISO                  | Yes (executive role)     |
| Detection Engineer         | Detection Eng         | Yes                      |

## 5.2 Optional / Observer Participants

| Role                          | Played By                          |
| ----------------------------- | ---------------------------------- |
| Junior L3 (learning)          | Observer                           |
| New IR Team member (learning) | Observer                           |
| Internal Auditor              | Observer (for compliance evidence) |
| HR Lead                       | Observer                           |
| Sub-team Leads                | Observer                           |

## 5.3 White Team (Facilitators + Evaluators)

| Role                                | Person                              |
| ----------------------------------- | ----------------------------------- |
| Lead Facilitator                    | IR Team Lead (or designated senior) |
| Co-Facilitator                      | Threat Intel Lead                   |
| Evaluator – IR Command              | SOC Manager                         |
| Evaluator – Forensics               | Senior L3 / Forensics Specialist    |
| Evaluator – Multi-Tenant Discipline | Compliance Lead                     |
| Evaluator – Regulatory              | Compliance Lead                     |
| Evaluator – Legal                   | Legal Counsel                       |
| Evaluator – Communication           | CISO or designate                   |
| Timekeeper                          | Training Lead                       |
| Scribe / Note-Taker                 | Training Lead                       |

---

# 6. Threat Actor Profile (Fictional – for Realism)

| Attribute                        | Detail                                                                     |
| -------------------------------- | -------------------------------------------------------------------------- |
| **Actor Name (fictional)**       | APT-Phantom-7                                                              |
| **Suspected Origin (fictional)** | State-aligned, East Asia (DO NOT use real nation names)                    |
| **Motivation**                   | Espionage – financial intelligence, M&A intel                              |
| **Active Since**                 | Approximately 4 years (fictional)                                          |
| **Targeting**                    | BFSI sector, Tier-1 banks, regional concentration                          |
| **Sophistication**               | High – custom malware, supply chain access, OPSEC discipline               |
| **Known TTPs (MITRE ATT&CK)**    | T1195.002, T1078, T1059.001, T1547, T1003, T1021, T1071, T1041, T1027      |
| **Custom Tooling**               | Custom backdoor "PhantomShell"; custom C2 framework                        |
| **Infrastructure**               | Compromised legitimate cloud infrastructure; fast-flux DNS                 |
| **Persistence**                  | WMI event subscriptions; scheduled tasks; service binaries                 |
| **Lateral Movement**             | RDP, WMI, SMB; harvested credentials                                       |
| **Exfiltration**                 | Encrypted HTTPS to compromised legitimate domains; staged in cloud storage |

---

# 7. Scenario Background

## 7.1 MSSP Context

The MSSP provides 24x7 MDR services to two regional BFSI clients:

- **BankAlpha** – Tier-1 commercial bank; ~50,000 endpoints; RBI-regulated
- **BankBeta** – Tier-1 commercial bank; ~40,000 endpoints; RBI-regulated

Both clients use the same shared IT vendor "GlobalITVendor" for endpoint management.

## 7.2 Initial Situation (Day 0 — Detection Day)

The MSSP receives the following alerts within 4 hours:

| Time      | Alert                                                                         | Tenant    |
| --------- | ----------------------------------------------------------------------------- | --------- |
| T+0       | EDR alert: unusual PowerShell execution on BankAlpha domain controller        | BankAlpha |
| T+90 min  | SIEM alert: large encrypted outbound traffic to unknown domain (BankAlpha)    | BankAlpha |
| T+3 hours | Threat Intel feed match: IoC from external advisory matches BankAlpha traffic | BankAlpha |
| T+4 hours | EDR alert: similar PowerShell pattern on BankBeta jump server                 | BankBeta  |

**Hidden background (revealed via injects):**

- APT-Phantom-7 compromised GlobalITVendor 9 months ago
- Backdoor "PhantomShell" deployed via legitimate vendor update channel
- Both BankAlpha and BankBeta received the trojanized update 7 months ago
- Actor has been conducting reconnaissance + credential harvesting for 7 months
- Active data staging began 30 days ago
- Active exfiltration began 5 days ago

---

# 8. Master Scenario Events List (MSEL) — FACILITATOR ONLY

⚠️ **CONFIDENTIAL — DO NOT SHARE WITH PARTICIPANTS BEFORE EXERCISE**

## 8.1 Phase 1: Detection & Initial Triage (T+0 to T+60 min)

| #   | T+     | Method  | Content                                                                           | Expected Response                                                             | Evaluator Notes              |
| --- | ------ | ------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------------------- |
| 1   | 0 min  | Verbal  | "EDR alert at BankAlpha DC: powershell.exe -enc <base64 string>"                  | L1/L2 triage, decode base64, escalate to L3                                   | TTA < 5 min                  |
| 2   | 10 min | Written | "SIEM correlation: same host has historical persistence via WMI"                  | L2 escalates to L3 immediately                                                | TTE < 15 min                 |
| 3   | 20 min | Verbal  | "Decoded PowerShell shows credential dumping (Mimikatz-like)"                     | L3 begins deep investigation; IR Team activation considered                   | L3 engagement < 25 min       |
| 4   | 30 min | Verbal  | "Threat Intel: IoC matches advisory from FS-ISAC re: APT campaign targeting BFSI" | TI Lead engaged; APT severity considered                                      | TI engagement < 35 min       |
| 5   | 45 min | Verbal  | "Historical SIEM shows similar PowerShell on this DC 7 MONTHS ago"                | Dwell time recognized; severity escalated to P1; IR Team activation triggered | Severity escalation accurate |
| 6   | 55 min | Verbal  | "SOC Lead requests IR Team activation per IRT Activation Criteria"                | IR Team Lead activates; war room initiated                                    | IR Team activation < 60 min  |

## 8.2 Phase 2: IR Team Activation & Initial Investigation (T+60 to T+120 min)

| #   | T+      | Method  | Content                                                                                | Expected Response                                           | Evaluator Notes               |
| --- | ------- | ------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------- |
| 7   | 65 min  | Verbal  | "IR Team Lead assumes Incident Command. Bridge call opens."                            | IC assumes command; bridge agenda set                       | IC assumption clear           |
| 8   | 75 min  | Written | "Initial L3 forensics: PhantomShell backdoor identified; matches external TI advisory" | Threat actor identification begins                          | Actor mapping started         |
| 9   | 85 min  | Verbal  | "EDR shows similar pattern on BankBeta jump server — different tenant!"                | **CCIC TRIGGER** — multi-tenant correlation; CCIC appointed | CCIC appointment < 90 min     |
| 10  | 90 min  | Verbal  | "Per-Client SDM (BankBeta) escalation: client noticed performance anomaly"             | BankBeta independent tenant investigation begins            | Tenant segregation maintained |
| 11  | 100 min | Verbal  | "TI Lead identifies common vector: GlobalITVendor update — SUPPLY CHAIN"               | Supply chain incident playbook triggered                    | Supply chain recognition      |
| 12  | 115 min | Verbal  | "Initial timeline: dwell time ~9 months; active exfil last 5 days"                     | Severity confirmed XC-P1 (Critical Cross-Client)            | Severity correct              |

## 8.3 Phase 3: Containment Decisions (T+120 to T+180 min)

| #   | T+      | Method  | Content                                                                              | Expected Response                                                            | Evaluator Notes                |
| --- | ------- | ------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- | ------------------------------ |
| 13  | 125 min | Verbal  | "Question: contain both clients simultaneously or stagger?"                          | IC decision per containment authority matrix; per-client authority respected | Authority matrix used          |
| 14  | 135 min | Written | "BankAlpha CISO calls demanding immediate isolation of all DCs"                      | Per-client SDM coordinates with client CISO; risks/options discussed         | Client authority respected     |
| 15  | 145 min | Verbal  | "Containment risk: isolation may tip off actor; lose visibility on lateral movement" | Risk/reward discussion; IC decision                                          | Decision framework applied     |
| 16  | 155 min | Verbal  | "BankBeta CISO requests joint call with BankAlpha CISO"                              | **DENIED** — tenant segregation; separate bridges per client                 | Multi-tenant discipline tested |
| 17  | 165 min | Verbal  | "Legal counsel weighs in: preserve evidence before containment for legal action"     | Legal hold issued; forensic preservation prioritized                         | Legal coordination engaged     |
| 18  | 175 min | Verbal  | "Containment strategy approved: staged, evidence-preserving, per-client"             | Containment playbook executed                                                | Coordination strong            |

## 8.4 Phase 4: Regulatory + Executive Engagement (T+180 to T+240 min)

| #   | T+      | Method  | Content                                                                       | Expected Response                                                       | Evaluator Notes       |
| --- | ------- | ------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------- |
| 19  | 185 min | Verbal  | "RBI reporting timeline: 2-6 hours from declaration — clock has been running" | Compliance Lead drafts RBI report (per client)                          | RBI awareness on time |
| 20  | 195 min | Verbal  | "CERT-In 6-hour reporting clock active — applies per affected entity"         | Compliance Lead drafts CERT-In report (per client)                      | CERT-In awareness     |
| 21  | 210 min | Verbal  | "MSSP CISO joins bridge — demands status briefing"                            | IC delivers executive briefing                                          | Exec comms quality    |
| 22  | 220 min | Verbal  | "BankAlpha CISO requests joint regulatory submission with MSSP"               | **DENIED** — client owns regulatory reporting; MSSP supports per-client | Boundary held         |
| 23  | 230 min | Written | "Press inquiry received by BankAlpha PR team"                                 | Legal + Client coordinate; MSSP does not engage press                   | Boundary held         |
| 24  | 240 min | Verbal  | "Question: engage law enforcement?"                                           | Legal Counsel + CISO decision; per-client decision authority            | Legal coordination    |

## 8.5 Phase 5: Attribution Analysis + Cross-Client TI (T+240 to T+300 min)

| #   | T+      | Method  | Content                                                                                         | Expected Response                                         | Evaluator Notes         |
| --- | ------- | ------- | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- | ----------------------- |
| 25  | 245 min | Verbal  | "TI Lead presents attribution analysis using Diamond Model"                                     | Attribution methodology applied; confidence levels stated | Methodology correct     |
| 26  | 260 min | Written | "Attribution confidence: MEDIUM to APT-Phantom-7 based on TTP overlap, infrastructure, malware" | Confidence levels articulated; limitations noted          | Confidence appropriate  |
| 27  | 270 min | Verbal  | "Question: should MSSP share sanitized IoC/TTP brief with other MSSP clients?"                  | CISO approval; sanitization process followed              | Sanitization process    |
| 28  | 285 min | Verbal  | "BankAlpha CISO asks: 'Who else is affected? Other banks?'"                                     | **No client disclosure** — sanitized response only        | Multi-tenant discipline |
| 29  | 295 min | Verbal  | "External CERT-In advisory issued during incident — confirms broader campaign"                  | Threat Intel integration confirms portfolio risk          | External TI integrated  |

## 8.6 Phase 6: Eradication & Recovery Planning (T+300 to T+360 min)

| #   | T+      | Method  | Content                                                                                      | Expected Response                                    | Evaluator Notes        |
| --- | ------- | ------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------- | ---------------------- |
| 30  | 305 min | Verbal  | "Eradication strategy: rebuild compromised systems; rotate ALL credentials"                  | Eradication plan per-client; coordinated with client | Plan comprehensive     |
| 31  | 315 min | Verbal  | "Question: trust GlobalITVendor going forward?"                                              | Vendor risk decision; client-led; MSSP advises       | Vendor risk discussion |
| 32  | 330 min | Written | "BankAlpha CISO requests MSSP recommendation on vendor relationship termination"             | MSSP provides advisory; client decides               | Advisory boundary      |
| 33  | 345 min | Verbal  | "Recovery timeline: phased; monitoring intensified; long-term hunt for residual persistence" | Long-term monitoring plan articulated                | Long-term plan strong  |
| 34  | 360 min | Verbal  | "Scenario freeze — move to hot wash"                                                         | Hot wash begins                                      | —                      |

---

# 9. Pre-Read for Participants (NON-CONFIDENTIAL)

## 9.1 Scenario Brief (Share with Participants Pre-TTX)

### Background

You will participate in a 4-6 hour tabletop exercise simulating a sophisticated APT campaign affecting two MSSP clients in the BFSI sector. The scenario involves a long-dwell-time intrusion via supply chain compromise, requiring deep forensic investigation, IR Team incident command, multi-tenant cross-client coordination (CCIC), regulatory engagement (RBI + CERT-In), legal coordination, and executive communication.

### Your Preparation

Before the TTX, please:

1. Review your role-specific playbooks (APT, Supply Chain)
2. Review your role-specific SOPs (IR Team, L3 Forensics, Threat Intel, Compliance)
3. Review the Cross-Client Incident Procedure
4. Review the Client Data Segregation Policy
5. Be ready to engage as your actual role under realistic pressure

### What You Will NOT Have

- The Master Scenario Events List (MSEL) — facilitator only
- Specific inject timing — to be revealed as the scenario progresses
- Resolution path — to be determined by your decisions

### Ground Rules

- This is a safe, no-blame learning environment
- Engage authentically as your role
- Make decisions using actual playbooks and SOPs
- Maintain multi-tenant discipline even under pressure
- All decisions will be documented and discussed in hot wash
- Hot wash will follow immediately; AAR within 14 days

---

# 10. Evaluation Framework (Mandatory)

## 10.1 Per-Objective Scoring

Use `TTX-Evaluation-Scorecard.md` for detailed scoring. Summary:

| Objective                             | Evaluator               | Pass Threshold      |
| ------------------------------------- | ----------------------- | ------------------- |
| OBJ-1: APT Detection via Multi-Source | L3 Evaluator            | Score ≥3            |
| OBJ-2: L3 Forensic Methodology        | L3 Evaluator            | Score ≥3            |
| OBJ-3: IR Team Incident Command       | IR Command Evaluator    | Score ≥3            |
| OBJ-4: CCIC Activation                | Multi-Tenant Evaluator  | Score ≥4 (critical) |
| OBJ-5: Attribution Analysis           | TI Evaluator            | Score ≥3            |
| OBJ-6: Regulatory Engagement          | Compliance Evaluator    | Score ≥3            |
| OBJ-7: Legal Coordination             | Legal Evaluator         | Score ≥3            |
| OBJ-8: Executive Communication        | Communication Evaluator | Score ≥3            |
| OBJ-9: Evidence Preservation          | L3 Evaluator            | Score ≥3            |
| OBJ-10: Sanitized Cross-Client TI     | Multi-Tenant Evaluator  | Score ≥4 (critical) |

## 10.2 Critical Failure Triggers

The TTX is marked **FAIL** if any of:

- Cross-client information leakage between SDMs/bridges
- Joint regulatory submission attempted across clients
- Joint bridge call with multiple clients
- Cross-client information disclosed to a client
- Containment authority bypassed by MSSP without client authorization
- Legal hold not issued before evidence handling
- CCIC not appointed within 30 min of 2nd client correlation

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

Based on prior APT TTX patterns, expect findings in:

| Area                          | Common Gaps                                       |
| ----------------------------- | ------------------------------------------------- |
| Multi-tenant discipline       | Temptation to discuss clients together            |
| CCIC timing                   | Late activation if not auto-triggered             |
| Attribution rigor             | Over-confidence; insufficient Diamond Model usage |
| Regulatory parallel reporting | Confusion about per-client vs joint               |
| Legal-first sequencing        | Containment before legal hold                     |
| Executive communication       | Technical-business translation gaps               |
| Long-term monitoring          | Underestimated effort post-eradication            |
| Vendor risk decisions         | Unclear advisory vs decision boundary             |
| Sanitized intel sharing       | Over-sanitization or under-sanitization           |

---

# 13. Improvement Areas to Probe (Facilitator Prompts)

If participants miss these, prompt with:

| Prompt                                           | Tests                              |
| ------------------------------------------------ | ---------------------------------- |
| "What if BankAlpha asks who else is affected?"   | Multi-tenant disclosure discipline |
| "What's your dwell-time analysis methodology?"   | L3 forensic rigor                  |
| "How do you preserve evidence while containing?" | Legal-forensic balance             |
| "What's the attribution confidence level?"       | Attribution methodology            |
| "Should you share IoCs with other MSSP clients?" | Sanitization process               |
| "What's the RBI timeline per client?"            | Regulatory awareness               |
| "Who decides to engage law enforcement?"         | Legal decision boundary            |
| "Joint bridge call with both clients?"           | Multi-tenant test                  |

---

# 14. Multi-Tenant Considerations (Mandatory)

This scenario is specifically designed to test multi-tenant discipline:

| Test                             | Inject                       |
| -------------------------------- | ---------------------------- |
| Tenant segregation               | Inject 9, 14, 16, 20, 22, 28 |
| CCIC activation                  | Inject 9                     |
| Per-client authority             | Inject 14, 22                |
| Sanitized TI sharing             | Inject 27                    |
| Cross-client disclosure pressure | Inject 28                    |
| Joint regulatory pressure        | Inject 22                    |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 15. Logistics Checklist (Mandatory)

## 15.1 T-30 Days

- [ ] TTX scheduled
- [ ] Calendar invites sent
- [ ] Venue confirmed (in-person/virtual/hybrid)
- [ ] Scenario reviewed and approved by IR Team Lead

## 15.2 T-7 Days

- [ ] Pre-read distributed to participants
- [ ] Role assignments confirmed
- [ ] Facilitator MSEL final
- [ ] Evaluator scorecards prepared
- [ ] Equipment tested

## 15.3 T-1 Day

- [ ] Reminder sent
- [ ] Materials printed
- [ ] Backup facilitator confirmed
- [ ] Catering arranged

## 15.4 Day of TTX

- [ ] Sign-in sheet
- [ ] Ground rules briefing
- [ ] Timekeeping started
- [ ] Recording (if applicable, with consent)
- [ ] Hot wash facilitation
- [ ] AAR timeline communicated

---

# 16. Required Materials (Mandatory)

| Material                          | Source                                                                             |
| --------------------------------- | ---------------------------------------------------------------------------------- |
| Scenario brief (pre-read)         | Section 9 of this document                                                         |
| MSEL (facilitator only)           | Section 8 of this document                                                         |
| Evaluation scorecards             | `TTX-Evaluation-Scorecard.md`                                                      |
| Reference: APT Playbook           | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                                 |
| Reference: Supply Chain Playbook  | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md`                   |
| Reference: Cross-Client Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| Reference: Multi-Tenant Policy    | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |
| Sign-in sheet                     | Template                                                                           |
| Timekeeping (visible clock)       | Mandatory                                                                          |
| Whiteboard / virtual whiteboard   | Mandatory                                                                          |
| Bridge call platform (simulated)  | Optional realism                                                                   |

---

# 17. AAR Template (Post-TTX)

After-action report will document:

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

**Reference:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md` Section 15

---

# 18. Quality Checklist (Per APT TTX Execution)

Before declaring this TTX complete:

- [ ] All 10 objectives evaluated
- [ ] Scorecards collected from all evaluators
- [ ] Hot wash conducted immediately post-TTX
- [ ] Critical failure triggers reviewed
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Action items entered in tracker
- [ ] Multi-tenant discipline observations documented
- [ ] CCIC effectiveness assessed
- [ ] Regulatory engagement effectiveness assessed
- [ ] Sanitized intel sharing process tested
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

| Process                         | Integration                   |
| ------------------------------- | ----------------------------- |
| Tabletop Exercise Guide         | Master methodology            |
| APT Playbook                    | Validated by this TTX         |
| Supply Chain Playbook           | Validated by this TTX         |
| Cross-Client Incident Procedure | Tested by this TTX            |
| Client Data Segregation Policy  | Tested by this TTX            |
| IR Team Onboarding              | TTX participation requirement |
| L3 Onboarding                   | TTX participation requirement |
| Lessons Learned Register        | AAR feeds register            |
| Playbook Update Log             | Playbook gaps tracked         |
| Detection Improvement Log       | Detection gaps tracked        |
| Control Gap Tracker             | Control gaps tracked          |
| Threat Actor Profile            | Refined post-TTX              |
| TTP Intelligence Report         | Refined post-TTX              |
| RBI Incident Reporting          | Tested by this TTX            |
| CERT-In Reporting               | Tested by this TTX            |
| Legal Counsel Engagement        | Tested by this TTX            |

---

# 21. Related Documents

| Document                         | Path                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------- |
| Tabletop Exercise Guide          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`                  |
| TTX Evaluation Scorecard         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`                 |
| TTX Ransomware Scenario          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`                  |
| TTX Insider Threat Scenario      | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md`              |
| TTX Data Breach Scenario         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`                  |
| APT Master Playbook              | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                                              |
| APT L3 Forensics                 | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md`                                        |
| APT ThreatIntel Integration      | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md`                             |
| APT LongTerm Monitoring          | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md`                                 |
| APT Attribution Analysis         | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md`                                |
| APT MITRE Mapping                | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md`                                       |
| Supply Chain Master Playbook     | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md`                                |
| Cross-Client Incident Procedure  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`              |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| IRT Activation Criteria          | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`                     |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`            |
| L3 Attribution Analysis          | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Attribution-Analysis.md`                          |
| L3 Threat Intel Integration      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`                      |
| RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Threat Actor Profile Template    | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`                    |
| TTP Intelligence Report          | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`                          |
| Lessons Learned Template         | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                             |
| Playbook Update Log              | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                             |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                       |

---

# 22. Revision History

| Version | Date        | Author                                | Changes         |
| ------- | ----------- | ------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / Threat Intel Lead | Initial version |

---

# 23. Approval

Approved by:

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| MSSP IR Team Lead      |      |           |      |
| MSSP Threat Intel Lead |      |           |      |
| MSSP SOC Manager       |      |           |      |
| MSSP CISO              |      |           |      |

---

**End of Document**
