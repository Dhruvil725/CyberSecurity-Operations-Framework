# Tabletop Exercise – Data Breach / Exfiltration Scenario

---

# 1. Document Control

| Field                | Value                                                     |
| -------------------- | --------------------------------------------------------- |
| Document Name        | TTX – Data Breach / Exfiltration Scenario                 |
| Document ID          | MSSP-TRN-TTX-002                                          |
| Version              | 1.0                                                       |
| Effective Date       | 30-May-2026                                               |
| Owner                | MSSP IR Team Lead / Compliance Lead                       |
| Approved By          | MSSP CISO                                                 |
| Classification       | Confidential – MSSP Internal                              |
| Review Cycle         | Annually (or upon regulatory update)                      |
| Scenario Difficulty  | High                                                      |
| Recommended Audience | L2 + L3 + IR Team + Compliance + Legal + DPO + CISO + SDM |

---

# 2. Purpose

This document defines a standardized **Data Breach / Exfiltration Tabletop Exercise Scenario** designed to test the MSSP's ability to detect, investigate, contain, and respond to a major data exfiltration incident affecting Personally Identifiable Information (PII), payment data, and confidential business data — validating L2/L3 investigation, IR Team incident command, legal coordination, DPDP/regulatory compliance, breach notification timelines, client coordination, executive communication, and reputational risk management.

A formal Data Breach TTX is critical because:

- data breaches carry the highest regulatory, financial, legal, and reputational exposure of any incident type
- DPDP Act, RBI, sector regulators, and international privacy regimes (GDPR, etc.) impose strict notification timelines
- breach notification decisions are time-critical and irreversible — practice prevents costly errors
- legal coordination before any external communication is mandatory but often skipped under pressure
- multi-tenant MSSPs face per-client breach notification obligations requiring strict tenant discipline
- DPO (Data Protection Officer) coordination is unfamiliar to many IR teams
- regulatory engagement (DPDP Board, RBI, sector regulators) under breach circumstances requires practice
- customer/data subject notification requires legal-approved communication
- press, social media, and reputational management require structured coordination
- forensic preservation for potential class action / regulatory enforcement requires expert handling
- evidence quantification ("how many records affected") under uncertainty is a key skill
- ISO 27001 A.5.34, NIST CSF RS.CO, RBI Cyber Security Framework require validated breach response
- without structured TTX, breach response gaps remain hidden until real incidents
- this scenario is the foundation for annual mandatory data breach exercise

This scenario ensures:

- structured data breach simulation across detection, investigation, scoping, containment
- breach notification timeline pressure (DPDP, RBI, CERT-In, sector-specific)
- legal-first sequencing validation
- DPO coordination practice
- per-client tenant segregation during breach
- evidence preservation for potential litigation/enforcement
- executive and reputational communication under pressure
- customer/data subject notification decision-making
- audit-ready exercise documentation

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`
- `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`
- `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`

---

# 3. Scenario Overview

| Field                               | Value                                                                                  |
| ----------------------------------- | -------------------------------------------------------------------------------------- |
| **Scenario Name**                   | "Operation Crystal Echo"                                                               |
| **Scenario Type**                   | Discussion-Based Tabletop Exercise                                                     |
| **Difficulty**                      | High                                                                                   |
| **Estimated Duration**              | 4-6 hours (full day with breaks recommended)                                           |
| **Threat Category**                 | Data Breach / Exfiltration                                                             |
| **Threat Actor (fictional)**        | Financially-motivated cybercriminal group ("Shadow Quill")                             |
| **Targeted Industry (in scenario)** | E-Commerce / FinTech (single MSSP client)                                              |
| **Affected Client (in scenario)**   | "PayWave" — fictional payment processor                                                |
| **Data Affected (in scenario)**     | 2.4M customer records (PII + payment metadata + KYC docs)                              |
| **Initial Access Vector**           | Exploited misconfigured cloud storage + compromised vendor credential                  |
| **Detection Method**                | Threat Intel — data discovered on dark web marketplace                                 |
| **Primary Objective**               | Test breach detection, notification timelines, legal coordination, DPDP/RBI compliance |

---

# 4. TTX Objectives (Mandatory)

| ID         | Objective                                                | Success Criteria                                             |
| ---------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| **OBJ-1**  | Validate breach detection via external threat intel      | TI Lead validates and escalates within 30 min                |
| **OBJ-2**  | Test L3 forensic scoping of data exfiltration            | L3 produces preliminary scope within 120 min                 |
| **OBJ-3**  | Validate IR Team activation for breach P1                | IR Team Lead assumes IC within 30 min                        |
| **OBJ-4**  | Test legal-first sequencing before notifications         | Legal engaged before any external communication              |
| **OBJ-5**  | Validate DPO coordination                                | DPO engaged within 1 hour                                    |
| **OBJ-6**  | Test DPDP breach notification workflow                   | DPDP timeline awareness; draft within 6 hours                |
| **OBJ-7**  | Test RBI breach reporting workflow                       | RBI report drafted within 2-6 hours per RBI                  |
| **OBJ-8**  | Test CERT-In reporting                                   | CERT-In report drafted within 6 hours                        |
| **OBJ-9**  | Validate customer/data subject notification decision     | Notification decision framework applied with legal           |
| **OBJ-10** | Test executive + reputational communication              | CISO briefed; press strategy coordinated with client + legal |
| **OBJ-11** | Validate forensic evidence preservation for litigation   | Legal hold issued; CoC documented; forensic-grade            |
| **OBJ-12** | Test multi-tenant discipline during single-client breach | No cross-client information leakage even under pressure      |

---

# 5. Participants and Roles (Mandatory)

## 5.1 Required Participants

| Role                     | Played By             | Active in Scenario       |
| ------------------------ | --------------------- | ------------------------ |
| IR Team Lead             | Senior IR Team member | Yes (Incident Commander) |
| L3 Forensics Lead        | Senior L3             | Yes                      |
| L2 Lead Analyst          | Senior L2             | Yes                      |
| Threat Intel Lead        | Threat Intel Lead     | Yes                      |
| SOC Lead                 | SOC Lead              | Yes                      |
| Per-Client SDM (PayWave) | SDM                   | Yes                      |
| Compliance Lead          | Compliance Lead       | Yes                      |
| Legal Counsel            | Legal Counsel         | Yes (critical role)      |
| DPO (MSSP or Client)     | DPO                   | Yes (critical role)      |
| MSSP CISO                | CISO                  | Yes (executive role)     |
| Detection Engineer       | Detection Eng         | Yes                      |

## 5.2 Optional / Observer Participants

| Role                          | Played By                          |
| ----------------------------- | ---------------------------------- |
| Junior L3 (learning)          | Observer                           |
| New IR Team member (learning) | Observer                           |
| Internal Auditor              | Observer (for compliance evidence) |
| HR Lead                       | Observer (insider angle awareness) |
| PR Lead (if applicable)       | Observer                           |

## 5.3 White Team (Facilitators + Evaluators)

| Role                                | Person                              |
| ----------------------------------- | ----------------------------------- |
| Lead Facilitator                    | IR Team Lead (or designated senior) |
| Co-Facilitator                      | Compliance Lead                     |
| Evaluator – IR Command              | SOC Manager                         |
| Evaluator – Forensic Scoping        | Senior L3                           |
| Evaluator – Legal Sequencing        | Legal Counsel                       |
| Evaluator – DPDP Compliance         | DPO or Compliance Lead              |
| Evaluator – Regulatory              | Compliance Lead                     |
| Evaluator – Multi-Tenant Discipline | Compliance Lead                     |
| Evaluator – Communication           | CISO or designate                   |
| Timekeeper                          | Training Lead                       |
| Scribe / Note-Taker                 | Training Lead                       |

---

# 6. Threat Actor Profile (Fictional – for Realism)

| Attribute                     | Detail                                                          |
| ----------------------------- | --------------------------------------------------------------- |
| **Actor Name (fictional)**    | Shadow Quill                                                    |
| **Motivation**                | Financial — data sale on dark web marketplaces                  |
| **Sophistication**            | Medium-High — opportunistic but skilled                         |
| **Targeting**                 | FinTech, payment processors, e-commerce                         |
| **Known TTPs (MITRE ATT&CK)** | T1190, T1078, T1530, T1567.002, T1567.001, T1041                |
| **Tooling**                   | Custom data harvesting scripts; cloud-native exfiltration tools |
| **Infrastructure**            | Cloud-based; dark web marketplaces for sale                     |
| **OPSEC**                     | Moderate — uses VPN, proxies, but reuses infrastructure         |
| **Monetization**              | Bulk record sales; targeted account takeover sales              |
| **Public Profile**            | Active on multiple dark web forums                              |

---

# 7. Scenario Background

## 7.1 MSSP Context

The MSSP provides 24x7 MDR services to PayWave, a fictional Indian payment processor:

- **PayWave** – Mid-size payment processor; ~2,500 employees; RBI-regulated payment aggregator; processes 8M transactions/day
- Database holds: 12M customer records (PII, KYC docs, payment metadata, transaction history)
- Subject to DPDP Act, RBI Payment Aggregator framework, PCI-DSS

## 7.2 Initial Situation (Day 0 — Detection Day)

The MSSP Threat Intel team identifies a dark web marketplace listing:

| Time     | Event                                                                                     | Source                     |
| -------- | ----------------------------------------------------------------------------------------- | -------------------------- |
| T+0      | TI Lead identifies dark web listing: "2.4M Indian payment processor records — fresh dump" | Dark web monitoring        |
| T+15 min | Sample data preview matches PayWave's customer ID format                                  | TI Lead analysis           |
| T+30 min | Sample includes KYC documents with PayWave logo watermarks (confirmed)                    | TI Lead validation         |
| T+45 min | Estimated breach window: 30-90 days (per data freshness analysis)                         | TI Lead initial assessment |

**Hidden background (revealed via injects):**

- Cloud storage bucket misconfigured 4 months ago by PayWave dev team
- Vendor "DataAnalyticsCo" credential compromised via phishing 3 months ago
- Actor accessed via vendor credential → discovered misconfigured bucket → exfiltrated over 6 weeks
- Last exfiltration activity: 8 days ago
- Data sold on dark web 3 days ago to multiple buyers

---

# 8. Master Scenario Events List (MSEL) — FACILITATOR ONLY

⚠️ **CONFIDENTIAL — DO NOT SHARE WITH PARTICIPANTS BEFORE EXERCISE**

## 8.1 Phase 1: Detection & Initial Validation (T+0 to T+60 min)

| #   | T+     | Method  | Content                                                                    | Expected Response                                        | Evaluator Notes             |
| --- | ------ | ------- | -------------------------------------------------------------------------- | -------------------------------------------------------- | --------------------------- |
| 1   | 0 min  | Verbal  | "TI Lead alert: dark web listing — 2.4M Indian payment processor records"  | TI Lead validates listing                                | TTA < 15 min                |
| 2   | 15 min | Written | "Sample data matches PayWave customer ID format"                           | TI Lead confirms client relevance; escalates to SOC Lead | Escalation < 20 min         |
| 3   | 30 min | Verbal  | "Sample includes KYC docs with PayWave watermark — high confidence breach" | SOC Lead notifies IR Team Lead; severity P1 declared     | Severity correct            |
| 4   | 45 min | Verbal  | "IR Team Lead activation triggered per IRT Activation Criteria"            | IR Team Lead activates; bridge call opens                | IR Team activation < 50 min |
| 5   | 55 min | Verbal  | "Per-Client SDM notification: PayWave needs to be informed"                | SDM prepares initial client notification (pending legal) | Client comms pending        |

## 8.2 Phase 2: Legal-First Sequencing (T+60 to T+120 min)

| #   | T+      | Method | Content                                                                               | Expected Response                                        | Evaluator Notes          |
| --- | ------- | ------ | ------------------------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------ |
| 6   | 65 min  | Verbal | "Pause: before notifying client, what's the legal sequence?"                          | Legal Counsel engaged FIRST                              | Legal-first applied      |
| 7   | 75 min  | Verbal | "Legal Counsel advises: legal hold issued; preserve all evidence"                     | Legal hold issued; forensic preservation begins          | Legal hold issued        |
| 8   | 85 min  | Verbal | "Client (PayWave) calls — they've seen the dark web posting via their own monitoring" | Coordinated response per legal guidance                  | Client comms coordinated |
| 9   | 95 min  | Verbal | "PayWave demands immediate public statement"                                          | Legal advises: NO public statement until scope confirmed | Legal restraint applied  |
| 10  | 105 min | Verbal | "DPO needs to be engaged per DPDP Act"                                                | DPO engaged; per-client DPO if separate                  | DPO engaged < 110 min    |
| 11  | 115 min | Verbal | "MSSP CISO joins bridge — wants status briefing"                                      | IR Team Lead delivers exec briefing                      | Exec comms quality       |

## 8.3 Phase 3: Forensic Scoping (T+120 to T+180 min)

| #   | T+      | Method  | Content                                                                                  | Expected Response                                  | Evaluator Notes               |
| --- | ------- | ------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------- | ----------------------------- |
| 12  | 125 min | Verbal  | "L3 begins forensic scoping — which systems were accessed?"                              | L3 begins systematic investigation                 | L3 methodology                |
| 13  | 135 min | Written | "Cloud audit logs show vendor credential 'DataAnalyticsCo' accessed customer-pii-bucket" | Vendor compromise vector identified                | Vector identification         |
| 14  | 145 min | Verbal  | "Bucket misconfiguration: public-read enabled 4 months ago — vendor cred not needed"     | Multiple vector hypothesis                         | Hypothesis quality            |
| 15  | 155 min | Written | "Cloud access logs: 47 unique IPs accessed bucket over 6 weeks"                          | Scope expanding; quantification challenge          | Scoping rigor                 |
| 16  | 165 min | Verbal  | "Question: how many records actually exfiltrated vs accessed?"                           | L3 discusses scoping methodology under uncertainty | Methodology under uncertainty |
| 17  | 175 min | Verbal  | "PayWave CISO asks: 'Tell us EXACT number affected'"                                     | Realistic scoping with confidence range provided   | Realistic communication       |

## 8.4 Phase 4: Regulatory Notification Timelines (T+180 to T+240 min)

| #   | T+      | Method  | Content                                                                  | Expected Response                                                                | Evaluator Notes             |
| --- | ------- | ------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------------- | --------------------------- |
| 18  | 185 min | Verbal  | "DPDP Act notification timeline applies — when does clock start?"        | DPO + Legal discuss DPDP timeline (currently as soon as practicable, max 72 hrs) | DPDP awareness              |
| 19  | 195 min | Verbal  | "RBI Payment Aggregator framework — 2-6 hour reporting timeline applies" | Compliance drafts RBI report                                                     | RBI timeline awareness      |
| 20  | 205 min | Verbal  | "CERT-In 6-hour reporting — clock has been running since detection"      | Compliance drafts CERT-In report                                                 | CERT-In timeline aware      |
| 21  | 215 min | Verbal  | "PCI-DSS notification — card brands must be notified"                    | Legal + Compliance manage card brand notification                                | PCI awareness               |
| 22  | 225 min | Verbal  | "Question: PayWave wants MSSP to file reports — who files what?"         | Client owns regulatory filing; MSSP supports                                     | Filing boundary             |
| 23  | 235 min | Written | "PayWave Legal requests joint regulatory submission"                     | Legal coordination per agreement; per-client filing                              | Joint vs separate clarified |

## 8.5 Phase 5: Customer / Data Subject Notification (T+240 to T+300 min)

| #   | T+      | Method | Content                                                                 | Expected Response                             | Evaluator Notes        |
| --- | ------- | ------ | ----------------------------------------------------------------------- | --------------------------------------------- | ---------------------- |
| 24  | 245 min | Verbal | "DPDP requires notification to affected data subjects — 2.4M customers" | Notification strategy discussion              | DPDP notification      |
| 25  | 260 min | Verbal | "Notification method: email vs SMS vs press notice — recommendations?"  | Multi-channel notification plan               | Multi-channel strategy |
| 26  | 275 min | Verbal | "Notification content — what must it include per DPDP?"                 | DPDP-compliant notification content discussed | Content compliance     |
| 27  | 285 min | Verbal | "Customer call center prep — how many additional agents needed?"        | Operational scaling discussion                | Ops planning           |
| 28  | 295 min | Verbal | "Press inquiry — Times of India asks for comment"                       | Coordinated press response via client + legal | Press boundary         |

## 8.6 Phase 6: Containment + Eradication + Recovery (T+300 to T+360 min)

| #   | T+      | Method | Content                                                                       | Expected Response                       | Evaluator Notes      |
| --- | ------- | ------ | ----------------------------------------------------------------------------- | --------------------------------------- | -------------------- |
| 29  | 305 min | Verbal | "Containment: bucket lockdown; vendor credential rotation; access reviews"    | Containment plan articulated            | Plan comprehensive   |
| 30  | 315 min | Verbal | "Question: rotate ALL vendor credentials or just compromised one?"            | Risk-based decision                     | Decision framework   |
| 31  | 330 min | Verbal | "Eradication: re-architect bucket access; vendor security review"             | Eradication plan articulated            | Plan strong          |
| 32  | 345 min | Verbal | "Recovery + monitoring: enhanced cloud monitoring; vendor monitoring"         | Long-term plan articulated              | Long-term plan       |
| 33  | 355 min | Verbal | "MSSP CISO asks: 'Any lessons applicable to other MSSP clients?' (sanitized)" | Sanitized cross-client TI brief planned | Sanitization process |
| 34  | 360 min | Verbal | "Scenario freeze — move to hot wash"                                          | Hot wash begins                         | —                    |

---

# 9. Pre-Read for Participants (NON-CONFIDENTIAL)

## 9.1 Scenario Brief (Share with Participants Pre-TTX)

### Background

You will participate in a 4-6 hour tabletop exercise simulating a major data breach affecting an MSSP client — a payment processor with 2.4M customer records exposed and discovered on a dark web marketplace. The scenario involves immediate breach validation, IR Team incident command, legal-first sequencing, DPO coordination, DPDP/RBI/CERT-In regulatory engagement, customer notification decisions, and reputational management.

### Your Preparation

Before the TTX, please:

1. Review your role-specific playbooks (Data Breach, Legal Notification, Regulatory Reporting)
2. Review your role-specific SOPs
3. Review DPDP Act notification requirements
4. Review RBI Payment Aggregator incident reporting framework
5. Review the Legal Counsel Engagement SOP
6. Be ready to engage as your actual role under realistic pressure

### What You Will NOT Have

- The Master Scenario Events List (MSEL) — facilitator only
- Specific inject timing
- Resolution path — to be determined by your decisions

### Ground Rules

- This is a safe, no-blame learning environment
- Engage authentically as your role
- Make decisions using actual playbooks and SOPs
- Maintain multi-tenant discipline (even though scenario is single-client)
- Legal-first sequencing is being tested — pause before external communication
- All decisions will be documented and discussed in hot wash
- Hot wash will follow immediately; AAR within 14 days

---

# 10. Evaluation Framework (Mandatory)

## 10.1 Per-Objective Scoring

Use `TTX-Evaluation-Scorecard.md` for detailed scoring. Summary:

| Objective                              | Evaluator               | Pass Threshold      |
| -------------------------------------- | ----------------------- | ------------------- |
| OBJ-1: Breach Detection via TI         | TI Evaluator            | Score ≥3            |
| OBJ-2: L3 Forensic Scoping             | Forensic Evaluator      | Score ≥3            |
| OBJ-3: IR Team Activation              | IR Command Evaluator    | Score ≥3            |
| OBJ-4: Legal-First Sequencing          | Legal Evaluator         | Score ≥4 (critical) |
| OBJ-5: DPO Coordination                | DPDP Evaluator          | Score ≥3            |
| OBJ-6: DPDP Notification Workflow      | DPDP Evaluator          | Score ≥3            |
| OBJ-7: RBI Reporting Workflow          | Compliance Evaluator    | Score ≥3            |
| OBJ-8: CERT-In Reporting               | Compliance Evaluator    | Score ≥3            |
| OBJ-9: Customer Notification Decision  | Legal Evaluator         | Score ≥3            |
| OBJ-10: Executive + Reputational Comms | Communication Evaluator | Score ≥3            |
| OBJ-11: Evidence Preservation          | L3 Evaluator            | Score ≥3            |
| OBJ-12: Multi-Tenant Discipline        | Multi-Tenant Evaluator  | Score ≥4 (critical) |

## 10.2 Critical Failure Triggers

The TTX is marked **FAIL** if any of:

- External communication issued before legal engagement
- Press statement made without legal + client approval
- DPDP notification timeline ignored or miscalculated
- RBI reporting timeline missed
- CERT-In reporting timeline missed
- Customer notification issued without legal-approved content
- Legal hold not issued before forensic activities
- Cross-client information leakage (even though single-client scenario)
- Joint regulatory filing without proper coordination
- Public scope numbers stated without confidence range qualification

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

Based on prior Data Breach TTX patterns, expect findings in:

| Area                          | Common Gaps                                              |
| ----------------------------- | -------------------------------------------------------- |
| Legal-first sequencing        | Pressure to notify client/regulators before legal review |
| DPDP awareness                | Confusion about notification timelines and content       |
| DPO coordination              | Unclear who owns DPO engagement (MSSP vs client)         |
| Scope quantification          | Overconfident statements; missing confidence ranges      |
| Press response                | Boundary confusion between MSSP and client               |
| Regulatory parallel reporting | Confusion about who files what                           |
| Card brand notification       | Often overlooked                                         |
| Customer notification content | DPDP-compliance gaps                                     |
| Evidence preservation         | Forensic activities before legal hold                    |
| Long-term monitoring          | Underestimated post-breach surveillance                  |

---

# 13. Improvement Areas to Probe (Facilitator Prompts)

If participants miss these, prompt with:

| Prompt                                                | Tests                     |
| ----------------------------------------------------- | ------------------------- |
| "Have you engaged legal before notifying the client?" | Legal-first sequencing    |
| "What's the DPDP notification timeline?"              | DPDP awareness            |
| "Who is the DPO — MSSP or client?"                    | DPO coordination          |
| "How confident is your scope number?"                 | Scoping rigor             |
| "Has the legal hold been issued?"                     | Evidence preservation     |
| "Who files the RBI report — MSSP or client?"          | Filing boundary           |
| "Card brand notification required?"                   | PCI awareness             |
| "Has the notification content been legally reviewed?" | Content compliance        |
| "What's your press strategy?"                         | Reputational management   |
| "Are there other MSSP clients potentially at risk?"   | Sanitized portfolio brief |

---

# 14. Multi-Tenant Considerations (Mandatory)

Although this is a single-client scenario, multi-tenant discipline is tested:

| Test                                  | Inject                                            |
| ------------------------------------- | ------------------------------------------------- |
| Cross-client mention temptation       | Throughout — no other client should be referenced |
| Sanitized portfolio TI sharing        | Inject 33                                         |
| Per-client regulatory filing boundary | Inject 22, 23                                     |
| Press statement boundary              | Inject 28                                         |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 15. Logistics Checklist (Mandatory)

## 15.1 T-30 Days

- [ ] TTX scheduled
- [ ] Calendar invites sent
- [ ] Venue confirmed (in-person/virtual/hybrid)
- [ ] Scenario reviewed and approved by IR Team Lead + Legal + Compliance

## 15.2 T-7 Days

- [ ] Pre-read distributed to participants
- [ ] Role assignments confirmed
- [ ] Facilitator MSEL final
- [ ] Evaluator scorecards prepared
- [ ] Legal + DPO availability confirmed
- [ ] Equipment tested

## 15.3 T-1 Day

- [ ] Reminder sent
- [ ] Materials printed
- [ ] Backup facilitator confirmed
- [ ] Catering arranged

## 15.4 Day of TTX

- [ ] Sign-in sheet
- [ ] Ground rules briefing
- [ ] Legal-first sequencing emphasized in ground rules
- [ ] Timekeeping started
- [ ] Recording (if applicable, with consent)
- [ ] Hot wash facilitation
- [ ] AAR timeline communicated

---

# 16. Required Materials (Mandatory)

| Material                                    | Source                                                                                          |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Scenario brief (pre-read)                   | Section 9 of this document                                                                      |
| MSEL (facilitator only)                     | Section 8 of this document                                                                      |
| Evaluation scorecards                       | `TTX-Evaluation-Scorecard.md`                                                                   |
| Reference: Data Breach Master Playbook      | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`                            |
| Reference: Data Breach Legal Notification   | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`                |
| Reference: Data Breach Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`              |
| Reference: Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Reference: RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| Reference: CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| DPDP Act reference (regulatory)             | External reference                                                                              |
| Sign-in sheet                               | Template                                                                                        |
| Timekeeping (visible clock)                 | Mandatory                                                                                       |
| Whiteboard / virtual whiteboard             | Mandatory                                                                                       |

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

# 18. Quality Checklist (Per Data Breach TTX Execution)

Before declaring this TTX complete:

- [ ] All 12 objectives evaluated
- [ ] Scorecards collected from all evaluators
- [ ] Hot wash conducted immediately post-TTX
- [ ] Critical failure triggers reviewed (especially legal-first)
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Action items entered in tracker
- [ ] DPDP awareness observations documented
- [ ] Regulatory engagement effectiveness assessed
- [ ] Legal coordination effectiveness assessed
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

| Process                                   | Integration                   |
| ----------------------------------------- | ----------------------------- |
| Tabletop Exercise Guide                   | Master methodology            |
| Data Breach Master Playbook               | Validated by this TTX         |
| Data Breach Legal Notification Playbook   | Validated by this TTX         |
| Data Breach Regulatory Reporting Playbook | Validated by this TTX         |
| Legal Counsel Engagement SOP              | Tested by this TTX            |
| RBI Incident Reporting SOP                | Tested by this TTX            |
| CERT-In Reporting SOP                     | Tested by this TTX            |
| Client Data Segregation Policy            | Tested by this TTX            |
| IR Team Onboarding                        | TTX participation requirement |
| L3 Onboarding                             | TTX participation requirement |
| Lessons Learned Register                  | AAR feeds register            |
| Playbook Update Log                       | Playbook gaps tracked         |
| Control Gap Tracker                       | Control gaps tracked          |
| Threat Actor Profile                      | Refined post-TTX              |

---

# 21. Related Documents

| Document                         | Path                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------- |
| Tabletop Exercise Guide          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`                  |
| TTX Evaluation Scorecard         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`                 |
| TTX Ransomware Scenario          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`                  |
| TTX APT Scenario                 | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`                         |
| TTX Insider Threat Scenario      | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md`              |
| Data Breach Master Playbook      | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`                            |
| Data Breach L1 Triage            | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md`                         |
| Data Breach L2 Investigation     | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md`                  |
| Data Breach L3 Forensics         | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md`                      |
| Data Breach Legal Notification   | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md`                |
| Data Breach Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md`              |
| Data Breach MITRE Mapping        | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md`                     |
| Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| IRT Activation Criteria          | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`                     |
| IRT Evidence Chain of Custody    | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md`               |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Lessons Learned Template         | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                             |
| Playbook Update Log              | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                             |
| Threat Actor Profile Template    | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`                    |

---

# 22. Revision History

| Version | Date        | Author                              | Changes         |
| ------- | ----------- | ----------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / Compliance Lead | Initial version |

---

# 23. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP IR Team Lead    |      |           |      |
| MSSP Compliance Lead |      |           |      |
| MSSP Legal Counsel   |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
